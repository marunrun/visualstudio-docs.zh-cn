---
title: C++核心准则检查器参考
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
# <a name="c-core-guidelines-checker-reference"></a>C++核心准则检查器参考

本部分列出C++了核心准则检查器警告。 有关代码分析的信息，请参阅[/analyze （代码分析）](/cpp/build/reference/analyze-code-analysis)和[快速入门： C/C++的代码分析](../code-quality/quick-start-code-analysis-for-c-cpp.md)。

> [!NOTE]
> 某些警告属于多个组，并非所有警告都有完整的参考主题。

## <a name="owner_pointer-group"></a>OWNER_POINTER 组

[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md)如果具有移动构造函数，则返回范围内的对象，而不是堆分配的对象。 请参阅[ C++核心准则 R。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26403 RESET_OR_DELETE_OWNER](C26403.md)重置或显式删除所有者 \<T > 指针 "% variable%"。 请参阅[ C++核心准则 R。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26404 DONT_DELETE_INVALID](C26404.md)请勿删除可能处于无效状态的所有者 \<T >。 请参阅[ C++核心准则 R。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26405 DONT_ASSIGN_TO_VALID](C26405.md)请勿分配给可能处于有效状态的所有者 \<T >。 请参阅[ C++核心准则 R。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26406 DONT_ASSIGN_RAW_TO_OWNER](C26406.md)请勿将原始指针分配给所有者 \<T >。 请参阅[ C++核心准则 R。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26407 DONT_HEAP_ALLOCATE_UNNECESSARILY](C26407.md)首选范围内的对象，请勿进行不必要的堆分配。 请参阅[ C++核心准则 5. 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)。

[C26429 USE_NOTNULL](C26429.md)符号 "% symbol%" 从未针对非 null 进行测试，可将其标记为 not_null。 请参阅[ C++核心准则 F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26430 TEST_ON_ALL_PATHS](C26430.md)未在所有路径上测试符号 "% symbol%" 的非 null。 请参阅[ C++核心准则 F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26431 DONT_TEST_NOTNULL](C26431.md)表达式 "% expr%" 的类型已 gsl：： not_null。 不要对非 null 进行测试。 请参阅[ C++核心准则 F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

## <a name="raw_pointer-group"></a>RAW_POINTER 组

[C26400 NO_RAW_POINTER_ASSIGNMENT](c26400.md)不要将分配或函数调用的结果分配给所有者 \<T > 返回值为原始指针;改用所有者 \<T >。 请参阅[ C++核心准则 ... 11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw)。

[C26401 DONT_DELETE_NON_OWNER](c26401.md)请勿删除不是所有者 \<T > 的原始指针。 请参阅[ C++核心准则 ... 11](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Ri-raw)。

如果具有移动构造函数，则[C26402 DONT_HEAP_ALLOCATE_MOVABLE_RESULT](C26402.md)   返回一个范围内的对象，而不是堆分配的对象。 请参阅[ C++核心准则 R。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-ptr)。

[C26408 NO_MALLOC_FREE](C26408.md)避免使用 malloc （）和 free （），首选 nothrow 版本的 new 和 delete。 请参阅[ C++核心准则 R。](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-mallocfree)

[C26409 NO_NEW_DELETE](C26409.md)避免显式调用 new 和 delete，请改用 std：： make_unique \<T >。 请参阅[ C++核心指导原则](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-newdelete)。

[C26429 USE_NOTNULL](C26429.md)符号 "% symbol%" 从未针对非 null 进行测试，可将其标记为 not_null。 请参阅[ C++核心准则 F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26430 TEST_ON_ALL_PATHS](C26430.md)未在所有路径上测试符号 "% symbol%" 的非 null。 请参阅[ C++核心准则 F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26431 DONT_TEST_NOTNULL](C26431.md)表达式 "% expr%" 的类型已 gsl：： not_null。 不要对非 null 进行测试。 请参阅[ C++核心准则 F. 23](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f23-use-a-not_nullt-to-indicate-that-null-is-not-a-valid-value)。

[C26481 NO_POINTER_ARITHMETIC](C26481.md)请勿使用指针算法。 请改用跨距。 请参阅[ C++核心准则的界限。](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md)。
表达式 "% expr%"：没有要进行指针衰减的数组。 请参阅[ C++核心准则边界。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)。

## <a name="unique_pointer-group"></a>UNIQUE_POINTER 组

[C26410 NO_REF_TO_CONST_UNIQUE_PTR](C26410.md)参数 "% parameter%" 是对 `const` 唯一指针的引用，请改用 const T * 或 const T &。 请参阅[ C++核心准则（32](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-uniqueptrparam)）。

[C26411 NO_REF_TO_UNIQUE_PTR](C26411.md)参数 "% parameter%" 是对唯一指针的引用，并且从未重新分配或重置，请改用 T * 或 T &。 请参阅[ C++核心准则 R. 33](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-reseat)。

[C26414 RESET_LOCAL_SMART_PTR](C26414.md)移动、复制、重新分配或重置本地智能指针 "% symbol%"。 请参阅[ C++核心准则 5. 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)。

[C26415 SMART_PTR_NOT_NEEDED](C26415.md)智能指针参数 "% symbol%" 仅用于访问包含的指针。 改用 T * 或 T &。 请参阅[ C++核心准则 R。](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam)

## <a name="shared_pointer-group"></a>SHARED_POINTER 组

[C26414 RESET_LOCAL_SMART_PTR](C26414.md)移动、复制、重新分配或重置本地智能指针 "% symbol%"。 请参阅[ C++核心准则 5. 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-scoped)。

[C26415 SMART_PTR_NOT_NEEDED](C26415.md)智能指针参数 "% symbol%" 仅用于访问包含的指针。 改用 T * 或 T &。 请参阅[ C++核心准则 R。](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-smartptrparam)

[C26416 NO_RVALUE_REF_SHARED_PTR](C26416.md)由右值引用传递共享指针参数 "% symbol%"。 改为通过值传递。 请参阅[ C++核心准则 R。](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-owner)

[C26417 NO_LVALUE_REF_SHARED_PTR](C26417.md)共享指针参数 "% symbol%" 按引用传递，且未重置或重新分配。 改用 T * 或 T &。 请参阅[ C++核心准则 R. 35](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam)。

[C26418 NO_VALUE_OR_CONST_REF_SHARED_PTR](C26418.md)共享指针参数 "% symbol%" 不会复制或移动。 改用 T * 或 T &。 请参阅[ C++核心准则-36](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rr-sharedptrparam-const)。

## <a name="declaration-group"></a>声明组

[C26426 NO_GLOBAL_INIT_CALLS](C26426.md)全局初始化表达式调用非 constexpr 函数 "% symbol%"。 请参阅[ C++核心准则 I. 22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects)。

[C26427 NO_GLOBAL_INIT_EXTERNS](C26427.md)全局初始化表达式访问外部对象 "% symbol%"。 请参阅[ C++核心准则 I. 22](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#i22-avoid-complex-initialization-of-global-objects)。

[C26444 NO_UNNAMED_RAII_OBJECTS](c26444.md)避免具有自定义构造和析构的未命名对象。 请参阅[ES：请勿（尝试）声明不带名称的局部变量](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)。

## <a name="class-group"></a>类组

[C26432 DEFINE_OR_DELETE_SPECIAL_OPS](C26432.md)如果定义或删除类型为 "% symbol%" 的任何默认操作，请定义或删除所有默认操作。 请参阅[ C++核心准则 c.](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c21-if-you-define-or-delete-any-default-operation-define-or-delete-them-all)。

[C26433 OVERRIDE_EXPLICITLY](c26433.md)函数 "% symbol%" 应标有 "override"。 请参阅[c. 128：虚函数应精确指定虚拟、替代或最终的一个](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final)。

[C26434 DONT_HIDE_METHODS](C26434.md)函数 "% symbol_1%" 隐藏了非虚拟函数 "% symbol_2%"。 请参阅[ C++核心准则 c.](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c128-virtual-functions-should-specify-exactly-one-of-virtual-override-or-final)。

[C26435 SINGLE_VIRTUAL_SPECIFICATION](c26435.md)函数 "% symbol%" 应仅指定 "virtual"、"override" 或 "final" 中的一个。 请参阅[c. 128：虚函数应精确指定虚拟、替代或最终的一个](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)。

[C26436 NEED_VIRTUAL_DTOR](C26436.md)具有虚拟函数的类型 "% symbol%" 需要公共虚拟析构函数或受保护的非虚拟析构函数。 请参阅[ C++核心准则 c.](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#c35-a-base-class-destructor-should-be-either-public-and-virtual-or-protected-and-nonvirtual)。

[C26443 NO_EXPLICIT_DTOR_OVERRIDE](c26443.md)重写析构函数不应使用显式 "重写" 或 "虚拟" 说明符。 请参阅[c. 128：虚函数应精确指定虚拟、替代或最终的一个](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)。

## <a name="type-group"></a>类型组

[C26437 DONT_SLICE](C26437.md)不切片。 请参阅[ C++核心准则 ES](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es63-dont-slice)。

## <a name="style-group"></a>样式组

[C26438 NO_GOTO](C26438.md)避免 `goto`。 请参阅[ C++核心原则](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es76-avoid-goto)。

## <a name="function-group"></a>函数组

[C26439 SPECIAL_NOEXCEPT](C26439.md)此类函数可能不会引发。 @No__t_0 声明。 请参阅[ C++核心原则 6. 6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)。

[C26440 DECLARE_NOEXCEPT](C26440.md)函数 "% symbol%" 可 `noexcept` 声明。 请参阅[ C++核心原则 6. 6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)。

[C26447 DONT_THROW_IN_NOEXCEPT](c26447.md)函数被声明为**noexcept** ，但会调用可能引发异常的函数。
请参阅[ C++核心准则： f.：如果函数可能不会引发，则将其声明为 noexcept](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#f6-if-your-function-may-not-throw-declare-it-noexcept)。

## <a name="concurrency-group"></a>并发组

[C26441 NO_UNNAMED_GUARDS](C26441.md)必须将 Guard 对象命名为。 请参阅[ C++核心准则 cp. 44](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#cp44-remember-to-name-your-lock_guards-and-unique_locks)。

## <a name="const-group"></a>常量组

[C26460 USE_CONST_REFERENCE_ARGUMENTS](c26460.md)函数 "% function%" 的引用参数 "% argument%" 可以标记为 `const`。 请参阅[ C++核心准则 con。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref)。

[C26461 USE_CONST_POINTER_ARGUMENTS](c26461.md)：函数 "% function%" 的指针参数 "% argument%" 可标记为指向 `const` 的指针。 请参阅[ C++核心准则 con。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-ref)。

[C26462 USE_CONST_POINTER_FOR_VARIABLE](c26462.md)"% Variable%" 指向的值仅分配一次，将其标记为指向 `const` 的指针。 请参阅[ C++核心准则。 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)。

[C26463 USE_CONST_FOR_ELEMENTS](c26463.md)数组 "% array%" 的元素仅分配一次，将元素标记 `const`。 请参阅[ C++核心准则。 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)。

[C26464 USE_CONST_POINTER_FOR_ELEMENTS](c26464.md)仅分配一次由数组 "% array%" 的元素指向的值，将元素标记为指向 `const` 的指针。 请参阅[ C++核心准则。 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)。

[C26496 USE_CONST_FOR_VARIABLE](c26496.md)仅分配一次变量 "% variable%"，将其标记为 `const`。 请参阅[ C++核心准则。 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con4-use-const-to-define-objects-with-values-that-do-not-change-after-construction)。

[C26497 USE_CONSTEXPR_FOR_FUNCTION](c26497.md)如果需要编译时计算，则可以将此函数% function% 标记 `constexpr`。 请参阅[ C++核心准则 a-f](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rf-constexpr)。

[C26498 USE_CONSTEXPR_FOR_FUNCTIONCALL](c26498.md)如果需要编译时计算，则此函数调用% function% 可使用 `constexpr`。 请参阅[ C++核心准则 5. 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Rconst-constexpr)。

## <a name="type-group"></a>类型组

[C26465 NO_CONST_CAST_UNNECESSARY](c26465.md)不要使用 `const_cast` 来强制转换为 `const`。 不需要 `const_cast`;此转换未删除 constness 或波动性。 请参阅[ C++核心准则类型。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-constcast)。

[C26466 NO_STATIC_DOWNCAST_POLYMORPHIC](c26466.md)不要使用 `static_cast` type.2。 从多态类型强制转换应使用 dynamic_cast。 请参阅[ C++核心准则类型。 2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-downcast)。

[C26471 NO_REINTERPRET_CAST_FROM_VOID_PTR](c26471.md)不要使用 `reinterpret_cast`。 Void * 的强制转换可以使用 `static_cast`。 请参阅[ C++核心准则类型。 1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)。

[C26472 NO_CASTS_FOR_ARITHMETIC_CONVERSION](C26472.md)不要使用 `static_cast` 进行算术转换。 使用大括号初始化、gsl：： narrow_cast 或 gsl：： narow。 请参阅[ C++核心准则类型。 1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)。

[C26473 NO_IDENTITY_CAST](C26473.md)请勿在源类型与目标类型相同的指针类型之间转换。 请参阅[ C++核心准则类型。 1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)。

[C26474 NO_IMPLICIT_CAST](C26474.md)当转换可以是隐式时，请勿在指针类型之间强制转换。 请参阅[ C++核心准则类型。 1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Pro-type-reinterpretcast)。

[C26475 NO_FUNCTION_STYLE_CASTS](C26475.md)不要使用函数样式 C 强制转换。 请参阅[ C++核心准则 ES](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#es49-if-you-must-use-a-cast-use-a-named-cast)。

[C26490 NO_REINTERPRET_CAST](c26490.md)不要使用 `reinterpret_cast`。 请参阅[ C++核心准则类型。 1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26491 NO_STATIC_DOWNCAST](c26490.md)不要使用 `static_cast` type.2。 请参阅[ C++核心准则类型。 2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26492 NO_CONST_CAST](c26492.md)不要使用 `const_cast` 来强制转换为 `const`。 请参阅[ C++核心准则类型。 3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26493 NO_CSTYLE_CAST](c26493.md)不要使用 C 样式强制转换。 请参阅[ C++核心准则类型 4](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26494 VAR_USE_BEFORE_INIT](c26494.md)变量 "% variable%" 未初始化。 始终初始化对象。 请参阅[ C++核心准则类型 5](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

[C26495 MEMBER_UNINIT](c26495.md)变量 "% variable%" 未初始化。 始终初始化成员变量。 请参阅[ C++核心准则类型 6](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-type)。

## <a name="bounds-group"></a>边界组

[C26446 USE_GSL_AT](c26446.md)更倾向于使用 `gsl::at()` 而不是未选中的下标运算符。 请参阅[ C++核心准则：界限。4：不要使用未进行边界检查的标准库函数和类型](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)。

[C26481 NO_POINTER_ARITHMETIC](C26481.md)。
请勿使用指针算法。 请改用跨距。 请参阅[ C++核心准则边界。1](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26482 NO_DYNAMIC_ARRAY_INDEXING](c26482.md)只使用常量表达式在数组中建立索引。 请参阅[ C++核心准则边界。2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26483 STATIC_INDEX_OUT_OF_RANGE](c26483.md)值% value% 超出界限（0，% 界限%）变量 "% variable%" 的。 仅使用数组界限内的常量表达式对数组进行索引。 请参阅[ C++核心准则边界。2](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

[C26485 NO_ARRAY_TO_POINTER_DECAY](C26485.md)表达式 "% expr%"：没有要进行指针衰减的数组。 请参阅[ C++核心准则边界。3](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-bounds)

## <a name="gsl-group"></a>GSL 组

[C26445 NO_SPAN_REF](c26445.md)对 `gsl::span` 或 `std::string_view` 的引用可能表示生存期问题。
请参阅[ C++核心准则 GSL：视图](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)

[C26446 USE_GSL_AT](c26446.md)更倾向于使用 `gsl::at()` 而不是未选中的下标运算符。 请参阅[ C++核心准则：界限。4：不要使用未进行边界检查的标准库函数和类型](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile)。

[C26448 USE_GSL_FINALLY](c26448.md)如果要执行最终操作，请考虑使用 `gsl::finally`。 请参阅[ C++核心准则： GSL. util：实用工具](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#SS-utilities)。

当暂时无效时，从临时创建的[C26449 NO_SPAN_FROM_TEMPORARY](c26449.md) 
 `gsl::span` 或 `std::string_view` 将无效。 请参阅[ C++核心准则： GSL： Views](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#gslview-views)。

## <a name="deprecated-warnings"></a>弃用的警告

在核心准则检查器的早期实验性规则集中存在以下警告，但现在已弃用，可以放心地忽略这些警告。 上述列表中的警告将取代警告。

- 26412 DEREF_INVALID_POINTER
- 26413 DEREF_NULLPTR
- 26420 ASSIGN_NONOWNER_TO_EXPLICIT_OWNER
- 26421 ASSIGN_VALID_OWNER
- 26422 VALID_OWNER_LEAVING_SCOPE
- 26423 ALLOCATION_NOT_ASSIGNED_TO_OWNER
- 26424 VALID_ALLOCATION_LEAVING_SCOPE
- 26425 ASSIGNING_TO_STATIC
- 26499 NO_LIFETIME_TRACKING

## <a name="see-also"></a>请参阅
[使用C++核心准则检查](using-the-cpp-core-guidelines-checkers.md)
