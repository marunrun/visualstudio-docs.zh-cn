---
title: Using the Legacy Activity Designer | Microsoft Docs
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
ms.openlocfilehash: a13aeeb3394ee6b8896376c0e7d520b90fb56fa6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302825"
---
# <a name="using-the-legacy-activity-designer"></a>使用旧版活动设计器
本主题介绍如何使用旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中的活动设计器。 在面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 时，请使用旧设计器。

 通过使用 Activity 设计器，可以创建自己的自定义活动。

## <a name="creating-a-custom-activity"></a>创建一个自定义活动
 遵循以下步骤使用 Activity 设计器创建一个自定义活动：

1. On the **Project** menu, click **Add Activity**.

2. Select the **Activity** or **Activity (with code separation)** template.

   1. Use the **Activity** template to create an activity with the activity definition and the user code in same code file.

   2. Use the **Activity (with code separation)** template to create an activity with the activity definition expressed as workflow markup and the user code in a separate code file.

3. Type an activity name or keep the default name, and then click **Add**.

   You can also create a set of custom activities by creating a new project of type **Workflow Activity Library**. For more information about this project type, see [How to: Create a Workflow Activity Library (Legacy)](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md).

## <a name="configuring-an-activity"></a>配置活动
 当 Activity 设计器处于活动状态时，可以使用属性浏览器来配置下表中列出的属性。

|Property|注释|
|--------------|--------------|
|**名称**|活动的名称。|
|**Base Class**|从中派生活动的基类。 The default base class is [SequenceActivity](https://go.microsoft.com/fwlink?LinkID=65020). In the **Properties** window, click the **Base Class** ellipses **[…]** to select another base class in the [Browse and Select a .NET Type Dialog Box (Legacy)](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md).|
|**描述**|用户定义的活动说明。|
|**启用**|Set to **True** by default to enable activity execution and validation. Set to **False** to disable activity execution and validation. For information about activity execution and validation, see [Developing Workflow Activities](https://go.microsoft.com/fwlink?LinkID=65024).|

## <a name="adding-child-activities"></a>添加子活动
 可以将子活动从工具箱拖到正在设计的活动。 然后可以使用属性浏览器配置每个子活动。

## <a name="see-also"></a>请参阅
 [Developing Workflow Activities](https://go.microsoft.com/fwlink?LinkID=65024) [Creating Custom Activities](https://go.microsoft.com/fwlink?LinkID=65021) [Legacy Workflow Activities](../workflow-designer/legacy-workflow-activities.md) [Custom Activities Samples](https://go.microsoft.com/fwlink?LinkID=65022) [How to: Create a Workflow Activity Library (Legacy)](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md) [Using the Legacy Workflow Designer](../workflow-designer/using-the-legacy-workflow-designer.md)