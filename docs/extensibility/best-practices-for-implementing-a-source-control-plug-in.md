---
title: 实现源代码管理插件的最佳实践 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, best practices
- best practices, source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: 85e73b73-29dc-464f-8734-ed308742c435
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89bc4065a450f82b3cdec33e94f4e17ea700d3c7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352208"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>实现源代码管理插件的最佳做法
以下技术的详细信息可帮助你可靠地实施了源代码管理插件中[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

## <a name="memory-management-issues"></a>内存管理问题
 在大多数情况下，集成的开发环境 (IDE)，这是调用方，释放并分配内存。 源代码管理插件返回调用方分配的缓冲区中的字符串和其他项。 在其中发生的特定函数的说明中注明了异常。

## <a name="arrays-of-file-names"></a>文件的名称的数组
 当传递的文件数组时，它将不传递为连续的文件的名称数组。 它是作为传递的指针的数组给文件的名称。 例如，在[SccGet](../extensibility/sccget-function.md)，通过传递文件名称`lpFileNames`参数，其中`lpFileNames`实际指向的指针`char **`。 `lpFileNames`[0] 是指向第一个名称， `lpFileNames`[1] 是指向第二个名称，依次类推。

## <a name="large-model"></a>大型模型
 所有指针都是 32 位，甚至在 16 位操作系统上。

## <a name="fully-qualified-paths"></a>完全限定的路径
 其中的文件名或目录指定为参数，它们必须完全限定的路径或 UNC 路径，而无需结束反斜杠。 它负责的源代码管理插件转换到如果，它是基础源代码控制系统的要求的相对路径。

## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>为已注册的 DLL 指定完全限定的路径
 IDE 无法再从相对路径加载 Dll (例如， *.\NewProvider.dll*)。 必须指定 DLL 的完整路径 (例如， *C:\Providers\NewProvider.dll*)。 此要求可在 IDE 的安全性增强通过阻止未经授权或模拟源控件 Dll 的加载。

## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>安装源代码管理插件时检查现有 VSSCI 插件
 计划安装您的源代码管理插件的用户可能已有现有的源代码管理插件安装在计算机上。 安装 （安装程序） 程序的插件创建应确定是否存在相关的注册表项的现有值。 如果已设置这些密钥，安装程序询问用户是否将插件注册为默认的源代码管理插件和替换已安装。

## <a name="error-result-codes-and-reporting"></a>错误结果代码和报告
 `SCC_OK`返回源控制函数的代码指示该操作已成功为所有文件。 如果操作失败，则应返回遇到的最后一个错误代码。

 用于报告的规则是，如果在 IDE 中发生错误，IDE 是负责报告它。 如果源代码管理系统中发生错误，源代码管理插件负责报告它。 例如，**当前未选择任何文件**而在 IDE 中，将报告**此文件已签出**会报告该插件。

## <a name="the-context-structure"></a>上下文结构
 在调用[SccInitialize](../extensibility/sccinitialize-function.md)，调用方传递`ppvContext`参数，它是 void 到未初始化的句柄。 源代码管理插件可以忽略此参数或者它可以分配任何类型的结构，并将向该结构的指针放入传递指针。 IDE 不理解此结构，但它到此结构将指针传递给在插件中的每个其他调用。 这提供了有价值的上下文缓存信息的插件，它可用于维护而无需使用全局变量在函数调用之间仍然存在的全局状态信息。 此插件负责释放上调用的结构[SccUninitialize](../extensibility/sccuninitialize-function.md)。

 如果插件集`SCC_CAP_REENTRANT`位[SccInitialize](../extensibility/sccinitialize-function.md) (具体来说，在`lpSccCaps`参数)，多个上下文结构用于跟踪已打开的所有项目。

## <a name="bitflags-and-other-command-options"></a>位标志和其他命令选项
 对于每个命令，如[SccGet](../extensibility/sccget-function.md)，IDE 可以指定多个更改命令的行为的选项。

 该 API 支持通过 IDE 的某些选项的设置`fOptions`参数。 这些选项所述[使用特定命令的位标志](../extensibility/bitflags-used-by-specific-commands.md)以及它们会影响的命令。 一般情况下，这些是为其不会提示用户的选项。

 以这种方式，未定义最用户可配置的设置选项，因为它们也会有所不同广泛源代码管理插件。因此，建议的机制是**高级**按钮。 例如，在**获取**对话框中，则 IDE 将显示它了解，但它还会显示的信息**高级**按钮如果插件具有此命令的选项。 当用户单击**高级**按钮，IDE 调用[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)启用源代码管理插件，以提示用户输入信息，例如位标志或日期/时间。 该插件返回期间传递的结构中返回此信息`SccGet`命令。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)