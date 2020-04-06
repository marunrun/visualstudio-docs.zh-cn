---
title: 视觉工作室 2015 SDK 中的源代码控制新增功能 |微软文档
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f90ae3e1d327b10e99713ad28aa2d5a06c0be34b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703400"
---
# <a name="whats-new-in-source-control-for-the-visual-studio-2015-sdk"></a>可视化工作室 2015 SDK 的源代码管理新增功能

在[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]中，可以通过实现源代码管理 VSPackage 提供深度集成的源代码管理解决方案。 本节介绍源代码管理 VS包的功能，并提供实现步骤的概述。

## <a name="the-source-control-vspackage"></a>源代码管理 VS 包

Visual Studio 支持两种类型的源代码管理解决方案。 在所有版本的 Visual Studio 中，您仍然可以集成基于源代码管理插件 API 的插件。 您还可以为源代码管理创建 VSPackage，该路径提供深度集成路径，[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]适用于需要高度复杂和自主的源代码管理解决方案。

VSPackage 几乎可以向 Visual Studio 添加任何类型的功能。 源代码管理 VSPackage 为 Visual Studio 提供了完整的源代码管理功能，从向用户呈现的 UI 到与源代码管理系统的后端通信。

实现源代码管理 VSPackage 需要"全无"策略。 源代码管理 VSPackage 的创建者必须投入大量精力来实现许多源代码管理接口和新的 UI 元素（对话框、菜单和工具栏），以涵盖整个源代码管理功能，以及任何包成功与 Visual Studio 集成所需的接口。

以下步骤概述了实现源代码管理包所需的内容。 有关详细信息，请参阅[创建源代码管理 VS 包](../../extensibility/internals/creating-a-source-control-vspackage.md)。

1. 创建提供专用源代码管理服务的 VSPackage。

2. 在 Visual Studio 提供的源代码管理相关服务中实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2><xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>接口（例如，和接口）。

3. 注册源代码管理 VSPackage。

4. 实现所有源代码管理 UI，包括菜单项、对话框、工具栏和上下文菜单。

5. 所有与源代码管理相关的事件在激活时都会传递到源代码管理 VSackage，并且必须由您的 VSPackage 处理。

6. 源代码管理 VSPackage 必须侦听事件，例如实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>接口的事件以及跟踪项目文档 （TPD） 事件（由<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>接口实现），并采取必要的操作。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [概述](../../extensibility/internals/source-control-integration-overview.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
