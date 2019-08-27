---
title: 如何：创建工作流控制台应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 51a2eea7-921c-49f1-b358-68afc27f1ee9
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a436027fc4194f762fc4b28545fdf5d4bd3b95b6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444609"
---
# <a name="how-to-create-a-workflow-console-application"></a>如何：创建工作流控制台应用程序
使用 [!INCLUDE[wf](../includes/wf-md.md)] 可为执行系统或人工流程创建工作流。 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 提供用于创建这些工作流的设计图面。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 可用于在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内创建工作流，也可集成到重新承载该设计器的其他应用程序。  
  
 本主题介绍如何使用 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中的 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 在控制台应用程序中创建工作流。  
  
### <a name="to-create-a-workflow-console-application"></a>创建工作流控制台应用程序  
  
1. 启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。  
  
2. 上**文件**菜单，依次指向**新建**，然后选择**项目...**.  
  
     **“新建项目”** 对话框随即打开。  
  
3. 在**已安装的模板**窗格中，选择**工作流**眖**Visual C#** 或者**Visual Basic**分组，具体取决于你语言首选项。  
  
4. 在中间窗格中，选择**工作流控制台应用程序**。  
  
5. 在中**名称**框中，输入您的项目以使其容易识别的描述性名称。  
  
6. 在中**位置**框中，输入想要保存你的项目，或者单击的目录**浏览**以导航到它。  
  
7. 在中**解决方案**框中，输入新解决方案的名称。 单击**确定**创建应用程序。  
  
    > [!NOTE]
    > 如果你想要添加到现有解决方案工作流控制台应用程序，打开该解决方案[!INCLUDE[vs2010](../includes/vs2010-md.md)]，右键单击中的解决方案**解决方案资源管理器**，然后选择**添加**，然后**新建项目...** 若要打开**新的项目**对话框。 按照此过程中的上述步骤继续操作。  
  
8. 该项目模板将在 XAML 中创建一个工作流定义并在源代码中创建控制台应用程序定义。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 将打开并显示所创建工作流的画布。  
  
9. 若要编写工作流，将活动或其他工作流项从**工具箱**到您的工作流中的设计图面。  
  
## <a name="see-also"></a>请参阅  
 [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)