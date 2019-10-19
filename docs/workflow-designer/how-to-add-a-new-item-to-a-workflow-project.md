---
title: 工作流设计器：向工作流项目添加新项
ms.date: 06/25/2018
ms.topic: conceptual
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a87efc24ef148600c31dbb07d7517f9235306102
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650416"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>如何：向工作流项目添加新项

创建工作流项目之后，可以将工作流活动、设计器和其他熟悉的 Visual Studio 项添加到项目。

下表列出了可添加到工作流项目的 Windows Workflow Foundation （WF）项：

| “属性” | 描述 |
|-| - |
| 活动 | 由其他活动组成的活动。 选择此项可将相同的 XAML 文件添加到项目中，就像为新项目选择 "**活动库**" 模板时所获得的那样。 有关此过程的详细信息，请参阅[创建工作流项目](creating-a-workflow-project.md)。 |
| 活动设计器 | 用于自定义活动的设计时体验的设计器。 选择此项可将相同文件添加到项目中，就像在为新项目选择 "**活动设计器库**" 模板时所获得的一样。 |
| Code 活动 | 一个采用代码编写执行逻辑的活动。 已为你生成一个源代码文件，该文件带有 <xref:System.Activities.CodeActivity.Execute%2A> 方法的重写。 |
| WCF 工作流服务 | 使用工作流活动生成的 [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] 服务。 选择此项可将相同文件添加到项目中，就像在为新项目选择**WCF 工作流服务应用程序**模板时所获得的一样。 有关此过程的详细信息，请参阅[如何：创建 WCF 工作流服务应用程序](/visualstudio/workflow-designer/creating-a-workflow-project)。 |

## <a name="to-add-a-new-item-to-a-workflow-project"></a>向工作流项目添加新项

1. 在“项目”菜单上，选择“添加新项”。

   此时将打开“添加新项”对话框。

1. 在左侧窗格中，选择 "**工作流**" 类别，然后选择 "工作流项模板"。

   > [!NOTE]
   > 如果看不到**工作流**类别，请首先安装 Visual Studio 的**Windows Workflow Foundation**组件。 有关详细说明，请参阅[安装 Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

1. 在对话框底部的 "**名称**" 框中，输入该项的名称。

1. 选择 "**添加**" 将该项添加到项目。

## <a name="see-also"></a>请参阅

- [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)