---
title: 如何：向工具箱添加活动 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: b3a8a785-5928-457a-8a50-30267e29503d
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 0aa6a76555a18c142acb8759b1bc71d56e9d7dcd
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690941"
---
# <a name="how-to-add-activities-to-the-toolbox"></a>如何：向工具箱添加活动
可以将活动添加到**工具箱**几种不同方式在解决方案中。 您可以从当前项目中添加活动，也可以从另一个项目或从另一个程序集引用活动。  
  
### <a name="to-add-an-activity-from-within-your-current-project"></a>从当前项目中添加活动  
  
1. 将新的自定义活动添加到当前工作流项目。 [!INCLUDE[crabout](../includes/crabout-md.md)] 将新的自定义活动添加到你的项目，请参阅[如何：将新项添加到工作流项目](../workflow-designer/how-to-add-a-new-item-to-a-workflow-project.md)。  
  
2. 向活动添加自定义逻辑。  
  
3. 生成项目。 如果生成成功中的新类别**工具箱**名为"\<*项目名称*>"将显示该类别中包含的自定义活动。  
  
    > [!NOTE]
    > 如果重置工具箱中，则将删除自定义活动，即使重新生成解决方案。 要在重置后使用自定义活动重新填充工具箱，请重新启动 [!INCLUDE[vs2010](../includes/vs2010-md.md)]。  
  
    > [!NOTE]
    > 工具箱只能显示具有给定名称的一个活动。 如果来自不同程序集的两个活动具有相同的类名称，将显示一个活动。  
  
    > [!NOTE]
    > 在编辑器实例间共享应用程序域；如果使用静态变量，也将在编辑器实例间共享它们。 如果这不是所需的行为，应使用一个服务跟踪变量实例。 请参阅[使用 ModelItem 编辑上下文](https://msdn.microsoft.com/library/7f9f1ea5-0147-4079-8eca-be94f00d3aa1)有关使用在设计器中的服务的信息。  
  
### <a name="to-add-an-activity-from-within-a-different-project"></a>从另一个项目中添加活动  
  
1. 打开包含至少一个工作流项目（自定义活动库项目或定义自定义活动的另一个工作流项目）的解决方案。  
  
2. 生成这两个项目。 如果生成成功中的新类别**工具箱**名为"\<*项目名称*>"将显示该类别中包含的自定义活动。  
  
### <a name="to-add-an-activity-to-the-toolbox-from-an-assembly"></a>从程序集中将活动添加到工具箱  
  
1. 打开工作流解决方案。  
  
2. 从**工具**菜单中，选择**选择工具箱项...**.  
  
3. 在中**选择工具箱项**对话框中，选择**System.Activities 组件**选项卡，然后单击**浏览...** 若要导航到包含你想要添加的自定义活动的程序集。  
  
4. 选择程序集，然后单击**确定**。 自定义活动组件将添加到组件列表中并自动处于选中状态。  
  
    1. 单击**确定**关闭对话框。  
  
5. 若要显示工具箱中，选择**工具箱**从**视图**菜单。  
  
6. 自定义活动将显示在**工具箱**之前添加了项中焦点所在的类别下。 例如，如果**常规**类别中选择了**工具箱**之前添加工具箱项，该活动将显示在**常规**类别。  
  
## <a name="see-also"></a>请参阅  
 [使用工作流设计器](../workflow-designer/using-the-workflow-designer.md)