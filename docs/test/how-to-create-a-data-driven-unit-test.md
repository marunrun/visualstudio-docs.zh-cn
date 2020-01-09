---
title: 创建数据驱动的单元测试
ms.date: 05/08/2019
ms.topic: conceptual
f1_keywords:
- vs.test.testresults.unittest.datadriven
- vs.test.testresults.unittest.datadriven.failure
helpviewer_keywords:
- unit tests, running
- unit tests, data-driven
- data-driven unit tests
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: f50dad637d9efa2db347ff9f1b4828abf8c733af
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589183"
---
# <a name="how-to-create-a-data-driven-unit-test"></a>如何：创建数据驱动的单元测试

可以使用 Microsoft 单元测试框架来托管代码，以设置单元测试方法，以便从数据源检索值。 针对数据源中的每一行连续运行此方法，这样就可以使用一种方法轻松地测试各种输入。

创建数据驱动的单元测试包括以下步骤：

1. 创建包含测试方法中使用的值的数据源。 数据源可以是在运行测试的计算机上注册的任何类型数据源。

2. 将私有 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> 字段和公共 `TestContext` 属性添加到测试类。

3. 创建单元测试方法并为其添加 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> 属性。

4. 使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A> 索引器属性检索测试中使用的值。

## <a name="the-method-under-test"></a>待测试的方法

例如，假定已具有：

1. 一个名为 `MyBank` 的解决方案，此解决方案接受并处理不同类型的帐户的交易。

2. `MyBank` 中名为 `BankDb` 的项目，此项目管理帐户的交易。

3. `BankDb` 项目中名为 `Maths` 的类，此类执行数学函数，以确保任何交易对银行有利。

4. 名为 `BankDbTests` 的单元测试项目，用于测试 `BankDb` 组件的行为。

5. 名为 `MathsTests` 的单元测试类，用于验证 `Maths` 类的行为。

我们将在 `Maths` 中测试一个使用循环添加两个整数的方法：

```csharp
public int AddIntegers(int first, int second)
{
    int sum = first;
    for( int i = 0; i < second; i++)
    {
        sum += 1;
    }
    return sum;
}
```

## <a name="create-a-data-source"></a>创建数据源

若要测试 `AddIntegers` 方法，需创建数据源，该数据源指定参数的值的范围和希望返回的总和。 在本示例中，我们将创建名为 `MathsData` 的 Sql Compact 数据库和包含以下列名和值的名为 `AddIntegersData` 的表

|FirstNumber|SecondNumber|Sum|
|-|------------------|-|
|0|1|1|
|1|1|2|
|2|-3|-1|

## <a name="add-a-testcontext-to-the-test-class"></a>向测试类添加 TestContext

单元测试框架创建  `TestContext` 对象来存储数据驱动测试的数据源信息。 然后，框架将此对象设置为创建的 `TestContext` 属性的值。

```csharp
private TestContext testContextInstance;
public TestContext TestContext
{
    get { return testContextInstance; }
    set { testContextInstance = value; }
}
```

在测试方法中，通过 `TestContext` 的 `DataRow` 索引器属性来访问数据。

> [!NOTE]
> .NET Core 不支持 [DataSource](xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute) 属性。 如果尝试在 .NET Core 或 UWP 单元测试项目中以这种方式访问测试数据，你将看到如下错误：“‘TestContext’不包含‘DataRow’的定义，并且找不到接受类型为‘TestContext’的第一个参数的可访问扩展方法‘DataRow’(是否缺少 using 指令或程序集引用?)”  。

## <a name="write-the-test-method"></a>编写测试方法

`AddIntegers` 的测试方法很简单。 针对数据源中的每一行，将 FirstNumber 和 SecondNumber 列值作为参数来调用 `AddIntegers`，并根据 Sum 列的值来验证返回值：   

```csharp
[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0; Data Source=C:\Data\MathsData.sdf;", "Numbers")]
[TestMethod()]
public void AddIntegers_FromDataSourceTest()
{
    var target = new Maths();

    // Access the data
    int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);
    int y = Convert.ToInt32(TestContext.DataRow["SecondNumber"]);
    int expected = Convert.ToInt32(TestContext.DataRow["Sum"]);
    int actual = target.IntegerMethod(x, y);
    Assert.AreEqual(expected, actual,
        "x:<{0}> y:<{1}>",
        new object[] {x, y});
}
```

`Assert` 方法包括一条消息，此消息显示失败的迭代的值 `x` 和 `y`。 默认情况下，声明的值 `expected` 和 `actual` 已包含在失败测试的详细信息中。

### <a name="specify-the-datasourceattribute"></a>指定 DataSourceAttribute

`DataSource` 属性指定数据源的连接字符串和测试方法中使用的表的名称。 连接字符串中的确切信息可能有所不同，具体取决于你使用的数据源类型。 在本例中，我们使用 SqlServerCe 数据库。

```csharp
[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0;Data Source=C:\Data\MathsData.sdf", "AddIntegersData")]
```

DataSource 属性具有三个构造函数。

```csharp
[DataSource(dataSourceSettingName)]
```

具有一个参数的构造函数使用解决方案的 app.config 文件中存储的连接信息  。 *DataSourceSettingsName* 是配置文件中的 Xml 元素的名称，它指定连接信息。

使用 app.config 文件可更改数据源的位置，而无需对单元测试本身进行更改  。 有关如何创建和使用“app.config”文件的信息，请参阅[演练：使用配置文件定义数据源](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md) 

```csharp
[DataSource(connectionString, tableName)]
```

含有两个参数的 `DataSource` 构造函数指定数据源的连接字符串和包含测试方法的数据的表的名称。

连接字符串取决于数据源的类型，但是它应包含指定数据提供程序的固定名称的 Provider 元素。

```csharp
[DataSource(
    dataProvider,
    connectionString,
    tableName,
    dataAccessMethod
    )]
```

### <a name="use-testcontextdatarow-to-access-the-data"></a>使用 TestContext.DataRow 访问数据

若要访问 `AddIntegersData` 表中的数据，请使用 `TestContext.DataRow` 索引器。 `DataRow` 是 <xref:System.Data.DataRow> 对象，因此根据索引或列名称检索列的值。 由于值作为对象返回，需将它们转换为合适的类型：

```csharp
int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);
```

## <a name="run-the-test-and-view-results"></a>运行测试并查看结果

完成测试方法的编写后，生成测试项目。 测试方法显示在“测试资源管理器”的“未运行的测试”组中   。 当运行、编写以及重新运行测试时，测试资源管理器在“失败的测试”、“通过的测试”和“未运行的测试”组中显示结果     。 你可以选择“运行全部”  来运行所有测试，或选择“运行”  来选择要运行的测试的子集。

当运行测试时，位于“测试资源管理器”顶部的测试结果栏是动态显示的  。 在测试运行结束时，如果所有测试均通过，则结果栏为绿色；如果有任何测试失败，结果栏为红色。 测试运行的摘要显示在测试资源管理器窗口底部的细节窗格中  。 选择一个测试以在底部窗格中查看该测试的详细信息。

> [!NOTE]
> 每行数据都有一个结果，还有一个摘要结果。 如果每行数据测试通过，则摘要运行显示为“已通过”  。 如果任何数据行测试失败，则摘要运行显示为“失败”  。

如果在我们的示例中运行 `AddIntegers_FromDataSourceTest` 方法，则结果栏变为红色，且测试方法移动到“失败的测试”  。 如果数据源中任一循环访问的方法失败，则数据驱动测试失败。 在测试资源管理器窗口中选择失败的数据驱动测试时，细节窗格将显示由数据行索引标识的每个迭代的结果  。 在本示例中 `AddIntegers` 算法好像没有正确处理负值。

当更正了要测试的方法，并重新运行测试，则结果栏变为绿色，并且测试方法移动到“通过的测试”  组中。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName>
- [单元测试代码](../test/unit-test-your-code.md)
- [使用测试资源管理器运行单元测试](../test/run-unit-tests-with-test-explorer.md)
- [使用 Microsoft 单元测试框架编写 .NET 的单元测试](../test/unit-test-your-code.md)
