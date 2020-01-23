---
title: 泛型方法的单元测试
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- generics, and unit tests
- unit tests, and generics
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 2158c889aefc85c908aa9ee42d45858fd11d557e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590808"
---
# <a name="unit-tests-for-generic-methods"></a>泛型方法的单元测试

可采用与其他方法完全一样的方式为泛型方法生成单元测试。 以下各节提供有关为泛型方法创建单元测试的信息和示例。

## <a name="type-arguments-and-type-constraints"></a>类型参数和类型约束

当 Visual Studio 为泛型类生成单元测试（例如 `MyList<T>`）时，它会生成两个方法：通用帮助器方法和测试方法。 如果 `MyList<T>` 具有一个或多个类型约束，则类型参数必须满足所有类型约束。 为确保待测试的泛型代码按预期对允许的所有输入均有效，该测试方法将调用具有你希望测试的所有约束的通用帮助器方法。

## <a name="examples"></a>示例
以下示例阐释泛型的单元测试：

- [编辑生成的测试代码](#EditingGeneratedTestCode)。 此示例分为两个部分：“生成的测试代码”和“编辑的测试代码”。 它演示如何将泛型方法生成的原始测试代码编辑成有用的测试方法。

- [使用类型约束](#TypeConstraintNotSatisfied)。 此示例演示使用类型约束的泛型方法的单元测试。 在此示例中，不满足类型约束。

### <a name="EditingGeneratedTestCode"></a> 示例 1：编辑生成的测试代码
本部分中的测试代码会测试一个名为 `SizeOfLinkedList()` 的带测试代码方法。 此方法返回一个整数，它指定链接列表中的节点数。

第一个代码示例（位于“生成的测试代码”部分）按照由 Visual Studio Enterprise 生成的原样显示未编辑的测试代码。 第二个示例（位于“编辑的测试代码”部分）显示可以如何使其测试两个不同数据类型（`int` 和 `char`）的 SizeOfLinkedList 方法的运行情况。

此代码阐释两种方法：

- 一是测试帮助器方法 `SizeOfLinkedListTestHelper<T>()`。 默认情况下，测试帮助器方法的名称中包含“TestHelper”。

- 二是测试方法 `SizeOfLinkedListTest()`。 每个测试方法都标有 TestMethod 特性。

#### <a name="generated-test-code"></a>生成的测试代码
以下测试代码由 `SizeOfLinkedList()` 方法生成。 由于这是未编辑的生成测试，因此必须对其进行修改，以正确测试 SizeOfLinkedList 方法。

```csharp
public void SizeOfLinkedListTestHelper<T>()
{
    T val = default(T); // TODO: Initialize to an appropriate value
    MyLinkedList<T> target = new MyLinkedList<T>(val); // TODO: Initialize to an appropriate value
    int expected = 0; // TODO: Initialize to an appropriate value
    int actual;
    actual = target.SizeOfLinkedList();
    Assert.AreEqual(expected, actual);
    Assert.Inconclusive("Verify the correctness of this test method.");
}

[TestMethod()]
public void SizeOfLinkedListTest()
{
   SizeOfLinkedListTestHelper<GenericParameterHelper>();
}
```

在前面的代码中，泛型类型参数是 `GenericParameterHelper`。 尽管可以进行编辑以支持特定的数据类型（如下面的示例所示），但可以在不编辑此语句的情况下运行测试。

#### <a name="edited-test-code"></a>编辑的测试代码
在下面的代码中，对测试方法和测试帮助器方法进行了编辑，使它们可以成功测试待测试代码方法 `SizeOfLinkedList()`。

##### <a name="test-helper-method"></a>测试帮助程序方法
测试帮助器方法执行以下步骤，它们分别对应于代码中标记为步骤 1 到步骤 5 的行。

1. 创建通用链接列表。

2. 向该链接列表追加四个节点。 这些节点的内容的数据类型未知。

3. 将链接列表的预期大小分配给变量 `expected`。

4. 计算链接列表的实际大小并将其分配给该变量 `actual`。

5. 用断言语句比较 `actual` 与 `expected`。 如果实际值不等于预期值，则测试失败。

##### <a name="test-method"></a>测试方法
测试方法已编译到代码中，运行名为 SizeOfLinkedListTest 的测试时将调用该代码。 它执行以下步骤，它们分别对应于代码中标记为步骤 6 和步骤 7 的行。

1. 调用测试帮助器方法时指定 `<int>`，以验证测试适用于 `integer` 变量。

2. 调用测试帮助器方法时指定 `<char>`，以验证测试适用于 `char` 变量。

```csharp
public void SizeOfLinkedListTestHelper<T>()
{
    T val = default(T);
    MyLinkedList<T> target = new MyLinkedList<T>(val); // step 1
    for (int i = 0; i < 4; i++) // step 2
    {
        MyLinkedList<T> newNode = new MyLinkedList<T>(val);
        target.Append(newNode);
    }
    int expected = 5; // step 3
    int actual;
    actual = target.SizeOfLinkedList(); // step 4
    Assert.AreEqual(expected, actual); // step 5
}

[TestMethod()]
public void SizeOfLinkedListTest()
{
    SizeOfLinkedListTestHelper<int>();  // step 6
    SizeOfLinkedListTestHelper<char>(); // step 7
}
```

> [!NOTE]
> 每次运行 SizeOfLinkedListTest 测试时，都将调用两次其 TestHelper 方法。 断言语句的计算结果必须每次都为 true，测试才能通过。 如果测试失败，也许分不清是指定了 `<int>` 的调用还是指定了 `<char>` 的调用导致了失败。 要找出答案，可以检查调用堆栈，或在测试方法中设置断点并在运行测试时进行调试。 有关详细信息，请参阅[如何：在 ASP.NET 解决方案中运行测试时进行调试](https://msdn.microsoft.com/Library/de4d7aa1-4a1e-467e-a19b-4a85ec245b8b)。

### <a name="TypeConstraintNotSatisfied"></a> 示例 2：使用类型约束
此示例演示使用未得到满足的类型约束的泛型方法的单元测试。 第一节显示待测试代码项目中的代码。 突出显示了类型约束。

第二部分显示测试项目中的代码。

#### <a name="code-under-test-project"></a>待测试代码项目

```csharp
using System;
using System.Linq;
using System.Collections.Generic;
using System.Text;

namespace ClassLibrary2
{
    public class Employee
    {
        public Employee(string s, int i)
        {
        }
    }

    public class GenericList<T> where T : Employee
    {
        private class Node
        {
            private T data;
            public T Data
            {
                get { return data; }
                set { data = value; }
            }
        }
    }
}
```

#### <a name="test-project"></a>测试项目

与所有新生成的单元测试相同，必须将结论性断言语句添加到此单元测试，以便使其返回有用结果。 不将它们添加到标有 TestMethod 特性的方法，而是添加到“TestHelper”方法，对此测试来说即 `DataTestHelper<T>()`。

在此示例中，泛型类型参数 `T` 具有约束 `where T : Employee`。 测试方法中未满足此约束。 因此，`DataTest()` 方法包含一个断言语句，提醒你要求提供已置于 `T` 上的类型约束。 此断言语句的消息如下所示：`("No appropriate type parameter is found to satisfies the type constraint(s) of T. " + "Please call DataTestHelper<T>() with appropriate type parameters.");`

换而言之，当从测试方法 `DataTest()` 调用 `DataTestHelper<T>()` 方法时，必须传递 `Employee` 类型的参数或从 `Employee` 派生的类。

```csharp
using ClassLibrary2;
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace TestProject1
{
    [TestClass()]
    public class GenericList_NodeTest
    {

        public void DataTestHelper<T>()
            where T : Employee
        {
            GenericList_Shadow<T>.Node target = new GenericList_Shadow<T>.Node(); // TODO: Initialize to an appropriate value
            T expected = default(T); // TODO: Initialize to an appropriate value
            T actual;
            target.Data = expected;
            actual = target.Data;
            Assert.AreEqual(expected, actual);
            Assert.Inconclusive("Verify the correctness of this test method.");
        }

        [TestMethod()]
        public void DataTest()
        {
            Assert.Inconclusive("No appropriate type parameter is found to satisfies the type constraint(s) of T. " +
            "Please call DataTestHelper<T>() with appropriate type parameters.");
        }
    }
}
```

## <a name="see-also"></a>请参阅

- [单元测试代码](../test/unit-test-your-code.md)
