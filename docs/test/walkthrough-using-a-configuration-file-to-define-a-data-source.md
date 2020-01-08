---
title: 使用配置文件来定义数据源
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- configuration files [Visual Studio ALM], defining data sources
- unit tests, walkthrough
- data sources, defining with configuration files
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c76d71c106dbd2b5cbe63ab2f36defdfbd6cf127
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590717"
---
# <a name="walkthrough-using-a-configuration-file-to-define-a-data-source"></a>演练：使用配置文件定义数据源

本演练演示如何使用 app.config 文件中定义的数据源进行单元测试。  你将学习如何创建用于定义可供 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> 类使用的数据源的 app.config 文件  。 本演练包括以下任务：

- 创建 app.config 文件  。

- 定义自定义配置节。

- 定义连接字符串。

- 定义数据源。

- 使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> 类访问数据源。

## <a name="prerequisites"></a>先决条件

若要完成本演练，你需要：

- Visual Studio Enterprise

- Microsoft Access 或 Microsoft Excel 至少为其中一个测试方法提供数据。

- 包含测试项目的 Visual Studio 解决方案。

## <a name="add-an-appconfig-file-to-the-project"></a>将 app.config 文件添加到项目

1. 如果测试项目已有 app.config 文件，请转到[定义自定义配置节](#define-a-custom-configuration-section)  。

2. 在解决方案资源管理器中右键单击测试项目，然后选择“添加” > “新建项”    。

     此时，“添加新项”  窗口会打开。

3. 选择“应用配置文件”  模板，然后单击“添加”  。

## <a name="define-a-custom-configuration-section"></a>定义自定义配置节

检查 app.config  文件。 它至少包含 XML 声明和一个根元素。

### <a name="to-add-the-custom-configuration-section-to-the-appconfig-file"></a>若要将自定义配置节添加到 app.config 文件

1. app.config 的根元素应为 configuration 元素   。 在 configuration  元素中创建一个 configSections  元素。 configSections  应为 app.config  文件中的第一个元素。

2. 在 configSections  元素中创建一个 section  元素。

3. 在 section  元素中，添加一个名为 `name` 的特性，并为其分配一个 `microsoft.visualstudio.testtools` 的值。 再添加一个名为 `type` 的特性，并为其分配一个 `Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.TestPlatform.TestFramework.Extensions` 的值。

section  元素应类似于：

```xml
<section name="microsoft.visualstudio.testtools" type="Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.TestPlatform.TestFramework.Extensions" />
```

> [!NOTE]
> 程序集名称必须与正在使用的版本一致。

## <a name="define-connection-strings"></a>定义连接字符串

连接字符串定义了用于访问数据源的提供程序特定信息。 配置文件中定义的连接字符串提供了跨应用程序可重用的数据提供程序信息。 在本节中，你将创建两个由自定义配置节中定义的数据源使用的连接字符串。

### <a name="to-define-connection-strings"></a>定义连接字符串

1. 在 configSections  元素后，创建一个 connectionStrings  元素。

2. 在 connectionStrings  元素中，创建两个 add  元素。

3. 在第一个 add  元素中，创建下列特性和值以连接到 Microsoft Access 数据库：

|特性|值|
|-|------------|
|`name`|`"MyJetConn"`|
|`connectionString`|`"Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;"`|
|`providerName`|`"System.Data.OleDb"`|

在第二个 add  元素中，创建下列特性和值以连接到 Microsoft Excel 电子表格：

|特性|值|
|-|-|
|`name`|`"MyExcelConn"`|
|`connectionString`|`"Dsn=Excel Files;dbq=data.xlsx;defaultdir=.\; driverid=790;maxbuffersize=2048;pagetimeout=5"`|
|`providerName`|`"System.Data.Odbc"`|

connectionStrings  元素应类似于：

```xml
<connectionStrings>
    <add name="MyJetConn" connectionString="Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;" providerName="System.Data.OleDb" />
    <add name="MyExcelConn" connectionString="Dsn=Excel Files;dbq=data.xlsx;defaultdir=.\; driverid=790;maxbuffersize=2048;pagetimeout=5" providerName="System.Data.Odbc" />
</connectionStrings>
```

## <a name="define-data-sources"></a>定义数据源

数据源节包含测试引擎用于从数据源检索数据的四个特性。

- `name` 定义了 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> 用于指定要使用哪个数据源的标识。

- `connectionString` 标识了在之前的“定义连接字符串”部分中创建的连接字符串。

- `dataTableName` 定义了保留要在测试中使用的数据的表格或工作表。

- `dataAccessMethod` 定义了访问数据源中的数据值的方法。

在本节中，定义两个数据源以在单元测试中使用。

### <a name="to-define-data-sources"></a>若要定义数据源

1. 在 connectionStrings  元素后，创建一个 microsoft.visualstudio.testtools  元素。 本节在“定义自定义配置节”中创建。

2. 在 microsoft.visualstudio.testtools  元素，创建一个 dataSources  元素。

3. 在 dataSources  元素中，创建两个 add  元素。

4. 在第一个 add  元素中，为 Microsoft Access 数据源创建下列特性和值：

|特性|值|
|-|------------|
|`name`|`"MyJetDataSource"`|
|`connectionString`|`"MyJetConn"`|
|`dataTableName`|`"MyDataTable"`|
|`dataAccessMethod`|`"Sequential"`|

在第二个 add  元素中，为 Microsoft Excel 数据源创建下列特性和值：

|特性|值|
|-|-|
|`Name`|`"MyExcelDataSource"`|
|`connectionString`|`"MyExcelConn"`|
|`dataTableName`|`"Sheet1$"`|
|`dataAccessMethod`|`"Sequential"`|

Microsoft.visualstudio.testtools  元素应类似于：

```xml
<microsoft.visualstudio.testtools>
    <dataSources>
        <add name="MyJetDataSource" connectionString="MyJetConn" dataTableName="MyDataTable" dataAccessMethod="Sequential"/>
        <add name="MyExcelDataSource" connectionString="MyExcelConn" dataTableName="Sheet1$" dataAccessMethod="Sequential"/>
    </dataSources>
</microsoft.visualstudio.testtools>
```

最终的 app.config  文件应类似于：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <configSections>
        <section name="microsoft.visualstudio.testtools" type="Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"/>
    </configSections>
    <connectionStrings>
        <add name="MyJetConn" connectionString="Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;" providerName="System.Data.OleDb" />
        <add name="MyExcelConn" connectionString="Dsn=Excel Files;dbq=data.xlsx;defaultdir=.\; driverid=790;maxbuffersize=2048;pagetimeout=5" providerName="System.Data.Odbc" />
    </connectionStrings>
    <microsoft.visualstudio.testtools>
        <dataSources>
            <add name="MyJetDataSource" connectionString="MyJetConn" dataTableName="MyDataTable" dataAccessMethod="Sequential"/>
            <add name="MyExcelDataSource" connectionString="MyExcelConn" dataTableName="Sheet1$" dataAccessMethod="Sequential"/>
        </dataSources>
    </microsoft.visualstudio.testtools>
</configuration>
```

## <a name="create-a-unit-test-that-uses-data-sources-defined-in-appconfig"></a>创建一个使用 app.config 中定义的数据源的单元测试

由于已定义了 app.config 文件，你将创建一个单元测试，它会使用位于 app.config 文件中定义的数据源中的数据   。 在本节中，我们将：

- 创建在 app.config 文件中找到的数据源  。

- 使用两个可比较每个数据源中的值的测试方法中的数据源。

### <a name="to-create-a-microsoft-access-data-source"></a>若要创建 Microsoft Access 数据源

1. 创建一个名为 testdatasource.accdb  的 Microsoft Access 数据库。

2. 在 testdatasource.accdb  中创建一个表并将其命名为 `MyDataTable`。

3. 使用 `Number` 数据类型在 `MyDataTable` 中创建两个分别名为 `Arg1` 和 `Arg2` 的字段。

4. 使用 `Arg1` 和 `Arg2` 的下列值将五个实体分别添加到 `MyDataTable`：(10,50)、(3,2)、(6,0)、(0,8) 和 (12312,1000)。

5. 保存并关闭数据库。

6. 更改连接字符串以指向数据库的位置。 更改 `Data Source` 的值以反映数据库的位置。

### <a name="to-create-a-microsoft-excel-data-source"></a>若要创建 Microsoft Excel 数据源

1. 创建一个名为 data.xlsx  的 Microsoft Excel 电子表格。

2. 如果 data.xlsx  中尚不存在名为 `Sheet1` 的工作表，则创建一个。

3. 在 `Sheet1` 中创建两个列标头，并将它们命名为 `Val1` 和 `Val2`。

4. 使用 `Val1` 和 `Val2` 的下列值将五个实体分别添加到 `Sheet1`：(1,1)、(2,2)、(3,3)、(4,4) 和 (5,0)。

5. 保存并关闭电子表格。

6. 更改连接字符串以指向电子表格的位置。 更改 `dbq` 的值以反映电子表格的位置。

### <a name="to-create-a-unit-test-using-the-appconfig-data-sources"></a>若要使用 app.config 数据源创建单元测试

1. 向测试项目添加一个单元测试。

2. 将单元测试中自动生成的内容替换为以下代码：

    ```csharp
    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;

    namespace TestProject1
    {
         [TestClass]
        public class UnitTest1
        {
            private TestContext context;

            public TestContext TestContext
            {
                get { return context; }
                set { context = value; }
            }

            [TestMethod()]
            [DeploymentItem("MyTestProject\\testdatasource.accdb")]
            [DataSource("MyJetDataSource")]
            public void MyTestMethod()
            {
                int a = Int32.Parse(context.DataRow["Arg1"].ToString());
                int b = Int32.Parse(context.DataRow["Arg2"].ToString());
                Assert.AreNotEqual(a, b, "A value was equal.");
            }

            [TestMethod()]
            [DeploymentItem("MyTestProject\\data.xlsx")]
            [DataSource("MyExcelDataSource")]
            public void MyTestMethod2()
            {
                Assert.AreEqual(context.DataRow["Val1"], context.DataRow["Val2"]);
            }
        }
    }
    ```

3. 检查数据源特性。 请注意 app.config 文件中的设置名称  。

4. 生成你的解决方案并运行 MyTestMethod 和 MyTestMethod2 测试。

> [!IMPORTANT]
> 部署数据源等项，以便部署目录中的测试可以访问它们。

## <a name="see-also"></a>请参阅

- [单元测试代码](../test/unit-test-your-code.md)
- [如何：创建数据驱动的单元测试](../test/how-to-create-a-data-driven-unit-test.md)
