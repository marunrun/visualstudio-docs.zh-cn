---
title: 使用旧版活动设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- activities, configuring
- custom activities
- Activity Designer
- child activities, adding
- activities, adding child
- activities, creating custom
ms.assetid: 2fea8a05-6e58-423d-94bf-a822b15ffb80
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cd8d18d95fabd858354c625d2c9b32459efc7193
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75846143"
---
# <a name="using-the-legacy-activity-designer"></a>使用旧版活动设计器
本主题介绍如何使用旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中的活动设计器。 在面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 时，请使用旧设计器。

 通过使用 Activity 设计器，可以创建自己的自定义活动。

## <a name="creating-a-custom-activity"></a>创建一个自定义活动
 遵循以下步骤使用 Activity 设计器创建一个自定义活动：

1. 在 " **项目** " 菜单上，单击 " **添加活动**"。

2. 选择 **活动** 或 **活动 (，并) 模板的代码分离 ** 。

   1. 使用 **活动** 模板可以创建一个活动，其中活动定义和用户代码位于同一代码文件中。

   2. 将 **活动 (与代码分离) 模板结合 ** 使用，以创建活动定义以工作流标记形式表示的活动，并在单独的代码文件中使用用户代码。

3. 键入活动名称或保留默认名称，然后单击 " **添加**"。

   还可以创建一组自定义活动，方法是创建一个类型为 " **工作流活动库**" 的新项目。 有关此项目类型的详细信息，请参阅 [如何：创建工作流活动库 (旧) ](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md)。

## <a name="configuring-an-activity"></a>配置活动
 当 Activity 设计器处于活动状态时，可以使用属性浏览器来配置下表中列出的属性。

|属性|注释|
|--------------|--------------|
|**名称**|活动的名称。|
|**基类**|从中派生活动的基类。 默认基类为 [SequenceActivity](https://msdn2.microsoft.com/library/system.workflow.activities.sequenceactivity.aspx)。 在 " **属性** " 窗口中，单击 **基类** 省略号 **[...]** ，以在 " [浏览并选择 .net 类型" 对话框 ](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md)中选择另一个基类 (旧) 。|
|**说明**|用户定义的活动说明。|
|**已启用**|默认情况下，设置为 **True** ，以启用活动执行和验证。 设置为 **False** 将禁用活动执行和验证。 有关活动执行和验证的信息，请参阅 [开发工作流活动](https://msdn2.microsoft.com/library/ms734413.aspx)。|

## <a name="adding-child-activities"></a>添加子活动
 可以将子活动从工具箱拖到正在设计的活动。 然后可以使用属性浏览器配置每个子活动。

## <a name="see-also"></a>另请参阅
 [开发工作流活动](https://msdn2.microsoft.com/library/ms734413.aspx)[创建自定义活动](https://msdn2.microsoft.com/library/bb675228.aspx)[旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)[自定义活动示例](https://msdn2.microsoft.com/library/bb472471.aspx)[如何：创建工作流活动库 (旧) ](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md) [使用旧工作流设计器](../workflow-designer/using-the-legacy-workflow-designer.md)
