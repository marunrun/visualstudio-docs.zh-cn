---
title: 创建显示 OData for SharePoint 的 Silverlight web 部件
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SPE.SilverlightWebPart
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 859944c51be0abf2e6a326a06a5e4432a69ee4ee
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655925"
---
# <a name="walkthrough-create-a-silverlight-web-part-that-displays-odata-for-sharepoint"></a>演练：创建显示 OData for SharePoint 的 Silverlight web 部件
  SharePoint 2010 通过 OData 公开其列表数据。 在 SharePoint 中，OData 服务由 RESTful 服务 ListData 实现。 本演练演示如何创建承载 Silverlight 应用程序的 SharePoint web 部件。 Silverlight 应用程序使用 ListData 显示 SharePoint 公告列表信息。 有关详细信息，请参阅[SharePoint FOUNDATION REST 接口](http://go.microsoft.com/fwlink/?LinkId=225999)和[Open Data Protocol](http://go.microsoft.com/fwlink/?LinkId=226000)。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Prerequisites
 你需要以下组件来完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]

## <a name="create-a-silverlight-application-and-silverlight-web-part"></a>创建 Silverlight 应用程序和 Silverlight web 部件
 首先，在 Visual Studio 中创建 Silverlight 应用程序。 Silverlight 应用程序使用 ListData 服务从 SharePoint 公告列表中检索数据。

> [!NOTE]
> 4\.0 之前的 Silverlight 版本均不支持引用 SharePoint 列表数据所需的接口。

#### <a name="to-create-a-silverlight-application-and-silverlight-web-part"></a>创建 Silverlight 应用程序和 Silverlight web 部件

1. 在菜单栏上，选择 "**文件**" " > **新建** > **项目**" 以显示 "**新建项目**" 对话框。

2. 展开 "**视觉对象C#**  " 或 " **Visual Basic**" 下的 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

3. 在 "模板" 窗格中，选择 " **SharePoint 2010 Silverlight Web 部件**" 模板。

4. 在 "**名称**" 框中，输入**SLWebPartTest** ，然后选择 "**确定"** 按钮。

    此时将显示 " **SharePoint 自定义向导**" 对话框。

5. 在 "**指定用于调试的站点和安全级别**" 页上，输入要在其中调试站点定义的 SharePoint 服务器站点的 URL，或者使用默认位置（ http://<em>system name</em>/）。

6. 在 "**此 SharePoint 解决方案的信任级别是什么？** " 部分中，选择 "**部署为场解决方案**" 选项按钮。

    虽然此示例使用场解决方案，但 Silverlight web 部件项目可以作为场或沙盒解决方案进行部署。 有关沙盒解决方案和场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 在 "**指定 Silverlight 配置信息**" 页的 "要**如何关联 silverlight Web 部件**" 部分中，选择 "**创建新的 silverlight 项目并将其与 Web 部件相关联"** 选项按钮。

8. 将**名称**更改为**SLApplication**，将**语言**设置为**Visual Basic**或**视觉C#对象**，然后将**silverlight 版本**设置为**silverlight 4.0**。

9. 选择 "**完成**" 按钮。 项目将显示在**解决方案资源管理器**中。

     此解决方案包含两个项目： Silverlight 应用程序和 Silverlight web 部件。 Silverlight 应用程序从 SharePoint 检索并显示列表数据，Silverlight web 部件承载 Silverlight 应用程序，使您可以在 SharePoint 中查看它。

## <a name="customize-the-silverlight-application"></a>自定义 Silverlight 应用程序
 将代码和设计元素添加到 Silverlight 应用程序。

#### <a name="to-customize-the-silverlight-application"></a>自定义 Silverlight 应用程序

1. 在 Silverlight 应用程序中添加对 System.web 的程序集引用。 有关详细信息，请参阅[如何：使用 "添加引用" 对话框添加或删除引用](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。

2. 在**解决方案资源管理器**中，打开 "**引用**" 的快捷菜单，然后选择 "**添加服务引用**"。

    > [!NOTE]
    > 如果使用 Visual Basic，则必须选择**解决方案资源管理器**顶部的 "**显示所有文件**" 图标以显示 "**引用**" 节点。

3. 在 "**添加服务引用**" 对话框的 "地址" 框中，输入 SharePoint 站点的 URL （如 **http://MySPSite** ），然后选择 "**开始**" 按钮。

     当 Silverlight 查找 SharePoint OData 服务 ListData 时，它会将该地址替换为完整的服务 URL。 在此示例中， http://myserver 变成 http://myserver/_vti_bin/ListData.svc 。

4. 选择 "**确定"** 按钮以将服务引用添加到项目，并使用默认服务名称 ServiceReference1。

5. 在菜单栏上，依次选择“生成” > “生成解决方案”。

6. 将新数据源添加到基于 SharePoint 服务的项目。 为此，请在菜单栏上选择 "**查看** > **其他 Windows**  > **数据源**"。

     "**数据源**" 窗口将显示所有可用的 SharePoint 列表数据，如 "任务"、"公告" 和 "日历"。

7. 将公告列表数据添加到 Silverlight 应用程序。 可以将 "通知" 从 "**数据源**" 窗口拖到 Silverlight 设计器中。

     这将创建一个绑定到 SharePoint 站点的 "公告" 列表的网格控件。

8. 调整网格控件的大小以适合 Silverlight 页。

9. 在 MainPage 代码文件（*MainPage.xaml.cs* for Visual C#或*MainPage* for Visual Basic）中，添加以下命名空间引用。

    ```vb
    ' Add the following three Imports statements.
    Imports SLApplication.ServiceReference1
    Imports System.Windows.Data
    Imports System.Data.Services.Client
    ```

    ```csharp
    // Add the following three using directives.
    using SLApplication.ServiceReference1;
    using System.Windows.Data;
    using System.Data.Services.Client;
    ```

10. 在类的顶部添加以下变量声明。

    ```vb
    Private context As TeamSiteDataContext
    Private myCollectionViewSource As CollectionViewSource
    Private announcements As New DataServiceCollection(Of AnnouncementsItem)()
    ```

    ```csharp
    private TeamSiteDataContext context;
    private CollectionViewSource myCollectionViewSource;
    DataServiceCollection<AnnouncementsItem> announcements = new DataServiceCollection<AnnouncementsItem>();
    ```

11. 将 `UserControl_Loaded` 过程替换为以下项。

    ```vb
    Private Sub UserControl_Loaded_1(sender As Object, e As RoutedEventArgs)
        ' The URL for the OData service.
        ' Replace <server name> in the next line with the name of your SharePoint server.
        context = New TeamSiteDataContext(New Uri("http://<server name>/_vti_bin/ListData.svc"))

        ' Do not load your data at design time.
        If Not System.ComponentModel.DesignerProperties.GetIsInDesignMode(Me) Then
            'Load your data here and assign the results to the CollectionViewSource.
            myCollectionViewSource =   DirectCast(Me.Resources("announcementsViewSource"), System.Windows.Data.CollectionViewSource)
            announcements.LoadCompleted += New EventHandler(Of LoadCompletedEventArgs)(AddressOf announcements_LoadCompleted)
            announcements.LoadAsync(context.Announcements)
        End If
    End Sub
    ```

    ```csharp
    private void UserControl_Loaded_1(object sender, RoutedEventArgs e)
    {
        // The URL for the OData service.
        // Replace <server name> in the next line with the name of your
        // SharePoint server.
        context = new TeamSiteDataContext(new Uri("http://ServerName>/_vti_bin/ListData.svc"));

        // Do not load your data at design time.
        if (!System.ComponentModel.DesignerProperties.GetIsInDesignMode(this))
        {
            //Load your data here and assign the results to the CollectionViewSource.
            myCollectionViewSource = (System.Windows.Data.CollectionViewSource)this.Resources["announcementsViewSource"];
            announcements.LoadCompleted += new EventHandler<LoadCompletedEventArgs>(announcements_LoadCompleted);
            announcements.LoadAsync(context.Announcements);
        }
    }
    ```

     请确保将*ServerName*占位符替换为运行 SharePoint 的服务器的名称。

12. 添加以下错误处理过程。

    ```vb
    Private Sub announcements_LoadCompleted(sender As Object, e As LoadCompletedEventArgs)
        ' Handle any errors.
        If e.[Error] Is Nothing Then
            myCollectionViewSource.Source = announcements
        Else
            MessageBox.Show(String.Format("ERROR: {0}", e.[Error].Message))
        End If
    End Sub

    ```

    ```csharp
    void announcements_LoadCompleted(object sender, LoadCompletedEventArgs e)
    {
        // Handle any errors.
        if (e.Error == null)
        {
            myCollectionViewSource.Source = announcements;
        }
        else
        {
            MessageBox.Show(string.Format("ERROR: {0}", e.Error.Message));
        }
    }
    ```

## <a name="modify-the-silverlight-web-part"></a>修改 Silverlight web 部件
 更改 Silverlight web 部件项目中的属性以启用 Silverlight 调试。

#### <a name="to-modify-the-silverlight-web-part"></a>修改 Silverlight web 部件

1. 打开 Silverlight web 部件项目（**SLWebPartTest**）的快捷菜单，然后选择 "**属性**"。

2. 在 "**属性**" 窗口中，选择 " **SharePoint** " 选项卡。

3. 如果尚未选中，请选中 "**启用 Silverlight 调试（而不是脚本调试）** " 复选框。

4. 保存项目。

## <a name="test-the-silverlight-web-part"></a>测试 Silverlight web 部件
 在 SharePoint 中测试新的 Silverlight web 部件，以确保其正确显示 SharePoint 列表数据。

#### <a name="to-test-the-silverlight-web-part"></a>测试 Silverlight web 部件

1. 选择**F5**键生成并运行 SharePoint 解决方案。

2. 在 SharePoint 的 "**网站操作**" 菜单上，选择 "**新建页**"。

3. 在 "**新建页面**" 对话框中，输入标题，如 " **SL Web 部件测试**"，然后选择 "**创建**" 按钮。

4. 在 "页面设计器" 中的 "**编辑工具**" 选项卡上，选择 "**插入**"。

5. 在选项卡栏上，选择 " **Web 部件**"。

6. 在 "**类别**" 框中，选择 "**自定义**" 文件夹。

7. 在**Web 部件**列表中，选择 Silverlight Web 部件，然后选择 "**添加**" 按钮，将该 web 部件添加到设计器中。

8. 对所需的网页进行所有添加后，选择 "**页面**" 选项卡，然后选择工具栏上的 "**保存 &" 关闭**"按钮。

     Silverlight web 部件现在应显示来自 SharePoint 站点的公告数据。 默认情况下，该页存储在 SharePoint 的 "网站页面" 列表中。

    > [!NOTE]
    > 跨域访问 Silverlight 中的数据时，Silverlight 会防止可用于利用 web 应用程序的安全漏洞。 如果在访问 Silverlight 中的远程数据时遇到问题，请参阅[使服务跨域边界可用](http://go.microsoft.com/fwlink/?LinkId=223276)。

## <a name="see-also"></a>请参阅
- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [部署、发布和升级 SharePoint 解决方案包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)
