---
title: 实现源代码管理插件的最佳做法 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, best practices
- best practices, source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: 85e73b73-29dc-464f-8734-ed308742c435
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 68491f22d63ae3ebb664b7c22188a661dccbf39a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740051"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>实现源代码管理插件的最佳做法
以下技术详细信息可以帮助您可靠地实现 中的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]源代码管理插件。

## <a name="memory-management-issues"></a>内存管理问题
 在大多数情况下，集成开发环境 （IDE），即调用方，释放和分配内存。 源代码管理插件返回调用方分配的缓冲区中的字符串和其他项。 异常在特定函数发生的位置的说明中注明。

## <a name="arrays-of-file-names"></a>文件名数组
 传递文件数组时，不会作为连续的文件名数组传递。 它作为指向文件名的指针数组传递。 例如，在[SccGet](../extensibility/sccget-function.md)中，文件名由`lpFileNames`参数传递，其中`lpFileNames`实际上是指向 的指针。 `char **` `lpFileNames`{0} 是指向名字的指针，[1]`lpFileNames`是指向第二个名称的指针，等等。

## <a name="large-model"></a>大模型
 所有指针都是 32 位，即使在 16 位操作系统上也是如此。

## <a name="fully-qualified-paths"></a>完全合格的路径
 如果文件名或目录被指定为参数，则它们必须是完全限定的路径或 UNC 路径，而不进行结束回斜杠。 如果是基础源代码管理系统的要求，源代码管理插件有责任将这些路径转换为相对路径。

## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>为注册的 DLL 指定完全限定的路径
 IDE 不再从相对路径加载 DLL（例如 *，._NewProvider.dll*）。 必须指定 DLL 的完整路径（例如 *，C：\提供程序\NewProvider.dll*）。 此要求通过防止加载未经授权的或模拟的源代码管理 DLL 来增强 IDE 的安全性。

## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>安装源代码管理插件时，请检查现有 VSSCI 插件
 计划安装源代码管理插件的用户可能已经在计算机上安装了现有的源代码管理插件。 您创建的插件的安装（设置）程序应确定是否存在相关注册表项的现有值。 如果已设置这些密钥，安装程序应询问用户是否将插件注册为默认源代码管理插件，并替换已安装的插件。

## <a name="error-result-codes-and-reporting"></a>错误结果代码和报告
 源代码`SCC_OK`控制函数的返回代码指示所有文件的操作都已成功。 如果操作失败，则预期将返回遇到的最后一个错误代码。

 报告的规则是，如果 IDE 中发生错误，IDE 负责报告错误。 如果源代码管理系统中出现错误，源代码管理插件负责报告它。 例如，IDE 不会报告**当前选定的任何文件**，而**此文件已签出**，插件将报告该文件。

## <a name="the-context-structure"></a>上下文结构
 在调用[Scc 初始化](../extensibility/sccinitialize-function.md)期间，调用方将参数`ppvContext`传递参数，参数是一个未初始化的句柄到 void。 源代码管理插件可以忽略此参数，也可以分配任何类型的结构，并将指向该结构的指针放入传递的指针中。 IDE 不理解此结构，但它将指向此结构的指针传递到插件中的每个其他调用中。 这为插件提供了有价值的上下文缓存信息，它可用于维护在函数调用之间持续存在的全局状态信息，而无需使用全局变量。 该插件负责在调用[SccUn初始化](../extensibility/sccuninitialize-function.md)时释放结构。

 如果插件在`SCC_CAP_REENTRANT`[Scc 初始化](../extensibility/sccinitialize-function.md)（特别是`lpSccCaps`参数中）中设置位，则使用多个上下文结构来跟踪打开的所有项目。

## <a name="bitflags-and-other-command-options"></a>比特标志和其他命令选项
 对于每个命令（如[SccGet），IDE](../extensibility/sccget-function.md)可以指定许多选项来更改命令的行为。

 API 支持 IDE 通过`fOptions`参数设置某些选项。 这些选项在[特定命令使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md)中描述，以及它们影响的命令。 通常，这些选项不会提示用户。

 大多数用户可配置的设置选项不是以这种方式定义的，因为它们在源代码管理插件之间差别很大。因此，建议的机制是一个**高级**按钮。 例如，在 **"获取"** 对话框中，IDE 仅显示它理解的信息，但如果插件具有此命令的选项，则该按钮也会显示 **"高级"** 按钮。 当用户单击 **"高级"** 按钮时，IDE 会调用[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)以启用源代码管理插件以提示用户获取信息，例如位标志或日期/时间。 插件在`SccGet`命令期间传递回的结构中返回此信息。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)
