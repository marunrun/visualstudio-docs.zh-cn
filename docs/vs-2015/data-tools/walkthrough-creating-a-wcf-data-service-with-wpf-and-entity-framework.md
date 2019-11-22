---
title: 'Walkthrough: Creating a WCF Data Service with WPF and Entity Framework | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
helpviewer_keywords:
- data services in Visual Studio
- WCF Data Services, Visual Studio
- ADO.NET Data Services, Visual Studio
- WCF data services in Visual Studio
ms.assetid: da66ad1b-a25d-485c-af13-2d18f0422e3d
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5abbb647f93c991d2de626a84e82f47e03f6f71e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299624"
---
# <a name="walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework"></a>演练：使用 WPF 和 Entity Framework 创建 WCF Data Service
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

This walkthrough demonstrates how to create a simple [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] that is hosted in an [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] Web application and then access it from a Windows Forms application.

 在此演练中，将：

- 创建 Web 应用程序以承载 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)]。

- 创建一个表示 Northwind 数据库中 Customers 表的 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]。

- 创建 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)]。

- 创建一个客户端应用程序，并添加对 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)]的引用。

- 启用对该服务的数据绑定并生成用户界面。

- 可以选择向应用程序添加筛选功能。

## <a name="prerequisites"></a>Prerequisites
 你需要以下组件来完成本演练：

- Northwind 示例数据库。

     如果你的开发计算机上没有此数据库，可以从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkID=98088)进行下载。 For instructions, see [Downloading Sample Databases](https://msdn.microsoft.com/library/ef9d69a1-9461-43fe-94bb-7c836754bcb5).

## <a name="creating-the-service"></a>创建服务
 若要创建 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)]，你将添加一个 Web 项目，创建一个[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]，然后通过此模型创建服务。

 首先，将添加一个 Web 项目以承载服务。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-create-the-web-project"></a>创建 Web 项目

1. On the menu bar, choose **File**, **New**,  **Project**.

2. 在“新建项目”对话框中，展开“Visual Basic”或展开“Visual C#”和“Web”节点，然后选择“ASP.NET Web 应用程序”模板。

3. 在“名称”文本框中，输入“NorthwindWeb”，然后选择“确定”按钮。

4. 在“新建 ASP.NET 项目”对话框的“选择模板”列表中，选择“空”，然后选择“确定”按钮。

   在此步骤中，你将创建一个表示 Northwind 数据库中 Customers 表的 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]。

#### <a name="to-create-the-entity-data-model"></a>创建实体数据模型

1. On the menu bar, choose **Project**, **Add New Item**.

2. 在“添加新项”对话框中，选择“数据”节点，然后选择“ADO.NET 实体数据模型”项。

3. In the **Name** text box, enter `NorthwindModel`, and then choose the **Add** button.

    此时将显示实体数据模型向导。

4. 在实体数据模型向导的“选择模型内容”页上，选择“数据库的 EF 设计器”项，然后选择“下一步”按钮。

5. 在 **“选择你的数据连接”** 页上执行下列步骤之一：

   - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

        或

   - 选择“新建连接”按钮来配置新数据连接。 For more information, see [Add new connections](../data-tools/add-new-connections.md).

6. 如果数据库需要密码，请选择“是，在连接字符串中包含敏感数据”选项按钮，然后选择“下一步”按钮。

   > [!NOTE]
   > 如果显示一个对话框，请选择“是”，将该文件保存到项目中。

7. 在“选择版本”页上，选择“Entity Framework 5.0”选项按钮，然后选择“下一步”按钮。

   > [!NOTE]
   > 为了使用具有 WCF 服务的 Entity Framework 6 的最新版本，你需要安装 WCF Data Services Entity Framework Provider NuGet 程序包。 See [Using WCF Data Services 5.6.0 with Entity Framework 6+](https://devblogs.microsoft.com/odata/using-wcf-data-services-5-6-0-with-entity-framework-6/).

8. 在“选择数据库对象”页上，展开“表”节点、选中“客户”复选框，然后选择“完成”按钮。

    随即显示实体模型关系图，NorthwindModel.edmx 文件也将添加到项目中。

   在此步骤中，你将创建并测试数据服务。

#### <a name="to-create-the-data-service"></a>创建数据服务

1. On the menu bar, choose **Project**, **Add New Item**.

2. 在“添加新项”对话框中，选择“Web”节点，然后选择“WCF Data Service 5.6”项。

3. In the **Name** text box, enter `NorthwindCustomers`, and then choose the **Add** button.

    The NorthwindCustomers.svc file appears in the **Code Editor**.

4. 在“代码编辑器”中，定位到第一个 `TODO:` 注释并使用以下内容替换该代码：

    [!code-csharp[WCFDataServiceWalkthrough#1](../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs#1)]
    [!code-vb[WCFDataServiceWalkthrough#1](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb#1)]

5. 使用下面的代码替换 `InitializeService` 事件处理程序中的注释：

    [!code-csharp[WCFDataServiceWalkthrough#2](../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs#2)]
    [!code-vb[WCFDataServiceWalkthrough#2](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb#2)]

6. On the menu bar, choose **Debug**, **Start Without Debugging** to run the service. 此时将打开一个浏览窗口，并显示该服务的 XML 架构。

7. In the **Address** bar, enter `Customers` at the end of the URL for NorthwindCustomers.svc, and then choose the **ENTER** key.

    Customers 表中的数据将以 XML 表示形式显示。

   > [!NOTE]
   > 某些情况下，Internet Explorer 会将数据错误解释为 RSS 源。 必须确保禁用显示 RSS 源的选项。 For more information, see [Troubleshooting Service References](../data-tools/troubleshooting-service-references.md).

8. 关闭浏览器窗口。

   在接下来的步骤中，将创建一个 Windows 窗体客户端应用程序以使用该服务。

## <a name="creating-the-client-application"></a>创建客户端应用程序
 若要创建客户端应用程序，你将另外添加一个项目，添加对该项目的服务引用，配置数据源，并创建一个用户界面以显示服务中的数据。

 在第一个步骤中，你将 Windows 窗体项目添加到解决方案中，并将其设置为启动项目。

#### <a name="to-create-the-client-application"></a>创建客户端应用程序

1. On the menu bar, choose File, **Add**, **New Project**.

2. In the **New Project** dialog box, expand the **Visual Basic** or **Visual C#** node and choose the **Windows** node, and then choose **Windows Forms Application**.

3. 在“名称”文本框中，输入 `NorthwindClient`，然后选择“确定”按钮。

4. 在“解决方案资源管理器”中，选择“NorthwindClient”项目节点。

5. 在菜单栏上，选择“项目”和“设为启动项目”。

   在此步骤中，将添加对 Web 项目中的 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)]的服务引用。

#### <a name="to-add-a-service-reference"></a>添加服务引用

1. On the menu bar, choose **Project**, **Add Service Reference**.

2. 在“添加服务引用”对话框中，选择“发现”按钮。

    NorthwindCustomers 服务的 URL 将显示在“地址”字段中。

3. 选择“确定”按钮以添加服务引用。

   在此步骤中，将配置数据源以启用对服务的数据绑定。

#### <a name="to-enable-data-binding-to-the-service"></a>启用对服务的数据绑定

1. On the menu bar, choose **View**, **Other Windows**, **Data Sources**.

2. 在“数据源”窗口中，选择“添加新数据源”按钮。

3. 在“数据源配置”向导的“选择数据源类型”页上，选择“对象”，然后选择“下一步”按钮。

4. 在“选择数据对象”页上，展开“NorthwindClient”节点，然后展开“NorthwindClient.ServiceReference1”节点。

5. 选中“Customer”复选框，然后选择“完成”按钮。

   在此步骤中，你将创建用于显示服务中的数据的用户界面。

#### <a name="to-create-the-user-interface"></a>创建用户界面

1. 在“数据源”窗口中，打开“Customers”节点的快捷菜单，然后选择“复制”。

2. 在“Form1.vb”或“Form1.cs”窗体设计器中，打开快捷菜单并选择“粘贴”。

    一个 <xref:System.Windows.Forms.DataGridView> 控件、一个 <xref:System.Windows.Forms.BindingSource> 组件以及一个 <xref:System.Windows.Forms.BindingNavigator> 组件将添加到窗体中。

3. 选择“CustomersDataGridView”控件，然后在“属性”窗口将“Dock”属性设为“填充”。

4. In **Solution Explorer**, open the shortcut menu for the **Form1** node and choose **View Code** to open the Code Editor, and add the following Imports or Using statement at the top of the file:

   ```vb
   Imports NorthwindClient.ServiceReference1
   ```

   ```csharp
   using NorthwindClient.ServiceReference1;
   ```

5. 将以下代码添加到 `Form1_Load` 事件处理程序中：

   ```vb
   Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
           Dim proxy As New NorthwindEntities _
   (New Uri("http://localhost:53161/NorthwindCustomers.svc/"))
           Me.CustomersBindingSource.DataSource = proxy.Customers
       End Sub
   ```

   ```csharp
   private void Form1_Load(object sender, EventArgs e)
   {
   NorthwindEntities proxy = new NorthwindEntities(new Uri("http://localhost:53161/NorthwindCustomers.svc/"));
   this.CustomersBindingSource.DataSource = proxy.Customers;
   }

   ```

6. In **Solution Explorer**, open the shortcut menu for the NorthwindCustomers.svc file and choose **View in Browser**. 此时将打开 Internet Explorer，并显示该服务的 XML 架构。

7. 从 Internet Explorer 地址栏中复制 URL。

8. 在步骤 4 中添加的代码中，选择 `http://localhost:53161/NorthwindCustomers.svc/` 并使用刚刚复制的 URL 替换它。

9. On the menu bar, choose **Debug**, **Start Debugging** to run the application. 此时将显示客户信息。

   现在，你有了一个可以使用的应用程序，该应用程序将显示 NorthwindCustomers 服务中的客户的列表。 如果希望通过该服务公开其他数据，则可以修改[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)]以包括 Northwind 数据库中的其他表。

   在下一个可选步骤中，将学习如何筛选服务返回的数据。

## <a name="adding-filtering-capabilities"></a>添加筛选功能
 在此步骤中，将自定义应用程序以根据客户的城市筛选数据。

#### <a name="to-add-filtering-by-city"></a>添加根据城市进行筛选的功能

1. 在“解决方案资源管理器”中，打开“Form1.vb”或“Form1.cs”节点的快捷菜单，然后选择“打开”。

2. 将“工具箱”中的 <xref:System.Windows.Forms.TextBox> 控件和 <xref:System.Windows.Forms.Button> 控件添加到窗体。

3. Open the shortcut menu for the <xref:System.Windows.Forms.Button> control, and choose **View Code**, and then add the following code in the `Button1_Click` event handler:

    ```vb
    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
            Dim proxy As New northwindEntities _
    (New Uri("http://localhost:53161/NorthwindCustomers.svc"))
            Dim city As String = TextBox1.Text

            If city <> "" Then
                Me.CustomersBindingSource.DataSource = From c In _
             proxy.Customers Where c.City = city
            End If

        End Sub
    ```

    ```csharp
    private void Button1_Click(object sender, EventArgs e)
    {
    ServiceReference1.northwindModel.northwindEntities proxy = new northwindEntities(new Uri("http://localhost:53161/NorthwindCustomers.svc"));
    string city = TextBox1.Text;

    if (!string.IsNullOrEmpty(city)) {
    this.CustomersBindingSource.DataSource = from c in proxy.Customers where c.City == city;
    }

    }
    ```

4. 在以上代码中，使用 `http://localhost:53161/NorthwindCustomers.svc` 事件处理程序中的 URL 替换 `Form1_Load`。

5. On the menu bar, choose **Debug**, **Start Debugging** to run the application.

6. 在文本框中，输入“London”，然后选择该按钮。 将仅显示来自 London 的客户。

## <a name="see-also"></a>请参阅
 [Windows Communication Foundation Services and WCF Data Services in Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) [How to: Add, Update, or Remove a WCF Data Service Reference](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md)
