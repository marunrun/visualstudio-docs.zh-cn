---
title: 什么是 Visual Studio 2015 sdk 的源代码管理中的新增功能 |Microsoft Docs
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio SDK], source control
- source control [Visual Studio SDK], what's new
ms.assetid: bcf85418-18fb-4824-9dae-d14bf3d56a77
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e12776c21d345d60992eeff4963498bcd7d56678
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323252"
---
# <a name="whats-new-in-source-control-for-the-visual-studio-2015-sdk"></a>什么是 Visual Studio 2015 SDK 的源代码管理中的新增功能

在[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]，可以通过实现源代码管理 VSPackage 提供深度集成的源代码控制解决方案。 本部分介绍的源代码管理 Vspackage 功能并提供实现步骤的概述。

## <a name="the-source-control-vspackage"></a>源代码管理 VSPackage

Visual Studio 支持两种类型的源代码管理解决方案。 在所有版本的 Visual Studio 中，仍可以集成源控件插件 API 基于插件。 您还可以创建用于提供深度集成的源代码管理 VSPackage[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]路径适用于要求高的复杂程度和自主性的源代码管理解决方案。

VSPackage 可以将几乎所有类型的功能都添加到 Visual Studio。 源代码管理 VSPackage 提供完整的源代码控制功能的 Visual Studio 中，从到与源代码管理系统的后端通信的用户显示的 UI。

实现源代码管理 VSPackage 需要一个"全或无"的策略。 源代码管理 VSPackage 的创建者必须投入大量的精力实现大量的源代码控制接口和新 UI 元素 （对话框、 菜单和工具栏） 以覆盖整个源控件功能及介面集成所需的任何包已成功使用 Visual Studio。

以下步骤为提供所需实现源代码管理包的一般概述。 有关详细信息，请参阅[创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)。

1. 创建提供专用源控制服务的 VSPackage。

2. 在 Visual Studio 提供的源控件相关服务实现接口 (例如，<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>接口)。

3. 注册您的源代码管理 VSPackage。

4. 实现所有的源代码管理 UI，包括菜单项、 对话框、 工具栏和上下文菜单。

5. 所有源控件相关的事件都传递给您的源代码管理 VSackage 时它处于活动状态，并且必须由你的 VSPackage。

6. 您的源代码管理 VSPackage 必须侦听事件，例如那些实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>接口以及跟踪项目文档 (TPD) 的事件 (由实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>接口) 并采取必要措施。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- [概述](../../extensibility/internals/source-control-integration-overview.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)