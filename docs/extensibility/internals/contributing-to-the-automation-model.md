---
title: 为自动化模型做出贡献 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK]
ms.assetid: 44de482d-93c8-41a4-843c-cefda995a03e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d660edc740229c3e91b99e1f59eb37b4e9312098
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709273"
---
# <a name="contribute-to-the-automation-model"></a>为自动化模型做出贡献
Visual Studio 提供了一组用于自定义环境的自动化接口。 自动化模型是使最终用户能够创建 Visual Studio 外接程序和扩展的对象模型。

 此外，作为 VSPackage 开发人员，您适合为自动化模型做出贡献;通过执行此操作，可以使 VSPackage 的最终用户创建外接程序，并且通常在 中使用 VSPackage 时[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供一致的用户体验。

 为了使最终用户体验保持一致，您可以在设计 VSPackage 时遵循一组准则，以便 VSPackage 的自动化模型遵循 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的想法。

## <a name="in-this-section"></a>在本节中
- [自动化模型概述](../../extensibility/internals/automation-model-overview.md)

 将自动化模型定义为控制公共环境主要方面的相关对象组。 这组对象在自动化模型的图表中绘制。

- [为 VS 包提供自动化](../../extensibility/internals/providing-automation-for-vspackages.md)

 讨论为 VSPackage 提供自动化的两种主要方法。

- [公开项目对象](../../extensibility/internals/exposing-project-objects.md)

 提供用于创建特定于 VSPackage 对象的分步说明。

- [项目建模](../../extensibility/internals/project-modeling.md)

 解释为新项目类型创建自动化所需的标准项目对象，并说明项目自动化遵循的路径。 本主题还提供类的声明和实现的列表。

- [公开事件](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)

 提供为自动化模型创建事件的分步说明。

- [选项页的自动化支持](../../extensibility/internals/automation-support-for-options-pages.md)

 描述如何通过扩展对象来返回用于支持 **"工具**"菜单上 VSPackage`DTE.Properties`自定义**选项**对话框属性的自动化对象。

- [提供代码自动化](../../extensibility/internals/providing-automation-for-code.md)

 说明不需要为代码创建自动化模型。 但是，本主题中提供了一个链接，该链接提供了代码模型的有见地信息。

- [如何：为 Windows 提供自动化](../../extensibility/internals/how-to-provide-automation-for-windows.md)

 说明，每当您想要在窗口中提供自动化对象，并且环境尚未提供现成的自动化对象时，提供自动化都是一个好主意。 讨论工具窗口和文档窗口的自动化。

- [使用自动化模型](../../extensibility/internals/using-the-automation-model.md)

 提供了两个代码示例，显示自动化使用者如何获取初始项目自动化对象。

- [配置和选定项目的自动化](../../extensibility/internals/automation-for-configuration-and-selecteditem-objects.md)

 提供有关配置和选定项目对象的自动化的信息。

## <a name="reference"></a>参考
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>提供一个代码示例，用于显示 VSPackage 如何参与 DTE 自动化对象模型。 列出参数、返回值和所选备注。
