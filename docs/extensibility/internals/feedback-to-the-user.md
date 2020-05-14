---
title: 向用户的反馈 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user model feedback
- environment, context
- IDE, context
- IDE, user feedback
ms.assetid: 2d472a24-3813-4f5f-9783-b491ad8a71ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 46b9190b16b9aa444384847bf209ccca50c7f768
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708403"
---
# <a name="feedback-to-the-user"></a>向用户的反馈
在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 中，有关可用功能的可视反馈基于用户当前选择和全局选择上下文。 下表列出了在不同的选择上下文中可用的功能。

|选择上下文|可用功能|
|-----------------------|-----------------------------|
|IDE|Global|
|当前产品集|特定于产品|
|活动层次结构|特定于层次结构类型的层次结构类型|
|活动层次结构项|层次结构项类型特定|
|活动文档|特定于文档类型的文档类型|
|最顶层多文档接口 （MDI） 窗口|特定于窗口类型|
|当前选择上下文|选择上下文特定|

 如果只显示用户所需的功能，并不断提供一致的选择和环境上下文反馈，则可以降低 IDE 中的复杂性。 每当 IDE 中打开窗口时，以下规则将适用：

- 如果窗口更改其选择上下文，则选择反馈在窗口中明确指示，**如果显示动态帮助**窗口，则更新以反映当前上下文。

- 如果窗口更改全局选择上下文，则所有特定于上下文的菜单、活动层次结构窗口和应用程序标题栏将更新以反映当前上下文。

- 窗口应在 **"属性"** 窗口中显示当前选择的属性，如果显示，则选择"**属性页"** 对话框。

- 如果窗口不显示属性或更改全局选择上下文，则当窗口不再是 IDE 中的活动窗口时，选择反馈不应保留在窗口中。

- 所有特定于文档的工具窗口都应持续反映活动文档。

- 菜单、工具栏和应用程序标题栏应反映最顶层的多文档接口 （MDI） 客户端窗口。

  例如，当打开可视化基本 Web 应用程序项目中**Web 窗体**的 HTML 视图并用户选择标记`<td>`时，会以下列方式提供反馈：

- 所选内容在活动窗口中指示，并反映在 **"属性"** 窗口中。

- 特定于文档**的工具箱**将更新以反映活动文档。

- 将显示**编辑器**工具栏和 **"表"** 菜单，标题栏将更新以反映 Web 窗体窗口。

- 活动层次结构窗口（通常是**解决方案资源管理器**）及其标题栏更新以反映当前上下文和上下文相关的**项目**菜单命令，现在应用于活动 Web 应用程序项目。

## <a name="see-also"></a>请参阅
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)
- [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)
