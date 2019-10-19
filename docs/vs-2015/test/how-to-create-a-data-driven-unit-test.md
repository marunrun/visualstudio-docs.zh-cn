---
title: 如何：创建数据驱动的单元测试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.test.testresults.unittest.datadriven
- vs.test.testresults.unittest.datadriven.failure
helpviewer_keywords:
- unit tests, running
- unit tests, data-driven
- data-driven unit tests
ms.assetid: a0322bc5-02c8-4f9f-af43-100a60b1bd28
caps.latest.revision: 35
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b9dc5ad44a73f517b91562209abfab8b0b3e8d4a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660525"
---
# <a name="how-to-create-a-data-driven-unit-test"></a>如何：创建数据驱动的单元测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

将 Microsoft 单元测试框架用于托管代码，可以设置单元测试方法从数据源中检索测试方法中使用的值。 针对数据源中的每一行连续运行此方法，这样就可以使用一种方法轻松地测试各种输入。

 本主题包含以下各节：

- [待测试的方法](../test/how-to-create-a-data-driven-unit-test.md#BKMK_The_method_under_test)

- [创建数据源](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Creating_a_data_source)

- [向测试类添加 TestContext](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Adding_a_TestContext_to_the_test_class)

- [编写测试方法](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Writing_the_test_method)

  - [指定 DataSourceAttribute](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Specifying_the_DataSourceAttribute)

  - [使用 TestContext.DataRow 访问数据](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Using_TestContext_DataRow_to_access_the_data)

- [运行测试并查看结果](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Running_the_test_and_viewing_results)

  创建数据驱动的单元测试包括以下步骤：

1. 创建包含测试方法中使用的值的数据源。 数据源可以是在运行测试的计算机上注册的任何类型数据源。

2. 将私有 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> 字段和公共 `TestContext` 属性添加到测试类。

3. 创建单元测试方法并为其添加 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> 属性。

4. 使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A> 索引器属性检索测试中使用的值。

## <a name="BKMK_The_method_under_test"></a>待测试的方法
 例如，假定我们已创建：

1. 一个名为 `MyBank` 的解决方案，此解决方案接受并处理不同类型的帐户的交易。

2. `MyBank` 中名为 `BankDb` 的项目，此项目管理帐户的交易。

3. `DbBank` 项目中名为 `Maths` 的类，此类执行数学函数，以确保任何交易对银行有利。

4. 名为 `BankDbTests` 的单元测试项目，用于测试 `BankDb` 组件的行为。

5. 名为 `MathsTests` 的单元测试类，用于验证 `Maths` 类的行为。

   我们将在 `Maths` 中测试一个方法，此方法使用循环添加两个整数：

```
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

## <a name="BKMK_Creating_a_data_source"></a>创建数据源
 若要测试 `AddIntegers` 方法，需创建数据源，该数据源指定参数的值的范围和希望返回的总和。 在本示例中，创建名为 `MathsData` 的 Sql Compact 数据库和包含以下列名和值的名为 `AddIntegersData` 的表

|FirstNumber|SecondNumber|Sum|
|-----------------|------------------|---------|
|0|1|1|
|1|1|2|
|2|-3|-1|

## <a name="BKMK_Adding_a_TestContext_to_the_test_class"></a>向测试类添加 TestContext
 单元测试框架创建  `TestContext` 对象来存储数据驱动测试的数据源信息。 然后，框架将此对象设置为我们创建的 `TestContext` 属性的值。

```

private TestContext testContextInstance;
public TestContext TestContext
{
    get { return testContextInstance; }
    set { testContextInstance = value; }
}

```

 在测试方法中，通过 `TestContext` 的 `DataRow` 索引器属性来访问数据。

## <a name="BKMK_Writing_the_test_method"></a>编写测试方法
 `AddIntegers` 的测试方法很简单。 针对数据源中的每一行，将 **FirstNumber** 和 **SecondNumber** 列值作为参数来调用 `AddIntegers`，并根据 **Sum** 列的值来验证返回值：

```

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

 请注意，`Assert` 方法包括一条消息，此消息显示失败的迭代的值 `x` 和 `y`。 默认情况下，失败测试的详细信息中已包含声明的值 `expected` 和 `actual`。

### <a name="BKMK_Specifying_the_DataSourceAttribute"></a>指定 DataSourceAttribute
 `DataSource` 属性指定数据源的连接字符串和测试方法中使用的表的名称。 连接字符串中的确切信息可能有所不同，具体取决于你使用的数据源类型。 在本例中，我们使用 SqlServerCe 数据库。

```
[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0;Data Source=C:\Data\MathsData.sdf", "AddIntegersData")]
```

 DataSource 属性具有三个构造函数。

```
[DataSource(dataSourceSettingName)]
```

 具有一个参数的构造函数使用解决方案的 app.config 文件中存储的连接信息。 *DataSourceSettingsName* 是配置文件中的 Xml 元素的名称，它指定连接信息。

 使用 app.config 文件可更改数据源的位置，而无需对单元测试本身进行更改。 有关如何创建和使用 app.config 文件的信息，请参阅[演练：使用配置文件来定义数据源](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md)

```
[DataSource(connectionString, tableName)]
```

 含有两个参数的 `DataSource` 构造函数指定数据源的连接字符串和包含测试方法的数据的表的名称。

 连接字符串取决于数据源的类型，但是它应包含指定数据提供程序的固定名称的 Provider 元素。

```
[DataSource(
    dataProvider,
    connectionString,
    tableName,
    dataAccessMethod
    )]
```

### <a name="BKMK_Using_TestContext_DataRow_to_access_the_data"></a>使用 TestContext.DataRow 访问数据
 若要访问 `AddIntegersData` 表中的数据，请使用 `TestContext.DataRow` 索引器。 `DataRow` 是 <xref:System.Data.DataRow> 对象，因此我们根据索引或列名称检索列的值。 由于值作为对象返回，因此需要将它们转换为合适的类型：

```
int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);

```

## <a name="BKMK_Running_the_test_and_viewing_results"></a>运行测试并查看结果
 完成测试方法的编写后，生成测试项目。 测试方法显示在测试资源管理器窗口中的“未运行的测试”组中。 当运行、编写以及重新运行测试时，测试资源管理器在“失败的测试”、“通过的测试”和“未运行的测试”组中显示结果。 可以选择“运行全部”来运行所有测试，或选择“运行...”来选择要运行的测试的子集。

 当运行测试时，位于资源管理器顶部的测试结果栏是动态显示的。 在测试运行结束时，如果所有测试均通过，则结果栏为绿色；如果有任何测试失败，结果栏为红色。 测试运行的摘要显示在测试资源管理器底部的详细信息窗格中。 选择一个测试以在底部窗格中查看该测试的详细信息。

 如果在本示例中运行 `AddIntegers_FromDataSourceTest` 方法，则结果栏变为红色，并且测试方法移动到“失败的测试”。如果数据源中的任何迭代方法失败，则数据驱动测试也会失败。 在测试资源管理器窗口中选择失败的数据驱动测试时，详细信息窗格将显示由数据行索引标识的每个迭代的结果。 在本示例中 `AddIntegers` 算法好像没有正确处理负值。

 当更正了要测试的方法，并重新运行测试，则结果栏变为绿色，并且测试方法移动到“通过的测试”组中。

## <a name="see-also"></a>请参阅
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute?displayProperty=fullName> <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext?displayProperty=fullName>
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A?displayProperty=fullName>
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName>
 [如何：创建和运行单元测试](https://msdn.microsoft.com/5e0f43cf-5e51-48e2-9c98-0eb9324bdc48)[单元测试代码](../test/unit-test-your-code.md)[运行单元测试使用测试资源管理器](../test/run-unit-tests-with-test-explorer.md)[编写适用于托管代码的 Microsoft 单元测试框架的 .NET Framework](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)单元测试
