---
title: 创建具有关联窗体和启动窗体的工作流
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
ms.openlocfilehash: 7946e48502ea4fd8e9e9382a20de3c8ce25987b3
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984682"
---
# <a name="walkthrough-create-a-workflow-with-association-and-initiation-forms"></a>演练：创建具有关联窗体和启动窗体的工作流
  本演练演示如何创建包含关联和初始窗体使用的基本顺序工作流。 这是一种 ASPX 窗体，当在工作流第一次与 SharePoint 管理员（关联窗体）关联时，以及当用户启动工作流（启动窗体）时，这些参数可以添加到工作流中。

 本演练概述了这样一种情况：用户想要为满足以下要求的支出报表创建审批工作流：

- 当工作流与列表相关联时，会提示管理员输入关联窗体，在该窗体中输入支出报表的美元限制。

- 员工将其支出报表上传到共享文档列表，启动工作流，然后在工作流启动窗体中输入支出总计。

- 如果员工支出报表总数超出了管理员的预定义限制，则会为该员工的经理创建一个任务以批准该支出报表。 但是，如果员工的支出报表总数小于或等于支出限制，则自动批准的消息将写入工作流的历史记录列表。

  本演练阐释了以下任务：

- 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中创建 SharePoint 列表定义顺序工作流项目。

- 创建工作流计划。

- 处理工作流活动事件。

- 创建工作流关联和启动窗体。

- 关联工作流。

- 手动启动工作流。

> [!NOTE]
> 虽然本演练使用顺序工作流项目，但对于状态机工作流，该过程是相同的。
>
> 此外，在以下说明中，计算机可能会为某些 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的用户界面元素显示不同的名称或位置。 你拥有的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 版本和你使用的设置将确定这些元素。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>Prerequisites
 你需要以下组件来完成本演练：

- 支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 和 SharePoint 版本。

- Visual Studio。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目
 首先，在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中创建一个顺序工作流项目。 顺序工作流是按顺序执行的一系列步骤，直到最后一个活动完成。 在此过程中，您将创建一个应用于 SharePoint 中 "共享文档" 列表的顺序工作流。 工作流的向导允许你将工作流与网站或列表定义关联，并使你能够确定工作流的启动时间。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目

1. 在菜单栏上，选择 "**文件**" " > **新建** > **项目**" 以显示 "**新建项目**" 对话框。

2. 展开 "**视觉对象C#**  " 或 " **Visual Basic**" 下的 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

3. 在 "**模板**" 窗格中，选择 " **SharePoint 2010 项目**" 项目模板。

4. 在 "**名称**" 框中，输入**ExpenseReport** ，然后选择 "**确定"** 按钮。

     " **SharePoint 自定义向导**" 随即出现。

5. 在 "**指定用于调试的站点和安全级别**" 页上，选择 "**部署为场解决方案**" 选项按钮，然后选择 "**完成**" 按钮以接受 "信任级别" 和 "默认站点"。

     此步骤还将解决方案的信任级别设置为场解决方案，这是工作流项目的唯一可用选项。

6. 在 **“解决方案资源管理器”** 中，选择项目节点。

7. 在菜单栏上，依次选择“项目” > “添加新项”。

8. 在 "**视觉C#对象**" 或 " **Visual Basic**" 下，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

9. 在 "**模板**" 窗格中，选择 "**顺序工作流（仅场解决方案）** " 模板，然后选择 "**添加**" 按钮。

     " **SharePoint 自定义向导**" 随即出现。

10. 在 "**指定用于调试的工作流名称**" 页上，接受默认名称（**ExpenseReport-workflow1.xaml**）。 保留默认工作流模板类型值（**列表工作流）** 。 选择“下一步”按钮。

11. 在 "**是否希望 Visual Studio 在调试会话中自动关联工作流？"** 页上，清除自动关联工作流模板的框（如果已选中）。

     此步骤允许您手动将工作流与 "共享文档" 列表相关联，后者将显示关联窗体。

12. 选择 "**完成**" 按钮。

## <a name="add-an-association-form-to-the-workflow"></a>向工作流添加关联窗体
 接下来，创建一个。当 SharePoint 管理员第一次将工作流与支出报表文档关联时显示的 ASPX 关联窗体。

#### <a name="to-add-an-association-form-to-the-workflow"></a>向工作流添加关联窗体

1. 在**解决方案资源管理器**中选择 " **workflow1.xaml** " 节点。

2. 在菜单栏上，选择 "**项目** > "**添加新项**"以显示"**添加新项**"对话框。

3. 在 "对话框" 树视图中，展开 **" C#视觉对象**" 或 " **Visual Basic** " （具体取决于您的项目语言），展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

4. 在模板列表中，选择 "**工作流关联窗体**" 模板。

5. 在 "**名称**" 文本框中，输入**ExpenseReportAssocForm**。

6. 选择 "**添加**" 按钮，将窗体添加到项目。

## <a name="designing-and-coding-the-association-form"></a>设计和编码关联窗体
 在此过程中，通过向关联窗体添加控件和代码来向其引入功能。

#### <a name="to-design-and-code-the-association-form"></a>设计关联窗体并对其进行编码

1. 在关联窗体（ExpenseReportAssocForm）中，找到 `ID="Main"`的 `asp:Content` 元素。

2. 直接在此内容元素中的第一行之后添加以下代码，以创建提示输入支出批准限制（*AutoApproveLimit*）的标签和文本框：

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" runat="server" />
    <br /><br />
    ```

3. 展开**解决方案资源管理器**中的**ExpenseReportAssocForm**文件以显示其依赖文件。

    > [!NOTE]
    > 如果项目处于 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]中，则必须选择 "**查看所有文件**" 按钮以执行此步骤。

4. 打开 ExpenseReportAssocForm 文件的快捷菜单，然后选择 "**查看代码**"。

5. 将 `GetAssociationData` 方法替换为：

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

## <a name="add-an-initiation-form-to-the-workflow"></a>向工作流添加启动窗体
 接下来，创建当用户针对其支出报表运行工作流时显示的启动窗体。

#### <a name="to-create-an-initiation-form"></a>创建启动窗体

1. 在**解决方案资源管理器**中选择 " **workflow1.xaml** " 节点。

2. 在菜单栏上，选择 "**项目** > "**添加新项**"，显示"**添加新项**"对话框。

3. 在 "对话框" 树视图中，展开 **" C#视觉对象**" 或 " **Visual Basic** " （具体取决于您的项目语言），展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

4. 在模板列表中，选择 "**工作流启动窗体**" 模板。

5. 在 "**名称**" 文本框中，输入**ExpenseReportInitForm**。

6. 选择 "**添加**" 按钮，将窗体添加到项目。

## <a name="designing-and-coding-the-initiation-form"></a>设计和编码启动窗体
 接下来，向启动窗体添加控件和代码。

#### <a name="to-code-the-initiation-form"></a>编写启动窗体代码

1. 在启动窗体（ExpenseReportInitForm）中，找到包含 `ID="Main"`的 `asp:Content` 元素。

2. 在此 content 元素中的第一行之后，添加以下代码以创建一个标签和文本框，其中显示在关联窗体中输入的支出批准限制（*AutoApproveLimit*），另一个用于提示输入的标签和文本框支出总计（*ExpenseTotal*）：

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" ReadOnly="true" runat="server" />
    <br /><br />
    <asp:Label ID="lblExpenseTotal" Text="Expense Total:" runat="server" />

    <asp:TextBox ID="ExpenseTotal" runat="server" />
    <br /><br />
    ```

3. 展开**解决方案资源管理器**中的**ExpenseReportInitForm**文件以显示其依赖文件。

4. 打开 ExpenseReportInitForm 文件的快捷菜单，然后选择 "**查看代码**"。

5. 将 `Page_Load` 方法替换为以下示例：

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

6. 将 `GetInitiationData` 方法替换为以下示例：

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

## <a name="cutomize-the-workflow"></a>Cutomize 工作流
 接下来，自定义工作流。 稍后，您将两个窗体关联到工作流。

#### <a name="to-customize-the-workflow"></a>自定义工作流

1. 通过在项目中打开 Workflow1.xaml，在工作流设计器中显示工作流。

2. 在 "**工具箱**" 中，展开 " **Windows Workflow 3.0** " 节点，找到 " **IfElse** " 活动。

3. 通过执行以下步骤之一将此活动添加到工作流中：

    - 打开 " **IfElse** " 活动的快捷菜单，选择 "**复制**"，在工作流设计器中的 " **onWorkflowActivated1** " 活动下打开行的快捷菜单，然后选择 "**粘贴**"。

    - 从**工具箱**中拖动**IfElse**活动，并将其连接到工作流设计器中**onWorkflowActiviated1**活动下的行。

4. 在 "工具箱" 中，展开 " **SharePoint 工作流**" 节点并找到 " **CreateTask** " 活动。

5. 通过执行以下步骤之一将此活动添加到工作流中：

    - 打开 " **CreateTask** " 活动的快捷菜单，选择 "**复制**"，在工作流设计器中的 " **IfElseActivity1** " 中，在 "此处" 区域中打开两个 "**删除" 活动**之一的快捷菜单，然后选择 "**粘贴**"。

    - 将 " **CreateTask** " 活动从 "**工具箱**" 拖动到 " **IfElseActivity1**" 中的两个 "**放置活动**" 区域之一。

6. 在 "**属性**" 窗口中，为 " **CorrelationToken** " 属性输入*taskToken*属性值。

7. 展开**CorrelationToken**属性，方法是选择旁边的加号（![树视图](../sharepoint/media/plus.gif "TreeView 加号")）。

8. 选择**OwnerActivityName**子属性上的下拉箭头，并设置*workflow1.xaml*值。

9. 选择**TaskId**属性，然后选择省略号（![ASP.NET Mobile 设计器椭圆形](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）按钮以显示 "**绑定属性**" 对话框。

10. 选择 "**绑定到新成员**" 选项卡，选择 "**创建字段**" 选项按钮，然后选择 "**确定"** 按钮。

11. 选择 "**任务**" 属性，然后选择省略号（"![ASP.NET 移动设计器椭圆形](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")"）按钮以显示 "**绑定属性**" 对话框。

12. 选择 "**绑定到新成员**" 选项卡，选择 "**创建字段**" 选项按钮，然后选择 "**确定"** 按钮。

13. 在 "**工具箱**" 中，展开 " **SharePoint 工作流**" 节点，找到 " **LogToHistoryListActivity** " 活动。

14. 通过执行以下步骤之一将此活动添加到工作流中：

    - 打开 " **LogToHistoryListActivity** " 活动的快捷菜单，选择 "复制"，在工作流设计器中的 " **IfElseActivity1** " 区域中打开其他 "**将** **活动放**入" 区域的快捷菜单，然后选择 "**粘贴"** .

    - 将 " **LogToHistoryListActivity** " 活动从 "**工具箱**" 拖放到 " **IfElseActivity1**" 中的 "其他**放置活动**" 区域。

## <a name="add-code-to-the-workflow"></a>将代码添加到工作流
 接下来，将代码添加到工作流，以使其能够正常工作。

#### <a name="to-add-code-to-the-workflow"></a>将代码添加到工作流

1. 在工作流设计器中打开 " **createTask1** " 活动的快捷菜单，然后选择 "**查看代码**"。

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
    > 在代码中，将 `somedomain\\someuser` 替换为要为其创建任务的域和用户名，如 "`Office\\JoeSch`"。 为了进行测试，最简单的方法是使用正在开发的帐户。

3. 在 `MethodInvoking` 方法下面，添加以下示例：

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

4. 在工作流设计器中，选择 " **ifElseBranchActivity1** " 活动。

5. 在 "**属性**" 窗口中，选择 "**条件**" 属性的下拉箭头，然后设置 "*代码条件*" 值。

6. 展开 "**条件**" 属性，方法是选择旁边的加号（![TreeView plus](../sharepoint/media/plus.gif "TreeView 加号")），然后将其值设置为*checkApprovalNeeded*。

7. 在工作流设计器中，打开 " **logToHistoryListActivity1** " 活动的快捷菜单，然后选择 "**生成处理程序**"，为 `MethodInvoking` 事件生成空方法。

8. 将 `MethodInvoking` 代码替换为以下代码：

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

9. 选择**F5**键以调试程序。

     这会对应用程序进行编译、打包、部署、激活其功能、回收 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] 应用程序池，然后在 "**站点 Url** " 属性中指定的位置启动浏览器。

## <a name="associating-the-workflow-to-the-documents-list"></a>将工作流关联到 "文档" 列表
 接下来，通过将工作流与 SharePoint 站点上的**SharedDocuments**列表关联来显示工作流关联窗体。

#### <a name="to-associate-the-workflow"></a>关联工作流

1. 选择 "快速启动" 栏上的 "**共享文档**" 链接。

2. 选择 "**库工具**" 选项卡上的 "**库**" 链接，然后选择 "**库设置**" 功能区按钮。

3. 在 "**权限和管理**" 部分中，选择 "**工作流设置**" 链接，然后在 "**工作流**" 页上选择 "**添加工作流**" 链接。

4. 在 "工作流设置" 页的顶部列表中，选择 " **ExpenseReport-workflow1.xaml** " 模板。

5. 在下一个字段中，输入**ExpenseReportWorkflow** ，然后选择 "**下一步**" 按钮。

     这会将工作流与**共享文档**列表相关联，并显示工作流关联窗体。

6. 在 "**自动批准限制**" 文本框中，输入**1200** ，然后选择 "**关联工作流**" 按钮。

## <a name="start-the-workflow"></a>启动工作流
 接下来，将工作流关联到 "**共享文档**" 列表中的一个文档，以显示工作流启动窗体。

#### <a name="to-start-the-workflow"></a>启动工作流

1. 在 SharePoint 页上，选择 "**主页**" 按钮。

2. 选择 "快速启动" 栏上的 "**共享文档**" 链接以显示 "**共享文档**" 列表。

3. 选择页面顶部的 "**库工具**" 选项卡上的 "**文档**" 链接，然后选择功能区上的 "**上载文档**" 按钮，将新文档上载到 "**共享文档**" 列表中。

4. 在 "**上载文档**" 对话框中，选择 "**浏览**" 按钮，选择任何文档文件，选择 "**打开**" 按钮，然后选择 "**确定"** 按钮。

     您可以在此对话框中更改文档的设置，但通过选择 "**保存**" 按钮将其保留为默认值。

5. 选择上传的文档，选择显示的下拉箭头，然后选择 "**工作流**" 项。

6. 选择 ExpenseReportWorkflow 旁的图像。

     这将显示工作流启动窗体。 （请注意，"**自动批准限制**" 框中显示的值是只读的，因为它是在关联窗体中输入的。）

7. 在 "**支出合计**" 文本框中，输入**1600**，然后选择 "**启动工作流**" 按钮。

     此时将再次显示 "**共享文档**" 列表。 **将值为** **ExpenseReportWorkflow**的新列添加到工作流刚刚启动的项。

8. 选择上传的文档旁边的下拉箭头，然后选择 "**工作流**" 项以显示 "工作流状态" 页。 选择 "**已完成工作流**" 下的 "**已完成**" 值。 任务列在 "**任务**" 部分下列出。

9. 选择任务的标题以显示其任务详细信息。

10. 返回到**SharedDocuments**列表，并使用同一文档或其他文档重新启动工作流。

11. 在起始页上输入一个小于或等于在 "关联" 页上输入的金额的数量（**1200**）。

     出现这种情况时，会创建历史记录列表中的条目，而不是任务。 该条目显示在工作流 "状态" 页的 "**工作流历史记录**" 部分中。 请注意历史记录事件的 "**结果**" 列中的消息。 它包含在 `logToHistoryListActivity1.MethodInvoking` 事件中输入的文本，其中包括已自动批准的量。

## <a name="next-steps"></a>后续步骤
 可以从以下主题中了解有关如何创建工作流模板的详细信息：

- 若要了解有关 SharePoint 工作流的详细信息，请参阅[Windows SharePoint Services 中的工作流](/previous-versions/office/developer/sharepoint-2010/ms416312(v=office.14))。

## <a name="see-also"></a>请参阅
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [演练：向工作流添加应用程序页](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)
