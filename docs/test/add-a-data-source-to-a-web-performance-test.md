---
title: 将数据源添加到 Web 性能测试
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- Web performance tests, walkthroughs
- Web performance tests, data binding (database)
ms.assetid: 2ada376d-f168-455d-9643-6acb535360c1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7c7f947be01500b0d45b81d404206722ac71084a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75565404"
---
# <a name="add-a-data-source-to-a-web-performance-test"></a>将数据源添加到 Web 性能测试

绑定数据以便为相同的测试提供不同的值，例如，为窗体 POST 参数提供不同的值。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

![将数据绑定到 Web 性能测试](../test/media/web_test_databinding_conceptual.png)

我们将使用一个示例 ASP.NET 应用程序。 它有三个 .aspx 页：默认页、红色页和蓝色页  。 默认页具有一个用于选择红色或蓝色的单选控件和一个提交按钮。 其他两个 .aspx 页非常简单  。 一个具有名为“红色”的标签，另一个具有名为“蓝色”的标签。 当您选择在默认页上进行提交时，将显示其他两个页面之一。 可以下载 [ColorWebApp](https://code.msdn.microsoft.com/Sample-ColorWebApp-76ff7506) 示例，或者直接使用自己的 Web 应用来跟随我们操作。

![运行要测试的 Web 应用程序](../test/media/web_test_databinding_runwebapp.png)

你的解决方案也应包含浏览 Web 应用程序的页面的 Web 性能测试。

![带 Web 性能测试的解决方案](../test/media/web_test_databinding_solution.png)

## <a name="create-a-sql-database"></a>创建一个 SQL 数据库

::: moniker range="vs-2017"

1. 如果还没有 Visual Studio Enterprise，可以从 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页进行下载。

2. 创建一个 SQL 数据库。

     ![添加新的 SQL 数据库](../test/media/web_test_databinding_sql_addnewdb.png)

3. 创建一个数据库项目。

     ![从数据库创建新项目](../test/media/web_test_databinding_sql_addnewdbproject.png)

4. 向数据库项目中添加表。

     ![向数据库项目添加新表](../test/media/web_test_databinding_sql_addnewdbtablename.png)

5. 向表中添加字段。

     ![向表中添加字段](../test/media/web_test_databinding_sql_addnewdbaddfields.png)

6. 发布数据库项目。

     ![从“解决方案资源管理器”发布数据库项目](../test/media/web_test_databinding_sql_addnewdbpublish.png)

7. 向字段中添加数据。

     ![向字段添加数据](../test/media/web_test_databinding_sql_addnewfieldsadddata.png)

::: moniker-end

::: moniker range="vs-2019"

1. 如果还没有 Visual Studio Enterprise，可以从 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页进行下载。

2. 创建一个 SQL 数据库。

     ![添加新的 SQL 数据库](../test/media/web_test_databinding_sql_addnewdb.png)

3. 创建一个数据库项目。

     ![从数据库创建新项目](../test/media/web_test_databinding_sql_addnewdbproject.png)

4. 向数据库项目中添加表。

     ![向数据库项目添加新表](../test/media/web_test_databinding_sql_addnewdbtablename.png)

5. 向表中添加字段。

     ![向表中添加字段](../test/media/web_test_databinding_sql_addnewdbaddfields.png)

6. 发布数据库项目。

     ![从“解决方案资源管理器”发布数据库项目](../test/media/web_test_databinding_sql_addnewdbpublish.png)

7. 向字段中添加数据。

     ![向字段添加数据](../test/media/web_test_databinding_sql_addnewfieldsadddata.png)

::: moniker-end

## <a name="add-the-data-source"></a>添加数据源

1. 添加数据源。

     ![向 Web 性能测试添加数据源](../test/media/web_test_databinding_sql_adddatasource.png)

2. 选择数据源的类型并为其命名。

     ![命名数据库源](../test/media/web_test_databinding_sql_adddatasourcedialog.png)

3. 创建连接。

     ![选择新连接](../test/media/web_test_databinding_sql_adddatasourcedialogconnectionnew.png)

     输入连接详细信息。

     ![输入 SQL 数据库连接属性](../test/media/web_test_databinding_sql_adddatasourcedialogconnection.png)

4. 选择要用于测试的表。

     ![将 Color 表添加为数据源](../test/media/web_test_databinding_sql_adddatasourcedialogaddtable.png)

     表将绑定到测试。

     ![添加到 Web 性能测试的数据源节点](../test/media/web_test_databinding_requestnodeadded_mdb.png)

5. 保存测试。

## <a name="bind-the-data"></a>绑定数据

1. 绑定 ColorName 字段  。

     ![将 ColorName 字段绑定到 RadioButtonList1 值](../test/media/web_test_databinding_sql_binddatasource.png)

2. 在“解决方案资源管理器”中，打开 Local.testsettings 文件并选择“每数据源行运行一次”选项    。

     ![编辑测试设置文件](../test/media/web_test_databinding_sql_testsettings.png)

3. 保存 Web 性能测试。

## <a name="run-the-test-with-the-data"></a>使用数据运行测试

1. 运行测试。

     ![运行 Web 性能测试来验证绑定](../test/media/web_test_databinding_sql_runtest.png)

     为每个数据行显示两个运行。 运行 1 发送页 Red.aspx 的请求，运行 2 发送页 Blue.aspx 的请求   。

     ![测试运行结果](../test/media/web_test_databinding_sql_runresults.png)

     在绑定到数据源时，可能会违反默认响应 URL 规则。 在这种情况下，运行 2 中的错误是由规则引起的，该规则期望来自原始测试记录的 Red.aspx 页，而数据绑定现在将其指向 Blue.aspx 页   。

2. 通过删除“响应 URL”验证规则并重新运行测试来纠正验证错误  。

     ![删除响应 URL 验证规则](../test/media/web_test_databinding_sql_deleteresponseurl.png)

     使用数据绑定通过 Web 性能测试。

     ![使用数据绑定的测试通过数](../test/media/web_test_databinding_sql_deleteresponseurlrunresults.png)

## <a name="q--a"></a>问题解答

### <a name="q-what-databases-can-i-use-as-a-data-source"></a>问：可将什么数据库用作数据源？

**答：** 可以使用：

- Microsoft SQL Azure。

- 任何版本的 Microsoft SQL Server 2005 或更高版本。

- Microsoft SQL Server 数据库文件（包括 SQL Express）。

- Microsoft ODBC。

- 使用 OLE DB 的 .NET Framework 提供程序的 Microsoft Access 文件。

- Oracle 7.3、8i、9i 或 10g。

### <a name="q-how-do-i-use-a-comma-separated-value-csv-text-file-as-a-data-source"></a>问：如何将逗号分隔的值 (CSV) 文本文件用作数据源？

**答：** 操作方法如下：

1. 创建一个文件夹来组织项目数据库项目并添加一个项。

     ![向数据文件夹添加新项](../test/media/web_test_databinding_foldernewitem.png)

2. 创建文本文件。

     ![命名新文本文件为 ColorData.csv](../test/media/web_test_databinding_foldernewitemtextfile.png)

3. 编辑文本文件并添加：

    ```text
    ColorId, ColorName
    0,Red
    1,Blue
    ```

4. 使用[添加数据源](#add-the-data-source)中的步骤，但选择 CSV 文件作为数据源。

     ![输入名称，并选择 CSV 文件](../test/media/web_test_databinding_adddatasourcedialog.png)

### <a name="q-what-if-my-existing-csv-file-does-not-contain-column-headers"></a>问：如果我的现有 CSV 文件不包含列标头，该怎么办？

**答：** 如果不能添加列标头，则可以使用架构说明文件将 CSV 文件视为数据库。

1. 添加名为 schema.ini 的新文本文件  。

     ![添加 schema.ini 文件](../test/media/web_test_databinding_schemafile.png)

2. 编辑该 schema.ini 文件，添加描述数据结构的信息  。 例如，描述 CSV 文件的架构文件可能如下所示：

    ```text
    [testdata.csv]
    ColNameHeader=False
    ```

3. 将数据源添加到测试。

     ![向 Web 性能测试添加数据源](../test/media/web_test_databinding_sql_adddatasource.png)

4. 如果正在使用 schema.ini 文件，请选择“数据库”（不是 CSV 文件）作为数据源，并为其命名   。

     ![添加数据库数据源](../test/media/web_test_databinding_adddatasourcecolortext.png)

5. 创建新连接。

     ![选择新连接](../test/media/web_test_databinding_sql_adddatasourcedialogconnectionnew.png)

6. 选择 OLE DB 的 .NET Framework 数据提供程序。

     ![选择 .NET Framework OLE DB 数据提供程序](../test/media/web_test_databinding_adddatasourcecolortext2.png)

7. 选择“高级”  。

     ![选择“高级”](../test/media/web_test_databinding_advanced.png)

8. 对于 Provider 属性，请选择 Microsoft.Jet.OLEDB.4.0，并将“扩展属性”设置为 Text;HDR=NO  。

     ![应用高级属性](../test/media/web_test_databinding_advancedproperties.png)

9. 键入包含架构文件的文件夹的名称并测试您的连接。

     ![输入指向数据文件夹的路径](../test/media/web_test_databinding_adddatasourcecolortext5.png)

10. 选择要使用的 CSV 文件。

     ![选择文本文件](../test/media/web_test_databinding_adddatasourcecolortext6.png)

     完成后，CSV 文件会以表格形式显示。

     ![添加到测试的数据源](../test/media/web_test_databinding_adddatasourcecolortext7.png)

### <a name="q-how-do-i-use-an-xml-file-as-a-data-source"></a>问：如何将 XML 文件用作数据源？

**答：** 可以。

1. 创建一个文件夹来组织项目数据库项目并添加一个项。

     ![向数据文件夹添加新项](../test/media/web_test_databinding_foldernewitem.png)

2. 创建 XML 文件。

     ![添加 ColorData.xml 文件](../test/media/web_test_databinding_additemxmlfile.png)

3. 编辑 XML 文件并添加您的数据：

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <ColorData>
        <Color>
            <ColorId>0</ColorId>
            <ColorName>Red</ColorName>
        </Color>
        <Color>
            <ColorId>1</ColorId>
            <ColorName>Blue</ColorName>
        </Color>
    </ColorData>
    ```

4. 使用[添加数据源](#add-the-data-source)中的步骤，但选择 XML 文件作为数据源。

     ![输入名称，并选择 XML 文件](../test/media/web_test_databinding_adddatasourcedialogxml.png)

### <a name="q-can-i-add-data-binding-to-a-web-service-request-that-uses-soap"></a>问：我是否能将数据绑定添加到使用 SOAP 的 Web 服务请求？

**答：** 可以，必须手动更改 SOAP XML。

1. 选择请求树中的 Web 服务请求，并在“属性”窗口中，选择 String Body 属性中的省略号 (…)。

     ![编辑 Web 服务字符串主体](../test/media/web_test_databinding_webservicerequest.png)

2. 使用下面的语法，将 SOAP 正文中的值替换为数据绑定值：

    ```xml
    {{DataSourceName.TableName.ColumnName}}
    ```

    例如，如果你有以下代码：

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <CheckStatus xmlns="http://tempuri.org/">
                <userName>string</userName> <password>string</password> <orderID>int</orderID>
            </CheckStatus>
        </soap:Body>
    </soap:Envelope>
    ```

    您可以将其更改为：

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <CheckStatus xmlns="http://tempuri.org/">
                <userName>{{DataSourceName.Users.Name}}</userName> <password>{{DataSourceName.Users.Password}}</password> <orderID>{{DataSourceName.Orders.OrderID}}</orderID>
            </CheckStatus>
        </soap:Body>
    </soap:Envelope>
    ```

3. 保存测试。
