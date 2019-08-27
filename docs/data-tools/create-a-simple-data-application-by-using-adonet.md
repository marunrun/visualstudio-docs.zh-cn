---
title: 使用 ADO.NET 创建简单的数据应用程序
ms.date: 08/23/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 2222841f-e443-4a3d-8c70-4506aa905193
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 98185eb44bc598d83eddd2690d4a321f8880f014
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68925695"
---
# <a name="create-a-simple-data-application-by-using-adonet"></a>使用 ADO.NET 创建简单的数据应用程序

当你创建操作数据库中的数据的应用程序时，就执行了如定义连接字符串、插入数据以及运行存储过程等基本任务。 通过遵循本主题, 可以了解如何使用 Visual C#或 Visual Basic 和 ADO.NET 在简单的 Windows 窗体 "Forms over data" 应用程序中与数据库交互。  所有 .NET 数据技术 (包括数据集、LINQ to SQL 和实体框架) 最终执行的步骤与本文中所示的步骤非常类似。

本文介绍了一种简单的方法, 可快速从数据库中获取数据。 如果你的应用程序需要以不重要的方式修改数据并更新数据库, 则应考虑使用实体框架, 并使用数据绑定自动将用户界面控件同步到基础数据中的更改。

> [!IMPORTANT]
> 要使代码保持简单，请不要包括生产就绪的异常处理。

## <a name="prerequisites"></a>系统必备

要创建应用程序，你将需要：

- Visual Studio。

- SQL Server Express LocalDB。 如果没有 SQL Server Express 的 LocalDB, 则可以从[SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)安装它。

本主题假定你熟悉 Visual Studio IDE 的基本功能, 并可以创建 Windows 窗体应用程序, 向项目中添加窗体, 放置按钮和窗体上的其他控件, 设置控件的属性以及编写简单事件。 如果你不熟悉这些任务, 建议你在开始本演练之前完成[Visual C# And Visual Basic 主题入门](../ide/quickstart-visual-basic-console.md)。

## <a name="set-up-the-sample-database"></a>设置示例数据库

按照以下步骤创建示例数据库:

1. 在 Visual Studio 中, 打开 "**服务器资源管理器**" 窗口。

2. 右键单击 "**数据连接**", 然后选择 "**新建 SQL Server 数据库**"。

3. 在 "**服务器名称**" 文本框中, 输入 **(localdb) \mssqllocaldb**。

4. 在 "**新数据库名称**" 文本框中, 输入**Sales**, 然后选择 **"确定"** 。

     将创建空的**销售**数据库并将其添加到服务器资源管理器中的 "数据连接" 节点。

5. 右键单击 "**销售**" 数据连接, 然后选择 "**新建查询**"。

     此时将打开查询编辑器窗口。

6. 将[Sales transact-sql 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/raw/master/docs/data-tools/samples/sales.sql)复制到剪贴板。

7. 将 T-sql 脚本粘贴到查询编辑器中, 然后选择 "**执行**" 按钮。

     一小段时间后, 查询将完成运行, 并创建数据库对象。 数据库包含两个表:客户和订单。 这些表最初不包含数据, 但你可以在运行将创建的应用程序时添加数据。 该数据库还包含四个简单的存储过程。

## <a name="create-the-forms-and-add-controls"></a>创建窗体并添加控件

1. 创建 Windows 窗体应用程序项目，然后将其命名为“SimpleDataApp”。

    Visual Studio 将创建项目以及若干个文件，其中包括名为“Form1”的空 Windows 窗体。

2. 添加两个 Windows 窗体到项目中，以使其具有三个窗体，然后给予它们下列名称：

   - **导航**

   - **NewCustomer**

   - **FillOrCancel**

3. 对于每个窗体，添加文本框、按钮和其他控件，如下图所示。 对于每个控件，设置表中描述的属性。

   > [!NOTE]
   > 分组框和标签控件可提高清晰度，但不在代码中使用。

   **Navigation 窗体**

   ![“导航”对话框](../data-tools/media/simpleappnav.png)

|Navigation 窗体的控件|属性|
| - |----------------|
|Button|Name = btnGoToAdd|
|Button|Name = btnGoToFillOrCancel|
|Button|Name = btnExit|

**NewCustomer 窗体**

![添加新客户或提交订单](../data-tools/media/simpleappnewcust.png)

|NewCustomer 窗体的控件|属性|
| - |----------------|
|文本框|Name = txtCustomerName|
|文本框|Name = txtCustomerID<br /><br /> Readonly = True|
|Button|Name = btnCreateAccount|
|NumericUpdown|DecimalPlaces = 0<br /><br /> Maximum = 5000<br /><br /> Name = numOrderAmount|
|DateTimePicker|Format = Short<br /><br /> Name = dtpOrderDate|
|Button|Name = btnPlaceOrder|
|Button|Name = btnAddAnotherAccount|
|Button|Name = btnAddFinish|

**FillOrCancel 窗体**

![填充或取消订单](../data-tools/media/simpleappcancelfill.png)

|FillOrCancel 窗体的控件|属性|
| - |----------------|
|文本框|Name = txtOrderID|
|Button|Name = btnFindByOrderID|
|DateTimePicker|Format = Short<br /><br /> Name = dtpFillDate|
|DataGridView|Name = dgvCustomerOrders<br /><br /> Readonly = True<br /><br /> RowHeadersVisible = False|
|Button|Name = btnCancelOrder|
|Button|Name = btnFillOrder|
|Button|Name = btnFinishUpdates|

## <a name="store-the-connection-string"></a>存储连接字符串
当应用程序尝试打开数据库的连接时，应用程序必须能够访问连接字符串。 若要避免在每个窗体上手动输入字符串, 请将该字符串存储在项目的*app.config*文件中, 并创建一个方法, 该方法在从应用程序中的任何窗体中调用方法时返回字符串。

您可以通过在**服务器资源管理器**中右键单击**Sales**数据连接, 然后选择 "**属性**" 来查找连接字符串。 找到**ConnectionString**属性, 然后使用**ctrl**+**A**、 **ctrl**+**C**选择字符串并将其复制到剪贴板。

1. 如果C#使用的是, 请在**解决方案资源管理器**中展开项目下的 "**属性**" 节点, 然后打开 "**设置**" 文件。
    如果使用的是 Visual Basic, 请在**解决方案资源管理器**中单击 "**显示所有文件**", 展开 "**我的项目**" 节点, 然后打开 "**设置**" 文件。

2. 在 "**名称**" 列中`connString`, 输入。

3. 在 "**类型**" 列表中, 选择 " **(连接字符串)** "。

4. 在 "**作用域**" 列表中, 选择 "**应用程序**"。

5. 在 "**值**" 列中, 输入连接字符串 (不带任何外引号), 然后保存所做的更改。

> [!NOTE]
> 在实际应用程序中, 应安全地存储连接字符串, 如[连接字符串和配置文件](/dotnet/framework/data/adonet/connection-strings-and-configuration-files)中所述。

## <a name="write-the-code-for-the-forms"></a>编写窗体代码

本部分简要概述了每种形式的用途。 它还提供了在单击窗体上的按钮时定义基础逻辑的代码。

### <a name="navigation-form"></a>Navigation 窗体

运行应用程序时，Navigation 窗体将打开。 按“添加帐户”按钮可以打开 NewCustomer 窗体。 按“填写或取消订单”按钮可以打开 FillOrCancel 窗体。 按“退出”按钮可以关闭应用程序。

#### <a name="make-the-navigation-form-the-startup-form"></a>使 Navigation 窗体成为启动窗体

如果使用 C#，则在“解决方案资源管理器”中，打开 Program.cs，然后将 `Application.Run` 行更改为 `Application.Run(new Navigation());`

如果使用 Visual Basic, 请在**解决方案资源管理器**中打开 "**属性**" 窗口, 选择 "**应用程序**" 选项卡, 然后在 "**启动窗体**" 列表中选择 " **simpledataapp.navigation** "。

#### <a name="create-auto-generated-event-handlers"></a>创建自动生成的事件处理程序

双击导航窗体上的三个按钮创建空的事件处理程序方法。 双击按钮还会在设计器代码文件中添加自动生成的代码, 该代码启用按钮单击以引发事件。

#### <a name="add-code-for-the-navigation-form-logic"></a>为导航窗体逻辑添加代码

在导航窗体的代码页中, 完成三个按钮单击事件处理程序的方法主体, 如下面的代码所示。

[!code-csharp[Navigation#1](../data-tools/codesnippet/CSharp/SimpleDataApp/Navigation.cs#1)]
[!code-vb[Navigation#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/Navigation.vb#1)]

### <a name="newcustomer-form"></a>NewCustomer 窗体

输入客户名称, 然后选择 "**创建帐户**" 按钮时, NewCustomer 窗体将创建客户帐户, 并 SQL SERVER 返回标识值作为新的客户 ID。 然后, 您可以通过指定一个金额和订单日期并选择 "**下订单**" 按钮, 为新帐户下订单。

#### <a name="create-auto-generated-event-handlers"></a>创建自动生成的事件处理程序

双击四个按钮, 为 NewCustomer 窗体上的每个按钮创建一个空的 Click 事件处理程序。 双击按钮还会在设计器代码文件中添加自动生成的代码, 该代码启用按钮单击以引发事件。

#### <a name="add-code-for-the-newcustomer-form-logic"></a>为 NewCustomer 窗体逻辑添加代码

若要完成 NewCustomer 窗体逻辑, 请按照以下步骤操作。

1. 将`System.Data.SqlClient`命名空间置于范围中, 这样就不必完全限定其成员的名称。

     ```csharp
     using System.Data.SqlClient;
     ```

     ```vb
     Imports System.Data.SqlClient
     ```

2. 将一些变量和帮助器方法添加到类, 如下面的代码所示。

     [!code-csharp[NewCustomer#1](../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs#1)]
     [!code-vb[NewCustomer#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb#1)]

3. 完成四个按钮单击事件处理程序的方法主体, 如下面的代码所示。

     [!code-csharp[NewCustomer#2](../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs#2)]
     [!code-vb[NewCustomer#2](../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb#2)]

### <a name="fillorcancel-form"></a>FillOrCancel 窗体

当您输入订单 ID, 然后单击 "**查找订单**" 按钮时, FillOrCancel 窗体将运行查询以返回订单。 返回的行在只读数据网格中显示。 如果选择 "**取消订单**" 按钮, 则可以将订单标记为已取消 (X); 如果选择 "**填充顺序**" 按钮, 则可以将订单标记为已填写 (F)。 如果再次选择 "**查找订单**" 按钮, 则会出现更新的行。

#### <a name="create-auto-generated-event-handlers"></a>创建自动生成的事件处理程序

通过双击按钮, 为 FillOrCancel 窗体上的四个按钮创建空的 Click 事件处理程序。 双击按钮还会在设计器代码文件中添加自动生成的代码, 该代码启用按钮单击以引发事件。

#### <a name="add-code-for-the-fillorcancel-form-logic"></a>为 FillOrCancel 窗体逻辑添加代码

若要完成 FillOrCancel 窗体逻辑, 请按照以下步骤操作。

1. 将以下两个命名空间置于范围内, 以便您无需完全限定其成员的名称。

     ```csharp
     using System.Data.SqlClient;
     using System.Text.RegularExpressions;
     ```

     ```vb
     Imports System.Data.SqlClient
     Imports System.Text.RegularExpressions
     ```

2. 将变量和 helper 方法添加到类, 如下面的代码所示。

     [!code-csharp[FillOrCancel#1](../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs#1)]
     [!code-vb[FillOrCancel#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb#1)]

3. 完成四个按钮单击事件处理程序的方法主体, 如下面的代码所示。

     [!code-csharp[FillOrCancel#2](../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs#2)]
     [!code-vb[FillOrCancel#2](../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb#2)]

## <a name="test-your-application"></a>测试应用程序

在对每个 Click 事件处理程序进行编码且完成编码后，请按 F5 键以生成并测试应用程序。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
