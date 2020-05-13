---
title: 解决方案概述
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, about solutions
ms.assetid: 3b21e3a1-170a-4485-941e-6b04b7b27886
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 767db749d953855cd5c6f81f356a195c830aa838
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705298"
---
# <a name="solutions-overview"></a>解决方案概述

解决方案是一个或多个项目分组，这些项目协同工作以创建应用程序。 与解决方案相关的项目和状态信息存储在两个不同的解决方案文件中。 [解决方案 （.sln） 文件](solution-dot-sln-file.md)基于文本，可以置于源代码控制之下并在用户之间共享。 [解决方案用户选项 （.suo） 文件](solution-user-options-dot-suo-file.md)是二进制的。 因此，.suo 文件不能置于源代码控制之下，并且包含特定于用户的信息。

任何 VSPackage 都可以写入任一类型的解决方案文件。 由于文件的性质，实现两个不同的接口来写入它们。 接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>将文本信息写入 .sln 文件，<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>并且接口将二进制流写入 .suo 文件。

> [!NOTE]
> 项目不必将自己的条目显式写入解决方案文件中;因此，项目不必将自己的条目显式写入解决方案文件中。环境处理项目的。 因此，除非要专门向解决方案文件添加其他内容，否则无需以这种方式注册 VSPackage。

每个支持解决方案持久性的 VSPackage 使用三<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>个接口：由环境实现并由 VSPackage 调用的接口和`IVsPersistSolutionProps`和`IVsPersistSolutionOpts`，它们都由 VSPackage 实现。 仅当`IVsPersistSolutionOpts`VSPackage 要将私有信息写入 .suo 文件时，才需要实现该接口。

打开解决方案时，将发生以下过程。

1. 环境读取解决方案。

2. 如果环境找到 ，`CLSID`它将加载相应的 VSPackage。

3. 如果加载了 VSPackage，环境将请求`QueryInterface`<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>VSPackage 所需的接口的接口。

   - 从 .sln 文件读取时，环境需要`QueryInterface``IVsPersistSolutionProps`。

   - 从 .suo 文件读取时，环境需要`QueryInterface``IVsPersistSolutionOpts`。

   有关这些文件使用的具体信息，请参阅[解决方案 （。Sln）](../../extensibility/internals/solution-dot-sln-file.md)文件和[解决方案用户选项 （。Suo） 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

> [!NOTE]
> 如果要创建新的解决方案配置，包括两个项目的配置，并且从生成中排除三分之一，则需要使用属性页 UI 或自动化。 不能直接更改解决方案生成管理器配置及其属性，但可以使用自动化模型中 DTE 中的`SolutionBuild`类操作解决方案生成管理器。 有关配置解决方案的详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionOpts>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
