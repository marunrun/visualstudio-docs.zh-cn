---
title: 创建 & 调试 SharePoint 工作流解决方案
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 65af3cbfc799a90d640579f8eed0e051fd5888f0
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014622"
---
# <a name="walkthrough-create-and-debug-a-sharepoint-workflow-solution"></a>演练：创建和调试 SharePoint 工作流解决方案
  本演练演示如何创建基本的顺序工作流模板。 工作流检查共享文档库的属性，以确定是否已查看文档。 如果文档已评审，则工作流将完成。

 本演练阐释了以下任务：

- 在中创建 SharePoint 列表定义顺序工作流项目 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

- 创建工作流活动。

- 处理工作流活动事件。

> [!NOTE]
> 虽然本演练使用顺序工作流项目，但对于状态机工作流项目，该过程是相同的。
>
> 此外，在以下说明中，计算机可能会为某些 Visual Studio 用户界面元素显示不同的名称或位置。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio。

## <a name="add-properties-to-the-sharepoint-shared-documents-library"></a>将属性添加到 SharePoint 共享文档库
 为了跟踪**共享文档**库中文档的检查状态，我们将为 SharePoint 站点上的共享文档创建三个新属性： `Status` 、 `Assignee` 和 `Review Comments` 。 我们在**共享文档**库中定义这些属性。

#### <a name="to-add-properties-to-the-sharepoint-shared-documents-library"></a>向 SharePoint 共享文档库添加属性

1. 在 Web 浏览器中打开 SharePoint 站点（如 http:// \<system name> /SitePages/Home.aspx）。

2. 在快速启动栏上，选择 " **SharedDocuments**"。

3. 在 "**库工具**" 功能区上选择 "**库**"，然后选择功能区中的 "**创建列**" 按钮，以创建新列。

4. 命名列**文档状态**，将其类型设置为 "**选择" （菜单以进行选择）**，指定以下三个选项，然后选择 **"确定"** 按钮：

    - **需要评审**

    - **评审完成**

    - **请求的更改**

5. 再创建两列，并将其命名为工作**负责人**并**查看注释**。 将 "工作负责人" 列类型设置为单行文本，并将 "查看注释" 列类型设置为多行文本。

## <a name="enable-documents-to-be-edited-without-requiring-a-check-out"></a>允许编辑文档而无需签出
 当可以编辑文档而无需将其签出时，可以更轻松地测试工作流模板。在下一个过程中，您将配置 SharePoint 站点以启用该站点。

#### <a name="to-enable-documents-to-be-edited-without-checking-them-out"></a>允许编辑文档而不签出文档

1. 在快速启动栏上，选择 "**共享文档**" 链接。

2. 在 "**库工具**" 功能区上，选择 "**库**" 选项卡，然后选择 "**库设置**" 按钮以显示 "**文档库设置**" 页。

3. 在 "**常规设置**" 部分中，选择 "**版本控制设置**" 链接以显示 "**版本控制设置**" 页。

4. 验证是否**需要签出文档**才能对其进行编辑 **。** 如果不是，则将其更改为 "**否**"，然后选择 **"确定"** 按钮。

5. 关闭浏览器。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目
 顺序工作流是一组步骤，这些步骤按顺序执行，直到最后一个活动完成。 在此过程中，我们将创建一个将应用于共享文档列表的顺序工作流。 工作流向导允许您将工作流与网站定义或列表定义关联起来，并使您能够确定工作流的启动时间。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，选择 "**文件**"  >  "**新建**  >  **项目**" 以显示 "**新建项目**" 对话框。

3. 展开 " **Visual c #** " 或 " **Visual Basic**" 下的 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

4. 在 "**模板**" 窗格中，选择 " **SharePoint 2010 项目**" 模板。

5. 在 "**名称**" 框中，输入**MySharePointWorkflow** ，然后选择 "**确定"** 按钮。

     " **SharePoint 自定义向导**" 随即出现。

6. 在 "**指定用于调试的站点和安全级别**" 页上，选择 "**部署为场解决方案**" 选项按钮，然后选择 "**完成**" 按钮以接受 "信任级别" 和 "默认站点"。

     此步骤将解决方案的信任级别设置为场解决方案，这是工作流项目的唯一可用选项。 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 在**解决方案资源管理器**中，选择 "项目" 节点，然后在菜单栏上选择 "**项目**" "  >  **添加新项**"。

8. 在 " **Visual c #** " 或 " **Visual Basic**下，展开" **SharePoint** "节点，然后选择" **2010** "节点。

9. 在 "**模板**" 窗格中，选择 "**顺序工作流（仅场解决方案）** " 模板，然后选择 "**添加**" 按钮。

     " **SharePoint 自定义向导**" 随即出现。

10. 在 "**指定用于调试的工作流名称**" 页上，接受默认名称（**MySharePointWorkflow-workflow1.xaml**）。 保留默认工作流模板类型值 "**列表工作流**"，然后选择 "**下一步**" 按钮。

11. 在 "**是否希望 Visual Studio 在调试会话中自动关联工作流？"** 页上，选择 "**下一步**" 按钮接受所有默认设置。

     此步骤会自动将工作流与共享文档库相关联。

12. 在 "**指定工作流的启动方式的条件"** 页上，保留 "**你希望工作流如何启动？"** 部分中选择的默认选项，然后选择 "**完成**" 按钮。

     此页面使你可以指定工作流的启动时间。 默认情况下，当用户在 SharePoint 中手动启动工作流或创建工作流关联的项时，工作流将启动。

## <a name="create-workflow-activities"></a>创建工作流活动
 工作流包含一个或多个表示要执行的操作的*活动*。 使用工作流设计器可以安排工作流的活动。 在此过程中，我们将向工作流添加两个活动： HandleExternalEventActivity 和 OnWorkFlowItemChanged。 这些活动用于监视 "**共享文档**" 列表中文档的检查状态

#### <a name="to-create-workflow-activities"></a>创建工作流活动

1. 工作流应显示在工作流设计器中。 如果不是，则在**解决方案资源管理器**中打开**Workflow1.cs**或**workflow1.xaml。**

2. 在设计器中，选择 " **OnWorkflowActivated1** " 活动。

3. 在 "**属性**" 窗口中，在 "已**调用**" 属性旁边输入**onWorkflowActivated** ，然后选择 enter 键。

     将打开代码编辑器，并将名为 onWorkflowActivated 的事件处理程序方法添加到 Workflow1.xaml 代码文件中。

4. 切换回 "工作流设计器"，打开 "工具箱"，然后展开 " **Windows workflow 3.0** " 节点。

5. 在 "**工具箱**" 的 " **Windows Workflow v3.0** " 节点中，执行以下一组步骤：

    1. 打开 " **While** " 活动的快捷菜单，然后选择 "**复制**"。 在工作流设计器中，打开 " **onWorkflowActivated1** " 活动下的行的快捷菜单，然后选择 "**粘贴**"。

    2. 将 " **While** " 活动从 "**工具箱**" 拖动到工作流设计器，并将该活动连接到 " **onWorkflowActivated1** " 活动下的行。

6. 选择 " **WhileActivity1** " 活动。

7. 在 "**属性**" 窗口中，将 "**条件**" 设置为 "代码条件"。

8. 展开 " **condition** " 属性，在 "子**条件**" 属性旁边输入**isWorkflowPending** ，然后选择 enter 键。

     将打开代码编辑器，并将名为 isWorkflowPending 的方法添加到 Workflow1.xaml 代码文件中。

9. 切换回 "工作流设计器"，打开 "工具箱"，然后展开 " **SharePoint 工作流**" 节点。

10. 在 "**工具箱**" 的 " **SharePoint 工作流**" 节点中，执行以下一组步骤：

    - 打开 " **OnWorkflowItemChanged** " 活动的快捷菜单，然后选择 "**复制**"。 在工作流设计器中，打开 " **whileActivity1** " 活动中的行的快捷菜单，然后选择 "**粘贴**"。

    - 将 " **OnWorkflowItemChanged** " 活动从 "**工具箱**" 拖动到工作流设计器，并将该活动连接到**whileActivity1**活动中的行。

11. 选择 " **onWorkflowItemChanged1** " 活动。

12. 在 "**属性**" 窗口中，设置下表中所示的属性。

    |properties|值|
    |--------------|-----------|
    |**CorrelationToken**|**workflowToken**|
    |**Invoked**|**onWorkflowItemChanged**|

## <a name="handle-activity-events"></a>处理活动事件
 最后，检查每个活动的文档状态。 如果已查看文档，则工作流完成。

#### <a name="to-handle-activity-events"></a>处理活动事件

1. 在*Workflow1.cs*或*workflow1.xaml*中，将以下字段添加到类的顶部 `Workflow1` 。 此字段在活动中用于确定工作流是否已完成。

    ```vb
    Dim workflowPending As Boolean = True
    ```

    ```csharp
    Boolean workflowPending = true;
    ```

2. 将以下方法添加到 `Workflow1` 类。 此方法检查 `Document Status` 文档列表的属性的值，以确定是否已查看文档。 如果将 `Document Status` 属性设置为 `Review Complete` ，则该 `checkStatus` 方法会将字段设置 `workflowPending` 为**false** ，以指示工作流已准备就绪，可以完成操作。

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

3. 将以下代码添加到 `onWorkflowActivated` 和 `onWorkflowItemChanged` 方法，以调用 `checkStatus` 方法。 工作流启动时， `onWorkflowActivated` 方法将调用 `checkStatus` 方法来确定是否已查看文档。 如果尚未查看，工作流将继续。 保存文档后， `onWorkflowItemChanged` 方法 `checkStatus` 再次调用方法以确定是否已查看文档。 当 `workflowPending` 字段设置为**true**时，工作流将继续运行。

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

4. 将以下代码添加到 `isWorkflowPending` 方法以检查属性的状态 `workflowPending` 。 每次保存文档时， **whileActivity1**活动将调用 `isWorkflowPending` 方法。 此方法检查 <xref:System.Workflow.Activities.ConditionalEventArgs.Result%2A> 对象的属性 <xref:System.Workflow.Activities.ConditionalEventArgs> ，以确定**WhileActivity1**活动是否应继续或完成。 如果将属性设置为**true**，则活动将继续。 否则，该活动将完成并完成工作流。

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
 启动调试器时，会将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流模板部署到 SharePoint 服务器，并将工作流与 "**共享文档**" 列表相关联。 若要测试工作流，请从**共享文档**列表的文档中启动工作流的实例。

#### <a name="to-test-the-sharepoint-workflow-template"></a>测试 SharePoint 工作流模板

1. 在*Workflow1.cs*或*workflow1.xaml*中，设置**onWorkflowActivated**方法旁边的断点。

2. 选择**F5**键生成并运行解决方案。

     此时会显示 SharePoint 站点。

3. 在 SharePoint 的导航窗格中，选择 "**共享文档**" 链接。

4. 在 "**共享文档**" 页上，选择 "**库工具**" 选项卡上的 "**文档**" 链接，然后选择 "**上载文档**" 按钮。

5. 在 "**上载文档**" 对话框中，选择 "**浏览**" 按钮，选择任何文档文件，选择 "**打开**" 按钮，然后选择 "**确定"** 按钮。

     这会将所选文档上传到**共享文档**列表并启动工作流。

6. 在中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，验证调试器是否在方法旁边的断点处停止 `onWorkflowActivated` 。

7. 选择**F5**键以继续执行。

8. 您可以在此处更改文档的设置，但现在可以通过选择 "**保存**" 按钮将它们保留为默认值。

     这会返回到默认 SharePoint 网站的 "**共享文档**" 页。

9. 在 "**共享文档**" 页上，验证**MySharePointWorkflow-workflow1.xaml**列下的值是否设置为 "**正在进行**"。 这表示工作流正在进行，并且文档正在等待评审。

10. 在 "**共享文档**" 页上，选择该文档，选择显示的箭头，然后选择 "**编辑属性**" 菜单项。

11. 将 "**文档状态**" 设置为 "**查看完成**"，然后选择 "**保存**" 按钮。

     这会返回到默认 SharePoint 网站的 "**共享文档**" 页。

12. 在 "**共享文档**" 页上，验证 "**文档状态**" 列下的值是否设置为 "**查看完成**"。 刷新 "**共享文档**" 页，并验证 " **MySharePointWorkflow-workflow1.xaml** " 列下的值是否设置为 "**已完成**"。 这表明工作流已完成，并且已查看文档。

## <a name="next-steps"></a>后续步骤
 可以从以下主题中了解有关如何创建工作流模板的详细信息：

- 若要了解有关 SharePoint 工作流活动的详细信息，请参阅[Sharepoint Foundation 的工作流活动](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))。

- 若要详细了解 Windows Workflow Foundation 活动，请参阅[System.object 命名空间](/dotnet/api/system.windows.media.color)。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
