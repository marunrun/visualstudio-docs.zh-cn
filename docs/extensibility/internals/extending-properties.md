---
title: 扩展属性 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, providing support
ms.assetid: 68e2cbd4-861c-453f-8c9f-4ab6afc80e67
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee70a4d88dfc6eb1dae5c0d8fba0fb1deb7a7621
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332189"
---
# <a name="extend-properties"></a>扩展属性
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **属性**时段 COM 和 COM + 组件的通用属性浏览器，并且支持所有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]产品。 **属性**窗口适用于`ITypeInfo`类型信息和 COM + 元数据以列出在集成的开发环境 (IDE) 中的任何其他窗口中的当前所选对象的设计时属性。

 **属性**窗口中，也可以通过按打开**F4**键盘，或选择**属性窗口**上**视图**菜单中，用于查看和编辑配置无关的设计时属性和所选对象的事件。 解决方案和项目，与关联的依赖于配置的属性显示在[属性页](../../extensibility/internals/property-pages.md)。 有关详细信息[管理的配置选项](../../extensibility/internals/managing-configuration-options.md)。

 ![属性窗口概述](../../extensibility/internals/media/vspropertieswindow.png "vsPropertiesWindow")属性窗口

 本部分提供关联到的各个区域的详细的信息**属性**窗口和必须实现的接口，然后调用来填充窗口。

## <a name="in-this-section"></a>本节内容
- [属性窗口概述](../../extensibility/internals/properties-window-overview.md)

 说明的用途**属性**相对于工具窗口和文档窗口的窗口。

- [模板策略和属性窗口](../../extensibility/internals/template-policy-and-the-properties-window.md)

 讨论如何在企业模板项目中，包含一个项目，以及如何该企业级模板项目可以强制执行策略。

- [属性窗口字段和接口](../../extensibility/internals/properties-window-fields-and-interfaces.md)

 介绍了所选内容，用于确定在显示的信息的基础**属性**窗口。

- [属性窗口对象列表](../../extensibility/internals/properties-window-object-list.md)

 描述的目的**属性**窗口对象列表中，描述如何，此列表中的不同对象触发时调用，环境将得到通知，已选择一个新的对象。

- [属性窗口按钮](../../extensibility/internals/properties-window-buttons.md)

 说明显示在四个默认按钮的用途**属性**窗口工具栏。

- [显示属性网格](../../extensibility/internals/properties-display-grid.md)

 介绍了其中网格中找到的属性名称和属性值字段。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 讨论项目的构建基块作为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE。

- [编译和生成](../../ide/compiling-and-building-in-visual-studio.md)

 介绍如何使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]持续测试和调试应用程序，在你生成应用的平台。

- [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)

 介绍`IDispatch`接口，它首先设计为支持自动化，提供了一个后期绑定机制来访问和检索有关方法和对象的属性的信息。

- [管理应用程序设置 (.NET)](../../ide/managing-application-settings-dotnet.md)

 提供允许你配置你的应用程序，以便属性值存储在外部配置文件而不是应用程序的已编译的代码中的应用程序设置概述。

- [解决方案和项目](../../ide/solutions-and-projects-in-visual-studio.md)

 介绍了如何[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]有效地管理等的引用、 数据连接、 文件夹和文件所需的开发工作通过解决方案和项目项。

- [扩展 Visual Studio 的其他部分](../../extensibility/extending-other-parts-of-visual-studio.md)

 说明如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 服务创建匹配 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的其余部分的 UI 元素。