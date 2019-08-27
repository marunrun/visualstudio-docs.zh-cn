---
title: 使用 ADO.NET 创建简单的数据应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
ms.assetid: 2222841f-e443-4a3d-8c70-4506aa905193
caps.latest.revision: 46
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 70fca5b1329dc9091e0672b41de0798d93aba01a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705173"
---
# <a name="create-a-simple-data-application-by-using-adonet"></a>使用 ADO.NET 创建简单的数据应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当你创建操作数据库中的数据的应用程序时，就执行了定义连接字符串、插入数据以及运行存储过程等基本任务。 通过按照本主题，了解如何使用 Visual C# 或 Visual Basic 和 ADO.NET 与从简单的 Windows 窗体"forms over data"应用程序中的数据库进行交互。  所有.NET 数据技术，包括数据集，LINQ to SQL 和实体框架 — 最终执行非常类似于本文中所示的步骤。  
  
 本文演示了以非常快的方式获取数据，这个数据库的简单方法。 如果你的应用程序需要修改重要的方法中的数据并更新数据库，则应考虑使用实体框架和使用数据绑定，以自动同步到基础数据中的更改的用户界面控件。  
  
> [!IMPORTANT]
> 要使代码保持简单，请不要包括生产就绪的异常处理。  
  
 **在本主题中**  
  
- [设置示例数据库](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_setupthesampledatabase)  
  
- [创建窗体并添加控件](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_createtheformsandaddcontrols)  
  
- [存储连接字符串](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_storetheconnectionstring)  
  
- [检索连接字符串](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_retrievetheconnectionstring)  
  
- [编写窗体代码](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_writethecodefortheforms)  
  
- [测试应用程序](../data-tools/create-a-simple-data-application-by-using-adonet.md#BKMK_testyourapplication)  
  
## <a name="prerequisites"></a>系统必备  
 要创建应用程序，你将需要：  
  
- Visual Studio Community Edition。  
  
- SQL Server Express LocalDB。  
  
- 按照中的步骤创建小型示例数据库[通过使用脚本创建 SQL 数据库](../data-tools/create-a-sql-database-by-using-a-script.md)。  
  
- 设置数据库后的数据库连接字符串。 您可以找到此值，通过打开**SQL Server 对象资源管理器**，打开数据库的快捷菜单，选择**属性**，并滚动到**ConnectionString**属性。  
  
  本主题假定你已经熟悉 Visual Studio IDE 的基本功能，并可以创建 Windows 窗体应用程序，将窗体添加到项目，将按钮和其他控件安装到这些窗体上，为这些控件设置属性，以及对简单事件进行编码。 如果您不熟悉这些任务，我们建议你先完成[Getting Started with Visual C# 和 Visual Basic](../ide/getting-started-with-visual-csharp-and-visual-basic.md)在开始本主题之前。  
  
## <a name="BKMK_setupthesampledatabase"></a> 设置示例数据库  
 本演练的示例数据库由客户和订单表组成。 表最初不包含数据，但你会在运行将创建的应用程序时添加数据。 该数据库中还有五个简单的存储过程。 [通过使用脚本创建 SQL 数据库](../data-tools/create-a-sql-database-by-using-a-script.md)包含创建表、 主键和外键、 约束和存储的过程的 TRANSACT-SQL 脚本。  
  
## <a name="BKMK_createtheformsandaddcontrols"></a> 创建窗体并添加控件  
  
1. 为 Windows 窗体应用程序，创建一个项目并将其 SimpleDataApp。  
  
    Visual Studio 将创建项目以及若干个文件，其中包括名为 Form1 的空 Windows 窗体。  
  
2. 添加两个 Windows 窗体到项目中，以使其具有三个窗体，然后给予它们下列名称：  
  
   - 导航  
  
   - NewCustomer  
  
   - FillOrCancel  
  
3. 对于每个窗体，添加文本框、按钮和其他控件，如下图所示。 对于每个控件，设置表中描述的属性。  
  
   > [!NOTE]
   > 分组框和标签控件可提高清晰度，但不在代码中使用。  
  
   **Navigation 窗体**  
  
   ![导航对话框](../data-tools/media/simpleappnav.png "SimpleAppNav")  
  
|Navigation 窗体的控件|属性|  
|--------------------------------------|----------------|  
|Button|Name = btnGoToAdd|  
|Button|Name = btnGoToFillOrCancel|  
|Button|Name = btnExit|  
  
 **NewCustomer 窗体**  
  
 ![添加新客户和订单](../data-tools/media/simpleappnewcust.png "SimpleAppNewCust")  
  
|NewCustomer 窗体的控件|属性|  
|---------------------------------------|----------------|  
|文本框|Name = txtCustomerName|  
|文本框|Name = txtCustomerID<br /><br /> Readonly = True|  
|Button|Name = btnCreateAccount|  
|NumericUpdown|DecimalPlaces = 0<br /><br /> Maximum = 5000<br /><br /> Name = numOrderAmount|  
|DateTimePicker|Format = Short<br /><br /> Name = dtpOrderDate|  
|Button|Name = btnPlaceOrder|  
|Button|Name = btnAddAnotherAccount|  
|Button|Name = btnAddFinish|  
  
 **FillOrCancel 窗体**  
  
 ![填充或取消订单](../data-tools/media/simpleappcancelfill.png "SimpleAppCancelFill")  
  
|FillOrCancel 窗体的控件|属性|  
|----------------------------------------|----------------|  
|文本框|Name = txtOrderID|  
|Button|Name = btnFindByOrderID|  
|DateTimePicker|Format = Short<br /><br /> Name = dtpFillDate|  
|DataGridView|Name = dgvCustomerOrders<br /><br /> Readonly = True<br /><br /> RowHeadersVisible = False|  
|Button|Name = btnCancelOrder|  
|Button|Name = btnFillOrder|  
|Button|Name = btnFinishUpdates|  
  
## <a name="BKMK_storetheconnectionstring"></a> 存储连接字符串  
 当应用程序尝试打开数据库的连接时，应用程序必须能够访问连接字符串。 若要避免在每个窗体上手动输入该字符串，将字符串存储在应用程序配置文件在项目中，并创建任意窗体应用程序中调用方法将返回字符串的方法。  
  
 您可以发现中的连接字符串**SQL Server 对象资源管理器**通过右键单击数据库，选择**属性**，然后查找 ConnectionString 属性。 使用 Ctrl + A 选择字符串。  
  
1. 在中**解决方案资源管理器**，选择**属性**节点下的项目，然后选择**Settings.settings**。  
  
2. 在中**名称**列中，输入`connString`。  
  
3. 在中**类型**列表中，选择 **（连接字符串）**。  
  
4. 在中**作用域**列表中，选择**应用程序**。  
  
5. 在中**值**列中，输入连接字符串 （而无需任何外部引号），然后保存所做的更改。  
  
> [!NOTE]
> 在实际的应用程序，您应在连接字符串，安全地存储中所述[连接字符串和配置文件](https://msdn.microsoft.com/library/37df2641-661e-407a-a3fb-7bf9540f01e8)。  
  
## <a name="BKMK_retrievetheconnectionstring"></a> 检索连接字符串  
  
1. 在菜单栏上，选择**项目** > **添加引用**，以及如何将对 System.Configuration.dll 的引用。  
  
2. 在菜单栏上，选择**项目** > **添加类**若要将类文件添加到你的项目，并随后将文件命名`Utility`。  
  
     Visual Studio 创建该文件并将其显示在**解决方案资源管理器**。  
  
3. 在 Utility 文件中，使用下列代码替换占位符代码。 请注意标识代码段的编号注释（前缀为 Util-）。 代码后的表明确了要点。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using System.Threading.Tasks;  
    //Util-1 More namespaces.  
    using System.Configuration;   
  
    namespace SimpleDataApp  
    {  
        internal class Utility  
        {  
  
            //Get the connection string from App config file.  
            internal static string GetConnectionString()  
            {  
                //Util-2 Assume failure.  
                string returnValue = null;  
  
                //Util-3 Look for the name in the connectionStrings section.  
                ConnectionStringSettings settings =  
                ConfigurationManager.ConnectionStrings["SimpleDataApp.Properties.Settings.connString"];  
  
                //If found, return the connection string.  
                if (settings != null)  
                    returnValue = settings.ConnectionString;  
  
                return returnValue;  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Imports System  
    Imports System.Collections.Generic  
    Imports System.Linq  
    Imports System.Text  
    Imports System.Threading.Tasks  
    ' Util-1 More namespaces.  
    Imports System.Configuration  
  
    Namespace SimpleDataApp  
        Friend Class Utility  
  
            ' Get connection string from App config file.  
            Friend Shared Function GetConnectionString() As String  
  
                ' Util-2 Assume failure.  
                Dim returnValue As String = Nothing  
  
                ' Util-3 Look for the name in the connectionStrings section.  
                Dim settings As ConnectionStringSettings = ConfigurationManager.ConnectionStrings("SimpleDataApp.My.MySettings.connString")  
  
                ' If found, return the connection string.  
                If settings IsNot Nothing Then  
                    returnValue = settings.ConnectionString  
                End If  
  
                Return returnValue  
            End Function  
        End Class  
    End Namespace  
    ```  
  
    |注释|描述|  
    |-------------|-----------------|  
    |Util-1|添加 `System.Configuration` 命名空间。|  
    |Util-2|定义变量 `returnValue`，并将其初始化为 `null` (C#) 或 `Nothing` (Visual Basic)。|  
    |Util-3|即使输入`connString`中的连接字符串的名称作为**属性**窗口中，必须指定`"SimpleDataApp.Properties.Settings.connString"`(C#) 或`"SimpleDataApp.My.MySettings.connString"`(Visual Basic) 代码中。|  
  
## <a name="BKMK_writethecodefortheforms"></a> 编写窗体代码  
 本节包含对每个窗体功能的简要概述，并显示创建窗体的代码。 标识代码段的编号注释。  
  
### <a name="navigation-form"></a>Navigation 窗体  
 运行应用程序时，Navigation 窗体将打开。 按“添加帐户”按钮可以打开 NewCustomer 窗体。 按“填写或取消订单”按钮可以打开 FillOrCancel 窗体。 按“退出”按钮可以关闭应用程序。  
  
#### <a name="make-the-navigation-form-the-startup-form"></a>使 Navigation 窗体成为启动窗体  
 如果正在使用 C# 中，在**解决方案资源管理器**，打开 Program.cs，并更改`Application.Run`这样的代码行： `Application.Run(new Navigation());`  
  
 如果在使用 Visual Basic**解决方案资源管理器**，打开**属性**窗口中，选择**应用程序**选项卡，然后选择**SimpleDataApp.Navigation**中**启动窗体**列表。  
  
#### <a name="create-event-handlers"></a>创建事件处理程序  
 双击窗体以创建空的事件处理程序方法的三个按钮。  
  
#### <a name="create-code-for-navigation"></a>为 Navigation 创建代码  
 在 Navigation 窗体中，使用下列代码替换现有代码。  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.ComponentModel;  
using System.Data;  
using System.Drawing;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows.Forms;  
  
namespace SimpleDataApp  
{  
    public partial class Navigation : Form  
    {  
        public Navigation()  
        {  
            InitializeComponent();  
        }  
  
        //Open the NewCustomer form as a dialog box, which will return focus to the calling form when it closes.  
        private void btnGoToAdd_Click(object sender, EventArgs e)  
        {  
            Form frm = new NewCustomer();  
            frm.Show();  
        }  
  
        //Open the FillorCancel form as a dialog box.  
        private void btnGoToFillOrCancel_Click(object sender, EventArgs e)  
        {  
            Form frm = new FillOrCancel();  
            frm.ShowDialog();  
        }  
  
        //Close the application, not just the Navigation form.  
        private void btnExit_Click(object sender, EventArgs e)  
        {  
            this.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.ComponentModel  
Imports System.Data  
Imports System.Drawing  
Imports System.Linq  
Imports System.Text  
Imports System.Threading.Tasks  
Imports System.Windows.Forms  
  
Namespace SimpleDataApp  
    Partial Public Class Navigation  
        Inherits Form  
        Public Sub New()  
            InitializeComponent()  
        End Sub  
  
        ' Open the NewCustomer form as a dialog box, which will return focus to the calling form when it closes.  
        Private Sub btnGoToAdd_Click() Handles btnGoToAdd.Click  
            Dim frm As Form = New NewCustomer()  
            frm.Show()  
        End Sub  
  
        ' Open the FillorCancel form as a dialog box.  
        Private Sub btnGoToFillOrCancel_Click() Handles btnGoToFillOrCancel.Click  
            Dim frm As Form = New FillOrCancel()  
            frm.ShowDialog()  
        End Sub  
  
        ' Close the application, not just the Navigation form.  
        Private Sub btnExit_Click() Handles btnExit.Click  
            Me.Close()  
        End Sub  
    End Class  
End Namespace  
  
```  
  
### <a name="newcustomer-form"></a>NewCustomer 窗体  
 当输入客户名称，然后选择**创建帐户**按钮，NewCustomer 窗体创建一个客户帐户，和 SQL Server 将返回一个 IDENTITY 值作为新帐号。 然后将新帐户的顺序放通过指定数量和订单日期并选择**下订单**按钮。  
  
#### <a name="create-event-handlers"></a>创建事件处理程序  
 为窗体上的每个按钮创建一个空的 Click 事件处理程序。  
  
#### <a name="create-code-for-newcustomer"></a>为 NewCustomer 创建代码  
 将下列代码添加到 NewCustomer 窗体。 使用编号注释和代码后的表单步执行每个代码块。  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.ComponentModel;  
using System.Data;  
using System.Drawing;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows.Forms;  
//NC-1 More namespaces.  
using System.Data.SqlClient;  
using System.Configuration;  
  
namespace SimpleDataApp  
{  
    public partial class NewCustomer : Form  
    {  
        //NC-2 Storage for IDENTITY values returned from database.  
        private int parsedCustomerID;  
        private int orderID;  
  
        //NC-3 Specify a connection string.  
        string connstr = SimpleDataApp.Utility.GetConnectionString();  
  
        public NewCustomer()  
        {  
            InitializeComponent();  
        }  
  
        //NC-4 Create account.  
        private void btnCreateAccount_Click(object sender, EventArgs e)  
        {  
            //NC-5 Set up and run stored procedure only if Customer Name is present.  
            if (isCustomerName())  
            {  
  
                //NC-6 Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                //NC-7 Create a SqlCommand, and identify it as a stored procedure.  
                SqlCommand cmdNewCustomer = new SqlCommand("Sales.uspNewCustomer", conn);  
                cmdNewCustomer.CommandType = CommandType.StoredProcedure;  
  
                //NC-8 Add input parameter from the stored procedure and specify what to use as its value.  
                cmdNewCustomer.Parameters.Add(new SqlParameter("@CustomerName", SqlDbType.NVarChar, 40));  
                cmdNewCustomer.Parameters["@CustomerName"].Value = txtCustomerName.Text;  
  
                //NC-9 Add output parameter.  
                cmdNewCustomer.Parameters.Add(new SqlParameter("@CustomerID", SqlDbType.Int));  
                cmdNewCustomer.Parameters["@CustomerID"].Direction = ParameterDirection.Output;  
  
                //NC-10 try-catch-finally  
                try  
                {  
                    //NC-11 Open the connection.  
                    conn.Open();  
  
                    //NC-12 Run the stored procedure.  
                    cmdNewCustomer.ExecuteNonQuery();  
  
                    //NC-13 Customer ID is an IDENTITY value from the database.   
                    this.parsedCustomerID = (int)cmdNewCustomer.Parameters["@CustomerID"].Value;  
                    this.txtCustomerID.Text = Convert.ToString(parsedCustomerID);  
  
                }  
                catch  
                {  
                    //NC-14 A simple catch.  
  
                    MessageBox.Show("Customer ID was not returned. Account could not be created.");  
                }  
                finally  
                {  
                    //NC-15 Close the connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //NC-16 Verify that Customer Name is present.  
        private bool isCustomerName()  
        {  
            if (txtCustomerName.Text == "")  
            {  
                MessageBox.Show("Please enter a name.");  
                return false;  
            }  
            else  
            {  
                return true;  
            }  
        }  
  
        //NC-17 Place order.  
        private void btnPlaceOrder_Click(object sender, EventArgs e)  
        {  
            //NC-18 Set up and run stored procedure only if required input is present.  
            if (isPlaceOrderReady())  
            {  
                // Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                //NC-19 Create SqlCommand and identify it as a stored procedure.  
                SqlCommand cmdNewOrder = new SqlCommand("Sales.uspPlaceNewOrder", conn);  
                cmdNewOrder.CommandType = CommandType.StoredProcedure;  
  
                //NC-20 @CustomerID, which was an output parameter from uspNewCustomer.  
                cmdNewOrder.Parameters.Add(new SqlParameter("@CustomerID", SqlDbType.Int));  
                cmdNewOrder.Parameters["@CustomerID"].Value = this.parsedCustomerID;  
  
                //NC-21 @OrderDate.  
                cmdNewOrder.Parameters.Add(new SqlParameter("@OrderDate", SqlDbType.DateTime, 8));  
                cmdNewOrder.Parameters["@OrderDate"].Value = dtpOrderDate.Value;  
  
                //NC-22 @Amount.  
                cmdNewOrder.Parameters.Add(new SqlParameter("@Amount", SqlDbType.Int));  
                cmdNewOrder.Parameters["@Amount"].Value = numOrderAmount.Value;  
  
                //NC-23 @Status. For a new order, the status is always O (open).  
                cmdNewOrder.Parameters.Add(new SqlParameter("@Status", SqlDbType.Char, 1));  
                cmdNewOrder.Parameters["@Status"].Value = "O";  
  
                //NC-24 Add return value for stored procedure, which is orderID.  
                cmdNewOrder.Parameters.Add(new SqlParameter("@RC", SqlDbType.Int));  
                cmdNewOrder.Parameters["@RC"].Direction = ParameterDirection.ReturnValue;  
  
                //try-catch-finally  
                try  
                {  
                    //Open connection.  
                    conn.Open();  
  
                    //Run the stored procedure.  
                    cmdNewOrder.ExecuteNonQuery();  
  
                    //NC-25 Display the order number.  
                    this.orderID = (int)cmdNewOrder.Parameters["@RC"].Value;  
                    MessageBox.Show("Order number " + this.orderID + " has been submitted.");  
                }  
                catch  
                {  
                    //A simple catch.  
                    MessageBox.Show("Order could not be placed.");  
                }  
                finally  
                {  
                    //Close connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //NC-26 Verify that order data is ready.  
        private bool isPlaceOrderReady()  
        {  
            // Verify that CustomerID is present.  
            if (txtCustomerID.Text == "")  
            {  
                MessageBox.Show("Please create customer account before placing order.");  
                return false;  
            }  
  
            // Verify that Amount isn't 0.   
            else if ((numOrderAmount.Value < 1))  
            {  
                MessageBox.Show("Please specify an order amount.");  
                return false;  
            }  
            else  
            {  
                // Order can be submitted.  
                return true;  
            }  
        }  
  
        //NC-27 Reset the form for another new account.  
        private void btnAddAnotherAccount_Click(object sender, EventArgs e)  
        {  
            this.ClearForm();  
        }  
  
        //NC-28 Clear values from controls.  
        private void ClearForm()  
        {  
            txtCustomerName.Clear();  
            txtCustomerID.Clear();  
            dtpOrderDate.Value = DateTime.Now;  
            numOrderAmount.Value = 0;  
            this.parsedCustomerID = 0;  
        }  
  
        //NC-29 Close the form.  
        private void btnAddFinish_Click(object sender, EventArgs e)  
        {  
            this.Close();  
        }  
  
    }  
}  
  
```  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.ComponentModel  
Imports System.Data  
Imports System.Drawing  
Imports System.Linq  
Imports System.Text  
Imports System.Threading.Tasks  
Imports System.Windows.Forms  
' NC-1 More namespaces.  
Imports System.Data.SqlClient  
Imports System.Configuration  
  
Namespace SimpleDataApp  
    Partial Public Class NewCustomer  
        Inherits Form  
  
        ' NC-2 Storage for IDENTITY values returned from database.  
        Private parsedCustomerID As Integer  
        Private orderID As Integer  
  
        ' NC-3 Specify a connection string.  
        Private connstr As String = SimpleDataApp.Utility.GetConnectionString()  
  
        Public Sub New()  
            InitializeComponent()  
        End Sub  
  
        ' NC-4 Create account.  
        Private Sub btnCreateAccount_Click() Handles btnCreateAccount.Click  
  
            ' NC-5 Set up and run stored procedure only if Customer Name is present.  
            If isCustomerName() Then  
  
                ' NC-6 Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' NC-7 Create a SqlCommand, and identify it as a stored procedure.  
                Dim cmdNewCustomer As New SqlCommand("Sales.uspNewCustomer", conn)  
                cmdNewCustomer.CommandType = CommandType.StoredProcedure  
  
                ' NC-8 Add input parameter from the stored procedure and specify what to use as its value.  
                cmdNewCustomer.Parameters.Add(New SqlParameter("@CustomerName", SqlDbType.NVarChar, 40))  
                cmdNewCustomer.Parameters("@CustomerName").Value = txtCustomerName.Text  
  
                ' NC-9 Add output parameter.  
                cmdNewCustomer.Parameters.Add(New SqlParameter("@CustomerID", SqlDbType.Int))  
                cmdNewCustomer.Parameters("@CustomerID").Direction = ParameterDirection.Output  
  
                ' NC-10 try-catch-finally  
                Try  
                    ' NC-11 Open the connection.  
                    conn.Open()  
  
                    ' NC-12 Run the stored procedure.  
                    cmdNewCustomer.ExecuteNonQuery()  
  
                    ' NC-13 Customer ID is an IDENTITY value from the database.   
                    Me.parsedCustomerID = CInt(cmdNewCustomer.Parameters("@CustomerID").Value)  
                    Me.txtCustomerID.Text = Convert.ToString(parsedCustomerID)  
  
                Catch  
                    ' NC-14 A simple catch.  
                    MessageBox.Show("Customer ID was not returned. Account could not be created.")  
                Finally  
                    ' NC-15 Close the connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' NC-16 Verify that Customer Name is present.  
        Private Function isCustomerName() As Boolean  
            If txtCustomerName.Text = "" Then  
                MessageBox.Show("Please enter a name.")  
                Return False  
            Else  
                Return True  
            End If  
        End Function  
  
        ' NC-17 Place order.  
        Private Sub btnPlaceOrder_Click() Handles btnPlaceOrder.Click  
  
            ' NC-18 Set up and run stored procedure only if necessary input is present.  
            If isPlaceOrderReady() Then  
  
                ' Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' NC-19 Create SqlCommand and identify it as a stored procedure.  
                Dim cmdNewOrder As New SqlCommand("Sales.uspPlaceNewOrder", conn)  
                cmdNewOrder.CommandType = CommandType.StoredProcedure  
  
                ' NC-20 @CustomerID, which was an output parameter from uspNewCustomer.  
                cmdNewOrder.Parameters.Add(New SqlParameter("@CustomerID", SqlDbType.Int))  
                cmdNewOrder.Parameters("@CustomerID").Value = Me.parsedCustomerID  
  
                ' NC-21 @OrderDate.  
                cmdNewOrder.Parameters.Add(New SqlParameter("@OrderDate", SqlDbType.DateTime, 8))  
                cmdNewOrder.Parameters("@OrderDate").Value = dtpOrderDate.Value  
  
                ' NC-22 @Amount.  
                cmdNewOrder.Parameters.Add(New SqlParameter("@Amount", SqlDbType.Int))  
                cmdNewOrder.Parameters("@Amount").Value = numOrderAmount.Value  
  
                ' NC-23 @Status. For a new order, the status is always O (open).  
                cmdNewOrder.Parameters.Add(New SqlParameter("@Status", SqlDbType.[Char], 1))  
                cmdNewOrder.Parameters("@Status").Value = "O"  
  
                ' NC-24 Add return value for stored procedure, which is orderID.  
                cmdNewOrder.Parameters.Add(New SqlParameter("@RC", SqlDbType.Int))  
                cmdNewOrder.Parameters("@RC").Direction = ParameterDirection.ReturnValue  
  
                ' try-catch-finally  
                Try  
                    ' Open connection.  
                    conn.Open()  
  
                    ' Run the stored procedure.  
                    cmdNewOrder.ExecuteNonQuery()  
  
                    ' NC-25 Display the order number.  
                    Me.orderID = CInt(cmdNewOrder.Parameters("@RC").Value)  
                    MessageBox.Show("Order number " & (Me.orderID).ToString & " has been submitted.")  
  
                Catch  
                    ' A simple catch.  
                    MessageBox.Show("Order could  not be placed.")  
  
                Finally  
                    ' Close connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' NC-26 Verify that order data is ready.  
        Private Function isPlaceOrderReady() As Boolean  
  
            ' Verify that CustomerID is present.  
            If txtCustomerID.Text = "" Then  
                MessageBox.Show("Please create customer account before placing order.")  
                Return False  
  
                ' Verify that Amount isn't 0.   
            ElseIf (numOrderAmount.Value < 1) Then  
  
                MessageBox.Show("Please specify an order amount.")  
                Return False  
            Else  
                ' Order can be submitted.  
                Return True  
            End If  
        End Function  
  
        ' NC-27 Reset the form for another new account.  
        Private Sub btnAddAnotherAccount_Click() Handles btnAddAnotherAccount.Click  
            Me.ClearForm()  
        End Sub  
  
        ' NC-28 Clear values from controls.  
        Private Sub ClearForm()  
            txtCustomerName.Clear()  
            txtCustomerID.Clear()  
            dtpOrderDate.Value = DateTime.Now  
            numOrderAmount.Value = 0  
            Me.parsedCustomerID = 0  
        End Sub  
  
        ' NC-29 Close the form.  
        Private Sub btnAddFinish_Click() Handles btnAddFinish.Click  
            Me.Close()  
        End Sub  
  
    End Class  
End Namespace  
```  
  
|注释|描述|  
|-------------|-----------------|  
|NC-1|添加`System.Data.SqlClient`和`System.Configuration`到命名空间的列表。|  
|NC-2|声明 `parsedCustomerID` 和 `orderID` 变量，以后将用到它们。|  
|NC-3|调用 `GetConnectionString` 方法以从应用配置文件中获取连接字符串，并将该值存储在 `connstr` 字符串变量中。|  
|NC-4|将代码添加到 `btnCreateAccount` 按钮的 Click 事件处理程序。|  
|NC-5|将对 `isCustomerName` 的调用包装在 Click 事件代码周围，以便让 `uspNewCustomer` 只在存在客户名称的情况下运行。|  
|NC-6|创建 `SqlConnection` 对象 (`conn`)，并在 `connstr` 的连接字符串中传递。|  
|NC-7|创建 `SqlCommand` 对象 `cmdNewCustomer`。<br /><br /> -指定`Sales.uspNewCustomer`作为要运行的存储过程。<br />-使用`CommandType`属性指定的命令是存储的过程。|  
|NC-8|从存储过程添加 `@CustomerName` 输入参数。<br /><br /> -将参数添加到`Parameters`集合。<br />-使用`SqlDbType`枚举来指定参数类型为 nvarchar(40)。<br />-指定`txtCustomerName.Text`作为源。|  
|NC-9|从存储过程添加输出参数。<br /><br /> -将参数添加到`Parameters`集合。<br />-使用`ParameterDirection.Output`来标识作为输出参数。|  
|NC-10|添加一个 Try – Catch – Finally 块来打开连接，运行存储的过程、 处理异常，然后关闭该连接。|  
|NC-11|打开在 NC-6 中创建的连接 (`conn`)。|  
|NC-12|使用`ExecuteNonQuery`方法`cmdNewCustomer`运行`Sales.uspNewCustomer`存储过程。 此存储过程运行`INSERT`语句中，不是查询。|  
|NC-13|`@CustomerID` 值以 IDENTITY 值的形式从数据库返回。 由于它是一个整数，您必须将其转换为一个字符串，使其显示在**客户 ID**文本框。<br /><br /> -你声明`parsedCustomerID`在 nc-2。<br />-存储`@CustomerID`中的值`parsedCustomerID`以供将来使用。<br />-将返回的客户 ID 转换为字符串，并将其插入到`txtCustomerID.Text`。|  
|NC-14|此示例中，将添加一个简单的 （不是生产质量） catch 子句。|  
|NC-15|请始终在使用完连接后将其关闭，以便可以将其释放到连接池。 请参阅[SQL Server 连接池 (ADO.NET)](https://msdn.microsoft.com/library/8xx3tyca\(l=en-us,v=VS.110\).aspx)。|  
|NC-16|定义用于验证客户名称是否存在的方法。<br /><br /> -如果文本框为空，则显示一条消息，并返回`false`，这是因为创建该帐户所需的名称。<br />-如果文本框不为空，返回`true`。|  
|NC-17|将代码添加到 `btnPlaceOrder` 按钮的 Click 事件处理程序。|  
|NC-18|将对 `isPlaceOrderReady` 的调用包装在 `btnPlaceOrder_Click` 事件代码周围，这样一来，如果不存在所需的输入，`uspPlaceNewOrder` 就不会运行。|  
|NC-19 到 NC-25|代码中的这些段类似于为 `btnCreateAccount_Click` 事件处理程序添加的代码。<br /><br /> -   NC-19. 创建 `SqlCommand` 对象 `cmdNewOrder`，并将 `Sales.uspPlaceOrder` 指定为存储过程。<br />-NC-20 到 nc-23 是存储过程的输入的参数。<br />-   NC-24. `@RC` 将包含一个返回值，该值是从数据库生成的订单 ID。 此参数的方向指定为 `ReturnValue`。<br />-   NC-25. 将订单 ID 的值存储在 NC-2 上声明的 `orderID` 变量中，并在消息框中显示该值。|  
|NC-26|定义用于验证客户 ID 是否存在，以及是否已经在 `numOrderAmount` 中指定了数量的方法。|  
|NC-27|调用 `btnAddAnotherAccount` Click 事件处理程序中的 `ClearForm` 方法。|  
|NC-28|如果想要添加另一个客户，请创建 `ClearForm` 方法以清除窗体中的值。|  
|NC29|关闭 NewCustomer 窗体，并使焦点返回到 Navigation 窗体。|  
  
### <a name="fillorcancel-form"></a>FillOrCancel 窗体  
 FillorCancel 窗体将运行查询时要返回订单输入订单 ID 并选择**查找订单**按钮。 返回的行在只读数据网格中显示。 如果您选择，可以将标记为已取消 (X) 的顺序**取消订单**按钮，也可以将订单标记为已填写 (F) 如果您选择**填写订单**按钮。 如果选择**查找订单**按钮再次，此时将显示已更新的行。  
  
#### <a name="create-event-handlers"></a>创建事件处理程序  
 为窗体上的四个按钮创建空的 Click 事件处理程序。  
  
#### <a name="create-code-for-fillorcancel"></a>为 FillOrCancel 创建代码  
 将下列代码添加到 FillOrCancel 窗体。 使用编号注释和代码后的表单步执行代码块。  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.ComponentModel;  
using System.Data;  
using System.Drawing;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Windows.Forms;  
//FC-1 More namespaces.  
using System.Text.RegularExpressions;  
using System.Data.SqlClient;  
using System.Configuration;  
  
namespace SimpleDataApp  
{  
    public partial class FillOrCancel : Form  
    {  
        //FC-2 Storage for OrderID.  
        private int parsedOrderID;  
  
        //FC-3 Specify a connection string.  
        string connstr = SimpleDataApp.Utility.GetConnectionString();  
  
        public FillOrCancel()  
        {  
            InitializeComponent();  
        }  
  
        //FC-4 Find an order.  
        private void btnFindByOrderID_Click(object sender, EventArgs e)  
        {  
            //FC-5 Prepare the connection and the command.  
            if (isOrderID())  
            {  
                //Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                //Define a query string that has a parameter for orderID.  
                string sql = "select * from Sales.Orders where orderID = @orderID";  
  
                //Create a SqlCommand object.  
                SqlCommand cmdOrderID = new SqlCommand(sql, conn);  
  
                //Define the @orderID parameter and its value.  
                cmdOrderID.Parameters.Add(new SqlParameter("@orderID", SqlDbType.Int));  
                cmdOrderID.Parameters["@orderID"].Value = parsedOrderID;  
  
                //try-catch-finally  
                try  
                {  
                    //FC-6 Run the command and display the results.  
                    //Open the connection.  
                    conn.Open();  
  
                    //Run the command by using SqlDataReader.  
                    SqlDataReader rdr = cmdOrderID.ExecuteReader();  
  
                    //Create a data table to hold the retrieved data.  
                    DataTable dataTable = new DataTable();  
  
                    //Load the data from SqlDataReader into the data table.  
                    dataTable.Load(rdr);  
  
                    //Display the data from the data table in the data grid view.  
                    this.dgvCustomerOrders.DataSource = dataTable;  
  
                    //Close the SqlDataReader.  
                    rdr.Close();  
                }  
                catch  
                {  
                    //A simple catch.  
                    MessageBox.Show("The requested order could not be loaded into the form.");  
                }  
                finally  
                {  
                    //Close the connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //FC-7 Cancel an order.  
        private void btnCancelOrder_Click(object sender, EventArgs e)  
        {  
            //Set up and run stored procedure only if OrderID is ready.  
            if (isOrderID())  
            {  
                //Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                // Create command and identify it as a stored procedure.  
                SqlCommand cmdCancelOrder = new SqlCommand("Sales.uspCancelOrder", conn);  
                cmdCancelOrder.CommandType = CommandType.StoredProcedure;  
  
                cmdCancelOrder.Parameters.Add(new SqlParameter("@orderID", SqlDbType.Int));  
                cmdCancelOrder.Parameters["@orderID"].Value = parsedOrderID;  
  
                // try-catch-finally  
                try  
                {  
                    // Open the connection.  
                    conn.Open();  
  
                    // Run the cmdCancelOrder command.  
                    cmdCancelOrder.ExecuteNonQuery();  
                }  
                // A simple catch.  
                catch  
                {  
                    MessageBox.Show("The cancel operation was not completed.");  
                }  
                finally  
                {  
                    //Close connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //FC-8 Fill an order.  
        private void btnFillOrder_Click(object sender, EventArgs e)  
        {  
            //Set up and run stored procedure only if OrderID is ready.  
            if (isOrderID())  
            {  
                //Create the connection.  
                SqlConnection conn = new SqlConnection(connstr);  
  
                //Create command and identify it as a stored procedure.  
                SqlCommand cmdFillOrder = new SqlCommand("Sales.uspFillOrder", conn);  
                cmdFillOrder.CommandType = CommandType.StoredProcedure;  
  
                // Add input parameter from the stored procedure.  
                cmdFillOrder.Parameters.Add(new SqlParameter("@orderID", SqlDbType.Int));  
                cmdFillOrder.Parameters["@orderID"].Value = parsedOrderID;  
  
                //Add the second input parameter.  
                cmdFillOrder.Parameters.Add(new SqlParameter("@FilledDate", SqlDbType.DateTime, 8));  
                cmdFillOrder.Parameters["@FilledDate"].Value = dtpFillDate.Value;  
  
                //try-catch-finally  
                try  
                {  
                    //Open the connection.  
                    conn.Open();  
  
                    //Run the cmdFillOrder command.  
                    cmdFillOrder.ExecuteNonQuery();  
                }  
                catch  
                {  
                    //A simple catch.  
                    MessageBox.Show("The fill operation was not completed.");  
                }  
                finally  
                {  
                    //Close the connection.  
                    conn.Close();  
                }  
            }  
        }  
  
        //FC-9 Verify that OrderID is ready.  
        private bool isOrderID()  
        {  
  
            //Check for input in the Order ID text box.  
            if (txtOrderID.Text == "")  
            {  
                MessageBox.Show("Please specify the Order ID.");  
                return false;  
            }  
  
            // Check for characters other than integers.  
            else if (Regex.IsMatch(txtOrderID.Text, @"^\D*$"))  
            {  
               //Show message and clear input.  
                MessageBox.Show("Please specify integers only.");  
                txtOrderID.Clear();  
                return false;  
            }  
            else  
            {  
                //Convert the text in the text box to an integer to send to the database.  
                parsedOrderID = Int32.Parse(txtOrderID.Text);  
                return true;  
            }  
        }  
  
        //Close the form.  
        private void btnFinishUpdates_Click(object sender, EventArgs e)  
        {  
            this.Close();  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Collections.Generic  
Imports System.ComponentModel  
Imports System.Data  
Imports System.Drawing  
Imports System.Linq  
Imports System.Text  
Imports System.Threading.Tasks  
Imports System.Windows.Forms  
' FC-1 More namespaces.  
Imports System.Text.RegularExpressions  
Imports System.Data.SqlClient  
Imports System.Configuration  
  
Namespace SimpleDataApp  
    Partial Public Class FillOrCancel  
        Inherits Form  
        ' FC-2 Storage for OrderID.  
        Private parsedOrderID As Integer  
  
        ' FC-3 Specify a connection string.  
        Private connstr As String = SimpleDataApp.Utility.GetConnectionString()  
  
        Public Sub New()  
            InitializeComponent()  
        End Sub  
  
        ' FC-4 Find an order.  
        Private Sub btnFindByOrderID_Click() Handles btnFindByOrderID.Click  
  
            ' FC-5 Prepare the connection and the command.  
  
            If isOrderID() Then  
                ' Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' Define the query string that has a parameter for orderID.  
                Dim sql As String = "select * from Sales.Orders where orderID = @orderID"  
  
                ' Create a SqlCommand object.  
                Dim cmdOrderID As New SqlCommand(sql, conn)  
  
                ' Define the @orderID parameter and its value.  
                cmdOrderID.Parameters.Add(New SqlParameter("@orderID", SqlDbType.Int))  
                cmdOrderID.Parameters("@orderID").Value = parsedOrderID  
  
                ' try-catch-finally  
                Try  
                    ' FC-6 Run the command and display the results.  
                    ' Open connection.  
                    conn.Open()  
  
                    ' Run the command by using SqlDataReader.  
                    Dim rdr As SqlDataReader = cmdOrderID.ExecuteReader()  
  
                    ' Create a data table to hold the retrieved data.  
                    Dim dataTable As New DataTable()  
  
                    ' Load the data from SqlDataReader into the data table.  
                    dataTable.Load(rdr)  
  
                    ' Display the data from the data table in the data grid view.  
                    Me.dgvCustomerOrders.DataSource = dataTable  
  
                    ' Close the SqlDataReader.  
                    rdr.Close()  
                Catch  
                    ' A simple catch.  
                    MessageBox.Show("The requested order could not be loaded into the form.")  
                Finally  
                    ' Close the connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' FC-7 Cancel an order.  
        Private Sub btnCancelOrder_Click() Handles btnCancelOrder.Click  
  
            ' Set up and run stored procedure only if OrderID is ready.  
            If isOrderID() Then  
  
                ' Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' Create the command and identify it as a stored procedure.  
                Dim cmdCancelOrder As New SqlCommand("Sales.uspCancelOrder", conn)  
                cmdCancelOrder.CommandType = CommandType.StoredProcedure  
  
                ' Add input parameter from the stored procedure.  
                cmdCancelOrder.Parameters.Add(New SqlParameter("@orderID", SqlDbType.Int))  
                cmdCancelOrder.Parameters("@orderID").Value = parsedOrderID  
  
                ' try-catch-finally  
                Try  
                    ' Open the connection.  
                    conn.Open()  
  
                    ' Run the cmdCancelOrder command.  
                    cmdCancelOrder.ExecuteNonQuery()  
                Catch  
                    ' A simple catch.  
                    MessageBox.Show("The cancel operation was not completed.")  
                Finally  
                    ' Close connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' FC-8 Fill an order.  
        Private Sub btnFillOrder_Click() Handles btnFillOrder.Click  
  
            ' Set up and run stored procedure only if OrderID is ready.  
            If isOrderID() Then  
  
                ' Create the connection.  
                Dim conn As New SqlConnection(connstr)  
  
                ' Create command and identify it as a stored procedure.  
                Dim cmdFillOrder As New SqlCommand("Sales.uspFillOrder", conn)  
                cmdFillOrder.CommandType = CommandType.StoredProcedure  
  
                ' Add input parameter from the stored procedure.  
                cmdFillOrder.Parameters.Add(New SqlParameter("@orderID", SqlDbType.Int))  
                cmdFillOrder.Parameters("@orderID").Value = parsedOrderID  
  
                ' Add second input parameter.  
                cmdFillOrder.Parameters.Add(New SqlParameter("@FilledDate", SqlDbType.DateTime, 8))  
                cmdFillOrder.Parameters("@FilledDate").Value = dtpFillDate.Value  
  
                ' try-catch-finally  
                Try  
                    ' Open the connection.  
                    conn.Open()  
  
                    ' Run the cmdFillOrder command.   
                    cmdFillOrder.ExecuteNonQuery()  
                Catch  
                    ' A simple catch.  
                    MessageBox.Show("The fill operation was not completed.")  
                Finally  
                    ' Close the connection.  
                    conn.Close()  
                End Try  
            End If  
        End Sub  
  
        ' FC-9 Verify that OrderID is ready.  
        Private Function isOrderID() As Boolean  
  
            ' Check for input in the Order ID text box.  
            If txtOrderID.Text = "" Then  
                MessageBox.Show("Please specify the Order ID.")  
                Return False  
  
                ' Check for characters other than integers.  
            ElseIf Regex.IsMatch(txtOrderID.Text, "^\D*$") Then  
  
                ' Show message and clear input.  
                MessageBox.Show("Please specify integers only.")  
                txtOrderID.Clear()  
                Return False  
  
            Else  
                ' Convert the text in the text box to an integer to send to the database.  
                parsedOrderID = Int32.Parse(txtOrderID.Text)  
                Return True  
  
            End If  
        End Function  
  
        ' Close the form.  
        Private Sub btnFinishUpdates_Click() Handles btnFinishUpdates.Click  
            Me.Close()  
        End Sub  
    End Class  
End Namespace  
```  
  
|注释|描述|  
|-------------|-----------------|  
|FC-1|添加`System.Data.SqlClient`， `System.Configuration`，和`System.Text.RegularExpressions`到命名空间的列表。|  
|FC-2|声明 `parsedOrderID` 变量。|  
|FC-3|调用 `GetConnectionString` 方法以从应用配置文件中获取连接字符串，并将该值存储在 `connstr` 字符串变量中。|  
|FC-4|将代码添加到 `btnFindOrderByID` 的 Click 事件处理程序。|  
|FC-5|在尝试运行 SQL 语句或存储过程之前，这些任务都是必需的。<br /><br /> -创建`SqlConnection`对象。<br />-定义 SQL 语句或指定的存储过程的名称。 （在这种情况下，将运行 `SELECT` 语句。）<br />-创建`SqlCommand`对象。<br />-定义任何参数的 SQL 语句或存储的过程。|  
|FC-6|此代码使用 `SqlDataReader` 和 `DataTable` 检索并显示查询结果。<br /><br /> -打开连接。<br />-创建`SqlDataReader`对象， `rdr`，通过运行`ExecuteReader`方法`cmdOrderID`。<br />-创建`DataTable`对象以保存检索到的数据。<br />-将数据从加载`SqlDataReader`对象插入`DataTable`对象。<br />-显示数据在数据网格视图中通过指定`DataTable`作为`DataSource`数据网格视图。<br />-关闭`SqlDataReader`。|  
|FC-7|将代码添加到 `btnCancelOrder` 的 Click 事件处理程序。 此代码运行 `Sales.uspCancelOrder` 存储过程。|  
|FC-8|将代码添加到 `btnFillOrder` 的 Click 事件处理程序。 此代码运行 `Sales.uspFillOrder` 存储过程。|  
|FC-9|创建一个方法来确认`OrderID`已准备好将作为参数提交`SqlCommand`对象。<br /><br /> -请确保 ID 已进入`txtOrderID`。<br />-使用`Regex.IsMatch`来定义非整数字符的简单检查。<br />-你声明`parsedOrderID`在 fc-2 变量。<br />-如果输入是有效的将文本转换为整数，并将存储中的值`parsedOrderID`变量。<br />-包装`isOrderID`方法围绕`btnFindByOrderID`， `btnCancelOrder`，和`btnFillOrder`Click 事件处理程序。|  
  
## <a name="BKMK_testyourapplication"></a> 测试应用程序  
 选择 F5 键以生成和测试后代码单击每个事件处理程序，你的应用程序，然后在完成编码。
