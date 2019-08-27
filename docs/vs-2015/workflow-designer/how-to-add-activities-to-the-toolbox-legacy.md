---
title: 如何：将活动添加到工具箱 （旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- Toolbox, adding activities
- activities, adding to Toolbox
ms.assetid: b66ea29c-120b-40ba-8a61-c1c8240850fa
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c3a8c6f397bbafdbdb29ecbb193c4200a26335c3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943352"
---
# <a name="how-to-add-activities-to-the-toolbox-legacy"></a>如何：向工具箱添加活动（旧版）
在生成的旧工作流解决方案时[!INCLUDE[wfd1](../includes/wfd1-md.md)]面向[!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)]或[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]，可以将自定义活动添加到工作流项目并将它们的设计器置于**工具箱**的简单访问权限。 您还可以直接添加活动**工具箱**从动态链接库 (DLL)。  
  
### <a name="to-add-an-activity-to-the-toolbox-from-a-dll"></a>从 DLL 中将活动添加到工具箱  
  
1. 右键单击下方的工具箱窗口界面**Windows 工作流**，然后单击**选择项**。  
  
2. 在中**选择工具箱项**对话框中，单击**System.Activities 组件**选项卡，然后依次**浏览**从窗口的右下角。  
  
3. 从包含要添加到的自定义活动实现的文件目录中选择 DLL**工具箱**，然后单击**打开**。  
  
4. 单击**确定**以完成将活动添加到工具箱。  
  
## <a name="see-also"></a>请参阅  
 [使用旧版活动设计器](../workflow-designer/using-the-legacy-activity-designer.md)   
 [旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)