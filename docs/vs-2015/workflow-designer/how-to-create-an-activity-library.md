---
title: 如何：创建活动库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 1eeebe74-7303-4345-8a83-fe37a26bc84b
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9463e46a7341a7da5c4aa79ae477d6aa0ff0c6cc
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686644"
---
# <a name="how-to-create-an-activity-library"></a>如何：创建活动库
自定义活动用于在工作流中对特定业务流程进行建模。 通过 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中的活动库模板，可使用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 直观地创建这种自定义活动。  
  
### <a name="to-create-a-workflow-activity-library"></a>创建工作流活动库  
  
1. 启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。  
  
2. 上**文件**菜单，依次指向**新建**，然后选择**项目...**.  
  
     **“新建项目”** 对话框随即打开。  
  
3. 在中**项目类型**窗格中，选择**工作流**眖**Visual C#** 项目或**Visual Basic**分组，具体取决于你语言首选项。  
  
4. 在中**模板**窗格中，选择**活动库**。  
  
5. 在中**名称**框中，为你的项目的描述性名称的类型，以使其容易识别。  
  
6. 在中**位置**框中，键入想要保存你的项目，或单击的目录**浏览**以导航到它。  
  
7. 在中**解决方案**框中，键入描述性名称为您的解决方案，然后单击**确定**。  
  
    > [!NOTE]
    > 如果你想要添加到现有解决方案工作流控制台应用程序，打开该解决方案[!INCLUDE[vs2010](../includes/vs2010-md.md)]，右键单击中的解决方案**解决方案资源管理器**，然后选择**添加**，然后**新建项目...** 若要打开**新的项目**对话框。 按照此过程中的上述步骤继续操作。  
  
8. 该项目模板将创建一个 XAML 格式的活动定义。 [!INCLUDE[wfd1](../includes/wfd1-md.md)]将打开并显示自定义活动的画布。  
  
9. 将从活动拖放**工具箱**到设计图面上要包含在自定义活动中。  
  
    > [!CAUTION]
    > 自定义活动的主体中只能有一个子活动；但是，该子活动可以是一个复合活动，如 <xref:System.Activities.Statements.Sequence> 活动或 <xref:System.Activities.Statements.Flowchart> 活动。  
  
## <a name="see-also"></a>请参阅  
 [如何：创建活动](https://msdn.microsoft.com/library/c09b1e99-21b5-4d96-9c04-ec31db3f4436)   
 [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)