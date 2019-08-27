---
title: 使用关联和初始化表单创建工作流
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- SharePoint development in Visual Studio, workflow association forms
- workflows [SharePoint development in Visual Studio]
- association forms [SharePoint development in Visual Studio]
- initiation forms [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, workflow initiation forms
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b64d1c9fbbd81a21ab268dfa29287895bd355197
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401155"
---
# <a name="walkthrough-create-a-workflow-with-association-and-initiation-forms"></a>演练：使用关联和初始化表单创建工作流
  本演练演示如何创建一个基本顺序工作流，其中包含使用关联和初始化窗体。 这些是启用 SharePoint 管理员 （关联窗体），首次关联以及由用户 （启动窗体） 启动工作流时要添加到工作流参数的 ASPX 窗体。

 本演练概述了用户要创建审批工作流的费用报告具有以下要求的方案：

- 在工作流与列表相关联时，在其中它们输入限制为美元的费用报告一个关联窗体提示管理员。

- 员工将其费用报表上载到共享文档列表，启动工作流，然后输入工作流发起窗体中的总费用。

- 如果员工支出报表总数超过了管理员的预定义的限制，一项任务被创建该员工的经理批准费用报表。 不过，如果员工的费用报表总数小于或等于支出限制，已自动批准的消息都写入到工作流的历史记录列表。

  本演练阐释了以下任务：

- 创建 SharePoint 列表定义顺序工作流项目中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

- 创建工作流计划。

- 处理工作流活动事件。

- 创建工作流关联和初始化窗体。

- 将工作流相关联。

- 手动启动工作流。

> [!NOTE]
> 尽管本演练使用顺序工作流项目，该过程是相同的状态机工作流。
>
> 此外，您的计算机可能会显示不同的名称或位置用于某些[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]下列说明中的用户界面元素。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Edition 都可以和你使用的设置确定这些元素。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的版本[!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)]和 SharePoint。

- Visual Studio。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目
 首先，创建一个顺序工作流项目中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 顺序工作流是一系列按顺序执行，直到最后一个活动完成的步骤。 在此过程中，将创建一个适用于在 SharePoint 中的共享文档列表的顺序工作流。 工作流的向导可以将工作流与站点或列表定义相关联，并可以确定工作流将启动。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>若要创建一个 SharePoint 顺序工作流项目

1. 在菜单栏上依次选择**文件** > **新建** > **项目**显示**新建项目**对话框。

2. 展开**SharePoint**节点下的**Visual C#** 或**Visual Basic**，然后选择**2010年**节点。

3. 在中**模板**窗格中，选择**SharePoint 2010 项目**项目模板。

4. 在中**名称**框中，输入**ExpenseReport** ，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。

5. 在中**指定用于调试的网站和安全级别**页上，选择**部署为场解决方案**选项按钮，然后选择**完成**按钮以接受信任级别和默认站点。

     此步骤还将解决方案的信任级别设置为场解决方案，这是工作流项目的唯一可用的选项。

6. 在 **“解决方案资源管理器”** 中，选择项目节点。

7. 在菜单栏上，依次选择“项目”   > “添加新项”  。

8. 下**Visual C#** 或**Visual Basic**，展开**SharePoint**节点，然后选择**2010年**节点。

9. 在中**模板**窗格中，选择**顺序工作流 （仅场解决方案）** 模板，然后选择**添加**按钮。

     **SharePoint 自定义向导**出现。

10. 在中**指定工作流名称来进行调试**页上，接受默认名称 (**ExpenseReport-Workflow1**)。 保留默认工作流模板类型值 (**列表工作流)** 。 选择“下一步”按钮  。

11. 在中**是否希望 Visual Studio 在调试会话中自动关联工作流？** 页上，清除自动关联工作流模板，如果选中此框。

     此步骤能让您手动将具有更高版本上的共享文档列表的工作，但该流关联窗体将显示相关联。

12. 选择**完成**按钮。

## <a name="add-an-association-form-to-the-workflow"></a>添加到工作流关联窗体
 接下来，创建。ASPX SharePoint 管理员首先将工作流关联的费用报告文档时显示的关联窗体。

#### <a name="to-add-an-association-form-to-the-workflow"></a>若要添加到工作流关联窗体

1. 选择**Workflow1**中的节点**解决方案资源管理器**。

2. 在菜单栏上依次选择**项目** > **添加新项**以显示**添加新项**对话框。

3. 在对话框中树视图中，展开**Visual C#** 或**Visual Basic** （具体取决于项目语言），展开**SharePoint**节点，然后选择**2010年**节点。

4. 在模板列表中，选择**工作流关联窗体**模板。

5. 在中**名称**文字框中，输入**ExpenseReportAssocForm.aspx**。

6. 选择**添加**按钮将窗体添加到项目。

## <a name="designing-and-coding-the-association-form"></a>设计和编码关联窗体
 在此过程中，通过向其添加控件和代码引入到关联窗体的功能。

#### <a name="to-design-and-code-the-association-form"></a>设计和编码关联窗体

1. 在关联窗体 (ExpenseReportAssocForm.aspx) 中找到`asp:Content`元素具有`ID="Main"`。

2. 此内容元素中的第一行，后面直接添加以下代码来创建标签和文本框中提示输入费用审批限额 (*AutoApproveLimit*):

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" runat="server" />
    <br /><br />
    ```

3. 展开**ExpenseReportAssocForm.aspx**中的文件**解决方案资源管理器**以显示其依赖的文件。

    > [!NOTE]
    > 如果你的项目处于[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]，必须选择**视图的所有文件**按钮以执行此步骤。

4. 打开 ExpenseReportAssocForm.aspx 文件的快捷菜单，然后选择**查看代码**。

5. 替换为`GetAssociationData`方法：

    ```vb
    Private Function GetAssociationData() As String
        ' TODO: Return a string that contains the association data that
        ' will be passed to the workflow. Typically, this is in XML
        ' format.
        Return Me.AutoApproveLimit.Text
    End Function
    ```

    ```csharp
    private string GetAssociationData()
    {
        // TODO: Return a string that contains the association data that
        // will be passed to the workflow. Typically, this is in XML
        // format.
        return this.AutoApproveLimit.Text;
    }
    ```

## <a name="add-an-initiation-form-to-the-workflow"></a>初始化窗体添加到工作流
 接下来，创建显示用户针对其费用报表在运行工作流时的启动窗体。

#### <a name="to-create-an-initiation-form"></a>若要创建初始化窗体

1. 选择**Workflow1**中的节点**解决方案资源管理器**。

2. 在菜单栏上依次选择**项目** > **添加新项**显示**添加新项**对话框。

3. 在对话框中树视图中，展开**Visual C#** 或**Visual Basic** （具体取决于项目语言），展开**SharePoint**节点，然后选择**2010年**节点。

4. 在模板列表中，选择**工作流发起窗体**模板。

5. 在中**名称**文字框中，输入**ExpenseReportInitForm.aspx**。

6. 选择**添加**按钮将窗体添加到项目。

## <a name="designing-and-coding-the-initiation-form"></a>设计和编码初始化窗体
 接下来，通过向其添加控件和代码引入到初始化窗体的功能。

#### <a name="to-code-the-initiation-form"></a>若要启动窗体的代码

1. 在初始化窗体 (ExpenseReportInitForm.aspx) 中找到`asp:Content`元素，其中包含`ID="Main"`。

2. 直接在此内容元素中的第一行，后面添加以下代码来创建标签和文本框中显示的费用审批限制 (*AutoApproveLimit*) 关联窗体和另一个标签中输入的和文本框中，提示输入费用总计 (*ExpenseTotal*):

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" ReadOnly="true" runat="server" />
    <br /><br />
    <asp:Label ID="lblExpenseTotal" Text="Expense Total:" runat="server" />

    <asp:TextBox ID="ExpenseTotal" runat="server" />
    <br /><br />
    ```

3. 展开**ExpenseReportInitForm.aspx**中的文件**解决方案资源管理器**以显示其依赖的文件。

4. 打开 ExpenseReportInitForm.aspx 文件的快捷菜单，然后选择**查看代码**。

5. 替换为`Page_Load`方法替换下面的示例：

    ```vb
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As
      EventArgs) Handles Me.Load
        InitializeParams()
        Me.AutoApproveLimit.Text = workflowList.WorkflowAssociations(New
          Guid(associationGuid)).AssociationData
        ' Optionally, add code here to pre-populate your form fields.
    End Sub
    ```

    ```csharp
    protected void Page_Load(object sender, EventArgs e)
    {
        InitializeParams();
        this.AutoApproveLimit.Text =
          workflowList.WorkflowAssociations[new
          Guid(associationGuid)].AssociationData;
    }
    ```

6. 替换为`GetInitiationData`方法替换下面的示例：

    ```vb
    ' This method is called when the user clicks the button to start the workflow.
    Private Function GetInitiationData() As String
        Return Me.ExpenseTotal.Text
        ' TODO: Return a string that contains the initiation data that
        ' will be passed to the workflow. Typically, this is in XML
        ' format.
        Return String.Empty
    End Function
    ```

    ```csharp
    // This method is called when the user clicks the button to start the workflow.
    private string GetInitiationData()
    {
        // TODO: Return a string that contains the initiation data that
        // will be passed to the workflow. Typically, this is in XML
        // format.
        return this.ExpenseTotal.Text;
    }
    ```

## <a name="cutomize-the-workflow"></a>自定义工作流
 接下来，自定义工作流。 更高版本，将关联到工作流的两种形式。

#### <a name="to-customize-the-workflow"></a>若要自定义工作流

1. 通过在项目中打开 Workflow1 的工作流设计器中显示工作流。

2. 在中**工具箱**，展开**Windows 工作流 v3.0**节点并找到**IfElse**活动。

3. 将此活动添加到工作流中，通过执行以下步骤之一：

    - 打开快捷菜单**IfElse**活动中，选择**副本**，打开下方的行的快捷菜单**onWorkflowActivated1**活动在工作流设计器然后选择**粘贴**。

    - 拖动**IfElse**活动从**工具箱**，并将其连接到下一行**onWorkflowActiviated1**工作流设计器中的活动。

4. 在工具箱中，展开**SharePoint 工作流**节点并找到**CreateTask**活动。

5. 将此活动添加到工作流中，通过执行以下步骤之一：

    - 打开快捷菜单**CreateTask**活动中，选择**副本**，打开两种状态之一的快捷菜单**在此处放置活动**中的区**IfElseActivity1**在工作流设计器中，然后选择**粘贴**。

    - 拖动**CreateTask**活动从**工具箱**拖动到一个两个**在此处放置活动**中的区**IfElseActivity1**。

6. 在中**属性**窗口中，输入的属性值为*taskToken*有关**CorrelationToken**属性。

7. 展开**CorrelationToken**属性通过选择加号 (![TreeView 加号](../sharepoint/media/plus.gif "TreeView 加号")) 旁边。

8. 在选择下拉箭头**OwnerActivityName**子属性，并设置*Workflow1*值。

9. 选择**TaskId**属性，然后选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆")) 按钮以显示**绑定属性**对话框。

10. 选择**绑定到新成员**选项卡上，选择**创建字段**选项按钮，然后选择**确定**按钮。

11. 选择**TaskProperties**属性，然后选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆")) 按钮以显示**将属性绑定**对话框。

12. 选择**绑定到新成员**选项卡上，选择**创建字段**选项按钮，然后选择**确定**按钮。

13. 在中**工具箱**，展开**SharePoint 工作流**节点，并找到**LogToHistoryListActivity**活动。

14. 将此活动添加到工作流中，通过执行以下步骤之一：

    - 打开快捷菜单**LogToHistoryListActivity**活动中，选择**副本**，打开快捷菜单，其他**在此处放置活动**内区域**IfElseActivity1**在工作流设计器中，然后选择**粘贴**。

    - 拖动**LogToHistoryListActivity**活动从**工具箱**，并将其放到另**在此处放置活动**内的区域**IfElseActivity1**.

## <a name="add-code-to-the-workflow"></a>将代码添加到工作流
 接下来，将代码添加到要为其提供功能的工作流。

#### <a name="to-add-code-to-the-workflow"></a>若要将代码添加到工作流

1. 打开快捷菜单**createTask1**活动在工作流设计器中，然后选择**查看代码**。

2. 添加以下方法：

    ```vb
    Private Sub createTask1_MethodInvoking(ByVal sender As
      System.Object, ByVal e As System.EventArgs)
        createTask1_TaskId1 = Guid.NewGuid
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser"
        createTask1_TaskProperties1.Description = "Please approve the
          expense report"
        createTask1_TaskProperties1.Title = "Expense Report Approval
          Needed"
    End Sub
    ```

    ```csharp
    private void createTask1_MethodInvoking(object sender, EventArgs e)
    {
        createTask1_TaskId1 = Guid.NewGuid();
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser";
        createTask1_TaskProperties1.Description = "Please approve the
          expense report";
        createTask1_TaskProperties1.Title = "Expense Report Approval
          Needed";
    }
    ```

    > [!NOTE]
    > 在代码中，替换`somedomain\\someuser`使用为其将在创建任务，例如，域和用户名称"`Office\\JoeSch`"。 对于测试是最容易使用开发时所用的帐户。

3. 下面`MethodInvoking`方法中，添加下面的示例：

    ```vb
    Private Sub checkApprovalNeeded(ByVal sender As Object, ByVal e As
      ConditionalEventArgs)
        Dim approval As Boolean = False
        If (Convert.ToInt32(workflowProperties.InitiationData) >
          Convert.ToInt32(workflowProperties.AssociationData)) Then
            approval = True
        End If
        e.Result = approval
    End Sub
    ```

    ```csharp
    private void checkApprovalNeeded(object sender, ConditionalEventArgs
      e)
    {
        bool approval = false;
        if (Convert.ToInt32(workflowProperties.InitiationData) >
          Convert.ToInt32(workflowProperties.AssociationData))
        {
            approval = true;
        }
        e.Result = approval;
    }
    ```

4. 在工作流设计器中，选择**ifElseBranchActivity1**活动。

5. 在中**属性**窗口中，选择的下拉箭头**条件**属性，且然后将设置*代码条件*值。

6. 展开**条件**属性通过选择加号 (![TreeView 加号](../sharepoint/media/plus.gif "TreeView 加号")) 旁边，然后将其值设置为*checkApprovalNeeded*.

7. 在工作流设计器中，打开快捷菜单**logToHistoryListActivity1**活动，然后选择**生成处理程序**生成的空方法`MethodInvoking`事件。

8. 替换为`MethodInvoking`以下代码：

    ```vb
    Private Sub logToHistoryListActivity1_MethodInvoking(ByVal sender As
      System.Object, ByVal e As System.EventArgs)
        Me.logToHistoryListActivity1.HistoryOutcome = ("Expense was auto
          approved for " + workflowProperties.InitiationData)
    End Sub
    ```

    ```csharp
    private void logToHistoryListActivity1_MethodInvoking(object sender,
      EventArgs e)
    {
        this.logToHistoryListActivity1.HistoryOutcome = "Expense was
          auto approved for " + workflowProperties.InitiationData;
    }
    ```

9. 选择**F5**键调试程序。

     这可以编译应用程序、 将其打包，将其部署、 激活其功能、 回收[!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)]应用程序池，并在指定位置处的浏览器然后开始**站点 Url**属性。

## <a name="associating-the-workflow-to-the-documents-list"></a>将关联到文档列表工作流
 接下来，通过将相关联的工作流中显示工作流关联窗体**SharedDocuments** SharePoint 站点上的列表。

#### <a name="to-associate-the-workflow"></a>关联工作流

1. 选择**Shared Documents**快速启动栏上的链接。

2. 选择**库**链接**库工具**选项卡，然后选择**库设置**功能区按钮。

3. 在中**权限和管理**部分中，选择**工作流设置**链接，然后选择**添加工作流**链接**的工作流**页。

4. 在顶部列表中的工作流设置页中，选择**ExpenseReport-Workflow1**模板。

5. 在下一步的字段中，输入**ExpenseReportWorkflow** ，然后选择**下一步**按钮。

     这将与流相关联**Shared Documents**列表并显示工作流关联窗体。

6. 中**自动 Approval Limit**文字框中，输入**1200年**，然后选择**关联工作流**按钮。

## <a name="start-the-workflow"></a>启动工作流
 接下来，将工作流中的文档之一相关联**Shared Documents**列表以显示工作流发起窗体。

#### <a name="to-start-the-workflow"></a>若要启动工作流

1. 在 SharePoint 页上，选择**主页**按钮。

2. 选择**Shared Documents**若要显示的快速启动栏上的链接**Shared Documents**列表。

3. 选择**文档**链接**库工具**页上，顶部选项卡，然后选择**上载文档**功能区上传到新的文档上的按钮**Shared Documents**列表。

4. 在**上载文档**对话框框中，选择**浏览**按钮，选择任何文档文件，选择**打开**按钮，，然后选择**确定**按钮。

     可以更改此对话框中的文档的设置，但将它们保留默认值通过选择**保存**按钮。

5. 选择已上传的文档，然后选择下拉箭头，在出现，然后选择**工作流**项。

6. 选择 ExpenseReportWorkflow 旁边的图像。

     这会显示工作流发起窗体。 (请注意，在显示的值**自动批准限制**框是只读的因为它已在关联窗体中输入。)

7. 在**总费用**文字框中，输入**1600年**，然后选择**启动工作流**按钮。

     这将显示**Shared Documents**再次列出。 名为的新列**ExpenseReportWorkflow**的值**Completed**添加到只需启动工作流的项。

8. 选择已上传的文档旁边的下拉箭头，然后选择**工作流**项目以显示工作流状态页。 选择**Completed**值下**完成工作流**。 任务列入**任务**部分。

9. 选择要显示其任务的详细信息的任务的标题。

10. 返回到**SharedDocuments**列出和重新启动工作流，使用同一文档或另一个。

11. 小于或等于关联页上输入量的启动页上输入的金额 (**1200年**)。

     当发生这种情况时，而不是一项任务创建历史记录列表中的条目。 该项显示在**工作流历史记录**工作流状态页部分。 请注意中的消息**结果**的历史记录事件的列。 它包含在输入的文本`logToHistoryListActivity1.MethodInvoking`事件，其中包括量，这是自动批准。

## <a name="next-steps"></a>后续步骤
 您可以了解有关如何从下面这些主题中创建工作流模板的详细信息：

- 若要了解有关 SharePoint 工作流的详细信息，请参阅[Windows SharePoint Services 中的工作流](http://go.microsoft.com/fwlink/?LinkID=166275)。

## <a name="see-also"></a>请参阅
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [演练：将应用程序页添加到工作流](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)
