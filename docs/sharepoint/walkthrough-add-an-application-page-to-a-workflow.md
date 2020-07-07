---
title: 演练：向工作流添加应用程序页 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, adding applications page to workflow
- application page [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f54914e6676e0cc2400fa04ebb089fac08f58c3c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015492"
---
# <a name="walkthrough-add-an-application-page-to-a-workflow"></a>演练：向工作流添加应用程序页
  本演练演示如何将显示从工作流派生的数据的应用程序页添加到工作流项目中。 它基于主题[演练：创建具有关联和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)中所述的项目。

 本演练演示了下列任务：

- 将 ASPX 应用程序页添加到 SharePoint 工作流项目。

- 从工作流项目中获取数据并对其进行操作。

- 在应用程序页上的表中显示数据。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 和 SharePoint 版本。

- Visual Studio。

- 还需要完成主题[演练：创建具有关联和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)中的项目。

## <a name="ammend-the-workflow-code"></a>Ammend 工作流代码
 首先，将一行代码添加到工作流，以便将 "结果" 列的值设置为支出报表的金额。 此值稍后会在支出报表汇总计算中使用。

#### <a name="to-set-the-value-of-the-outcome-column-in-the-workflow"></a>设置工作流中的结果列的值

1. 从主题[演练：创建具有关联和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md) [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

2. 打开*Workflow1.cs*或*workflow1.xaml*的代码（取决于编程语言）。

3. 在该方法的底部 `createTask1_MethodInvoking` ，添加以下代码：

    ```vb
    createTask1_TaskProperties1.ExtendedProperties("Outcome") =
      workflowProperties.InitiationData
    ```

    ```csharp
    createTask1_TaskProperties1.ExtendedProperties["Outcome"] =
      workflowProperties.InitiationData;
    ```

## <a name="create-an-application-page"></a>"创建应用程序" 页
 接下来，将 ASPX 窗体添加到项目。 此窗体将显示从费用报表工作流项目中获取的数据。 为此，你将添加一个应用程序页。 应用程序页使用与其他 SharePoint 页相同的母版页，这意味着它将与 SharePoint 站点上的其他页类似。

#### <a name="to-add-an-application-page-to-the-project"></a>向项目添加应用程序页

1. 选择 ExpenseReport 项目，然后在菜单栏上选择 "项目" " **Project**  >  **添加新项**"。

2. 在 "**模板**" 窗格中，选择 "**应用程序" 页**模板，使用项目项的默认名称（**ApplicationPage1**），然后选择 "**添加**" 按钮。

3. 在 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ApplicationPage1 的中，将 `PlaceHolderMain` 节替换为以下内容：

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
        <asp:Label ID="Label1" runat="server" Font-Bold="True"
            Text="Expenses that exceeded allotted amount" Font-Size="Medium"></asp:Label>
        <br />
        <asp:Table ID="Table1" runat="server">
        </asp:Table>
    </asp:Content>
    ```

     此代码会将表与标题一起添加到页面中。

4. 通过将部分替换为以下内容，将标题添加到应用程序页 `PlaceHolderPageTitleInTitleArea` ：

    ```aspx-csharp
    <asp:Content ID="PageTitleInTitleArea" ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server" >
        Expense Report Summary
    </asp:Content>
    ```

## <a name="code-the-application-page"></a>编写应用程序页面代码
 接下来，将代码添加到支出报表摘要应用程序页。 当打开该页面时，代码会扫描 SharePoint 中的任务列表，以获取超出分配的支出限制的支出。 该报表将列出每个项以及费用的总和。

#### <a name="to-code-the-application-page"></a>编写应用程序页面代码

1. 选择 " **ApplicationPage1** " 节点，然后在菜单栏上选择 "**查看**  >  **代码**" 以在应用程序页后显示代码。

2. 在类的顶部，将**using**或**Import**语句替换为以下内容：

    ```vb
    Imports System
    Imports Microsoft.SharePoint
    Imports Microsoft.SharePoint.WebControls
    Imports System.Collections
    Imports System.Data
    Imports System.Web.UI
    Imports System.Web.UI.WebControls
    Imports System.Web.UI.WebControls.WebParts
    Imports System.Drawing
    Imports Microsoft.SharePoint.Navigation
    ```

    ```csharp
    using System;
    using Microsoft.SharePoint;
    using Microsoft.SharePoint.WebControls;
    using System.Collections;
    using System.Data;
    using System.Web.UI;
    using System.Web.UI.WebControls;
    using System.Web.UI.WebControls.WebParts;
    using System.Drawing;
    using Microsoft.SharePoint.Navigation;
    ```

3. 将以下代码添加到 `Page_Load` 方法中：

    ```vb
    Try
        ' Reference the Tasks list on the SharePoint site.
        ' Replace "TestServer" with a valid SharePoint server name.
        Dim site As SPSite = New SPSite("http://TestServer")
        Dim list As SPList = site.AllWebs(0).Lists("Tasks")
        ' string text = "";
        Dim sum As Integer = 0
        Table1.Rows.Clear()
        ' Add table headers.
        Dim hr As TableHeaderRow = New TableHeaderRow
        hr.BackColor = Color.LightBlue
        Dim hc1 As TableHeaderCell = New TableHeaderCell
        Dim hc2 As TableHeaderCell = New TableHeaderCell
        hc1.Text = "Expense Report Name"
        hc2.Text = "Amount Exceeded"
        hr.Cells.Add(hc1)
        hr.Cells.Add(hc2)
        ' Add the TableHeaderRow as the first item
        ' in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr)
        ' Iterate through the tasks in the Task list and collect those
        ' that have values in the "Related Content" and "Outcome" fields
        ' - the fields written to when expense approval is required.
        For Each item As SPListItem In list.Items
            Dim s_relContent As String = ""
            Dim s_outcome As String = ""
            Try
                ' Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related Content")
                s_outcome = item.GetFormattedValue("Outcome")
            Catch erx As System.Exception
                ' Task does not have fields - skip it.
                Continue For
            End Try
            ' Convert amount to an int and keep a running total.
            If (Not String.IsNullOrEmpty(s_relContent) And Not
              String.IsNullOrEmpty(s_outcome)) Then
                sum = (sum + Convert.ToInt32(s_outcome))
                Dim relContent As TableCell = New TableCell
                relContent.Text = s_relContent
                Dim outcome As TableCell = New TableCell
                outcome.Text = ("$" + s_outcome)
                Dim dataRow2 As TableRow = New TableRow
                dataRow2.Cells.Add(relContent)
                dataRow2.Cells.Add(outcome)
                Table1.Rows.Add(dataRow2)
            End If
        Next
        ' Report the sum of the reports in the table footer.
        Dim tfr As TableFooterRow = New TableFooterRow
        tfr.BackColor = Color.LightGreen
        ' Create a TableCell object to contain the
        ' text for the footer.
        Dim ftc1 As TableCell = New TableCell
        Dim ftc2 As TableCell = New TableCell
        ftc1.Text = "TOTAL: "
        ftc2.Text = ("$" + Convert.ToString(sum))
        ' Add the TableCell object to the Cells
        ' collection of the TableFooterRow.
        tfr.Cells.Add(ftc1)
        tfr.Cells.Add(ftc2)
        ' Add the TableFooterRow to the Rows
        ' collection of the table.
        Table1.Rows.Add(tfr)
    Catch errx As Exception
        System.Diagnostics.Debug.WriteLine(("Error: " + errx.ToString))
    End Try
    ```

    ```csharp
    try
    {
        // Reference the Tasks list on the SharePoint site.
        // Replace "TestServer" with a valid SharePoint server name.
        SPSite site = new SPSite("http://TestServer");
        SPList list = site.AllWebs[0].Lists["Tasks"];

        // string text = "";
        int sum = 0;

        Table1.Rows.Clear();

        // Add table headers.
        TableHeaderRow hr = new TableHeaderRow();
        hr.BackColor = Color.LightBlue;
        TableHeaderCell hc1 = new TableHeaderCell();
        TableHeaderCell hc2 = new TableHeaderCell();
        hc1.Text = "Expense Report Name";
        hc2.Text = "Amount Exceeded";
        hr.Cells.Add(hc1);
        hr.Cells.Add(hc2);
        // Add the TableHeaderRow as the first item
        // in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr);

        // Iterate through the tasks in the Task list and collect those
        // that have values in the "Related Content" and "Outcome"
        // fields - the fields written to when expense approval is
        // required.
        foreach (SPListItem item in list.Items)
        {
            string s_relContent = "";
            string s_outcome = "";

            try
            {
                // Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related
                  Content");
                s_outcome = item.GetFormattedValue("Outcome");
            }
            catch
            {
                // Task does not have fields - skip it.
                continue;
            }

            if (!String.IsNullOrEmpty(s_relContent) &&
              !String.IsNullOrEmpty(s_outcome))
            {
                // Convert amount to an int and keep a running total.
                sum += Convert.ToInt32(s_outcome);
                TableCell relContent = new TableCell();
                relContent.Text = s_relContent;
                TableCell outcome = new TableCell();
                outcome.Text = "$" + s_outcome;
                TableRow dataRow2 = new TableRow();
                dataRow2.Cells.Add(relContent);
                dataRow2.Cells.Add(outcome);
                Table1.Rows.Add(dataRow2);
            }
        }

        // Report the sum of the reports in the table footer.
           TableFooterRow tfr = new TableFooterRow();
        tfr.BackColor = Color.LightGreen;

        // Create a TableCell object to contain the
        // text for the footer.
        TableCell ftc1 = new TableCell();
        TableCell ftc2 = new TableCell();
        ftc1.Text = "TOTAL: ";
        ftc2.Text = "$" + Convert.ToString(sum);

        // Add the TableCell object to the Cells
        // collection of the TableFooterRow.
        tfr.Cells.Add(ftc1);
        tfr.Cells.Add(ftc2);

        // Add the TableFooterRow to the Rows
        // collection of the table.
        Table1.Rows.Add(tfr);
    }

    catch (Exception errx)
    {
        System.Diagnostics.Debug.WriteLine("Error: " + errx.ToString());
    }
    ```

    > [!WARNING]
    > 请确保在代码中将 "TestServer" 替换为运行 SharePoint 的有效服务器的名称。

## <a name="test-the-application-page"></a>测试应用程序页
 接下来，确定应用程序页是否正确显示了支出数据。

#### <a name="to-test-the-application-page"></a>测试应用程序页

1. 选择**F5**键以运行项目并将其部署到 SharePoint。

2. 选择 "**主页**" 按钮，然后选择 "快速启动" 栏上的 "**共享文档**" 链接，以显示 SharePoint 站点上的 "共享文档" 列表。

3. 若要表示此示例的费用报表，请选择页面顶部的 " **LibraryTools** " 选项卡上的 "**文档**" 链接，并选择工具功能区上的 "**上载文档**" 按钮，将一些新文档上载到 "文档" 列表中。

4. 上传一些文档后，可通过选择页面顶部的 " **LibraryTools** " 选项卡上的**库**链接，然后选择工具功能区上的 "**库设置**" 按钮来实例化工作流。

5. 在 "**文档库设置**" 页中，选择 "**权限和管理**" 部分中的 "**工作流设置**" 链接。

6. 在 "**工作流设置**" 页中，选择 "**添加工作流**" 链接。

7. 在 "**添加工作流**" 页面中，选择 " **ExpenseReport-workflow1.xaml** " 工作流，输入工作流的名称（例如 " **ExpenseTest**"），然后选择 "**下一步**" 按钮。

    此时将显示工作流关联窗体。 使用它报告支出限制金额。

8. 在关联窗体中，在 "**自动批准限制**" 框中输入**1000** ，然后选择 "**关联工作流**" 按钮。

9. 选择 "**主页**" 按钮返回到 SharePoint 主页。

10. 选择 "快速启动" 栏上的 "**共享文档**" 链接。

11. 选择其中一个已上传的文档以显示下拉箭头，选择它，然后选择 "**工作流**" 项。

12. 选择 ExpenseTest 旁的图像以显示工作流启动窗体。

13. 在 "**支出合计**" 文本框中，输入大于1000的值，然后选择 "**启动工作流**" 按钮。

     如果报告的支出超出分配的支出金额，则会将任务添加到任务列表。 已**完成**值为**ExpenseTest**的列也会添加到 "共享文档" 列表中的 "费用报表" 项。

14. 在 "共享文档" 列表中对其他文档重复步骤 11-13。 （确切的文档数并不重要。）

15. 通过在 Web 浏览器中打开以下 URL 来显示 "费用报表摘要应用程序" 页： **Http://**<em>SystemName</em>**/_layouts/expensereport/applicationpage1.aspx**。

     "费用报表摘要" 页列出超出了分配金额的所有支出报表、它们超过了的金额以及所有报表的总金额。

## <a name="next-steps"></a>后续步骤
 有关 SharePoint 应用程序页的详细信息，请参阅[为 Sharepoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

 若要详细了解如何使用 Visual Studio 中的 Visual Web Designer 设计 SharePoint 页面内容，请参阅以下主题：

- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)。

- [为 web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>另请参阅

- [演练：创建具有关联窗体和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)