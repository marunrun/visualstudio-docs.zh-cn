---
title: 演练：分析 SharePoint 应用程序 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, profiling
- performance testing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, performance testing
- profiling [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 27024f3b28b97a1a5d0befc3d70dbf8144fb9e24
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77277648"
---
# <a name="walkthrough-profile-a-sharepoint-application"></a>演练：分析 SharePoint 应用程序
  本演练演示在 Visual Studio 中如何使用分析工具优化 SharePoint 应用程序的性能。 此示例应用程序是 SharePoint 功能事件接收器，其中包含降低功能事件接收器性能的空闲循环。 Visual Studio 探查器使你能够查找并消除最昂贵（执行速度最慢）的项目部分，也称为*热路径*。

 本演练演示了下列任务：

- [添加功能和功能事件接收器](#add-a-feature-and-feature-event-receiver)。

- [配置和部署 SharePoint 应用程序](#configure-and-deploy-the-sharepoint-application)。

- [运行 SharePoint 应用程序](#run-the-sharepoint-application)。

- [查看和解释配置文件结果](#view-and-interpret-the-profile-results)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]。

## <a name="create-a-sharepoint-project"></a>创建 SharePoint 项目
 首先，创建一个 SharePoint 项目。

### <a name="to-create-a-sharepoint-project"></a>创建 SharePoint 项目

1. 在菜单栏上，选择 "**文件**" " > **新建** > **项目**" 以显示 "**新建项目**" 对话框。

2. 展开 "**视觉对象C#**  " 或 " **Visual Basic**" 下的 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

3. 在 "模板" 窗格中，选择 " **SharePoint 2010 项目**" 模板。

4. 在 "**名称**" 框中，输入**ProfileTest**，然后选择 "**确定"** 按钮。

    " **SharePoint 自定义向导**" 随即出现。

5. 在 "**指定用于调试的站点和安全级别**" 页上，输入要在其中调试站点定义的 SharePoint 服务器站点的 URL，或者使用默认位置（ http://<em>system name</em>/）。

6. 在 "**此 SharePoint 解决方案的信任级别是什么？** " 部分中，选择 "**部署为场解决方案**" 选项按钮。

    目前，只能分析场解决方案。 有关沙盒解决方案与场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 单击“完成”按钮。 项目将显示在**解决方案资源管理器**中。

## <a name="add-a-feature-and-feature-event-receiver"></a>添加功能和功能事件接收器
 接下来，向项目中添加功能和该功能的事件接收器。 此事件接收器将包含要分析的代码。

### <a name="to-add-a-feature-and-feature-event-receiver"></a>添加功能和功能事件接收器。

1. 在**解决方案资源管理器**中，打开 "**功能**" 节点的快捷菜单，选择 "**添加功能**"，并将名称保留为默认值**Feature1**。

2. 在**解决方案资源管理器**中，打开**Feature1**的快捷菜单，然后选择 "**添加事件接收器**"。

     这将为功能添加一个代码文件以及一些注释掉的事件处理程序，并打开要编辑的文件。

3. 在事件接收器类中，添加以下变量声明。

    ```vb
    ' SharePoint site/subsite.
    Private siteUrl As String = "http://localhost"
    Private webUrl As String = "/"
    ```

    ```csharp
    // SharePoint site/subsite.
    private string siteUrl = "http://localhost";
    private string webUrl = "/";
    ```

4. 将 `FeatureActivated` 过程替换为以下代码。

    ```vb
    Public Overrides Sub FeatureActivated(properties As SPFeatureReceiverProperties)
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim announcementsList As SPList = web.Lists("Announcements")

                    ' Add a new announcement to the Announcements list.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Activated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was activated on: " & DateTime.Now.ToString()
                    ' Waste some time.
                    TimeCounter()
                    ' Update the list.
                    listItem.Update()
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

                    // Add a new announcement to the Announcements list.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Activated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was activated on: " +
    DateTime.Now.ToString();
                    // Waste some time.
                    TimeCounter();
                    // Update the list.
                    listItem.Update();
                }
            }
        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }
    }
    ```

5. 在 `FeatureActivated`过程下面添加以下过程。

    ```vb

    Public Sub TimeCounter()
        Dim result As Integer
        For i As Integer = 0 To 99999
            For j As Integer = 0 To 9999
                result = i * j
            Next j
        Next i
    End Sub
    ```

    ```csharp
    public void TimeCounter()
    {
        for (int i = 0; i < 100000; i++)
        {
            for (int j = 0; j < 10000; j++)
            {
                int result = i * j;
            }
        }
    }
    ```

6. 在**解决方案资源管理器**中，打开项目（**ProfileTest**）的快捷菜单，然后选择 "**属性**"。

7. 在 "**属性**" 对话框中，选择 " **SharePoint** " 选项卡。

8. 在 "**活动部署配置**" 列表中，选择 "**无激活**"。

     选择此部署配置后，可以随后在 SharePoint 中手动激活功能。

9. 保存项目。

## <a name="configure-and-deploy-the-sharepoint-application"></a>配置和部署 SharePoint 应用程序
 SharePoint 项目现已就绪，将其配置并部署到 SharePoint 服务器。

### <a name="to-configure-and-deploy-the-sharepoint-application"></a>配置和部署 SharePoint 应用程序

1. 在 "**分析**" 菜单上，选择 "**启动性能向导**"。

2. 在 "**性能向导**" 的第一页上，将 "分析方法" 保留为 " **CPU 采样**"，然后选择 "**下一步**" 按钮。

     其他分析方法可用于更高级的分析情形。 有关详细信息，请参阅[了解性能收集方法](../profiling/understanding-performance-collection-methods.md)。

3. 在 "**性能向导**" 的第二页上，将配置文件目标保留为 " **ProfileTest** " 并选择 "**下一步**" 按钮。

     如果解决方案包含多个项目，它们将显示在此列表中。

4. 在**性能向导**第三页上，清除 "**启用层交互分析**" 复选框，然后选择 "**下一步**" 按钮。

     层交互分析 (TIP) 功能用于衡量查询数据库的应用程序的性能，并显示网页的请求次数。 本示例不需要这些数据，因此我们不启用此功能。

5. 在 "**性能向导**" 的第四页上，选中 "在**向导完成后启动分析**" 复选框处于选中状态，然后选择 "**完成**" 按钮。

     该向导在服务器上启用应用程序分析，显示 "**性能资源管理器**" 窗口，然后生成、部署和运行 SharePoint 应用程序。

## <a name="run-the-sharepoint-application"></a>运行 SharePoint 应用程序
 激活 SharePoint 中的功能，触发要运行的 `FeatureActivation` 事件代码。

### <a name="to-run-the-sharepoint-application"></a>运行 SharePoint 应用程序

1. 在 SharePoint 中，打开 "**站点操作**" 菜单，然后选择 "**站点设置**"。

2. 在 "**站点操作**" 列表中，选择 "**管理站点功能**" 链接。

3. 在 "**功能**" 列表中，选择 " **ProfileTest Feature1**" 旁边的 "**激活**" 按钮。

     执行此操作时将出现暂停，这是由于在 `FeatureActivated` 函数中调用了空闲循环。

4. 在 "**快速启动**" 栏上，选择 "**列表**"，然后**在 "列表**" 列表中选择 "**公告**"。

     注意，新公告已添加到列表中，表明已激活此功能。

5. 关闭 SharePoint 网站。

     关闭 SharePoint 后，探查器将创建并显示一个示例分析报告，并将其保存为**ProfileTest**项目的文件夹中的 .vsp 文件。

## <a name="view-and-interpret-the-profile-results"></a>查看和解释配置文件结果
 现在你已运行并分析 SharePoint 应用程序，请查看测试结果。

### <a name="to-view-and-interpret-the-profile-results"></a>查看和解释配置文件结果

1. 在示例分析报告的 "**执行单个工作最多的函数**" 部分中，请注意，`TimeCounter` 位于列表的顶部附近。

     此位置表示 `TimeCounter` 是示例数最高的函数之一，这表明它是应用程序中最大的性能瓶颈之一。 此情况并不奇怪，因为这是为了实现演示目的而有意设计的。

2. 在 "**执行单个工作最多的函数**" 部分中，选择 "`ProcessRequest`" 链接以显示 `ProcessRequest` 函数的成本分布。

     在 `ProcessRequest`的 "**被调用函数**" 部分中，请注意， **FeatureActiviated**函数作为开销最高的函数列出。

3. 在 "**被调用函数**" 部分中，选择 " **FeatureActivated** " 按钮。

     在**FeatureActivated**的 "**被调用函数**" 部分中，`TimeCounter` 函数作为开销最高的函数列出。 在 "**函数代码视图**" 窗格中，突出显示的代码（`TimeCounter`）是热点，指示需要更正的位置。

4. 关闭示例分析报告。

     若要随时再次查看报表，请在 "**性能资源管理器**" 窗口中打开 .vsp 文件。

## <a name="fix-the-code-and-reprofile-the-application"></a>修复代码并 reprofile 应用程序
 现在已找出 SharePoint 应用程序中的作用点函数，请将其修复。

### <a name="to-fix-the-code-and-reprofile-the-application"></a>修复代码并重新分析应用程序

1. 在功能事件接收器代码中，注释掉 `TimeCounter` 中的 `FeatureActivated` 方法调用，防止它被调用。

2. 保存项目。

3. 在**性能资源管理器**中，打开 "目标" 文件夹，然后选择 " **ProfileTest** " 节点。

4. 在**性能资源管理器**工具栏上的 "**操作**" 选项卡中，选择 "**开始分析**" 按钮。

     如果要在分析应用程序之前更改任何分析属性，请改为选择 "**启动性能向导**" 按钮。

5. 按照本主题前面的**运行 SharePoint 应用程序**部分中的说明进行操作。

     现在已消除对空闲循环的调用，功能应更快激活。 示例分析报告应反映此情况。

## <a name="see-also"></a>另请参阅
- [性能会话概述](../profiling/performance-session-overview.md)
- [性能分析初学者指南](../profiling/beginners-guide-to-performance-profiling.md)
- [通过 Visual Studio 探查器查找应用程序瓶颈](https://msdn.microsoft.com/magazine/cc337887.aspx)
