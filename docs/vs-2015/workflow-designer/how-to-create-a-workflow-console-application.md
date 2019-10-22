---
title: 如何：创建工作流控制台应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 51a2eea7-921c-49f1-b358-68afc27f1ee9
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f1334655f2a8b8587922628664e43784b54ce971
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72604921"
---
# <a name="how-to-create-a-workflow-console-application"></a>如何：创建工作流控制台应用程序
使用 [!INCLUDE[wf](../includes/wf-md.md)] 可为执行系统或人工流程创建工作流。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供用于创建这些工作流的设计图面。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 可用于在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内创建工作流，也可集成到重新承载该设计器的其他应用程序。

 本主题介绍如何使用 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中的 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 在控制台应用程序中创建工作流。

### <a name="to-create-a-workflow-console-application"></a>创建工作流控制台应用程序

1. 启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。

2. 在 "**文件**" 菜单上，指向 "**新建**"，然后选择 "**项目 ...** "。

     **“新建项目”** 对话框随即打开。

3. 在 "**已安装的模板**" 窗格中，从**视觉C#对象**或**Visual Basic**分组选择 "**工作流**"，具体取决于你的首选项。

4. 在中间窗格中，选择 "**工作流控制台应用程序**"。

5. 在 "**名称**" 框中，输入项目的描述性名称以便于识别。

6. 在 "**位置**" 框中，输入要保存项目的目录，或者单击 "**浏览**" 导航到该目录。

7. 在 "**解决方案**" 框中，输入新解决方案的名称。 单击 **"确定"** 以创建该应用程序。

    > [!NOTE]
    > 如果要向现有解决方案添加工作流控制台应用程序，请在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中打开该解决方案，右键单击**解决方案资源管理器**中的解决方案，然后依次选择 "**添加**"、"**新建项目 ...** " 打开 "**新建项目**" 对话框。 按照此过程中的上述步骤继续操作。

8. 该项目模板将在 XAML 中创建一个工作流定义并在源代码中创建控制台应用程序定义。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 将打开并显示所创建工作流的画布。

9. 若要编写工作流，请将活动或其他工作流项从**工具箱**拖到工作流中的设计图面。

## <a name="see-also"></a>请参阅
 [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)