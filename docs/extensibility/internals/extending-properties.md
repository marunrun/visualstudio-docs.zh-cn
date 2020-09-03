---
title: 扩展属性 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7064128c54434b0a7bb8799e62b751e765511c48
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708416"
---
# <a name="extend-properties"></a>扩展属性
" [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **属性** " 窗口是 COM 和 com + 组件的通用属性浏览器，支持所有 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 产品。 " **属性** " 窗口与 `ITypeInfo` 类型信息和 com + 元数据一起使用，以便在集成开发环境 (IDE) 的任何其他窗口中列出当前所选对象的设计时属性。

 可以通过按键盘上的**F4**或选择 "**视图**" 菜单上的 "**属性" 窗口**打开的 "**属性**" 窗口，用于查看和编辑所选对象的独立于配置的、设计时属性和事件。 与解决方案和项目关联的配置相关属性将显示在 [属性页](../../extensibility/internals/property-pages.md)上。 有关详细信息，请 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)。

 ![属性窗口概述](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow") 属性窗口

 本节提供的详细信息与 " **属性** " 窗口的各个区域以及您必须实现并调用以填充窗口的接口相关。

## <a name="in-this-section"></a>本节内容
- [属性窗口概述](../../extensibility/internals/properties-window-overview.md)

 说明 " **属性** " 窗口相对于工具窗口和文档窗口的用途。

- [模板策略和属性窗口](../../extensibility/internals/template-policy-and-the-properties-window.md)

 讨论一个项目如何包含在企业模板项目中，以及该企业模板项目如何强制实施策略。

- [属性窗口字段和接口](../../extensibility/internals/properties-window-fields-and-interfaces.md)

 说明用于确定 " **属性** " 窗口中显示的信息的选择的基础。

- [属性窗口对象列表](../../extensibility/internals/properties-window-object-list.md)

 描述 " **属性** " 窗口对象列表的用途，描述如何，当此列表中的不同对象触发调用时，将通知环境已选择了新的对象。

- [属性窗口按钮](../../extensibility/internals/properties-window-buttons.md)

 说明 " **属性** " 窗口工具栏上显示的四个默认按钮的用途。

- [属性显示网格](../../extensibility/internals/properties-display-grid.md)

 说明在网格中找到属性名称和属性值字段的位置。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 讨论作为 IDE 构建基块的项目 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)

 介绍如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 平台在生成应用程序时对其进行连续测试和调试。

- [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)

 介绍 `IDispatch` 接口，该接口最初旨在支持自动化，提供一种后期绑定机制来访问和检索对象的方法和属性的相关信息。

- [管理应用程序设置 (.NET)](../../ide/managing-application-settings-dotnet.md)

 概述应用程序设置，这些设置使你可以配置应用程序，以便将属性值存储在外部配置文件而不是应用程序的已编译代码中。

- [解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)

 说明如何 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 有效地管理通过解决方案和项目进行开发工作所需的项（如引用、数据连接、文件夹和文件）。

- [扩展 Visual Studio 的其他部分](../../extensibility/extending-other-parts-of-visual-studio.md)

 说明如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 服务创建匹配 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的其余部分的 UI 元素。
