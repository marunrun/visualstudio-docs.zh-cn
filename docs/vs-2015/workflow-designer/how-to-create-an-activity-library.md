---
title: 如何：创建活动库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 1eeebe74-7303-4345-8a83-fe37a26bc84b
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9dec73d392dc6af74e5daef99bd6d306f7d58409
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662746"
---
# <a name="how-to-create-an-activity-library"></a>如何：创建活动库
自定义活动用于在工作流中对特定业务流程进行建模。 通过 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中的活动库模板，可使用 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 直观地创建这种自定义活动。

### <a name="to-create-a-workflow-activity-library"></a>创建工作流活动库

1. 启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。

2. 在 "**文件**" 菜单上，指向 "**新建**"，然后选择 "**项目 ...** "。

     **“新建项目”** 对话框随即打开。

3. 在 "**项目类型**" 窗格中，根据你的语言首选项，从**视觉C#** 项目或**Visual Basic**分组中选择 "**工作流**"。

4. 在 "**模板**" 窗格中选择 "**活动库**"。

5. 在 "**名称**" 框中，键入项目的描述性名称以便于识别。

6. 在 "**位置**" 框中，键入要保存项目的目录，或者单击 "**浏览**" 导航到该项目。

7. 在 "**解决方案**" 框中，键入解决方案的描述性名称，然后单击 **"确定"** 。

    > [!NOTE]
    > 如果要向现有解决方案添加工作流控制台应用程序，请在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中打开该解决方案，右键单击**解决方案资源管理器**中的解决方案，然后依次选择 "**添加**"、"**新建项目 ...** " 打开 "**新建项目**" 对话框。 按照此过程中的上述步骤继续操作。

8. 该项目模板将创建一个 XAML 格式的活动定义。 [!INCLUDE[wfd1](../includes/wfd1-md.md)]将打开并显示自定义活动的画布。

9. 将活动从**工具箱**拖到设计图面上，以将其包含在您的自定义活动中。

    > [!CAUTION]
    > 自定义活动的主体中只能有一个子活动；但是，该子活动可以是一个复合活动，如 <xref:System.Activities.Statements.Sequence> 活动或 <xref:System.Activities.Statements.Flowchart> 活动。

## <a name="see-also"></a>请参阅
 [如何：创建](https://msdn.microsoft.com/library/c09b1e99-21b5-4d96-9c04-ec31db3f4436)[创建工作流项目](../workflow-designer/creating-a-workflow-project.md)的活动