---
title: 扩展属性 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708416"
---
# <a name="extend-properties"></a>扩展属性
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**属性**窗口是 COM 和 COM+ 组件的通用属性浏览器，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]支持所有产品。 **属性**窗口使用`ITypeInfo`类型信息和 COM+ 元数据来列出集成开发环境 （IDE） 中任何其他窗口中当前选定对象的设计时属性。

 属性**窗口**可通过按键盘上的**F4**或 **"视图"** 菜单上的 **"属性窗口**"打开，用于查看和编辑与配置无关的设计时间属性和选定对象的事件。 与配置相关的属性（与解决方案和项目关联）显示在[属性页上](../../extensibility/internals/property-pages.md)。 有关详细信息，[管理配置选项](../../extensibility/internals/managing-configuration-options.md)。

 ![属性窗口概述](../../extensibility/internals/media/vspropertieswindow.png "vs属性窗口")属性窗口

 本节提供的详细信息，这些信息与**属性**窗口的各个区域以及要填充窗口而必须实现和调用的接口有关。

## <a name="in-this-section"></a>在本节中
- [属性窗口概述](../../extensibility/internals/properties-window-overview.md)

 解释"**属性"** 窗口相对于工具窗口和文档窗口的用途。

- [模板策略和属性窗口](../../extensibility/internals/template-policy-and-the-properties-window.md)

 讨论项目如何包含在企业模板项目中，以及企业模板项目如何强制实施策略。

- [属性窗口字段和接口](../../extensibility/internals/properties-window-fields-and-interfaces.md)

 解释确定 **"属性"** 窗口中显示的信息的选择基础。

- [属性窗口对象列表](../../extensibility/internals/properties-window-object-list.md)

 描述**属性**窗口对象列表的用途，描述当来自此列表的不同对象触发调用时，如何通知环境已选择新对象。

- [属性窗口按钮](../../extensibility/internals/properties-window-buttons.md)

 解释 **"属性"** 窗口工具栏上显示的四个默认按钮的用途。

- [属性显示网格](../../extensibility/internals/properties-display-grid.md)

 说明在网格中找到属性名称和属性值字段的位置。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 将项目作为 IDE 的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]构建基块进行讨论。

- [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)

 描述如何在构建应用程序时使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]该平台进行持续测试和调试应用程序。

- [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)

 描述首先`IDispatch`用于支持自动化的接口，它提供了一个后期绑定机制来访问和检索有关对象的方法和属性的信息。

- [管理应用程序设置 (.NET)](../../ide/managing-application-settings-dotnet.md)

 提供应用程序设置的概述，这些设置允许您配置应用程序，以便属性值存储在外部配置文件中，而不是应用程序的编译代码中。

- [解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)

 说明如何通过[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]解决方案和项目有效地管理项目，如引用、数据连接、文件夹和文件。

- [扩展视觉工作室的其他部分](../../extensibility/extending-other-parts-of-visual-studio.md)

 说明如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 服务创建匹配 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的其余部分的 UI 元素。
