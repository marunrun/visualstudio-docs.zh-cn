---
title: 使用 Microsoft.VisualStudio.TestTools.CppUnitTestFramework | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: d1ac9188-d79f-407e-9f3a-80dbefa66317
caps.latest.revision: 10
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c561555df40bc02c3c9f3090ee1de4c0f329bcdc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657175"
---
# <a name="using-microsoftvisualstudiotesttoolscppunittestframework"></a>使用 Microsoft.VisualStudio.TestTools.CppUnitTestFramework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题列出了 `Microsoft::VisualStudio::CppUnitTestFramework` 命名空间的公共成员。

 头文件位于 _VisualStudio2012[x86]InstallFolder_**\VC\UnitTest\include** 文件夹中。

 lib 文件位于 _VisualStudio2012[x86]InstallFolder_**\VC\UnitTest\lib** 文件夹。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> 在本主题中
 [CppUnitTest.h](#BKMK_CppUnitTest_h)

- [创建测试类和方法](#BKMK_Create_test_classes_and_methods)

- [初始化和清理](#BKMK_Initialize_and_cleanup)

  - [测试方法](#BKMK_Test_methods)

  - [测试类](#BKMK_Test_classes)

  - [测试模块](#BKMK_Test_modules)

- [创建测试属性](#BKMK_Create_test_attributes)

  - [测试方法属性](#BKMK_Test_method_attributes)

  - [测试类属性](#BKMK_Test_class_attributes)

  - [测试模块属性](#BKMK_Test_module_attributes)

  - [预定义属性](#BKMK_Pre_defined_attributes)

    [CppUnitTestAssert.h](#BKMK_CppUnitTestAssert_h)

  - [常规断言](#BKMK_General_Asserts)

    - [相等](#BKMK_General_Are_Equal)

    - [不相等](#BKMK_General_Are_Not_Equal)

    - [相同](#BKMK_General_Are_Same)

    - [不相同](#BKMK_General_Are_Not_Same)

    - [为 Null](#BKMK_General_Is_Null)

    - [不为 Null](#BKMK_General_Is_Not_Null)

    - [为 True](#BKMK_General_Is_True)

    - [为 False](#BKMK_General_Is_False)

    - [失败](#BKMK_General_Fail)

  - [Windows 运行时断言](#BKMK_WinRT_Asserts)

    - [相等](#BKMK_WinRT_Are_Equal)

    - [相同](#BKMK_WinRT_Are_Same)

    - [不相等](#BKMK_WinRT_Are_Not_Equal)

    - [不相同](#BKMK_WinRT_Are_Not_Same)

    - [为 Null](#BKMK_WinRT_Is_Null)

    - [不为 Null](#BKMK_WinRT_Is_Not_Null)

  - [异常断言](#BKMK_Exception_Asserts)

    - [预期异常](#BKMK_Expect_Exception)

      [CppUnitTestLogger.h](#BKMK_CppUnitTestLogger_h)

    - [记录器类](#BKMK_Logger)

    - [编写消息](#BKMK_Write_Message)

## <a name="cppunittesth"></a><a name="BKMK_CppUnitTest_h"></a> CppUnitTest.h

### <a name="create-test-classes-and-methods"></a><a name="BKMK_Create_test_classes_and_methods"></a> 创建测试类和方法

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

### <a name="initialize-and-cleanup"></a><a name="BKMK_Initialize_and_cleanup"></a> 初始化和清理

#### <a name="test-methods"></a><a name="BKMK_Test_methods"></a> 测试方法

```cpp
TEST_METHOD_INITIALIZE(methodName)
{
    // method initialization code
}

```

 将 methodName  定义为在运行每个测试方法运行之前的方法。 `TEST_METHOD_INITIALIZE` 只能在测试类中定义一次，且必须在测试类中定义。

```cpp
TEST_METHOD_CLEANUP(methodName)
{
    // test method cleanup  code
}

```

 将 methodName  定义为在运行每个测试方法之后运行的方法。 `TEST_METHOD_CLEANUP` 只能在测试类中定义一次，且必须在测试类的范围内定义。

#### <a name="test-classes"></a><a name="BKMK_Test_classes"></a> 测试类

```cpp
TEST_CLASS_INITIALIZE(methodName)
{
    // test class initialization  code
}

```

 将 methodName  定义为在创建每个测试方法之后运行的方法。 `TEST_CLASS_INITIALIZE` 只能在测试类中定义一次，且必须在测试类的范围内定义。

```cpp
TEST_CLASS_CLEANUP(methodName)
{
    // test class cleanup  code
}

```

 将 methodName  定义为在创建每个测试方法之后运行的方法。 `TEST_CLASS_CLEANUP` 只能在测试类中定义一次，且必须在测试类的范围内定义。

#### <a name="test-modules"></a><a name="BKMK_Test_modules"></a> 测试模块

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

### <a name="create-test-attributes"></a><a name="BKMK_Create_test_attributes"></a> 创建测试属性

#### <a name="test-method-attributes"></a><a name="BKMK_Test_method_attributes"></a> 测试方法属性

```cpp
BEGIN_TEST_METHOD_ATTRIBUTE(testMethodName)
    TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_METHOD_ATTRIBUTE()
```

 将使用一个或多个 `TEST_METHOD_ATTRIBUTE` 宏定义的属性添加到测试方法 testClassName**。

 `TEST_METHOD_ATTRIBUTE` 宏定义一个具有名称 attributeName  和值 attributeValue  的属性。

#### <a name="test-class-attributes"></a><a name="BKMK_Test_class_attributes"></a> 测试类属性

```cpp
BEGIN_TEST_CLASS_ATTRIBUTE(testClassName)
    TEST_CLASS_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_CLASS_ATTRIBUTE()
```

 将使用一个或多个 `TEST_CLASS_ATTRIBUTE` 宏定义的属性添加到测试类 testClassName  。

 `TEST_CLASS_ATTRIBUTE` 宏定义一个具有名称 attributeName  和值 attributeValue  的属性。

#### <a name="test-module-attributes"></a><a name="BKMK_Test_module_attributes"></a> 测试模块属性

```cpp
BEGIN_TEST_MODULE_ATTRIBUTE(testModuleName)
    TEST_MODULE_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_MODULE_ATTRIBUTE()
```

 将使用一个或多个 `TEST_MODULE_ATTRIBUTE` 宏定义的属性添加到测试模块 testModuleName  。

 `TEST_MODULE_ATTRIBUTE` 宏定义一个具有名称 attributeName  和值 attributeValue  的属性。

#### <a name="pre-defined-attributes"></a><a name="BKMK_Pre_defined_attributes"></a> 预定义属性
 可以为上面介绍的宏 `TEST_METHOD_ATTRIBUTE`、`TEST_CLASS_ATTRIBUTE` 或 `TEST_MODULE_ATTRIBUTE` 替换这些预定义属性。

```cpp
TEST_OWNER(ownerAlias)
```

 定义一个具有名称 `Owner` 和属性值 ownerAlias** 的属性。

```cpp
TEST_DESCRIPTION(description)
```

 定义一个具有名称 `Description` 和属性值 description** 的属性。

```cpp
TEST_PRIORITY(priority)
```

 定义一个具有名称 `Priority` 和属性值 priority** 的属性。

```cpp
TEST_WORKITEM(workitem)
```

 定义一个具有名称 `WorkItem` 和属性值 workItem** 的属性。

```cpp
TEST_IGNORE()
```

 定义一个具有名称 `Ignore` 和属性值 `true` 的属性。

## <a name="cppunittestasserth"></a><a name="BKMK_CppUnitTestAssert_h"></a> CppUnitTestAssert.h

### <a name="general-asserts"></a><a name="BKMK_General_Asserts"></a> 常规断言

#### <a name="are-equal"></a><a name="BKMK_General_Are_Equal"></a> 相等
 验证两个对象是否相等

```cpp
template<typename T>
static void AreEqual(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 验证两个双精度值是否相等

```cpp
static void AreEqual(
    double expected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 验证两个浮点值是否相等

```cpp
static void AreEqual(
    float expected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 验证两个 char* 字符串是否相等

```cpp
static void AreEqual(
    const char* expected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 验证两个 w_char* 字符串是否相等

```cpp
static void AreEqual(
    const wchar_t* expected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-not-equal"></a><a name="BKMK_General_Are_Not_Equal"></a> 不相等
 验证两个双精度值是否不相等

```cpp
static void AreNotEqual(
    double notExpected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 验证两个浮点值是否不相等

```cpp
static void AreNotEqual(
    float notExpected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 验证两个 char* 字符串是否不相等

```cpp
static void AreNotEqual(
    const char* notExpected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 验证两个 w_char* 字符串是否不相等

```cpp
static void AreNotEqual(
    const wchar_t* notExpected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 基于运算符 == 验证两个引用是否不相等。

```cpp
template<typename T>
static void AreNotEqual(
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-same"></a><a name="BKMK_General_Are_Same"></a> 相同
 验证两个引用是否引用相同对象实例（标识）。

```cpp
template<typename T>
static void AreSame(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-not-same"></a><a name="BKMK_General_Are_Not_Same"></a> 不相同
 验证两个引用是否不引用相同对象实例（标识）。

```cpp
template<typename T>
static void AreNotSame (
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-null"></a><a name="BKMK_General_Is_Null"></a> 为 Null
 验证指针是否为 NULL。

```cpp
template<typename T>
static void IsNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-not-null"></a><a name="BKMK_General_Is_Not_Null"></a> 不为 Null
 验证指针是否不为 NULL

```cpp
template<typename T>
static void IsNotNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-true"></a><a name="BKMK_General_Is_True"></a> 为 True
 验证条件是否为 true

```cpp
static void IsTrue(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-false"></a><a name="BKMK_General_Is_False"></a> 为 False
 验证条件是否为 false

```cpp
static void IsFalse(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="fail"></a><a name="BKMK_General_Fail"></a> 失败
 强制测试用例结果为失败

```cpp
static void Fail(
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

### <a name="windows-runtime-asserts"></a><a name="BKMK_WinRT_Asserts"></a> Windows 运行时断言

#### <a name="are-equal"></a><a name="BKMK_WinRT_Are_Equal"></a> 相等
 验证两个 Windows 运行时指针是否相等。

```
template<typename T>
static void AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

 验证两个 Platform::String^ 字符串是否相等。

```
template<typename T>
static void AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-same"></a><a name="BKMK_WinRT_Are_Same"></a> 相同
 验证两个 Windows 运行时引用是否引用相同对象。

```
template<typename T>
static void AreSame(
    T% expected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-not-equal"></a><a name="BKMK_WinRT_Are_Not_Equal"></a> 不相等
 验证两个 Windows 运行时指针是否不相等。

```
template<typename T>
static void AreNotEqual(
    T^ notExpected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

 验证两个 Platform::String^ 字符串是否不相等。

```
static void AreNotEqual(
    Platform::String^ notExpected,
    Platform::String^ actual,
    bool ignoreCase = false,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-not-same"></a><a name="BKMK_WinRT_Are_Not_Same"></a> 不相同
 验证两个 Windows 运行时引用是否不引用相同对象。

```
template<typename T>
static void AreNotSame(
    T% notExpected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="is-null"></a><a name="BKMK_WinRT_Is_Null"></a> 为 Null
 验证 Windows 运行时指针是否为 nullptr。

```
template<typename T>
static void IsNull(
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="is-not-null"></a><a name="BKMK_WinRT_Is_Not_Null"></a> 不为 Null
 验证 Windows 运行时指针是否不为 nullptr。

```
template<typename T>
static void IsNotNull(
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

### <a name="exception-asserts"></a><a name="BKMK_Exception_Asserts"></a> 异常断言

#### <a name="expect-exception"></a><a name="BKMK_Expect_Exception"></a> 预期异常
 验证函数是否会引发异常：

```
template<typename _EXPECTEDEXCEPTION, typename _FUNCTOR>
static void ExpectException(
    _FUNCTOR functor,
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo= NULL)
```

 验证函数是否会引发异常：

```
template<typename _EXPECTEDEXCEPTION, typename _RETURNTYPE>
    static void ExpectException(
    _RETURNTYPE (*func)(),
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo = NULL)
```

## <a name="cppunittestloggerh"></a><a name="BKMK_CppUnitTestLogger_h"></a> CppUnitTestLogger.h

### <a name="logger"></a><a name="BKMK_Logger"></a> 记录器
 Logger 类包含要写入到的静态方法

```
class Logger
```

### <a name="write-message"></a><a name="BKMK_Write_Message"></a> 编写消息

```
static void
Logger::WriteMessage(const wchar_t* message)
```

```
static void
Logger::WriteMessage(const char* message)
```

## <a name="example"></a>示例
 此代码是一个示例

```
////////////////////////////////////////////////////////////
/* USAGE EXAMPLE
// The following is an example of VSCppUnit usage.
// It includes examples of attribute metadata, fixtures,
// unit tests with assertions, and custom logging.

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

## <a name="see-also"></a>另请参阅
 [单元测试代码](../test/unit-test-your-code.md)[单元测试本机代码在测试资源管理器](https://msdn.microsoft.com/8a09d6d8-3613-49d8-9ffe-11375ac4736c)[中向现有的 c + + 应用程序添加单元测试](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)
