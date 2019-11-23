---
title: C + + Core Guidelines 检查程序引用
ms.date: 03/22/2018
ms.topic: reference
helpviewer_keywords:
- code analysis, C++ core check
ms.assetid: f1429463-136e-41ed-8a75-a8dbf0b4fd89
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 9a5fe14c1bcb2b375a104a928513134b1789d437
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745963"
---
# <a name="c-core-guidelines-checker-reference"></a>C + + Core Guidelines 检查程序引用

本部分列出了 c + + 核心准则检查程序警告。 有关代码分析的信息，请参阅[/analyze （代码分析）](/cpp/build/reference/analyze-code-analysis)并[快速入门： C/c + + 代码分析](../code-quality/quick-start-code-analysis-for-c-cpp.md)。

> [!NOTE]
> 一些警告属于多个组，而不是所有警告都有一个完整的参考主题。

## <a name="owner_pointer-group"></a>OWNER_POINTER 组

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md)返回限定了作用域的对象而不是堆分配，如果它具有移动构造函数。 请参阅[c + + 核心准则 R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26403 RESET_OR_DELETE_OWNER](C26403.md)重置或显式删除所有者\<T > 指针 %变量 %。 请参阅[c + + 核心准则 R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26404 DONT_DELETE_INVALID](C26404.md)未删除的所有者\<T > 的可能处于无效状态。 请参阅[c + + 核心准则 R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26405 DONT_ASSIGN_TO_VALID](C26405.md)不将分配给所有者\<T > 的可能处于有效状态。 请参阅[c + + 核心准则 R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26406 DONT_ASSIGN_RAW_TO_OWNER](C26406.md)现在将原始指针分配给所有者\<T >。 请参阅[c + + 核心准则 R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26407 DONT_HEAP_ALLOCATE_UNNECESSARILY](C26407.md)首选范围内的对象，不堆不必要的分配。 请参阅[c + + 核心准则 R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)。

[C26429 USE_NOTNULL](C26429.md)符号 %符号 %永远不会测试值是否为 null，可以将它标记为空白。 请参阅[c + + 核心准则 F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26430 TEST_ON_ALL_PATHS](C26430.md)符号 %符号 %不测试值是否为 null 的所有路径上。 请参阅[c + + 核心准则 F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26431 DONT_TEST_NOTNULL](C26431.md)表达式 %expr%的类型已经是 gsl:: not_null。 测试它为 null。 请参阅[c + + 核心准则 F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

## <a name="raw_pointer-group"></a>RAW_POINTER 组

[C26400 NO_RAW_POINTER_ASSIGNMENT](c26400.md)不执行分配或函数调用的结果将包含所有者\<T > 的值返回到原始指针; 使用所有者\<T > 改为。 请参阅[c + + 核心准则 I.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw)。

[C26401 DONT_DELETE_NON_OWNER](c26401.md)请勿删除不是所有者的原始指针\<T >。 请参阅[c + + 核心准则 I.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw)。

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md)  返回限定了作用域的对象而不是堆分配，如果它具有移动构造函数。 请参阅[c + + 核心准则 R.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26408 NO_MALLOC_FREE](C26408.md)避免使用 malloc （） 和 free （），首选 nothrow 版本的 new 与 delete。 请参阅[c + + 核心准则 R.10](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-mallocfree)。

[C26409 NO_NEW_DELETE](C26409.md)避免调用 new 和显式删除，请使用 std::make_unique\<T > 改为。 请参阅[c + + 核心准则 R.11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-newdelete)。

[C26429 USE_NOTNULL](C26429.md)符号 %符号 %永远不会测试值是否为 null，可以将它标记为空白。 请参阅[c + + 核心准则 F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26430 TEST_ON_ALL_PATHS](C26430.md)符号 %符号 %不测试值是否为 null 的所有路径上。 请参阅[c + + 核心准则 F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26431 DONT_TEST_NOTNULL](C26431.md)表达式 %expr%的类型已经是 gsl:: not_null。 测试它为 null。 请参阅[c + + 核心准则 F.23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26481 NO_POINTER_ARITHMETIC](C26481.md)不使用指针算法。 请改用跨度。 请参阅[c + + 核心准则 Bounds.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)。

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md)。
表达式 %expr%： 组到指针的衰减。 请参阅[c + + 核心准则 Bounds.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)。

## <a name="unique_pointer-group"></a>UNIQUE_POINTER 组

[C26410 NO_REF_TO_CONST_UNIQUE_PTR](C26410.md)参数 %参数 %是指`const`唯一指针，使用 const T * 或 const T &。 请参阅[c + + 核心准则 R.32](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-uniqueptrparam)。

[C26411 NO_REF_TO_UNIQUE_PTR](C26411.md)参数 %参数 %是对唯一指针的引用，并且永远不会重新分配或重置，改用 T * 或 &。 请参阅[c + + 核心准则 R.33](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-reseat)。

[C26414 RESET_LOCAL_SMART_PTR](C26414.md)移动、 复制、 重新分配，或重置本地智能指针 %符号 %。 请参阅[c + + 核心准则 R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)。

[C26415 SMART_PTR_NOT_NEEDED](C26415.md)智能指针参数 %符号 %仅用于访问包含的指针。 改用 T * 或 &。 请参阅[c + + 核心准则 R.30](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam)。

## <a name="shared_pointer-group"></a>SHARED_POINTER 组

[C26414 RESET_LOCAL_SMART_PTR](C26414.md)移动、 复制、 重新分配，或重置本地智能指针 %符号 %。 请参阅[c + + 核心准则 R.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)。

[C26415 SMART_PTR_NOT_NEEDED](C26415.md)智能指针参数 %符号 %仅用于访问包含的指针。 改用 T * 或 &。 请参阅[c + + 核心准则 R.30](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam)。

[C26416 NO_RVALUE_REF_SHARED_PTR](C26416.md)共享指针参数 %符号 %通过右值引用传递。 而是按值传递。 请参阅[c + + 核心准则 R.34](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-owner)。

[C26417 NO_LVALUE_REF_SHARED_PTR](C26417.md)通过引用传递并不会重置或重新分配共享指针参数 %符号 %。 改用 T * 或 &。 请参阅[c + + 核心准则 R.35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam)。

[C26418 NO_VALUE_OR_CONST_REF_SHARED_PTR](C26418.md)未复制或移动共享指针参数 %符号 %。 改用 T * 或 &。 请参阅[c + + 核心准则 R.36](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-const)。

## <a name="declaration-group"></a>声明组

[C26426 NO_GLOBAL_INIT_CALLS](C26426.md)全局初始值设定项调用非 constexpr 函数 %符号 %。 请参阅[c + + 核心准则 I.22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects)。

[C26427 NO_GLOBAL_INIT_EXTERNS](C26427.md)全局初始值设定项访问外部对象 %符号 %。 请参阅[c + + 核心准则 I.22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects)。

[C26444 NO_UNNAMED_RAII_OBJECTS](c26444.md)避免未命名的自定义构造和析构的对象。 请参阅[ES.84： 无 （尝试） 声明没有名称的本地变量](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)。

## <a name="class-group"></a>类组

[C26432 DEFINE_OR_DELETE_SPECIAL_OPS](C26432.md)定义或删除类型 %符号 %中的任何默认操作，如果定义或将其全部删除。 请参阅[c + + 核心准则 C.21](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c21-if-you-define-or-delete-any-default-operation-define-or-delete-them-all)。

[C26433 OVERRIDE_EXPLICITLY](c26433.md)函数 '%符号 %' 应标记为 override。 请参阅[C.128： 虚函数应明确指定的虚拟的重写时，或最终](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final)。

[C26434 DONT_HIDE_METHODS](C26434.md)函数 %symbol_1 移动 %将隐藏非虚拟函数 %symbol_2%。 请参阅[c + + 核心准则 C.128](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final)。

[C26435 SINGLE_VIRTUAL_SPECIFICATION](c26435.md)函数 '%符号 %' 应明确指定为 virtual、 替代或 final。 请参阅[C.128： 虚函数应明确指定的虚拟的重写时，或最终](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)。

[C26436 NEED_VIRTUAL_DTOR](C26436.md)类型具有虚拟函数的 %符号 %需要任一公共虚拟或受保护非虚拟析构函数。 请参阅[c + + 核心准则 C.35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c35-a-base-class-destructor-should-be-either-public-and-virtual-or-protected-and-nonvirtual)。

[C26443 NO_EXPLICIT_DTOR_OVERRIDE](c26443.md)重写析构函数不应使用显式重写或虚拟说明符。 请参阅[C.128： 虚函数应明确指定的虚拟的重写时，或最终](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)。

## <a name="type-group"></a>组类型

[C26437 DONT_SLICE](C26437.md)请勿使用切片。 请参阅[c + + 核心准则 ES.63](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es63-dont-slice)。

## <a name="style-group"></a>样式组

[C26438 NO_GOTO](C26438.md)避免`goto`。 请参阅[c + + 核心准则 ES.76](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es76-avoid-goto)。

## <a name="function-group"></a>函数组

[C26439 SPECIAL_NOEXCEPT](C26439.md)可能不会引发此类型的函数。 将其声明`noexcept`。 请参阅[c + + 核心准则 F.6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)。

[C26440 DECLARE_NOEXCEPT](C26440.md)可将函数 '%符号 %' 声明`noexcept`。 请参阅[c + + 核心准则 F.6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)。

[C26447 DONT_THROW_IN_NOEXCEPT](c26447.md)该函数声明**noexcept**但调用一个函数，它可能会引发异常。
请参阅[c + + Core Guidelines: F.6： 如果你的函数可能不会引发，将其声明 noexcept](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)。

## <a name="concurrency-group"></a>并发组

[C26441 NO_UNNAMED_GUARDS](C26441.md)临界对象必须命名为。 请参阅[c + + 核心准则 cp.44](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#cp44-remember-to-name-your-lock_guards-and-unique_locks)。

## <a name="const-group"></a>CONST 组

[C26460 USE_CONST_REFERENCE_ARGUMENTS](c26460.md)函数 %函数 %的引用参数 %参数 %可以标记为`const`。 请参阅[c + + 核心准则 con.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref)。

[C26461 USE_CONST_POINTER_ARGUMENTS](c26461.md)： 函数 %函数 %的指针参数 '%参数 %' 可以标记为指向`const`。 请参阅[c + + 核心准则 con.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref)。

[C26462 USE_CONST_POINTER_FOR_VARIABLE](c26462.md)指向由 %变量 %的值分配仅一次，将其标记为指向`const`。 请参阅[c + + 核心准则 con.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)。

[C26463 USE_CONST_FOR_ELEMENTS](c26463.md)阵列 %数组 %的元素分配一次，将元素标记`const`。 请参阅[c + + 核心准则 con.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)。

[C26464 USE_CONST_POINTER_FOR_ELEMENTS](c26464.md)指向的数组 %数组 %的元素的值仅分配一次，将元素标记为指向`const`。 请参阅[c + + 核心准则 con.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)。

[C26496 USE_CONST_FOR_VARIABLE](c26496.md)一次只能分配给变量 %变量 %是，将其标记为`const`。 请参阅[c + + 核心准则 con.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)。

[C26497 USE_CONSTEXPR_FOR_FUNCTION](c26497.md)无法标记此函数 %函数 %`constexpr`如果需要编译时计算。 请参阅[c + + 核心准则 F.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rf-constexpr)。

[C26498 USE_CONSTEXPR_FOR_FUNCTIONCALL](c26498.md)可以使用此函数调用 %函数 %`constexpr`如果需要编译时计算。 请参阅[c + + 核心准则 con.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-constexpr)。

## <a name="type-group"></a>组类型

[C26465 NO_CONST_CAST_UNNECESSARY](c26465.md)不要使用`const_cast`转换掉`const`。 `const_cast` 不是必需的;未通过此转换被删除常量性或易变性。 请参阅[c + + 核心准则 Type.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-constcast)。

[C26466 NO_STATIC_DOWNCAST_POLYMORPHIC](c26466.md)不要使用`static_cast`向下转换。 从多态类型强制转换应使用 dynamic_cast。 请参阅[c + + 核心准则 Type.2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-downcast)。

[C26471 NO_REINTERPRET_CAST_FROM_VOID_PTR](c26471.md)不要使用`reinterpret_cast`。 可以使用从 void * 转换`static_cast`。 请参阅[c + + 核心准则 Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)。

[C26472 NO_CASTS_FOR_ARITHMETIC_CONVERSION](C26472.md)不要使用`static_cast`有关算术转换。 使用大括号初始化、 gsl，:: narrow_cast 或 gsl:: narow。 请参阅[c + + 核心准则 Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)。

[C26473 NO_IDENTITY_CAST](C26473.md)其中的源类型和目标类型是相同的指针类型间强制转换。 请参阅[c + + 核心准则 Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)。

[C26474 NO_IMPLICIT_CAST](C26474.md)间指针类型时转换可能是隐式强制转换。 请参阅[c + + 核心准则 Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)。

[C26475 NO_FUNCTION_STYLE_CASTS](C26475.md)不使用函数样式 c-casts。 请参阅[c + + 核心准则 ES.49](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es49-if-you-must-use-a-cast-use-a-named-cast)。

[C26490 NO_REINTERPRET_CAST](c26490.md)不要使用`reinterpret_cast`。 请参阅[c + + 核心准则 Type.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26491 NO_STATIC_DOWNCAST](c26490.md)不要使用`static_cast`向下转换。 请参阅[c + + 核心准则 Type.2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26492 NO_CONST_CAST](c26492.md)不要使用`const_cast`转换掉`const`。 请参阅[c + + 核心准则 Type.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26493 NO_CSTYLE_CAST](c26493.md)请勿使用 C 样式转换。 请参阅[c + + 核心准则 Type.4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26494 VAR_USE_BEFORE_INIT](c26494.md)变量 %变量 %未初始化。 始终初始化对象。 请参阅[c + + 核心准则 Type.5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26495 MEMBER_UNINIT](c26495.md)变量 %变量 %未初始化。 务必初始化成员变量。 请参阅[c + + 核心准则 Type.6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

## <a name="bounds-group"></a>边界组

[C26446 USE_GSL_AT](c26446.md)更愿意使用`gsl::at()`而不是未选中的下标运算符。 请参阅[c + + Core Guidelines: Bounds.4： 不使用标准库函数和类型不是边界检查](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)。

[C26481 NO_POINTER_ARITHMETIC](C26481.md)。
请勿使用指针算法。 请改用跨度。 请参阅[c + + 核心准则 Bounds.1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26482 NO_DYNAMIC_ARRAY_INDEXING](c26482.md)仅使用常量表达式数组中的索引。 请参阅[c + + 核心准则 Bounds.2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26483 STATIC_INDEX_OUT_OF_RANGE](c26483.md)值 %value%已超出界限 （0，%绑定的 %） 的变量 %变量 %。 仅使用数组界限内的常量表达式在数组索引。 请参阅[c + + 核心准则 Bounds.2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md)表达式 %expr%： 组到指针的衰减。 请参阅[c + + 核心准则 Bounds.3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

## <a name="gsl-group"></a>GSL 组

[C26445 NO_SPAN_REF](c26445.md)对的引用`gsl::span`或`std::string_view`可能表示存在生存期问题。
请参阅[c + + 核心准则 GSL.view： 视图](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)

[C26446 USE_GSL_AT](c26446.md)更愿意使用`gsl::at()`而不是未选中的下标运算符。 请参阅[c + + Core Guidelines: Bounds.4： 不使用标准库函数和类型不是边界检查](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)。

[C26448 USE_GSL_FINALLY](c26448.md)如果要执行最终操作，请考虑使用 `gsl::finally`。 请参阅[c + + 核心准则： GSL.util： 实用程序](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-utilities)。

[C26449 NO_SPAN_FROM_TEMPORARY](c26449.md) 
 `gsl::span`或`std::string_view`创建从该临时将无效时临时失效。 请参阅[c + + 核心准则： GSL.view： 视图](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)。

## <a name="deprecated-warnings"></a>已弃用的警告

出现以下警告中的核心准则检查器中，早期试验性的规则集存在，但现已弃用，可以安全地忽略。 通过上面的列表中的警告，警告所取代。

- 26412 DEREF_INVALID_POINTER
- 26413 DEREF_NULLPTR
- 26420 ASSIGN_NONOWNER_TO_EXPLICIT_OWNER
- 26421 ASSIGN_VALID_OWNER
- 26422 VALID_OWNER_LEAVING_SCOPE
- 26423 ALLOCATION_NOT_ASSIGNED_TO_OWNER
- 26424 VALID_ALLOCATION_LEAVING_SCOPE
- 26425 ASSIGNING_TO_STATIC
- 26499 NO_LIFETIME_TRACKING

## <a name="see-also"></a>另请参阅
[使用 c + + Core Guidelines 检查器](using-the-cpp-core-guidelines-checkers.md)
