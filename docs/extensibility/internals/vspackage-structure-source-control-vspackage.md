---
title: VS 包结构（源控制 VS 包） |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b3f09b189e1e4b47187586e66c74315ee32495c8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703808"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 结构（源代码管理 VSPackage）

源代码管理包 SDK 提供了创建 VSPackage 的指南，该集成了源代码管理实施者将其源代码管理功能与 Visual Studio 环境集成。 VSPackage 是一个 COM 组件，通常由 Visual Studio 集成开发环境 （IDE） 按需加载，该组件基于包在其注册表条目中通告的服务。 每个 VS 包<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>都必须实现 。 VSPackage 通常使用 Visual Studio IDE 提供的服务，并提供其自己的某些服务。

VSPackage 声明其菜单项并通过 .vsct 文件建立默认项状态。 Visual Studio IDE 显示处于此状态的菜单项，直到加载 VSPackage。 随后，VSPackage 的方法的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>实现被调用以启用或禁用菜单项。

## <a name="source-control-package-characteristics"></a>源代码管理包特性

源代码管理 VSPackage 深度集成到可视化工作室中。 VSPackage 语义包括：

- 通过 VSPackage（`IVsPackage`接口）实现接口

- UI 命令实现（.vsct 文件和接口实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>）

- 在视觉工作室注册 VS 包。

源代码管理 VSPackage 必须与以下其他 Visual Studio 实体通信：

- 项目

- 编辑器

- 解决方案

- Windows

- 正在运行的文档表

### <a name="visual-studio-environment-services-that-may-be-consumed"></a>可能使用的视觉工作室环境服务

<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>

SV注册供应商服务

<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>

<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>

### <a name="vsip-interfaces-implemented-and-called"></a>实现和调用的 VSIP 接口

源代码管理包是 VSPackage，因此可以直接与在 Visual Studio 注册的其他 VSPackage 进行交互。 为了提供源控制功能的全部范围，源代码管理 VSPackage 可以处理项目或 shell 提供的接口。

可视化工作室中的每个项目都必须实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>才能在可视化工作室 IDE 中识别为项目。 但是，此接口对于源代码管理来说不够专业。 预期受源代码管理的项目实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>。 源代码管理 VSPackage 使用此接口查询项目的内容，并为其提供字形和绑定信息（在服务器位置和受源代码控制的项目的磁盘位置之间建立连接所需的信息）。

源代码管理 VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>实现 ，这反过来又允许项目注册自己进行源代码管理并检索其状态字形。

有关源代码管理 VSPackage 必须考虑的接口的完整列表，请参阅[相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)。

## <a name="see-also"></a>请参阅

- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
- [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)
