---
title: 解决方案用户选项（.Suo）文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6f21e4a4a6530692709247e64b0d84aa7b06eb3a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723802"
---
# <a name="solution-user-options-suo-file"></a>解决方案用户选项 (.Suo) 文件
解决方案用户选项（.suo）文件包含每用户解决方案选项。 不应将此文件签入到源代码管理中。

 解决方案用户选项（.suo）文件是以二进制格式存储的结构化存储或复合文件。 将用户信息保存到流，并将流的名称保存为密钥，该密钥将用于标识 .suo 文件中的信息。 解决方案用户选项文件用于存储用户首选项设置，当 Visual Studio 保存解决方案时，会自动创建该文件。

 当环境打开 .suo 文件时，它会枚举当前加载的所有 Vspackage。 如果 VSPackage 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts> 接口，则环境将调用 VSPackage 上的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A> 方法，要求其从 .suo 文件加载其所有数据。

 VSPackage 负责了解它可能已写入 .suo 文件的流。 对于它编写的每个流，VSPackage 通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> 调用环境以加载由密钥标识的特定流，这是流的名称。 然后，环境回调到 VSPackage，以读取传递流名称的特定流和指向 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A> 方法的 `IStream` 指针。

 此时，将对 `LoadUserOptions` 进行另一次调用，以查看是否有必须读取 .suo 文件的另一个部分。 此过程将一直继续，直到该环境中的所有数据流都已读完并处理。

 保存或关闭解决方案时，环境将使用指向 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A> 方法的指针调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A> 方法。 包含要保存的二进制信息的 `IStream` 传递到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A> 方法，后者随后将该信息写入 .suo 文件并再次调用 `SaveUserOptions` 方法，以查看是否有另一个要写入到 .suo 文件的信息流。

 这两个方法（`SaveUserOptions` 和 `WriteUserOptions`）将以递归方式调用，以将每个要保存到 .suo 文件中的信息流，并传入指向 `IVsSolutionPersistence` 的指针。 它们以递归方式调用，以允许向 .suo 文件写入多个流。 通过这种方式，用户信息会随解决方案一起保留，并且保证在下一次打开解决方案时存在。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [解决方案](../../extensibility/internals/solutions-overview.md)