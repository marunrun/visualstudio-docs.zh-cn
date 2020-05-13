---
title: 解决方案用户选项 （.Suo） 文件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .suo files, VSPackages
- suo files, VSPackages
- solutions, .suo files
- solutions, user options
- solution user options (.suo) file
ms.assetid: 75258e0d-600d-4a3d-94f4-3d7ac12cb47c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9469663d3ac258e1c568778894d8584c68c13632
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705321"
---
# <a name="solution-user-options-suo-file"></a>解决方案用户选项 (.Suo) 文件
解决方案用户选项 （.suo） 文件包含每个用户的解决方案选项。 不应将此文件签入源代码控制。

 解决方案用户选项 （.suo） 文件是以二进制格式存储的结构化存储或复合文件。 将用户信息保存到流中，其中流的名称是用于标识 .suo 文件中的信息的密钥。 解决方案用户选项文件用于存储用户首选项设置，并在 Visual Studio 保存解决方案时自动创建。

 当环境打开 .suo 文件时，它会枚举所有当前加载的 VS 包。 如果 VSPackage 实现了<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>接口，则环境调用 VSPackage 上<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.LoadUserOptions%2A>的方法，要求其从 .suo 文件加载其所有数据。

 VSPackage 有责任知道它可能写入了 .suo 文件中的流。 对于它编写的每个流，VSPackage 通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A>加载由密钥（即流的名称）标识的特定流回环境。 然后，环境调用 VSPackage 读取传递流的名称和指向方法的`IStream`<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.LoadPackageUserOpts%2A>指针的特定流。

 此时，将发出另一个调用，`LoadUserOptions`以查看是否还有必须读取的 .suo 文件的另一个部分。 此过程将一直持续到环境读取和处理 .suo 文件中的所有数据流。

 保存或关闭解决方案时，环境使用指向 方法的<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence.SavePackageSolutionProps%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.SaveUserOptions%2A>指针调用方法。 `IStream`包含要保存的二进制信息将传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts.WriteUserOptions%2A>方法，该方法然后将信息写入 .suo 文件，然后再次调用`SaveUserOptions`该方法以查看是否有另一个信息流要写入 .suo 文件。

 这两种方法`SaveUserOptions`和`WriteUserOptions`调用，对于要保存到 .suo 文件的每个信息流，将指针传递到 。 `IVsSolutionPersistence` 它们被递归地调用，以允许将多个流写入 .suo 文件。 这样，用户信息将随解决方案一起保留，并保证在下次打开解决方案时会在那里。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- [解决方案](../../extensibility/internals/solutions-overview.md)
