---
title: 工作流设计器：将新项添加到工作流项目
ms.date: 06/25/2018
ms.topic: conceptual
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 29e4c03eef2a276995890bbd6b723fa457aefde2
ms.sourcegitcommit: ba5e072c9fedeff625a1332f22dcf3644d019f51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432031"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>如何：将新项添加到工作流项目

创建工作流项目后，可以将工作流活动、 设计器和其他熟悉的 Visual Studio 项添加到你的项目。

下表列出了可以添加到工作流项目的 Windows Workflow Foundation (WF) 项：

| 名称 | 描述 |
|-| - |
| 活动 | 由其他活动组成的活动。 选择此项将同一个 XAML 文件添加到项目，选择时要获得**活动库**新项目模板。 有关此过程的详细信息，请参阅[创建工作流项目](creating-a-workflow-project.md)。 |
| 活动设计器 | 用于自定义活动的设计时体验的设计器。 选择此项将相同文件添加到项目，选择时要获得**活动设计器库**新项目模板。 |
| Code 活动 | 一个采用代码编写执行逻辑的活动。 已为你生成一个源代码文件，该文件带有 <xref:System.Activities.CodeActivity.Execute%2A> 方法的重写。 |
| WCF 工作流服务 | 使用工作流活动生成的 [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] 服务。 选择此项将相同文件添加到项目，选择时要获得**WCF 工作流服务应用程序**新项目模板。 有关此过程的详细信息，请参阅[如何：创建 WCF 工作流服务应用程序](/visualstudio/workflow-designer/creating-a-workflow-project)。 |

## <a name="to-add-a-new-item-to-a-workflow-project"></a>向工作流项目添加新项

1. 在“项目”菜单上，选择“添加新项”   。

   此时将打开“添加新项”  对话框。

1. 在左侧窗格中，选择**工作流**类别，并选择工作流项目模板。

   > [!NOTE]
   > 如果没有看到**工作流**类别中，首次安装**Windows Workflow Foundation**组件的 Visual Studio。 有关详细说明，请参阅[安装 Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

1. 输入中的项的名称**名称**对话框底部的框。

1. 选择**添加**将该项添加到项目。

## <a name="see-also"></a>请参阅

- [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)