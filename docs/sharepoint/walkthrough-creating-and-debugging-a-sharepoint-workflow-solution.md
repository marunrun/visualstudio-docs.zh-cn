---
title: 创建和调试 SharePoint 工作流解决方案
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Workflow.WorkflowConditions
- VS.SharePointTools.Workflow.WorkflowList
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 51682ba54d6a6ae0698ade6bb52d5972cd63111f
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401048"
---
# <a name="walkthrough-create-and-debug-a-sharepoint-workflow-solution"></a>演练：创建和调试 SharePoint 工作流解决方案
  本演练演示如何创建一个基本顺序工作流模板。 工作流检查以确定文档是否已评审的共享的文档库的属性。 如果已查看过该文档，则工作流完成。

 本演练阐释了以下任务：

- 创建 SharePoint 列表定义顺序工作流项目中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

- 创建工作流活动。

- 处理工作流活动事件。

> [!NOTE]
> 尽管本演练使用顺序工作流项目，该过程是相同的状态机工作流项目。
>
> 此外，您的计算机可能会显示不同的名称或位置的某些 Visual Studio 用户界面元素中的以下说明进行操作。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio。

## <a name="add-properties-to-the-sharepoint-shared-documents-library"></a>将属性添加到 SharePoint 的共享的文档库
 若要跟踪的文档中查看状态**共享文档**库中，我们将在我们的 SharePoint 站点上创建共享文档的三个新属性： `Status`， `Assignee`，和`Review Comments`。 我们定义了这些属性中的**Shared Documents**库。

#### <a name="to-add-properties-to-the-sharepoint-shared-documents-library"></a>若要将属性添加到共享 SharePoint 文档库

1. 打开 SharePoint 站点，如 http://\<系统名称 > / SitePages/Home.aspx，Web 浏览器中的。

2. 在快速启动栏上依次选择**SharedDocuments**。

3. 选择**库**上**库工具**功能区，然后选择**创建列**在功能区中创建一个新列的按钮。

4. 命名的列**Document Status**，将其类型设置为**选择 （菜单可供选择）** ，指定以下三个选项，然后选择**确定**按钮：

    - **需要评审**

    - **检查完毕**

    - **更改请求**

5. 创建两个更多的列并将它们命名**代理人**并**评审评论**。 将单行文本，作为代理人列类型和评审评论列类型设置为多行文本。

## <a name="enable-documents-to-be-edited-without-requiring-a-check-out"></a>启用要进行编辑而无需签出文档
 若要测试工作流模板，可以编辑文档而无需签出时容易。在下一步的过程中，您可以配置 SharePoint 站点以进行此操作。

#### <a name="to-enable-documents-to-be-edited-without-checking-them-out"></a>若要启用要进行编辑而不签出文档

1. 在快速启动栏上依次选择**Shared Documents**链接。

2. 上**库工具**功能区中，选择**库**选项卡，然后选择**库设置**按钮以显示**文档库设置**页。

3. 在中**常规设置**部分中，选择**版本控制设置**链接，以显示**版本控制设置**页。

4. 验证的设置**要求文档签出，然后可以编辑这些**是**否**。 如果不是，将其更改为**否**，然后选择**确定**按钮。

5. 关闭浏览器。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目
 顺序工作流是一组按顺序执行，直到最后一个活动完成的步骤。 在此过程中，我们创建一个顺序工作流将应用于我们共享文档的列表。 工作流向导允许您将工作流与站点定义或列表定义相关联，并可以确定工作流将启动。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>若要创建一个 SharePoint 顺序工作流项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上依次选择**文件** > **新建** > **项目**显示**新建项目**对话框。

3. 展开**SharePoint**节点下的**Visual C#** 或**Visual Basic**，然后选择**2010年**节点。

4. 在中**模板**窗格中，选择**SharePoint 2010 项目**模板。

5. 在中**名称**框中，输入**MySharePointWorkflow** ，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。

6. 在中**指定用于调试的网站和安全级别**页上，选择**部署为场解决方案**选项按钮，然后选择**完成**按钮以接受信任级别和默认站点。

     此步骤会将该解决方案的信任级别设置为场解决方案，工作流项目的唯一可用的选项。 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 在中**解决方案资源管理器**，选择项目节点，然后，在菜单栏上选择**项目** > **添加新项**。

8. 下**Visual C#** 或**Visual Basic**，展开**SharePoint**节点，然后选择**2010年**节点。

9. 在中**模板**窗格中，选择**顺序工作流 （仅场解决方案）** 模板，然后选择**添加**按钮。

     **SharePoint 自定义向导**出现。

10. 在中**指定工作流名称来进行调试**页上，接受默认名称 (**MySharePointWorkflow-Workflow1**)。 保留默认工作流模板类型值，**列表工作流**，然后选择**下一步**按钮。

11. 在中**是否希望 Visual Studio 在调试会话中自动关联工作流？** 页上，选择**下一步**按钮以接受所有默认设置。

     此步骤会自动将工作流与共享文档库关联。

12. 在中**指定为工作流的启动方式的条件**页上，保留默认选项中选择**您希望如何启动工作流？** 部分并选择**完成**按钮。

     此页可以指定工作流启动时。 默认情况下，工作流将启动时在用户手动启动它在 SharePoint 或创建工作流所关联到的项时。

## <a name="create-workflow-activities"></a>创建工作流活动
 工作流包含一个或多个*活动*表示要执行的操作。 使用工作流设计器来安排工作流活动。 在此过程中，我们将向工作流添加两个活动：HandleExternalEventActivity 和 OnWorkFlowItemChanged。 这些活动监视中的文档的检查状态**Shared Documents**列表

#### <a name="to-create-workflow-activities"></a>若要创建工作流活动

1. 工作流应显示在工作流设计器。 如果不存在，然后打开**Workflow1.cs**或**Workflow1.vb**中**解决方案资源管理器**。

2. 在设计器中，选择**OnWorkflowActivated1**活动。

3. 在中**属性**窗口中，输入**onWorkflowActivated**旁边**Invoked**属性，然后选择 Enter 键。

     在代码编辑器将打开，并且名为 onWorkflowActivated 的事件处理程序方法添加到 Workflow1 代码文件。

4. 切换回工作流设计器，打开工具箱，然后展开**Windows 工作流 v3.0**节点。

5. 在中**Windows 工作流 v3.0**的节点**工具箱**，执行以下步骤集之一：

    1. 打开快捷菜单**虽然**活动，然后选择**副本**。 在工作流设计器中，打开下方的行的快捷菜单**onWorkflowActivated1**活动，然后选择**粘贴**。

    2. 拖动**虽然**活动从**工具箱**到工作流设计器中，并将该活动连接到下一行**onWorkflowActivated1**活动。

6. 选择**WhileActivity1**活动。

7. 在中**属性**窗口中，将**条件**到代码条件。

8. 展开**条件**属性中，输入**isWorkflowPending**子旁边**条件**属性，然后选择 Enter 键。

     在代码编辑器将打开，并且一个名为 isWorkflowPending 方法添加到 Workflow1 代码文件。

9. 切换回工作流设计器，打开工具箱，然后展开**SharePoint 工作流**节点。

10. 在中**SharePoint 工作流**的节点**工具箱**，执行以下步骤集之一：

    - 打开快捷菜单**OnWorkflowItemChanged**活动，然后选择**副本**。 在工作流设计器中，打开内的行的快捷菜单**whileActivity1**活动，然后选择**粘贴**。

    - 拖动**OnWorkflowItemChanged**活动从**工具箱**到工作流设计器，并将该活动连接到内部行**whileActivity1**活动。

11. 选择**onWorkflowItemChanged1**活动。

12. 在中**属性**窗口中，设置属性下, 表中所示。

    |属性|值|
    |--------------|-----------|
    |**CorrelationToken**|**workflowToken**|
    |**调用**|**onWorkflowItemChanged**|

## <a name="handle-activity-events"></a>处理活动事件
 最后，检查从每个活动文档的状态。 如果文档已审核，已完成工作流。

#### <a name="to-handle-activity-events"></a>若要处理的活动事件

1. 在中*Workflow1.cs*或*Workflow1.vb*，将以下字段添加到顶部`Workflow1`类。 在活动中使用此字段来确定是否已完成工作流。

    ```vb
    Dim workflowPending As Boolean = True
    ```

    ```csharp
    Boolean workflowPending = true;
    ```

2. 将以下方法添加到 `Workflow1` 类。 此方法检查的值`Document Status`要确定是否已评审文档的文档列表的属性。 如果`Document Status`属性设置为`Review Complete`，然后`checkStatus`方法设置`workflowPending`字段**false**来指示工作流已准备好完成。

    ```vb
    Private Sub checkStatus()
        If CStr(workflowProperties.Item("Document Status")) = "Review Complete" Then
            workflowPending = False
        End If
    End Sub
    ```

    ```csharp
    private void checkStatus()
    {
        if ((string)workflowProperties.Item["Document Status"] == "Review Complete")
        workflowPending = false;
    }
    ```

3. 将以下代码添加到`onWorkflowActivated`并`onWorkflowItemChanged`方法来调用`checkStatus`方法。 当工作流启动，则`onWorkflowActivated`方法调用`checkStatus`方法来确定文档是否已评审。 如果它没有经过审核，工作流继续。 当保存文档时，`onWorkflowItemChanged`方法调用`checkStatus`方法再次以确定是否已评审文档。 虽然`workflowPending`字段设置为**true**，工作流将继续运行。

    ```vb
    Private Sub onWorkflowActivated(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub

    Private Sub onWorkflowItemChanged(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub
    ```

    ```csharp
    private void onWorkflowActivated(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }

    private void onWorkflowItemChanged(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }
    ```

4. 将以下代码添加到`isWorkflowPending`方法来检查的状态`workflowPending`属性。 保存文档时，每次**whileActivity1**活动调用`isWorkflowPending`方法。 此方法将检查<xref:System.Workflow.Activities.ConditionalEventArgs.Result%2A>的属性<xref:System.Workflow.Activities.ConditionalEventArgs>对象，以确定是否**WhileActivity1**活动应继续还是完成。 如果该属性设置为 **，则返回 true**，活动继续执行。 否则为在活动完成，则工作流完成。

    ```vb
    Private Sub isWorkflowPending(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ConditionalEventArgs)
        e.Result = workflowPending
    End Sub
    ```

    ```csharp
    private void isWorkflowPending(object sender, ConditionalEventArgs e)
    {
        e.Result = workflowPending;
    }
    ```

5. 保存项目。

## <a name="test-the-sharepoint-workflow-template"></a>测试 SharePoint 工作流模板
 当您启动调试器时[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将工作流模板部署到 SharePoint 服务器并将关联的工作流**Shared Documents**列表。 若要测试的工作流，启动工作流的实例，从文档中**Shared Documents**列表。

#### <a name="to-test-the-sharepoint-workflow-template"></a>若要测试的 SharePoint 工作流模板

1. 在中*Workflow1.cs*或*Workflow1.vb*，设置断点旁边**onWorkflowActivated**方法。

2. 选择**F5**键生成并运行解决方案。

     SharePoint 网站随即出现。

3. 在 SharePoint 中的导航窗格中，选择**Shared Documents**链接。

4. 在中**Shared Documents**页上，选择**文档**链接**库工具**选项卡，然后选择**上载文档**按钮.

5. 在**上载文档**对话框框中，选择**浏览**按钮，选择任何文档文件，选择**打开**按钮，，然后选择**确定**按钮。

     这会将上传到所选的文档**Shared Documents**列表并启动工作流。

6. 在中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，验证，调试器将停止在断点处旁边`onWorkflowActivated`方法。

7. 选择**F5**密钥以继续执行。

8. 可以更改文档设置的但将它们保留默认值现在通过选择**保存**按钮。

     你将返回到**Shared Documents**页的默认 SharePoint Web 站点。

9. 在中**Shared Documents**页上，确认下面的值**MySharePointWorkflow-Workflow1**列设置为**正在进行中**。 这表明工作流正在进行中并且在文档正在等待审阅。

10. 在中**Shared Documents**页上，选择文档，选择箭头，在出现，然后选择**编辑属性**菜单项。

11. 设置**Document Status**到**Review Complete**，然后选择**保存**按钮。

     你将返回到**Shared Documents**页的默认 SharePoint Web 站点。

12. 在中**Shared Documents**页上，确认下面的值**Document Status**列设置为**Review Complete**。 刷新**Shared Documents**页上，并验证下面的值**MySharePointWorkflow-Workflow1**列设置为**已完成**。 这指示已完成工作流和该文档已检查了。

## <a name="next-steps"></a>后续步骤
 您可以了解有关如何从下面这些主题中创建工作流模板的详细信息：

- 若要了解有关 SharePoint 工作流活动的详细信息，请参阅[为 SharePoint Foundation 工作流活动](http://go.microsoft.com/fwlink/?LinkId=178992)。

- 若要了解有关 Windows Workflow Foundation 活动的详细信息，请参阅[System.Workflow.Activities Namespace](http://go.microsoft.com/fwlink/?LinkId=178993)。

## <a name="see-also"></a>请参阅
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
