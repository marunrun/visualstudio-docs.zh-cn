---
title: 工作流设计器-如何：向工具箱添加活动
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: b3a8a785-5928-457a-8a50-30267e29503d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ebe3f4c3daf5ee3a0f64a0197967b6da62a467b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85815820"
---
# <a name="how-to-add-activities-to-the-toolbox"></a>如何：向工具箱添加活动

可以通过多种不同的方式将活动添加到解决方案中的 " **工具箱** "。 您可以从当前项目中添加活动，也可以从另一个项目或从另一个程序集引用活动。

## <a name="to-add-an-activity-from-within-your-current-project"></a>从当前项目中添加活动

1. 将新的自定义活动添加到当前工作流项目。 有关向项目添加新的自定义活动的详细信息，请参阅 [如何：向工作流项目添加新项](../workflow-designer/how-to-add-a-new-item-to-a-workflow-project.md)。

2. 向活动添加自定义逻辑。

3. 生成项目。 如果生成成功，则会显示 **工具箱** 中名为 "" 的新类别，其中 \<*project name*> 包含包含在该类别中的自定义活动。

    > [!NOTE]
    > 如果重置工具箱中，则将删除自定义活动，即使重新生成解决方案。 若要在重置后通过自定义活动重新填充工具箱，请重启 Visual Studio。

    > [!NOTE]
    > 工具箱只能显示具有给定名称的一个活动。 如果来自不同程序集的两个活动具有相同的类名称，将显示一个活动。

    > [!NOTE]
    > 在编辑器实例间共享应用程序域；如果使用静态变量，也将在编辑器实例间共享它们。 如果这不是所需的行为，应使用一个服务跟踪变量实例。 有关在设计器中使用服务的信息，请参阅 [使用 ModelItem 编辑上下文](/dotnet/framework/windows-workflow-foundation/using-the-modelitem-editing-context) 。

## <a name="to-add-an-activity-from-within-a-different-project"></a>从另一个项目中添加活动

1. 打开包含至少一个工作流项目（自定义活动库项目或定义自定义活动的另一个工作流项目）的解决方案。

2. 生成这两个项目。 如果生成成功，则会显示 **工具箱** 中名为 "" 的新类别，其中 \<*project name*> 包含包含在该类别中的自定义活动。

## <a name="to-add-an-activity-to-the-toolbox-from-an-assembly"></a>从程序集中将活动添加到工具箱

1. 打开工作流解决方案。

2. 从 " **工具** " 菜单中，选择 " **选择工具箱项"**。

3. 在 " **选择工具箱项** " 对话框中，选择 "系统" " **组件** " 选项卡，然后单击 " **浏览** " 导航到包含要添加的自定义活动的程序集。

4. 选择该程序集，然后单击 **"确定"**。 自定义活动组件将添加到组件列表中并自动处于选中状态。

    1. 单击 **“确定”**，关闭对话框。

5. 若要显示工具箱，请在 "**视图**" 菜单中选择 **"工具箱**"。

6. 自定义活动将显示在 "工具箱" 中的 " **工具箱** " 下，该项添加之前处于焦点的类别。 例如，如果在添加工具箱项之前在 "**工具箱**" 中选择了 "**常规**" 类别，则活动将显示在 "**常规**" 类别下。

## <a name="see-also"></a>另请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
