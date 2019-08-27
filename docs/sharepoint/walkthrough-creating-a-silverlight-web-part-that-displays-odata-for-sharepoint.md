---
title: 创建显示 SharePoint OData 的 Silverlight web 部件
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
ms.openlocfilehash: f248ce4403e771d9ab8b6d13fe55fd5ca1c960d4
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401132"
---
# <a name="walkthrough-create-a-silverlight-web-part-that-displays-odata-for-sharepoint"></a>演练：创建显示 SharePoint OData 的 Silverlight web 部件
  SharePoint 2010 通过 OData 公开其列表数据。 在 SharePoint 中，由 RESTful 服务 ListData.svc 实现 OData 服务。 本演练演示如何创建承载 Silverlight 应用程序的 SharePoint web 部件。 Silverlight 应用程序使用 ListData.svc 显示 SharePoint 公告列表信息。 有关详细信息，请参阅[SharePoint Foundation REST 接口](http://go.microsoft.com/fwlink/?LinkId=225999)并[开放数据协议](http://go.microsoft.com/fwlink/?LinkId=226000)。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]。

## <a name="create-a-silverlight-application-and-silverlight-web-part"></a>创建 Silverlight 应用程序和 Silverlight web 部件
 首先，在 Visual Studio 中创建 Silverlight 应用程序。 Silverlight 应用程序通过使用 ListData.svc 服务从 SharePoint Announcements 列表检索数据。

> [!NOTE]
> 任何版本的 Silverlight 4.0 之前引用 SharePoint 列表数据不支持所需的接口。

#### <a name="to-create-a-silverlight-application-and-silverlight-web-part"></a>若要创建 Silverlight 应用程序和 Silverlight web 部件

1. 在菜单栏上依次选择**文件** > **新建** > **项目**显示**新建项目**对话框。

2. 展开**SharePoint**节点下的**Visual C#** 或**Visual Basic**，然后选择**2010年**节点。

3. 在模板窗格中，选择**SharePoint 2010 Silverlight Web 部件**模板。

4. 在中**名称**框中，输入**SLWebPartTest** ，然后选择**确定**按钮。

    **SharePoint 自定义向导**对话框随即出现。

5. 上**指定用于调试的网站和安全级别**页上，输入你想要调试站点定义的 SharePoint 服务器站点的 URL 或使用默认位置 (http://<em>系统名称</em>/).

6. 在中**此 SharePoint 解决方案的信任级别是什么？** 部分中，选择**部署为场解决方案**选项按钮。

    虽然此示例中使用的场解决方案，但 Silverlight web 部件项目可以部署为场或沙盒解决方案。 有关沙盒解决方案和场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 在中**要如何关联 Silverlight Web 部件**一部分**指定 Silverlight 配置信息**页上，选择**创建新的 Silverlight 项目和将其与 web 部件关联**选项按钮。

8. 更改**名称**到**SLApplication**，将**语言**为**Visual Basic**或**Visual C#** ，然后设置**Silverlight 版本**到**Silverlight 4.0**。

9. 选择**完成**按钮。 项目出现在**解决方案资源管理器**。

     该解决方案包含两个项目： 一个 Silverlight 应用程序和 Silverlight web 部件。 Silverlight 应用程序检索并显示从 SharePoint 列表数据和 Silverlight web 部件承载 Silverlight 应用程序，您可以查看在 SharePoint 中。

## <a name="customize-the-silverlight-application"></a>自定义 Silverlight 应用程序
 将代码和设计元素添加到 Silverlight 应用程序。

#### <a name="to-customize-the-silverlight-application"></a>若要自定义 Silverlight 应用程序

1. 在 Silverlight 应用程序中添加对 system.windows.data 的引用程序集引用。 有关详细信息，请参阅[如何：添加或删除引用通过使用添加引用对话框中](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)。

2. 在中**解决方案资源管理器**，打开快捷菜单**引用**，然后选择**添加服务引用**。

    > [!NOTE]
    > 如果您正在使用 Visual Basic，则必须选择**显示所有文件**顶部的图标**解决方案资源管理器**以显示**引用**节点。

3. 中的地址框**添加服务引用**对话框框中，输入您的 SharePoint 站点的 URL，例如 **http://MySPSite** ，然后选择**转**按钮。

     时 Silverlight 定位 SharePoint OData 服务 ListData.svc，将使用完整的服务的 URL 替换该地址。 对于本例，请 http://myserver 变得 http://myserver/_vti_bin/ListData.svc 。

4. 选择**确定**按钮添加到项目中，服务引用，然后使用默认服务名称 ServiceReference1。

5. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

6. 将新的数据源添加到项目根据 SharePoint 服务。 若要执行此操作，请在菜单栏上，选择**视图** > **其他 Windows** > **数据源**。

     **数据源**窗口将显示所有可用的 SharePoint 列表数据，如任务、 公告、 和日历。

7. 将公告列表数据添加到 Silverlight 应用程序。 可以将"公告"从拖**数据源**窗口拖到 Silverlight 设计器。

     这将创建一个网格控件绑定到 SharePoint 站点的公告列表。

8. 调整网格控件大小以适应 Silverlight 页面的大小。

9. 在 MainPage.xaml 的代码文件 (*MainPage.xaml.cs*对于 Visual C# 或*MainPage.xaml.vb*适用于 Visual Basic)，添加以下命名空间引用。

    ```vb
    ' Add the following three Imports statements.
    Imports SLApplication.ServiceReference1
    Imports System.Windows.Data
    Imports System.Data.Services.Client
    ```

    ```csharp
    // Add the following three using statements.
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

11. 替换为`UserControl_Loaded`使用以下过程。

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

     确保替换*ServerName*占位符替换为运行 SharePoint 的服务器的名称。

12. 添加以下的错误处理过程。

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
 更改以启用 Silverlight 调试 Silverlight web 部件项目中的属性。

#### <a name="to-modify-the-silverlight-web-part"></a>若要修改的 Silverlight web 部件

1. 打开 Silverlight web 部件项目的快捷菜单 (**SLWebPartTest**)，然后选择**属性**。

2. 在中**属性**窗口中，选择**SharePoint**选项卡。

3. 如果尚未选择它，请选择**启用 Silverlight 调试 （而不 Script 调试）** 复选框。

4. 保存项目。

## <a name="test-the-silverlight-web-part"></a>测试 Silverlight web 部件
 测试新的 Silverlight web 部件在 SharePoint 中以确保它正确显示 SharePoint 列表数据。

#### <a name="to-test-the-silverlight-web-part"></a>若要测试 Silverlight web 部件

1. 选择**F5**键生成并运行 SharePoint 解决方案。

2. 在 SharePoint 中，在**站点操作**菜单中，选择**新页面**。

3. 在**新页面**对话框中，输入一个标题，如**SL Web 部件测试**，然后选择**创建**按钮。

4. 在页面设计器上**编辑工具**选项卡上，选择**插入**。

5. 在选项卡条中，选择**Web 部件**。

6. 在中**类别**框中，选择**自定义**文件夹。

7. 在中**Web 部件**列表中，选择 Silverlight web 部件，然后选择**添加**按钮将 web 部件添加到设计器。

8. 所做所有添加到所需的 web 页面后，请选择**页上**选项卡，然后选择**保存并关闭**工具栏上的按钮。

     现在应显示 Silverlight web 部件从 SharePoint 站点发布数据。 默认情况下，页面存储在 SharePoint 中的站点页面列表。

    > [!NOTE]
    > 在访问在 Silverlight 中跨域的数据时，Silverlight 可防止可以被用来利用 web 应用程序的安全漏洞。 如果在访问在 Silverlight 中的远程数据时遇到问题，请参阅[使服务跨域边界可用](http://go.microsoft.com/fwlink/?LinkId=223276)。

## <a name="see-also"></a>请参阅
- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [部署、 发布和升级 SharePoint 解决方案包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)
