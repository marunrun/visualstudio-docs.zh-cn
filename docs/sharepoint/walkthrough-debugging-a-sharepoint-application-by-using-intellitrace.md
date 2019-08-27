---
title: 调试 SharePoint 应用程序使用 IntelliTrace
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 59407696743b15262db83f915feb075a10e22225
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401040"
---
# <a name="walkthrough-debug-a-sharepoint-application-by-using-intellitrace"></a>演练：使用 IntelliTrace 调试 SharePoint 应用程序

通过使用 IntelliTrace，您可以更轻松地调试 SharePoint 解决方案。 传统的调试器为您提供解决方案的快照仅在当前时刻。 但是，可以使用 IntelliTrace 来查看过去发生在你的解决方案中的事件和它们发生并导航到代码的上下文。

 本演练演示如何使用 Microsoft Monitoring Agent 从已部署应用程序收集 IntelliTrace 数据调试 Visual Studio 中的 SharePoint 2010 或 SharePoint 2013 项目。 若要分析该数据，必须使用 Visual Studio Enterprise。 此项目包含功能接收器的激活该功能时，将任务添加到任务列表和公告到公告列表。 停用该功能后，将任务标记为已完成，并且第二个公告添加到公告列表。 但是，该过程包含一个逻辑错误，阻止项目正常运行。 通过使用 IntelliTrace，您将找到并更正该错误。

 **适用于：** 本主题中的信息适用于 Visual Studio 中创建的 SharePoint 2010 和 SharePoint 2013 解决方案。

 本演练阐释了以下任务：

- [创建功能接收器](#create-a-feature-receiver)

- [将代码添加到功能接收器](#add-code-to-the-feature-receiver)

- [测试项目](#test-the-project)

- [使用 Microsoft Monitoring Agent 收集 IntelliTrace 数据](#collect-intellitrace-data-by-using-microsoft-monitoring-agent)

- [调试并修复 SharePoint 解决方案](#debug-and-fix-the-sharepoint-solution)

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备

你需要以下组件来完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- Visual Studio Enterprise。

## <a name="create-a-feature-receiver"></a>创建功能接收器

首先，创建一个具有功能接收器的空 SharePoint 项目。

1. 创建 SharePoint 2010 或 SharePoint 2013 解决方案项目，并将其命名**IntelliTraceTest**。

     **SharePoint 自定义向导**出现时，你的项目和解决方案的信任级别可以在其中指定 SharePoint 站点。

2. 选择**部署为场解决方案**选项按钮，然后选择**完成**按钮。

     IntelliTrace 仅对场解决方案。

3. 在中**解决方案资源管理器**，打开快捷菜单**功能**节点，然后选择**添加功能**。

     *Feature1.feature*出现。

4. 为 Feature1.feature，打开快捷菜单，然后选择**添加事件接收器**将代码模块添加到该功能。

## <a name="add-code-to-the-feature-receiver"></a>将代码添加到功能接收器

接下来，将代码添加到功能接收器中的两个方法：`FeatureActivated`和`FeatureDeactivating`。 每当激活或停用在 SharePoint 中，分别一项功能时，将触发这些方法。

1. 在顶部`Feature1EventReceiver`类中，添加以下代码，其中声明指定 SharePoint 站点和子站点的变量：

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

2. 将 `FeatureActivated` 方法替换为以下代码：

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

3. 将 `FeatureDeactivating` 方法替换为以下代码：

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

现在，代码添加到功能接收器，并运行数据收集器，部署并运行 SharePoint 解决方案以测试是否正常工作。

> [!IMPORTANT]
> 对于本例，请在 FeatureDeactivating 事件处理程序引发错误。 稍后在本演练中，通过使用数据收集器创建的.iTrace 文件找到此错误。

1. 将解决方案部署到 SharePoint，并在浏览器中打开 SharePoint 站点。

     该功能会自动激活，从而导致其功能接收器添加公告和任务。

2. 显示公告和任务列表的内容。

     公告列表应包含名为的新公告**已激活功能：IntelliTraceTest_Feature1**，并且任务列表中应具有名为的新任务**停用功能：IntelliTraceTest_Feature1**。 如果缺少任一一项时，验证是否已激活该功能。 如果未激活，则将其激活。

3. 通过执行以下步骤停用功能：

   1. 上**站点操作**在 SharePoint 中，菜单中，选择**站点设置**。

   2. 下**站点操作**，选择**管理站点功能**链接。

   3. 下一步**IntelliTraceTest Feature1**，选择**停用**按钮。

   4. 在警告页上选择**停用此功能**链接。

      FeatureDeactivating() 事件处理程序将引发错误。

## <a name="collect-intellitrace-data-by-using-microsoft-monitoring-agent"></a>使用 Microsoft Monitoring Agent 收集 IntelliTrace 数据

如果运行 SharePoint 的系统上安装 Microsoft Monitoring Agent，则可以通过使用 IntelliTrace 返回的泛型信息比更具体的数据来调试 SharePoint 解决方案。 此代理适用 Visual Studio 之外使用 PowerShell cmdlet 以捕获你的 SharePoint 解决方案运行时的调试信息。

> [!NOTE]
> 在本部分中的配置信息是特定于此示例。 有关其他配置选项的详细信息，请参阅[使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)。

1. 正在运行 SharePoint 的计算机上[设置 Microsoft 监视代理并开始监视你的解决方案](../debugger/using-the-intellitrace-stand-alone-collector.md)。

2. 停用功能：

   1. 上**站点操作**在 SharePoint 中，菜单中，选择**站点设置**。

   2. 下**站点操作**，选择**管理站点功能**链接。

   3. 下一步**IntelliTraceTest Feature1**，选择**停用**按钮。

   4. 在警告页上选择**停用此功能**链接。

      出错时 （在这种情况下，由于 FeatureDeactivating() 事件处理程序中引发的错误）。

3. 在 PowerShell 窗口中，运行[Stop-webapplicationmonitoring](http://go.microsoft.com/fwlink/?LinkID=313687)命令以创建.iTrace 文件，停止监视，然后重新启动您的 SharePoint 解决方案。

     **Stop-WebApplicationMonitoring**  *"\<SharePointSite>\\<SharePointAppName\>"*

## <a name="debug-and-fix-the-sharepoint-solution"></a>调试并修复 SharePoint 解决方案

现在您可以在 Visual Studio 查找并修复 SharePoint 解决方案中的错误中查看 IntelliTrace 日志文件。

1. 在 \IntelliTraceLogs 文件夹中，打开 Visual Studio 中的.iTrace 文件。

     **IntelliTrace 摘要**页将出现。 SharePoint 相关 ID (GUID) 不处理了错误，因为出现的未经处理的异常区域**分析**部分。 选择**调用堆栈**按钮如果想要查看发生错误的调用堆栈。

2. 选择**调试异常**按钮。

     如果系统提示，请加载符号文件。 在中**IntelliTrace**窗口中，异常将突出显示为"引发：出现严重错误 ！"。

     在 IntelliTrace 窗口中，选择要显示的代码，失败的异常。

3. 通过打开 SharePoint 解决方案然后注释掉或删除纠正该错误**引发**FeatureDeactivating() 过程顶部的语句。

4. 重新生成 Visual Studio 中的解决方案，然后将它重新部署到 SharePoint。

5. 通过执行以下步骤停用功能：

    1. 上**站点操作**在 SharePoint 中，菜单中，选择**站点设置**。

    2. 下**站点操作**，选择**管理站点功能**链接。

    3. 下一步**IntelliTraceTest Feature1**，选择**停用**按钮。

    4. 在警告页上选择**停用此功能**链接。

6. 打开任务列表中，并确认**状态**停用任务的值为"已完成"并将其**完成百分比**值是 100%。

     现在代码正常运行。

## <a name="see-also"></a>请参阅

- [验证和调试 SharePoint 代码](../sharepoint/verifying-and-debugging-sharepoint-code.md)
- [IntelliTrace](../debugger/intellitrace.md)
- [演练：使用单元测试来验证 SharePoint 代码](/previous-versions/visualstudio/visual-studio-2010/gg599006\(v\=vs.100\))