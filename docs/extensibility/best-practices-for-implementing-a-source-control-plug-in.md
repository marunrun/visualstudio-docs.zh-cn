---
title: 实现源代码管理插件的最佳实践 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80740051"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>实现源代码管理插件的最佳实践
以下技术详细信息可帮助你在中可靠地实现源代码管理插件 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="memory-management-issues"></a>内存管理问题
 在大多数情况下，集成开发环境 (IDE) ，它是调用方，可释放和分配内存。 源代码管理插件返回调用方分配的缓冲区中的字符串和其他项。 异常在发生的特定函数说明中进行了说明。

## <a name="arrays-of-file-names"></a>文件名数组
 传递文件数组时，不会将其作为文件名的连续数组进行传递。 它作为指向文件名的指针数组进行传递。 例如，在 [SccGet](../extensibility/sccget-function.md)中，通过参数传递文件名 `lpFileNames` ，其中 `lpFileNames` 实际上是指向的指针 `char **` 。 `lpFileNames`[0] 是指向第一个名称的指针， `lpFileNames` [1] 是指向第二个名称的指针，依此类推。

## <a name="large-model"></a>大型模型
 所有指针均为32位，甚至是在16位操作系统上。

## <a name="fully-qualified-paths"></a>完全限定路径
 如果文件名或目录被指定为参数，则它们必须是完全限定的路径或 UNC 路径，不含结束反斜杠。 如果这是基础源代码管理系统的要求，则源代码管理插件负责将这些项转换为相对路径。

## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>为注册的 DLL 指定完全限定的路径
 IDE 不再从相对路径加载 Dll (例如 *.\NewProvider.dll*) 。 必须指定 DLL 的完整路径 (例如 *C:\Providers\NewProvider.dll*) 。 此要求通过阻止加载未经授权或模拟的源代码管理 Dll，增强了 IDE 的安全性。

## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>安装源代码管理插件时检查现有的 VSSCI 插件
 计划安装源代码管理插件的用户可能已在计算机上安装了现有源代码管理插件。 对于您创建的插件，安装 (安装程序) 程序应确定是否存在相关注册表项的现有值。 如果已设置这些密钥，则安装程序应要求用户是否将插件注册为默认源代码管理插件，并替换已安装的插件。

## <a name="error-result-codes-and-reporting"></a>错误结果代码和报告
 `SCC_OK`源代码管理函数的返回代码指示操作已成功完成所有文件。 如果操作失败，则应返回最后一个错误代码。

 报告的规则是，如果 IDE 中发生错误，IDE 将负责报告该错误。 如果源代码管理系统中发生错误，则源代码管理插件负责报告该错误。 例如，IDE **不会报告当前选择的任何文件** ，而 **此文件已签出** ，该插件会报告此文件。

## <a name="the-context-structure"></a>上下文结构
 调用 [SccInitialize](../extensibility/sccinitialize-function.md)时，调用方传递 `ppvContext` 参数，该参数是 void 的未初始化句柄。 源代码管理插件可以忽略此参数，也可以分配任意类型的结构，并将该结构的指针放入传递的指针。 IDE 不了解此结构，但它会将指向此结构的指针传递到插件中的其他每个调用。 这为插件提供有价值的上下文缓存信息，该插件可用于维护在不使用全局变量的情况下在函数调用中保持的全局状态信息。 此插件负责在对 [SccUninitialize](../extensibility/sccuninitialize-function.md)的调用上释放结构。

 如果插件在 SccInitialize 中设置 `SCC_CAP_REENTRANT` ([SccInitialize](../extensibility/sccinitialize-function.md) ，则在 `lpSccCaps` 参数) 中，将使用多个上下文结构来跟踪所有打开的项目。

## <a name="bitflags-and-other-command-options"></a>Bitflags 和其他命令选项
 对于每个命令（如 [SccGet](../extensibility/sccget-function.md)），IDE 可以指定多个更改命令行为的选项。

 API 支持 IDE 通过参数设置某些选项 `fOptions` 。 这些选项在 [特定命令使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md) 和它们影响的命令中进行了介绍。 通常，这些是不会提示用户的选项。

 大多数用户可配置的设置选项不是以这种方式定义的，因为它们在源代码管理插件之间存在很大的差异。因此，建议的机制是 " **高级** " 按钮。 例如，在 " **获取** " 对话框中，IDE 只显示它理解的信息，如果该插件具有此命令的选项，它还会显示 " **高级** " 按钮。 当用户单击 " **高级** " 按钮时，IDE 将调用 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) ，以使源代码管理插件可以提示用户输入信息，如 bitflags 或日期/时间。 此插件在命令期间传递回的结构中返回此信息 `SccGet` 。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)
