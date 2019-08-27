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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5755c6a3b4ece5b40c7799d83bdf33966d5c2b3e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855773"
---
# <a name="using-the-legacy-activity-designer"></a>使用旧版活动设计器
本主题介绍如何使用旧 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 中的活动设计器。 在面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 时，请使用旧设计器。  
  
 通过使用 Activity 设计器，可以创建自己的自定义活动。  
  
## <a name="creating-a-custom-activity"></a>创建一个自定义活动  
 遵循以下步骤使用 Activity 设计器创建一个自定义活动：  
  
1. 上**项目**菜单上，单击**添加活动**。  
  
2. 选择**活动**或**Activity （具有单独的代码）** 模板。  
  
   1. 使用**活动**模板来创建一个活动的活动定义和用户代码位于同一代码文件。  
  
   2. 使用**Activity （具有单独的代码）** 模板以创建表示为工作流标记和单独的代码文件中的用户代码的活动定义一个活动。  
  
3. 键入活动名称或保留默认名称，然后单击**添加**。  
  
   此外可以通过创建一个新类型的项目创建一组自定义活动**工作流活动库**。 有关此项目类型的详细信息，请参阅[如何：创建工作流活动库 （旧版）](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md)。  
  
## <a name="configuring-an-activity"></a>配置活动  
 当 Activity 设计器处于活动状态时，可以使用属性浏览器来配置下表中列出的属性。  
  
|属性|注释|  
|--------------|--------------|  
|**名称**|活动的名称。|  
|**基类**|从中派生活动的基类。 默认基类是[SequenceActivity](http://go.microsoft.com/fwlink?LinkID=65020)。 在中**属性**窗口中，单击**基类**省略号 **[...]** 选择中的另一个基类[浏览并选择.NET 类型对话框 （旧版）](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md)。|  
|**说明**|用户定义的活动说明。|  
|**启用**|设置为 **，则返回 True**默认情况下若要启用活动执行和验证。 设置为**False**禁用活动执行和验证。 有关活动执行和验证的信息，请参阅[开发工作流活动](http://go.microsoft.com/fwlink?LinkID=65024)。|  
  
## <a name="adding-child-activities"></a>添加子活动  
 可以将子活动从工具箱拖到正在设计的活动。 然后可以使用属性浏览器配置每个子活动。  
  
## <a name="see-also"></a>请参阅  
 [开发工作流活动](http://go.microsoft.com/fwlink?LinkID=65024)   
 [创建自定义活动](http://go.microsoft.com/fwlink?LinkID=65021)   
 [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)   
 [自定义活动示例](http://go.microsoft.com/fwlink?LinkID=65022)   
 [如何：创建工作流活动库 （旧版）](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md)   
 [使用旧版工作流设计器](../workflow-designer/using-the-legacy-workflow-designer.md)