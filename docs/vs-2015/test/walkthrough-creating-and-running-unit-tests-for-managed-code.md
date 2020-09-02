---
title: 演练：创建并运行托管代码的单元测试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit tests, walkthrough
- unit tests, creating
- unit tests, generating
- unit tests, running
- unit tests, authoring
ms.assetid: 2b018b18-b412-4e0e-b0ee-b580a2f3ba9c
caps.latest.revision: 85
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 631a180789f5fff373799b78222c25a50ab32912
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657091"
---
# <a name="walkthrough-creating-and-running-unit-tests-for-managed-code"></a>演练：创建并运行托管代码的单元测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练将使用托管代码的 Microsoft 单元测试框架和 Visual Studio 测试资源管理器引导你逐步完成一系列单元测试的创建、运行和自定义。 你将从正处于开发过程中的 C# 项目开始，创建执行该项目代码的测试，运行测试并检查结果。 然后，可以更改项目代码并重新运行测试。

 本主题包含以下各节：

 [准备演练](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Prepare_the_walkthrough)

 [创建单元测试项目](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_a_unit_test_project)

 [创建测试类](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_the_test_class)

- [测试类要求](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Test_class_requirements)

  [创建第一个测试方法](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_the_first_test_method)

- [测试方法要求](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Test_method_requirements)

  [生成并运行测试](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Build_and_run_the_test)

  [修复代码并重新运行测试](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Fix_your_code_and_rerun_your_tests)

  [使用单元测试以改进代码](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Use_unit_tests_to_improve_your_code)

> [!NOTE]
> 此演练使用用于托管代码的 Microsoft 单元测试框架。 测试资源管理器还可以在具有测试资源管理器适配器的第三方单元测试框架中运行测试。 有关详细信息，请参阅 [安装第三方单元测试框架](../test/install-third-party-unit-test-frameworks.md)

> [!NOTE]
> 有关如何从命令行运行测试的信息，请参阅[演练：使用命令行测试实用工具](https://msdn.microsoft.com/library/52c11992-9e94-4067-a4b7-59f19d69d867)。

## <a name="prerequisites"></a>先决条件

- Bank 项目。 请参阅 [用于创建单元测试的示例项目](../test/sample-project-for-creating-unit-tests.md)。

## <a name="prepare-the-walkthrough"></a><a name="BKMK_Prepare_the_walkthrough"></a> 准备演练

1. 打开 Visual Studio。

2. 在 **“文件”** 菜单上指向 **“新建”** ，然后单击 **“项目”** 。

    此时将出现“新建项目”对话框。

3. 在 **“已安装的模板”** 下单击 **“Visual C#”**。

4. 在应用程序类型的列表中单击 **“类库”**。

5. 在 **“名称”** 框中键入 `Bank` ，然后单击 **“确定”**。

   > [!NOTE]
   > 如果名称“Bank”已被使用，请为该项目选择其他名称。

    将创建新的 Bank 项目并将其显示在解决方案资源管理器中，而且将在代码编辑器中打开 Class1.cs 文件。

   > [!NOTE]
   > 如果代码编辑器中未打开 Class1.cs 文件，请在解决方案资源管理器中双击文件 Class1.cs 将其打开。

6. 复制[用于创建单元测试的示例项目](../test/sample-project-for-creating-unit-tests.md)中的源代码。

7. 将 Class1.cs 的原始内容替换为[用于创建单元测试的示例项目](../test/sample-project-for-creating-unit-tests.md)中的代码。

8. 将文件保存为 BankAccount.cs

9. 在“生成”菜单中，单击“生成解决方案”。

   现在你有一个名为“Bank”的项目。 它包含要测试的源代码和用于对该源代码进行测试的工具。 Bank 的命名空间 **“BankAccountNS”** 包含公共类 **“BankAccount”**，在以下过程中将对该类的方法进行测试。

   在本次快速入门中，我们重点关注 `Debit` 方法。Debit 方法是在从帐户提取资金时调用的，包含以下代码：

```csharp
// method under test
public void Debit(double amount)
{
    if(amount > m_balance)
    {
        throw new ArgumentOutOfRangeException("amount");
    }
    if (amount < 0)
    {
        throw new ArgumentOutOfRangeException("amount");
    }
    m_balance += amount;
}

```

## <a name="create-a-unit-test-project"></a><a name="BKMK_Create_a_unit_test_project"></a> 创建单元测试项目
 **系统必备**：按照 [Prepare the walkthrough](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Prepare_the_walkthrough)过程中的步骤执行操作。

#### <a name="to-create-a-unit-test-project"></a>创建单元测试项目

1. 在 **“文件”** 菜单中，选择 **“添加”**，再选择 **“新建项目...”**。

2. 在 "新建项目" 对话框中，展开 " **已安装**"，展开 " **Visual c #**"，然后选择 " **测试**"。

3. 从模板列表中选择 **“单元测试项目”**。

4. 在 **“名称”** 框中，输入 BankTest，然后选择 **“确定”**。

     将“BankTests”  项目添加到“Bank”  解决方案。

5. 在 **“BankTests”** 项目中，添加对 **“Bank”** 解决方案的引用。

     在解决方案资源管理器中，选择 " **banktests"** "项目中的"**引用**"，然后从上下文菜单中选择"**添加引用 ...** "。

6. 在“引用管理器”对话框中，展开“解决方案”，然后选中“Bank”项********。

## <a name="create-the-test-class"></a><a name="BKMK_Create_the_test_class"></a> 创建测试类
 我们需要一个测试类来验证 `BankAccount` 类。 我们可以使用由项目模板生成的 UnitTest1.cs，但在对文件和类命名时应更具描述性。 通过重命名“解决方案资源管理器”中的文件，我们就可以一步完成这个操作。

 **重命名类文件**

 在“解决方案资源管理器”中，从 BankTests 项目中选择 UnitTest1.cs 文件。 从上下文菜单中，选择 " **重命名**"，然后将该文件重命名为 BankAccountTests.cs。 当显示对话框询问你是否希望重命名项目中对代码元素“UnitTest1”的所有引用时，选择 **“是”** 。 此步骤会将类的名称更改为 `BankAccountTest`。

 BankAccountTests.cs 文件现包含下列代码：

```csharp
// unit test code
using System;
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace BankTests
{
    [TestClass]
    public class BankAccountTests
    {
        [TestMethod]
        public void TestMethod1()
        {
        }
    }
}
```

 **向所测试项目添加 using 语句**

 我们还可以向类中添加 using 语句以供所测试项目调用，而无需使用完全限定名。 在类文件顶部添加：

```csharp
using BankAccountNS;
```

### <a name="test-class-requirements"></a><a name="BKMK_Test_class_requirements"></a> 测试类要求
 对测试类的最低要求如下：

- 在托管代码的 Microsoft 单元测试框架中，任何包含要在“测试资源管理器”中运行的单元测试方法的类都需要有 `[TestClass]` 特性。

- 你希望“测试资源管理器”运行的每个测试方法都必须具有 `[TestMethod]`特性。

  单元测试项目中可以具有不含 `[TestClass]` 特性的其他类，测试类中可以具有不含 `[TestMethod]` 特性的其他方法。 可以在测试方法中使用这些其他的类和方法。

## <a name="create-the-first-test-method"></a><a name="BKMK_Create_the_first_test_method"></a> 创建第一个测试方法
 在此过程中，我们将编写单元测试方法以验证 `Debit` 类的 `BankAccount` 方法的行为。 方法如上所列。

 通过分析所测试的方法，我们确定至少需要检查三个行为：

1. 方法引发 [ArgumentOutOfRangeException] (<!-- TODO: review code entity reference <xref:assetId:///ArgumentOutOfRangeException?qualifyHint=False&amp;autoUpgrade=True>  -->如果借方金额大于余额，则 ) 。

2. 如果借方金额小于零，它还会引发 `ArgumentOutOfRangeException` 。

3. 如果对 1.) 和 2.) 的检查合格，该方法会从帐户余额中减去该金额。

   首次测试时，我们会验证是否从帐户中提取了正确的有效金额（大于零且小于帐户余额）。

#### <a name="to-create-a-test-method"></a>创建测试方法

1. 向 BankAccountTests.cs 文件中添加 using `BankAccountNS;` 语句。

2. 将以下方法添加到该 `BankAccountTests` 类：

   ```csharp
   // unit test code
   [TestMethod]
   public void Debit_WithValidAmount_UpdatesBalance()
   {
       // arrange
       double beginningBalance = 11.99;
       double debitAmount = 4.55;
       double expected = 7.44;
       BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

       // act
       account.Debit(debitAmount);

       // assert
       double actual = account.Balance;
       Assert.AreEqual(expected, actual, 0.001, "Account not debited correctly");
   }
   ```

   此方法更加简单。 我们设置了有期初余额的新 `BankAccount` 对象，然后提取有效金额。 使用托管代码 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A> 方法的 Microsoft 单元测试框架来验证期末余额是否符合我们的预期。

### <a name="test-method-requirements"></a><a name="BKMK_Test_method_requirements"></a> 测试方法要求
 测试方法必须满足以下要求：

- 必须用 `[TestMethod]` 特性修饰该方法。

- 该方法必须返回 `void`。

- 该方法不能含有参数。

## <a name="build-and-run-the-test"></a><a name="BKMK_Build_and_run_the_test"></a> 生成并运行测试

#### <a name="to-build-and-run-the-test"></a>生成并运行测试

1. 在 **“生成”** 菜单上，选择 **“生成解决方案”** 。

     如果没有错误，会显示“单元测试资源管理器”窗口，其中 **“Debit_WithValidAmount_UpdatesBalance”** 在 **“未运行的测试”** 组中列出。 如果“测试资源管理器”在成功生成后未显示，请在菜单上选择 “测试”****，再选择“窗口”****，然后选择“测试资源管理器”****。

2. 选择 **“全部运行”** 以运行测试。 运行测试时，窗口顶部的状态栏是动画处理的。 测试运行结束时，如果测试方法全部通过，状态栏将变为绿色；如果有任何测试失败，状态栏将变为红色。

3. 在这种情况下，测试就失败了。 测试方法将移动到 **“失败的测试”**。 组中列出。 在“测试资源管理器”中选择该方法可在窗口底部查看详细信息。

## <a name="fix-your-code-and-rerun-your-tests"></a><a name="BKMK_Fix_your_code_and_rerun_your_tests"></a> 修复代码并重新运行测试
 **分析测试结果**

 测试结果包含一条描述失败的消息。 对于 `AreEquals` 方法，消息会显示所需的内容 ( (<strong>所需 \<*XXX*> </strong>的参数) 以及实际收到的 (**实际 \<*YYY*> **参数) 。 我们本来预期余额会比期初余额越来越少，但却增加了取款金额。

 复查 Debit 代码后发现，单元测试成功找到 bug。 取款金额本应从帐户余额中减去，结果却增加到帐户余额中。

 **更正 bug**

 若要更正错误，只需将代码行

```csharp
m_balance += amount;
```

 替换为

```csharp
m_balance -= amount;
```

 **重新运行测试**

 在测试资源管理器中，选择 " **全部运行** " 以重新运行测试。 红色/绿色栏变为绿色，测试移动到 **“已通过的测试”** 组。

## <a name="use-unit-tests-to-improve-your-code"></a><a name="BKMK_Use_unit_tests_to_improve_your_code"></a> 使用单元测试以改进代码
 本部分介绍了分析的迭代过程、单元测试开发和重构如何帮助你增加成品代码的可靠性和有效性。

 **分析问题**

 在创建测试方法以确认是否在 `Debit` 方法中正确扣除了有效金额后，我们就可以转到原始分析中的其他案例：

1. 如果借方金额大于余额，该方法将引发 `ArgumentOutOfRangeException` 。

2. 如果借方金额小于零，它还会引发 `ArgumentOutOfRangeException` 。

   **创建测试方法**

   首次尝试创建测试方法以解决这些问题的做法看似可行：

```csharp
//unit test method
[TestMethod]
[ExpectedException(typeof(ArgumentOutOfRangeException))]
public void Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()
{
    // arrange
    double beginningBalance = 11.99;
    double debitAmount = -100.00;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // act
    account.Debit(debitAmount);

    // assert is handled by ExpectedException
}

```

 我们使用 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute> 特性去断言正确的异常已抛出。 除非 `ArgumentOutOfRangeException` 已抛出，否则该特性将导致测试失败。 以正负 `debitAmount` 值运行测试，然后将所测试的方法暂时修改为在金额小于零时抛出泛型 <xref:System.ApplicationException> ，可证明测试行为正确。 若要测试提取金额大于余额的情况，只需执行以下操作即可：

1. 新建一个名为 `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange`的测试方法。

2. 将 `Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange` 中的方法主体复制到新方法中。

3. 将 `debitAmount` 设置为比余额大的一个数字。

   **运行测试**

   以不同的 `debitAmount` 值运行两种方法可证明测试能够恰当处理其余的情况。 运行所有三种测试可确认原始分析中的所有情况已正确覆盖。

   **继续分析**

   但是，最后两个测试方法还是有点麻烦。 其中任一测试运行时，我们都无法确定所测试代码中的哪个条件会抛出异常。 如果能区分这两种条件，也许会有帮助。 我们再深入思考此问题，就会了然 - 得知违反的条件会增加我们对测试的信心。 对于处理所测试方法抛出的异常的生产机制，该信息也非常可能带来帮助。 在方法抛出异常时生成更多信息将有助于解决所有问题，但是 `ExpectedException` 特性无法提供此信息。

   再次查看所测试的方法，就会看到两个条件语句都使用 `ArgumentOutOfRangeException` 构造函数，该函数使用变量名称作为参数：

```csharp
throw new ArgumentOutOfRangeException("amount");
```

 通过搜索 MSDN 库，我们发现存在报告信息非常丰富的构造函数。 <xref:System.ArgumentOutOfRangeException.%23ctor%2A>`(String, Object, String)` 包括变量名称、变量值和用户定义的消息。 我们可以重构所测试的方法，以使用此构造函数。 更理想的做法是使用公开的类型成员来指定错误。

 **重构所测试的代码**

 我们首先为类范围内的错误消息定义两个常量：

```csharp
// class under test
public const string DebitAmountExceedsBalanceMessage = "Debit amount exceeds balance";
public const string DebitAmountLessThanZeroMessage = "Debit amount less than zero";
```

 然后修改 `Debit` 方法中的两个条件语句：

```csharp
// method under test
// ...
    if (amount > m_balance)
    {
        throw new ArgumentOutOfRangeException("amount", amount, DebitAmountExceedsBalanceMessage);
    }

    if (amount < 0)
    {
        throw new ArgumentOutOfRangeException("amount", amount, DebitAmountLessThanZeroMessage);
    }
// ...
```

 **重构测试方法**

 在我们的测试方法中，首先移除 `ExpectedException` 特性。 在其位置上，我们捕获抛出的异常并验证其是否在正确的条件语句中抛出。 但是，我们现在必须在两个选项之间作出决定，以验证其余的条件。 例如，在 `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` 方法中，可以执行下列操作之一：

- 断言异常的 `ActualValue` 属性（ `ArgumentOutOfRangeException` 构造函数的第二个参数）大于期初余额。 此选项要求我们依据测试方法的 `ActualValue` 变量来测试异常的 `beginningBalance` 属性，还要求验证 `ActualValue` 是否大于零。

- 断言消息（构造函数的第三个参数）包括 `DebitAmountExceedsBalanceMessage` 类中定义的 `BankAccount` 。

  使用 Microsoft 单元测试框架中的 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=fullName> 方法无需进行第一个选项所要求的计算，即可验证第二个选项。

  修改 `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` 的第二次尝试可能类似于：

```csharp
[TestMethod]
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
{
    // arrange
    double beginningBalance = 11.99;
    double debitAmount = 20.0;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // act
    try
    {
        account.Debit(debitAmount);
    }
    catch (ArgumentOutOfRangeException e)
    {
        // assert
        StringAssert.Contains(e.Message, BankAccount. DebitAmountExceedsBalanceMessage);
    }
}
```

 **重测、重写和重新分析**

 我们使用不同的值重新对测试方法进行测试时，遇到以下情况：

1. 如果通过使用一个断言（其中 `debitAmount` 大于余额）捕获到正确的错误，则 `Contains` 断言成功并将忽略异常，因此测试方法成功。 这是我们想要的行为。

2. 如果我们使用小于 0 的 `debitAmount` ，则该断言失败，因为返回了错误的错误消息。 如果要在测试代码路径下的方法中的另一个点引入一个临时 `ArgumentOutOfRange` 异常，断言也会失败。 这也是好的。

3. 如果 `debitAmount` 值有效（即小于余额，但大于零），则不会捕获到异常，因此永远不会捕获断言。 测试方法通过。 这样是不好的，因为如果未抛出异常，我们希望测试方法失败。

   第三种情况是测试方法中的 bug。 为了尝试解决该问题，我们在测试方法末尾添加了 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A> 断言，以处理未抛出异常的情况。

   但重新测试表明，如果捕获到正确的异常，测试现将失败。 catch 语句重置异常，而方法继续执行，因而在新断言处失败。 为了解决这个新问题，我们在 `return` 之后添加 `StringAssert`语句。 重新测试后证明问题得以解决。 `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` 的最终版本如下：

```csharp
[TestMethod]
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
{
    // arrange
    double beginningBalance = 11.99;
    double debitAmount = 20.0;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // act
    try
    {
        account.Debit(debitAmount);
    }
    catch (ArgumentOutOfRangeException e)
    {
        // assert
        StringAssert.Contains(e.Message, BankAccount. DebitAmountExceedsBalanceMessage);
        return;
    }
    Assert.Fail("No exception was thrown.");
}

```

 在最后部分，我们为改进测试代码而做出的努力最终提高了测试方法的可靠性和信息量。 但更重要的是，额外的分析也改善了所测试项目中的代码。
