---
title: 使用 IntelliTrace 调试 SharePoint 应用程序
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IntelliTrace [SharePoint development in Visual Studio]
- standalone data collector
- SharePoint development in Visual Studio, IntelliTrace
- data collector
- IntelliTrace
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 041a110ee39ae7711756b8d689bdf68ae2368caf
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015749"
---
# <a name="walkthrough-debug-a-sharepoint-application-by-using-intellitrace"></a>演练：使用 IntelliTrace 调试 SharePoint 应用程序

通过使用 IntelliTrace，你可以更轻松地调试 SharePoint 解决方案。 传统的调试器在当前时间仅为你的解决方案生成快照。 但是，你可以使用 IntelliTrace 来查看解决方案中发生的过去事件以及发生这些事件的上下文，并导航到代码。

 本演练演示如何使用 Microsoft Monitoring Agent 从已部署的应用程序收集 IntelliTrace 数据，从而在 Visual Studio 中调试 SharePoint 2010 或 SharePoint 2013 项目。 若要分析这些数据，必须使用 Visual Studio Enterprise。 此项目合并了功能接收器，在激活该功能后，会将任务添加到 "任务列表" 和 "公告" 列表中。 停用此功能后，该任务将标记为 "已完成"，并将第二个公告添加到 "公告" 列表中。 但是，该过程包含一个逻辑错误，该错误会阻止项目正常运行。 通过使用 IntelliTrace，可以找到并更正错误。

 **适用于：** 本主题中的信息适用于在 Visual Studio 中创建的 SharePoint 2010 和 SharePoint 2013 解决方案。

 本演练阐释了以下任务：

- [创建功能接收器](#create-a-feature-receiver)

- [向功能接收器中添加代码](#add-code-to-the-feature-receiver)

- [测试项目](#test-the-project)

- [使用 Microsoft Monitoring Agent 收集 IntelliTrace 数据](#collect-intellitrace-data-by-using-microsoft-monitoring-agent)

- [调试并修复 SharePoint 解决方案](#debug-and-fix-the-sharepoint-solution)

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- Visual Studio Enterprise。

## <a name="create-a-feature-receiver"></a>创建功能接收器

首先，创建一个具有功能接收器的空 SharePoint 项目。

1. 创建 SharePoint 2010 或 SharePoint 2013 项目，并将其命名为**IntelliTraceTest**。

     此时将显示 " **Sharepoint 自定义向导**"，您可以在其中同时为项目和解决方案的信任级别指定 sharepoint 站点。

2. 选择 "**部署为场解决方案**" 选项按钮，然后选择 "**完成**" 按钮。

     IntelliTrace 仅适用于场解决方案。

3. 在**解决方案资源管理器**中，打开 "**功能**" 节点的快捷菜单，然后选择 "**添加功能**"。

     *Feature1*出现。

4. 打开 Feature1 的快捷菜单，然后选择 "**添加事件接收器**" 将代码模块添加到该功能。

## <a name="add-code-to-the-feature-receiver"></a>将代码添加到功能接收器

接下来，将代码添加到功能接收器中的两个方法： `FeatureActivated` 和 `FeatureDeactivating` 。 每当在 SharePoint 中激活或停用功能时，这些方法都会触发。

1. 在类的顶部 `Feature1EventReceiver` ，添加以下代码，该代码声明用于指定 SharePoint 站点和子站点的变量：

    ```vb
    ' SharePoint site and subsite.
    Private siteUrl As String = "http://localhost"
    Private webUrl As String = "/"
    ```

    ```csharp
    // SharePoint site and subsite.
    private string siteUrl = "http://localhost";
    private string webUrl = "/";
    ```

2. 将 `FeatureActivated`方法替换为以下代码：

    ```vb
    Public Overrides Sub FeatureActivated(ByVal properties As SPFeatureReceiverProperties)
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim announcementsList As SPList = web.Lists("Announcements")
                    Dim taskList As SPList = web.Lists("Tasks")

                    ' Add an announcement to the Announcements list.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Activated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was activated on: " & DateTime.Now.ToString()
                    listItem.Update()

                    ' Add a task to the Task list.
                    Dim newTask As SPListItem = taskList.Items.Add()
                    newTask("Title") = "Deactivate feature: " & Convert.ToString(properties.Definition.DisplayName)
                    newTask.Update()
                End Using
            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try

    End Sub
    ```

    ```csharp
    public override void FeatureActivated(SPFeatureReceiverProperties properties)
    {
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList announcementsList = web.Lists["Announcements"];
                    SPList taskList = web.Lists["Tasks"];

                    // Add an announcement to the Announcements list.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Activated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was activated on: " + DateTime.Now.ToString();
                    listItem.Update();

                    // Add a task to the Task list.
                    SPListItem newTask = taskList.Items.Add();
                    newTask["Title"] = "Deactivate feature: " + properties.Definition.DisplayName;
                    newTask.Update();
                }
            }
        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }

    }
    ```

3. 将 `FeatureDeactivating`方法替换为以下代码：

    ```vb
    Public Overrides Sub FeatureDeactivating(ByVal properties As SPFeatureReceiverProperties)
        ' The following line induces an error to demonstrate debugging.
        ' Remove this line later for proper operation.
        Throw New System.InvalidOperationException("Serious error occurred!")
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim taskList As SPList = web.Lists("Tasks")
                    Dim announcementsList As SPList = web.Lists("Announcements")

                    ' Add an announcement that the feature was deactivated.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Deactivated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was deactivated on: " & DateTime.Now.ToString()
                    listItem.Update()

                    ' Find the task that the feature receiver added to the Task list when the
                    ' feature was activated.
                    Dim qry As New SPQuery()
                    qry.Query = "<Where><Contains><FieldRef Name='Title' /><Value Type='Text'>Deactivate</Value></Contains></Where>"
                    Dim taskItems As SPListItemCollection = taskList.GetItems(qry)

                    For Each taskItem As SPListItem In taskItems
                        ' Mark the task as complete.
                        taskItem("PercentComplete") = 1
                        taskItem("Status") = "Completed"
                        taskItem.Update()
                    Next
                End Using

            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try

    End Sub
    ```

    ```csharp
    public override void FeatureDeactivating(SPFeatureReceiverProperties properties)
    {
        // The following line induces an error to demonstrate debugging.
        // Remove this line later for proper operation.
        throw new System.InvalidOperationException("A serious error occurred!");
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList taskList = web.Lists["Tasks"];
                    SPList announcementsList = web.Lists["Announcements"];

                    // Add an announcement that the feature was deactivated.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Deactivated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was deactivated on: " + DateTime.Now.ToString();
                    listItem.Update();

                    // Find the task that the feature receiver added to the Task list when the
                    // feature was activated.
                    SPQuery qry = new SPQuery();
                    qry.Query = "<Where><Contains><FieldRef Name='Title' /><Value Type='Text'>Deactivate</Value></Contains></Where>";
                    SPListItemCollection taskItems = taskList.GetItems(qry);

                    foreach (SPListItem taskItem in taskItems)
                    {
                        // Mark the task as complete.
                        taskItem["PercentComplete"] = 1;
                        taskItem["Status"] = "Completed";
                        taskItem.Update();
                    }
                }
            }

        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }
    }
    ```

## <a name="test-the-project"></a>测试项目

将代码添加到功能接收器并运行数据收集器后，请部署并运行 SharePoint 解决方案以测试其是否正常工作。

> [!IMPORTANT]
> 在此示例中，FeatureDeactivating 事件处理程序中会引发错误。 稍后在本演练中，您将使用数据收集器创建的 .Itrace 文件来查找此错误。

1. 将解决方案部署到 SharePoint，然后在浏览器中打开 SharePoint 站点。

     此功能自动激活，导致其功能接收器添加公告和任务。

2. 显示 "公告" 和 "任务" 列表的内容。

     "公告" 列表应包含名为 "已**激活" 功能**的新公告： "IntelliTraceTest_Feature1"，并且 "任务" 列表应包含名为 "**停用" 功能**的新任务： "IntelliTraceTest_Feature1"。 如果缺少上述任何一项，请验证该功能是否已激活。 如果未激活，请激活它。

3. 通过执行以下步骤停用此功能：

   1. 在 SharePoint 中的 "**站点操作**" 菜单上，选择 "**站点设置**"。

   2. 在 "**站点操作**" 下，选择 "**管理站点功能**" 链接。

   3. 在 " **IntelliTraceTest Feature1**" 旁边，选择 "**停用**" 按钮。

   4. 在 "警告" 页上，选择 "**停用此功能**" 链接。

      FeatureDeactivating （）事件处理程序引发错误。

## <a name="collect-intellitrace-data-by-using-microsoft-monitoring-agent"></a>使用 Microsoft Monitoring Agent 收集 IntelliTrace 数据

如果在运行 SharePoint 的系统上安装 Microsoft Monitoring Agent，则可以通过使用比 IntelliTrace 返回的一般信息更具体的数据来调试 SharePoint 解决方案。 当 SharePoint 解决方案运行时，代理将使用 PowerShell cmdlet 来捕获调试信息，从而在 Visual Studio 之外工作。

> [!NOTE]
> 本部分中的配置信息特定于此示例。 有关其他配置选项的详细信息，请参阅[使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)。

1. 在运行 SharePoint 的计算机上，[设置 Microsoft Monitoring Agent 并开始监视解决方案](../debugger/using-the-intellitrace-stand-alone-collector.md)。

2. 停用此功能：

   1. 在 SharePoint 中的 "**站点操作**" 菜单上，选择 "**站点设置**"。

   2. 在 "**站点操作**" 下，选择 "**管理站点功能**" 链接。

   3. 在 " **IntelliTraceTest Feature1**" 旁边，选择 "**停用**" 按钮。

   4. 在 "警告" 页上，选择 "**停用此功能**" 链接。

      出现错误（在这种情况下，因为在 FeatureDeactivating （）事件处理程序中引发了错误）。

3. 在 PowerShell 窗口中运行[stop-webapplicationmonitoring](/previous-versions/system-center/powershell/system-center-2012-r2/dn472753(v=sc.20))命令，以创建 .itrace 文件、停止监视和重新启动 SharePoint 解决方案。

     **Stop-webapplicationmonitoring***" \<SharePointSite> \\<SharePointAppName \> "*  

## <a name="debug-and-fix-the-sharepoint-solution"></a>调试并修复 SharePoint 解决方案

现在，你可以在 Visual Studio 中查看 IntelliTrace 日志文件，以查找和修复 SharePoint 解决方案中的错误。

1. 在 \IntelliTraceLogs 文件夹中，在 Visual Studio 中打开 .Itrace 文件。

     此时将显示 " **IntelliTrace 摘要**" 页。 由于未处理错误，因此在**分析**部分的未经处理的异常区域中会出现 SHAREPOINT 相关 ID （GUID）。 如果要查看发生错误的调用堆栈，请选择 "**调用堆栈**" 按钮。

2. 选择 "**调试异常**" 按钮。

     如果系统提示，则加载符号文件。 在**IntelliTrace**窗口中，异常突出显示为 "引发：出现严重错误！"。

     在 "IntelliTrace" 窗口中，选择异常以显示失败的代码。

3. 若要修复此错误，请打开 SharePoint 解决方案，然后注释掉或删除 FeatureDeactivating （）过程顶部的**throw**语句。

4. 在 Visual Studio 中重新生成解决方案，然后将其重新部署到 SharePoint。

5. 通过执行以下步骤停用此功能：

    1. 在 SharePoint 中的 "**站点操作**" 菜单上，选择 "**站点设置**"。

    2. 在 "**站点操作**" 下，选择 "**管理站点功能**" 链接。

    3. 在 " **IntelliTraceTest Feature1**" 旁边，选择 "**停用**" 按钮。

    4. 在 "警告" 页上，选择 "**停用此功能**" 链接。

6. 打开任务列表，并验证 "停用" 任务的 "**状态**" 值是否为 "已完成"，并且其**完成百分比**值为100%。

     代码现在正常运行。

## <a name="see-also"></a>另请参阅

- [验证和调试 SharePoint 代码](../sharepoint/verifying-and-debugging-sharepoint-code.md)
- [IntelliTrace](../debugger/intellitrace.md)
- [演练：使用单元测试验证 SharePoint 代码](/previous-versions/visualstudio/visual-studio-2010/gg599006\(v\=vs.100\))