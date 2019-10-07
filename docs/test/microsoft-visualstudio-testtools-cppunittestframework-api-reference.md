---
title: Microsoft.VisualStudio.TestTools.CppUnitTestFramework API
ms.date: 09/27/2019
ms.topic: reference
ms.author: mblome
manager: jillfra
ms.workload:
- multiple
author: mikeblome
ms.openlocfilehash: 327aa6f79f7eda6ecc3f1c0a7b2576a87287b1c0
ms.sourcegitcommit: 628eb202a1153ebfe69c668f966f821b98b34b34
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2019
ms.locfileid: "71720517"
---
# <a name="microsoftvisualstudiotesttoolscppunittestframework-api-reference"></a>Microsoft.VisualStudio.TestTools.CppUnitTestFramework API 参考

本主题列出了 `Microsoft::VisualStudio::CppUnitTestFramework` 命名空间的公共成员。 使用这些 API 可编写基于 Microsoft 本机单元测试框架的 C++ 单元测试。 本主题末尾有一个[用法示例](#example)。

标头和 lib 文件位于 \<Visual Studio 安装文件夹>\VC\Auxiliary\VS\UnitTest  下。

头文件和 lib 路径会在本机测试项目中自动配置。

## <a name="In_this_topic"></a> 在本主题中

[CppUnitTest.h](#cppUnitTest_h)

- [创建测试类和方法](#create_test_classes_and_methods)

- [初始化和清理](#Initialize_and_cleanup)

  - [测试方法](#test_methods)

  - [测试类](#test_classes)

  - [测试模块](#test_modules)

- [创建测试属性](#create_test_attributes)

  - [测试方法属性](#test_method_attributes)

  - [测试类属性](#test_class_attributes)

  - [测试模块属性](#test_module_attributes)

  - [预定义属性](#pre_defined_attributes)

    [CppUnitTestAssert.h](#cppUnitTestAssert_h)

  - [常规断言](#general_asserts)

    - [相等](#general_are_equal)

    - [不相等](#general_are_not_equal)

    - [相同](#general_are_same)

    - [不相同](#general_are_not_same)

    - [为 Null](#general_is_null)

    - [不为 Null](#general_is_not_null)

    - [为 True](#general_is_True)

    - [为 False](#general_is_false)

    - [失败](#general_Fail)

  - [Windows 运行时断言](#winrt_asserts)

    - [相等](#winrt_are_equal)

    - [相同](#winrt_are_same)

    - [不相等](#winrt_are_not_equal)

    - [不相同](#winrt_are_not_same)

    - [为 Null](#winrt_is_null)

    - [不为 Null](#winrt_is_not_null)

  - [异常断言](#exception_asserts)

    - [预期异常](#expect_exception)

      [CppUnitTestLogger.h](#cppunittestlogger_h)

    - [记录器类](#logger)

    - [编写消息](#write_message)

  - [用法示例](#example)

## <a name="cppUnitTest_h"></a> CppUnitTest.h

### <a name="create_test_classes_and_methods"></a> 创建测试类和方法

```cpp
TEST_CLASS(className)
```

对于包含测试方法的每个类是必需的。 将 className  标识为测试类。 `TEST_CLASS` 必须在名称范围的范围内声明。

```cpp
TEST_METHOD(methodName)
{
    // test method body
}
```

将 methodName  定义为测试方法。 `TEST_METHOD` 必须在该方法的类的范围内声明。

### <a name="Initialize_and_cleanup"></a> 初始化和清理

#### <a name="test_methods"></a> 测试方法

```cpp
TEST_METHOD_INITIALIZE(methodName)
{
    // method initialization code
}
```

将 methodName  定义为在运行每个测试方法运行之前的方法。 `TEST_METHOD_INITIALIZE` 只能在测试类中定义一次，且必须在测试类的范围内定义。

```cpp
TEST_METHOD_CLEANUP(methodName)
{
    // test method cleanup  code
}
```

将 methodName  定义为在运行每个测试方法之后运行的方法。 `TEST_METHOD_CLEANUP` 只能在测试类中定义一次，且必须在测试类的范围内定义。

#### <a name="test_classes"></a> 测试类

```cpp
TEST_CLASS_INITIALIZE(methodName)
{
    // test class initialization  code
}
```

将 methodName 定义为在创建每个测试类之前运行的方法  。 `TEST_CLASS_INITIALIZE` 只能在测试类中定义一次，且必须在测试类的范围内定义。

```cpp
TEST_CLASS_CLEANUP(methodName)
{
    // test class cleanup  code
}
```

将 methodName  定义为在创建每个测试方法之后运行的方法。 `TEST_CLASS_CLEANUP` 只能在测试类中定义一次，且必须在测试类的范围内定义。

#### <a name="test_modules"></a> 测试模块

```cpp
TEST_MODULE_INITIALIZE(methodName)
{
    // module initialization code
}
```

定义在加载模块时运行的方法 methodName  。 `TEST_MODULE_INITIALIZE` 只能在测试模块中定义一次，且必须在命名空间范围内声明。

```cpp
TEST_MODULE_CLEANUP(methodName)
```

定义在卸载模块时运行的方法 methodName  。 `TEST_MODULE_CLEANUP` 只能在测试模块中定义一次，且必须在命名空间范围内声明。

### <a name="create_test_attributes"></a> 创建测试属性

#### <a name="test_method_attributes"></a> 测试方法属性

```cpp
BEGIN_TEST_METHOD_ATTRIBUTE(testMethodName)
    TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_METHOD_ATTRIBUTE()
```

将使用一个或多个 `TEST_METHOD_ATTRIBUTE` 宏定义的属性添加到测试方法 testMethodName  。

`TEST_METHOD_ATTRIBUTE` 宏定义一个具有名称 attributeName  和值 attributeValue  的属性。

#### <a name="test_class_attributes"></a> 测试类属性

```cpp
BEGIN_TEST_CLASS_ATTRIBUTE(testClassName)
    TEST_CLASS_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_CLASS_ATTRIBUTE()
```

将使用一个或多个 `TEST_CLASS_ATTRIBUTE` 宏定义的属性添加到测试类 testClassName  。

`TEST_CLASS_ATTRIBUTE` 宏定义一个具有名称 attributeName  和值 attributeValue  的属性。

#### <a name="test_module_attributes"></a> 测试模块属性

```cpp
BEGIN_TEST_MODULE_ATTRIBUTE(testModuleName)
    TEST_MODULE_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_MODULE_ATTRIBUTE()
```

将使用一个或多个 `TEST_MODULE_ATTRIBUTE` 宏定义的属性添加到测试模块 testModuleName  。

`TEST_MODULE_ATTRIBUTE` 宏定义一个具有名称 attributeName  和值 attributeValue  的属性。

#### <a name="pre_defined_attributes"></a> 预定义属性

提供这些预定义的属性宏，以便为常见情况提供便利。 它们可以代替上述宏 `TEST_METHOD_ATTRIBUTE`。

```cpp
TEST_OWNER(ownerAlias)
```

定义一个具有名称 `Owner` 和属性值 ownerAlias  的 `TEST_METHOD_ATTRIBUTE`。

```cpp
TEST_DESCRIPTION(description)
```

定义一个具有名称 `Description` 和属性值 description  的 `TEST_METHOD_ATTRIBUTE`。

```cpp
TEST_PRIORITY(priority)
```

定义一个具有名称 `Priority` 和属性值 priority  的 `TEST_METHOD_ATTRIBUTE`。

```cpp
TEST_WORKITEM(workitem)
```

定义一个具有名称 `WorkItem` 和属性值 workItem  的 `TEST_METHOD_ATTRIBUTE`。

```cpp
TEST_IGNORE()
```

定义一个具有名称 `Ignore` 和属性值 `true` 的 `TEST_METHOD_ATTRIBUTE`。

## <a name="cppUnitTestAssert_h"></a> CppUnitTestAssert.h

### <a name="general_asserts"></a> 常规断言

#### <a name="general_are_equal"></a> 相等
验证两个对象是否相等

```cpp
template<typename T>
static void Assert::AreEqual(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

验证两个双精度值是否相等

```cpp
static void Assert::AreEqual(
    double expected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

验证两个浮点值是否相等

```cpp
static void Assert::AreEqual(
    float expected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

验证两个 char* 字符串是否相等

```cpp
static void Assert::AreEqual(
    const char* expected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

验证两个 w_char* 字符串是否相等

```cpp
static void Assert::AreEqual(
    const wchar_t* expected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="general_are_not_equal"></a> 不相等
验证两个双精度值是否不相等

```cpp
static void Assert::AreNotEqual(
    double notExpected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

验证两个浮点值是否不相等

```cpp
static void Assert::AreNotEqual(
    float notExpected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

验证两个 char* 字符串是否不相等

```cpp
static void Assert::AreNotEqual(
    const char* notExpected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

验证两个 w_char* 字符串是否不相等

```cpp
static void Assert::AreNotEqual(
    const wchar_t* notExpected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

基于运算符 == 验证两个引用是否不相等。

```cpp
template<typename T>
static void Assert::AreNotEqual(
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="general_are_same"></a> 相同
验证两个引用是否引用相同对象实例（标识）。

```cpp
template<typename T>
static void Assert::AreSame(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="general_are_not_same"></a> 不相同
验证两个引用是否不引用相同对象实例（标识）。

```cpp
template<typename T>
static void Assert::AreNotSame (
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="general_is_null"></a> 为 Null
验证指针是否为 NULL。

```cpp
template<typename T>
static void Assert::IsNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="general_is_not_null"></a> 不为 Null
验证指针是否不为 NULL

```cpp
template<typename T>
static void Assert::IsNotNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="general_is_True"></a> 为 True
验证条件是否为 true

```cpp
static void Assert::IsTrue(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="general_is_false"></a> 为 False
验证条件是否为 false

```cpp
static void Assert::IsFalse(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="general_Fail"></a> 失败
强制测试用例结果为失败

```cpp
static void Assert::Fail(
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

### <a name="winrt_asserts"></a> Windows 运行时断言

#### <a name="winrt_are_equal"></a> 相等
验证两个 Windows 运行时指针是否相等。

```cpp
template<typename T>
static void Assert::AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

验证两个 Platform::String^ 字符串是否相等。

```cpp
template<typename T>
static void Assert::AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="winrt_are_same"></a> 相同
验证两个 Windows 运行时引用是否引用相同对象。

```cpp
template<typename T>
static void Assert::AreSame(
    T% expected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="winrt_are_not_equal"></a> 不相等
验证两个 Windows 运行时指针是否不相等。

```cpp
template<typename T>
static void Assert::AreNotEqual(
    T^ notExpected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

验证两个 Platform::String^ 字符串是否不相等。

```cpp
static void Assert::AreNotEqual(
    Platform::String^ notExpected,
    Platform::String^ actual,
    bool ignoreCase = false,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="winrt_are_not_same"></a> 不相同
验证两个 Windows 运行时引用是否不引用相同对象。

```cpp
template<typename T>
static void Assert::AreNotSame(
    T% notExpected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="winrt_is_null"></a> 为 Null
验证 Windows 运行时指针是否为 nullptr。

```cpp
template<typename T>
static void Assert::IsNull(
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="winrt_is_not_null"></a> 不为 Null
验证 Windows 运行时指针是否不为 nullptr。

```cpp
template<typename T>
static void Assert::IsNotNull(
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

### <a name="exception_asserts"></a> 异常断言

#### <a name="expect_exception"></a> 预期异常
验证函数是否会引发异常：

```cpp
template<typename _EXPECTEDEXCEPTION, typename _FUNCTOR>
static void Assert::ExpectException(
    _FUNCTOR functor,
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo= NULL)
```

验证函数是否会引发异常：

```cpp
template<typename _EXPECTEDEXCEPTION, typename _RETURNTYPE>
    static void Assert::ExpectException(
    _RETURNTYPE (*func)(),
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo = NULL)
```

## <a name="cppunittestlogger_h"></a> CppUnitTestLogger.h

### <a name="logger"></a> 记录器
Logger 类包含要写入到输出窗口  的静态方法。

### <a name="write_message"></a> 编写消息
将字符串写入到输出窗口 

```cpp
static void Logger::WriteMessage(const wchar_t* message)
```

```cpp
static void Logger::WriteMessage(const char* message)
```

## <a name="example"></a> 示例
此代码是一个 VSCppUnit 用法示例。 它包含属性元数据、装置、具有断言的单元测试以及自定义日志记录的示例。

```cpp
// USAGE EXAMPLE

#include <CppUnitTest.h>

using namespace Microsoft::VisualStudio::CppUnitTestFramework;

BEGIN_TEST_MODULE_ATTRIBUTE()
    TEST_MODULE_ATTRIBUTE(L"Date", L"2010/6/12")
END_TEST_MODULE_ATTRIBUTE()

TEST_MODULE_INITIALIZE(ModuleInitialize)
{
    Logger::WriteMessage("In Module Initialize");
}

TEST_MODULE_CLEANUP(ModuleCleanup)
{
    Logger::WriteMessage("In Module Cleanup");
}

TEST_CLASS(Class1)
{

public:

    Class1()
    {
        Logger::WriteMessage("In Class1");
    }

    ~Class1()
    {
        Logger::WriteMessage("In ~Class1");
    }

    TEST_CLASS_INITIALIZE(ClassInitialize)
    {
        Logger::WriteMessage("In Class Initialize");
    }

    TEST_CLASS_CLEANUP(ClassCleanup)
    {
        Logger::WriteMessage("In Class Cleanup");
    }

    BEGIN_TEST_METHOD_ATTRIBUTE(Method1)
        TEST_OWNER(L"OwnerName")
        TEST_PRIORITY(1)
    END_TEST_METHOD_ATTRIBUTE()

    TEST_METHOD(Method1)
    {
        Logger::WriteMessage("In Method1");
        Assert::AreEqual(0, 0);
    }

    TEST_METHOD(Method2)
    {
        Assert::Fail(L"Fail");
    }
};
```

## <a name="see-also"></a>请参阅

- [单元测试代码](../test/unit-test-your-code.md)
- [编写适用于 C/C++ 的单元测试](writing-unit-tests-for-c-cpp.md)
