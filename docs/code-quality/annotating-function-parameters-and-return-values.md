---
title: 对函数参数和返回值进行批注
ms.date: 07/11/2019
ms.topic: conceptual
f1_keywords:
- _Outptr_opt_result_bytebuffer_to_
- _Inout_updates_all_opt_
- _Post_equal_to_
- _Outptr_opt_result_maybenull_
- _Out_writes_bytes_all_
- _Out_writes_all_opt_
- _In_opt_
- _Outptr_
- _Outptr_result_maybenull_
- _Outref_result_bytebuffer_all_maybenull_
- _Inout_updates_opt_z_
- _Inout_updates_z_
- _Out_writes_
- _Out_writes_to_ptr_opt_z_
- _In_reads_to_ptr_opt_
- _Ret_writes_to_maybenull_
- _Outref_result_maybenull_
- _Ret_writes_bytes_
- _Outptr_result_bytebuffer_
- _Out_writes_opt_
- _Inout_updates_bytes_opt_
- _In_z_
- _Inout_updates_to_
- _Ret_maybenull_
- _Ret_writes_bytes_to_
- _Ret_z_
- _COM_Outptr_
- _Ret_maybenull_z_
- _Out_opt_
- _In_reads_opt_z_
- _Outptr_result_bytebuffer_to_
- _Ret_notnull_
- _COM_Outptr_opt_result_maybenull_
- _Inout_updates_to_opt_
- _Inout_updates_
- _Outptr_opt_result_buffer_
- _Outptr_result_buffer_to_
- _Out_writes_to_ptr_opt_
- _Out_writes_bytes_all_opt_
- _Inout_updates_all_
- _Deref_inout_range_
- _Ret_writes_
- _Out_writes_z_
- _Ret_writes_to_
- _Out_writes_to_ptr_z_
- _Out_writes_bytes_to_opt_
- _In_reads_or_z_
- _Inout_updates_bytes_to_
- _In_reads_z_
- _In_opt_z_
- _Outref_result_buffer_maybenull_
- _Ret_range_
- _COM_Outptr_opt_
- _Ouptr_opt_result_maybenull_z_
- _In_reads_opt_
- _Inout_
- _Field_range_
- _Ret_writes_z_
- _Out_writes_to_
- _Out_writes_to_ptr_
- _Inout_opt_z_
- _Outref_
- _Deref_out_range_
- _Outref_result_buffer_
- _Outref_result_buffer_to_
- _Outref_result_bytebuffer_to_maybenull_
- _In_reads_bytes_
- _Outptr_opt_result_buffer_to_
- _Outref_result_buffer_all_
- _Out_writes_bytes_to_
- _Result_zeroonfailure_
- _In_reads_bytes_opt_
- _Outref_result_buffer_to_maybenull_
- _Outref_result_bytebuffer_all_
- _Outref_result_buffer_all_maybenull_
- _Ret_writes_maybenull_z_
- _In_range_
- _Inout_updates_bytes_all_opt_
- _Outref_result_bytebuffer_to_
- _Inout_updates_bytes_to_opt_
- _Pre_equal_to_
- _Ret_writes_bytes_maybenull_
- _COM_Outptr_result_maybenull_
- _Ret_writes_maybenull_
- _Out_writes_bytes_
- _Outptr_opt_
- _Out_writes_opt_z_
- _Outref_result_nullonfailure_
- _Outptr_opt_result_z_
- _Inout_opt_
- _Deref_in_range_
- _Outptr_result_z_
- _In_reads_to_ptr_opt_z_
- _Struct_size_bytes_
- _Outptr_result_nullonfailure_
- _In_
- _Inout_updates_bytes_
- _In_reads_to_ptr_z_
- _Ret_writes_bytes_to_maybenull
- _Outptr_opt_result_nullonfailure_
- _In_reads_to_ptr_
- _Outptr_result_buffer_
- _Out_
- _Outref_result_bytebuffer_maybenull_
- _Outptr_result_maybenull_z_
- _In_reads_
- _Inout_updates_opt_
- _Out_writes_to_opt_
- _Outptr_opt_result_bytebuffer_
- _Out_writes_all_
- _Out_range_
- _Inout_updates_bytes_all_
- _Inout_z_
- _Outref_result_bytebuffer_
- _Result_nullonfailure_
- _Ret_null_
- _Scanf_format_string_
- _Scanf_s_format_string_
- _Printf_format_string_
ms.assetid: 82826a3d-0c81-421c-8ffe-4072555dca3a
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- multiple
ms.openlocfilehash: 8f07650e47398b028460776f41557a3f853eaad3
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68919617"
---
# <a name="annotating-function-parameters-and-return-values"></a>对函数参数和返回值进行批注
本文介绍了简单函数参数 (标量) 的批注的典型用法, 以及大多数类型的缓冲区。  本文还介绍了批注的常见用法模式。 有关与函数相关的其他注释, 请参阅[注释函数行为](../code-quality/annotating-function-behavior.md)。

## <a name="pointer-parameters"></a>指针参数
对于下表中的批注, 当批注指针参数时, 如果指针为 null, 则分析器将报告错误。  这适用于指针和指向的任何数据项。

**批注和说明**

- `_In_`

     批注输入参数, 这些参数是标量、结构、指向结构的指针, 等等。  显式可用于简单的标量。  参数必须在预状态中有效, 且不会被修改。

- `_Out_`

     批注输出参数, 它们是标量、结构、指向结构的指针, 等等。  不要将此应用于无法返回值的对象, 例如, 通过值传递的标量。  该参数不必在预处理状态中有效, 但在 post 状态中必须有效。

- `_Inout_`

     批注函数将更改的参数。  它必须在前置状态和 post 状态中有效, 但在调用之前和之后, 将被视为具有不同的值。 必须应用于可修改的值。

- `_In_z_`

     指向以 null 结尾的字符串的指针, 该字符串用作输入。  该字符串必须在预状态中有效。  首选的`PSTR`变体 (已经具有正确的批注) 是首选的。

- `_Inout_z_`

     指向将修改的以 null 结尾的字符数组的指针。  它必须在调用之前和之后有效, 但假定值已更改。  可以移动 null 终止符, 但只能访问直到原始 null 终止符的元素。

- `_In_reads_(s)`

     `_In_reads_bytes_(s)`

     指向数组的指针, 该数组由函数读取。  数组的大小`s`为元素, 所有元素都必须有效。

     `_bytes_`变体提供的大小以字节为单位, 而不是元素。 仅在无法将大小表示为元素时使用此值。  例如, 仅`char`当使用`wchar_t`的类似`_bytes_`函数时, 字符串才使用变体。

- `_In_reads_z_(s)`

     指向数组的指针, 该数组以 null 值终止并具有已知大小。 直到空终止符的元素, 或者`s` , 如果没有空终止符, 则必须在预状态中有效。  如果大小是已知的 (以字节为`s`单位), 则按元素大小进行缩放。

- `_In_reads_or_z_(s)`

     指向数组的指针, 该数组以 null 值终止或具有已知的大小, 或者两者都具有已知的大小。 直到空终止符的元素, 或者`s` , 如果没有空终止符, 则必须在预状态中有效。  如果大小是已知的 (以字节为`s`单位), 则按元素大小进行缩放。  (用于`strn`系列。)

- `_Out_writes_(s)`

     `_Out_writes_bytes_(s)`

     一个指针, 指向将由`s`函数编写的元素数组 (resp)。  数组元素不必在预处理中有效, 并且在 post 状态中有效的元素数是未指定的。  如果参数类型上存在批注, 则它们将在 post 状态下应用。 例如，考虑下面的代码。

     `typedef _Null_terminated_ wchar_t *PWSTR; void MyStringCopy(_Out_writes_ (size) PWSTR p1,    _In_ size_t size,    _In_ PWSTR p2);`

     在此示例中, 调用方为`size` `p1`提供元素的缓冲区。  `MyStringCopy`使其中一些元素有效。 更重要的`_Null_terminated_` `p1`是, 上`PWSTR`的批注表示在 post 状态下以 null 结尾。  通过这种方式, 有效元素的数目仍是明确定义的, 但不需要特定元素计数。

     `_bytes_`变体提供的大小以字节为单位, 而不是元素。 仅在无法将大小表示为元素时使用此值。  例如, 仅`char`当使用`wchar_t`的类似`_bytes_`函数时, 字符串才使用变体。

- `_Out_writes_z_(s)`

     指向元素数组的`s`指针。  元素不必在预状态中有效。  在后期状态中, 通过空终止符向上传递的元素必须是有效的。  如果大小是已知的 (以字节为`s`单位), 则按元素大小进行缩放。

- `_Inout_updates_(s)`

     `_Inout_updates_bytes_(s)`

     指向数组的指针, 该数组在函数中进行读取和写入。  它的大小`s`是元素, 在预状态和后状态下有效。

     `_bytes_`变体提供的大小以字节为单位, 而不是元素。 仅在无法将大小表示为元素时使用此值。  例如, 仅`char`当使用`wchar_t`的类似`_bytes_`函数时, 字符串才使用变体。

- `_Inout_updates_z_(s)`

     指向数组的指针, 该数组以 null 值终止并具有已知大小。 通过 null 终止符向上 (必须存在) 的元素必须在前置状态和 post 状态中有效。  公告状态中的值假设不同于预处理状态中的值;这包括 null 结束符的位置。 如果大小是已知的 (以字节为`s`单位), 则按元素大小进行缩放。

- `_Out_writes_to_(s,c)`

     `_Out_writes_bytes_to_(s,c)`

     `_Out_writes_all_(s)`

     `_Out_writes_bytes_all_(s)`

     指向元素数组的`s`指针。  元素不必在预状态中有效。  在后期状态中, 最多`c`个元素的元素必须有效。  如果大小是已知的 (以字节为`s`单位`c` )、按比例调整大小, `_bytes_`或者使用变体 (定义为:

     `_Out_writes_to_(_Old_(s), _Old_(s))    _Out_writes_bytes_to_(_Old_(s), _Old_(s))`

     换言之, 缓冲区`s`中的每个位于预状态的元素都在 post 状态下有效。  例如：

     `void *memcpy(_Out_writes_bytes_all_(s) char *p1,    _In_reads_bytes_(s) char *p2,    _In_ int s); void * wordcpy(_Out_writes_all_(s) DWORD *p1,     _In_reads_(s) DWORD *p2,    _In_ int s);`

- `_Inout_updates_to_(s,c)`

     `_Inout_updates_bytes_to_(s,c)`

     指向数组的指针, 该数组由函数读取和写入。  它的大小`s`为元素, 所有元素都必须在预状态中有效, 并且`c`元素必须在 post 状态下有效。

     `_bytes_`变体提供的大小以字节为单位, 而不是元素。 仅在无法将大小表示为元素时使用此值。  例如, 仅`char`当使用`wchar_t`的类似`_bytes_`函数时, 字符串才使用变体。

- `_Inout_updates_z_(s)`

     指向数组的指针, 该数组以 null 值终止并具有已知大小。 通过 null 终止符向上 (必须存在) 的元素必须在前置状态和 post 状态中有效。  公告状态中的值假设不同于预处理状态中的值;这包括 null 结束符的位置。 如果大小是已知的 (以字节为`s`单位), 则按元素大小进行缩放。

- `_Out_writes_to_(s,c)`

     `_Out_writes_bytes_to_(s,c)`

     `_Out_writes_all_(s)`

     `_Out_writes_bytes_all_(s)`

     指向元素数组的`s`指针。  元素不必在预状态中有效。  在后期状态中, 最多`c`个元素的元素必须有效。  如果大小是已知的 (以字节为`s`单位`c` )、按比例调整大小, `_bytes_`或者使用变体 (定义为:

     `_Out_writes_to_(_Old_(s), _Old_(s))    _Out_writes_bytes_to_(_Old_(s), _Old_(s))`

     换言之, 缓冲区`s`中的每个位于预状态的元素都在 post 状态下有效。  例如:

     `void *memcpy(_Out_writes_bytes_all_(s) char *p1,    _In_reads_bytes_(s) char *p2,    _In_ int s); void * wordcpy(_Out_writes_all_(s) DWORD *p1,     _In_reads_(s) DWORD *p2,    _In_ int s);`

- `_Inout_updates_to_(s,c)`

     `_Inout_updates_bytes_to_(s,c)`

     指向数组的指针, 该数组由函数读取和写入。  它的大小`s`为元素, 所有元素都必须在预状态中有效, 并且`c`元素必须在 post 状态下有效。

     `_bytes_`变体提供的大小以字节为单位, 而不是元素。 仅在无法将大小表示为元素时使用此值。  例如, 仅`char`当使用`wchar_t`的类似`_bytes_`函数时, 字符串才使用变体。

- `_Inout_updates_all_(s)`

     `_Inout_updates_bytes_all_(s)`

     指向数组的指针, 该数组由大小`s`元素的函数进行读取和写入。 定义为等效于:

     `_Inout_updates_to_(_Old_(s), _Old_(s))    _Inout_updates_bytes_to_(_Old_(s), _Old_(s))`

     换句话说, 缓冲区`s`中的每个位于预状态的元素都在前置状态和 post 状态下有效。

     `_bytes_`变体提供的大小以字节为单位, 而不是元素。 仅在无法将大小表示为元素时使用此值。  例如, 仅`char`当使用`wchar_t`的类似`_bytes_`函数时, 字符串才使用变体。

- `_In_reads_to_ptr_(p)`

     指向数组的指针, 该数组的表达式`p`  -  `_Curr_` (即`p`减号`_Curr_`) 由相应的语言标准定义。  之前的元素`p`必须在预状态中有效。

- `_In_reads_to_ptr_z_(p)`

     指向以 null 结尾的数组的指针, 该数组的`p`表达式 -  `_Curr_` (即`p`减号`_Curr_`) 由相应的语言标准定义。  之前的元素`p`必须在预状态中有效。

- `_Out_writes_to_ptr_(p)`

     指向数组的指针, 该数组的表达式`p`  -  `_Curr_` (即`p`减号`_Curr_`) 由相应的语言标准定义。  之前`p`的元素不必处于预处理状态, 并且在 post 状态中必须有效。

- `_Out_writes_to_ptr_z_(p)`

     指向以 null 结尾的数组的指针, 该数组的`p`表达式 -  `_Curr_` (即`p`减号`_Curr_`) 由相应的语言标准定义。  之前`p`的元素不必处于预处理状态, 并且在 post 状态中必须有效。

## <a name="optional-pointer-parameters"></a>可选指针参数

当指针参数批注包含`_opt_`时, 它指示参数可以为 null。 否则, 批注的执行与不包含`_opt_`的版本相同。 下面列出`_opt_`了指针参数批注的变体:

||||
|-|-|-|
|`_In_opt_`<br /><br /> `_Out_opt_`<br /><br /> `_Inout_opt_`<br /><br /> `_In_opt_z_`<br /><br /> `_Inout_opt_z_`<br /><br /> `_In_reads_opt_`<br /><br /> `_In_reads_bytes_opt_`<br /><br /> `_In_reads_opt_z_`|`_Out_writes_opt_`<br /><br /> `_Out_writes_opt_z_`<br /><br /> `_Inout_updates_opt_`<br /><br /> `_Inout_updates_bytes_opt_`<br /><br /> `_Inout_updates_opt_z_`<br /><br /> `_Out_writes_to_opt_`<br /><br /> `_Out_writes_bytes_to_opt_`<br /><br /> `_Out_writes_all_opt_`<br /><br /> `_Out_writes_bytes_all_opt_`|`_Inout_updates_to_opt_`<br /><br /> `_Inout_updates_bytes_to_opt_`<br /><br /> `_Inout_updates_all_opt_`<br /><br /> `_Inout_updates_bytes_all_opt_`<br /><br /> `_In_reads_to_ptr_opt_`<br /><br /> `_In_reads_to_ptr_opt_z_`<br /><br /> `_Out_writes_to_ptr_opt_`<br /><br /> `_Out_writes_to_ptr_opt_z_`|

## <a name="output-pointer-parameters"></a>输出指针参数
输出指针参数需要特殊表示法, 以消除参数上的空值和指向的位置。

**批注和说明**

- `_Outptr_`

   参数不能为 null, 并且在 post 状态下, 指向位置不能为 null, 并且必须有效。

- `_Outptr_opt_`

   参数可以为 null, 但在 post 状态中, 所指向的位置不能为 null, 并且必须是有效的。

- `_Outptr_result_maybenull_`

   参数不能为 null, 并且在后置位置, 指向位置可以为 null。

- `_Outptr_opt_result_maybenull_`

   参数可以为 null, 并且在后置位置, 指向位置可以为 null。

  在下表中, 将在注释名称中插入附加子字符串, 以便进一步限定批注的含义。  各种子字符串分别`_z`为`_COM_` `_buffer_`、 `_bytebuffer_`、、和`_to_`。

> [!IMPORTANT]
> 如果要批注的接口是 COM, 请使用这些批注的 COM 形式。 不要将 COM 批注用于任何其他类型接口。

**批注和说明**

- `_Outptr_result_z_`

   `_Outptr_opt_result_z_`

   `_Outptr_result_maybenull_z_`

   `_Ouptr_opt_result_maybenull_z_`

   返回的指针具有`_Null_terminated_`批注。

- `_COM_Outptr_`

   `_COM_Outptr_opt_`

   `_COM_Outptr_result_maybenull_`

   `_COM_Outptr_opt_result_maybenull_`

   返回的指针具有 COM 语义, 因此会出现`_On_failure_`返回指针为 null 的后置条件。

- `_Outptr_result_buffer_(s)`

   `_Outptr_result_bytebuffer_(s)`

   `_Outptr_opt_result_buffer_(s)`

   `_Outptr_opt_result_bytebuffer_(s)`

   返回的指针指向大小`s`元素或字节的有效缓冲区。

- `_Outptr_result_buffer_to_(s, c)`

   `_Outptr_result_bytebuffer_to_(s, c)`

   `_Outptr_opt_result_buffer_to_(s,c)`

   `_Outptr_opt_result_bytebuffer_to_(s,c)`

   返回的指针指向大小`s`元素或字节的缓冲区, 其中第一个`c`是有效的。

  某些接口约定假定输出参数在失败时 null。  除显式 COM 代码外, 下表中的窗体是首选的。  对于 COM 代码, 请使用上一节中列出的相应 COM 窗体。

  **批注和说明**

- `_Result_nullonfailure_`

   修改其他批注。 如果函数失败, 则结果设置为 null。

- `_Result_zeroonfailure_`

   修改其他批注。 如果函数失败, 则结果设置为零。

- `_Outptr_result_nullonfailure_`

   如果函数成功, 则返回的指针指向有效的缓冲区; 如果函数失败, 则返回 null。 此批注适用于非可选参数。

- `_Outptr_opt_result_nullonfailure_`

   如果函数成功, 则返回的指针指向有效的缓冲区; 如果函数失败, 则返回 null。 此批注适用于可选参数。

- `_Outref_result_nullonfailure_`

   如果函数成功, 则返回的指针指向有效的缓冲区; 如果函数失败, 则返回 null。 此批注用于引用参数。

## <a name="output-reference-parameters"></a>输出引用参数

引用参数的常见用途是用于输出参数。  对于简单的输出引用参数 (例如) `int&`,`_Out_`提供正确的语义。  但是, 当输出值为指针时 (例如`int *&`, 类似`_Outptr_ int **`于不提供正确语义的等效指针批注)。  若要简洁地表达指针类型的输出引用参数的语义, 请使用这些复合批注:

**批注和说明**

- `_Outref_`

     结果在 post 状态中必须有效, 且不能为 null。

- `_Outref_result_maybenull_`

     结果必须在 post 状态中有效, 但在 post 状态中可能为 null。

- `_Outref_result_buffer_(s)`

     结果在 post 状态中必须有效, 且不能为 null。 指向大小`s`元素的有效缓冲区。

- `_Outref_result_bytebuffer_(s)`

     结果在 post 状态中必须有效, 且不能为 null。 指向大小`s`为字节的有效缓冲区。

- `_Outref_result_buffer_to_(s, c)`

     结果在 post 状态中必须有效, 且不能为 null。 指向`s`元素的缓冲区, 其中第一个`c`是有效的。

- `_Outref_result_bytebuffer_to_(s, c)`

     结果在 post 状态中必须有效, 且不能为 null。 指向第一个`c`有效`s`字节的缓冲区。

- `_Outref_result_buffer_all_(s)`

     结果在 post 状态中必须有效, 且不能为 null。 指向有效元素大小`s`的有效缓冲区。

- `_Outref_result_bytebuffer_all_(s)`

     结果在 post 状态中必须有效, 且不能为 null。 指向有效元素`s`字节的有效缓冲区。

- `_Outref_result_buffer_maybenull_(s)`

     结果必须在 post 状态中有效, 但在 post 状态中可能为 null。 指向大小`s`元素的有效缓冲区。

- `_Outref_result_bytebuffer_maybenull_(s)`

     结果必须在 post 状态中有效, 但在 post 状态中可能为 null。 指向大小`s`为字节的有效缓冲区。

- `_Outref_result_buffer_to_maybenull_(s, c)`

     结果必须在 post 状态中有效, 但在 post 状态中可能为 null。 指向`s`元素的缓冲区, 其中第一个`c`是有效的。

- `_Outref_result_bytebuffer_to_maybenull_(s,c)`

     结果必须在 post 状态中有效, 但在 post 状态下可能为 null。 指向第一个`c`有效`s`字节的缓冲区。

- `_Outref_result_buffer_all_maybenull_(s)`

     结果必须在 post 状态中有效, 但在 post 状态下可能为 null。 指向有效元素大小`s`的有效缓冲区。

- `_Outref_result_bytebuffer_all_maybenull_(s)`

     结果必须在 post 状态中有效, 但在 post 状态下可能为 null。 指向有效元素`s`字节的有效缓冲区。

## <a name="return-values"></a>返回值

函数的返回值与`_Out_`参数类似, 但在不同的取消引用级别, 无需考虑指向结果的指针的概念。  对于以下批注, 返回值为批注对象: 标量、指向结构的指针或指向缓冲区的指针。 这些批注具有与对应`_Out_`批注相同的语义。

|||
|-|-|
|`_Ret_z_`<br /><br /> `_Ret_writes_(s)`<br /><br /> `_Ret_writes_bytes_(s)`<br /><br /> `_Ret_writes_z_(s)`<br /><br /> `_Ret_writes_to_(s,c)`<br /><br /> `_Ret_writes_maybenull_(s)`<br /><br /> `_Ret_writes_to_maybenull_(s)`<br /><br /> `_Ret_writes_maybenull_z_(s)`|`_Ret_maybenull_`<br /><br /> `_Ret_maybenull_z_`<br /><br /> `_Ret_null_`<br /><br /> `_Ret_notnull_`<br /><br /> `_Ret_writes_bytes_to_`<br /><br /> `_Ret_writes_bytes_maybenull_`<br /><br /> `_Ret_writes_bytes_to_maybenull_`|

## <a name="format-string-parameters"></a>格式字符串参数

- `_Printf_format_string_`指示参数是要在`printf`表达式中使用的格式字符串。

     **示例**

    ```cpp
    int MyPrintF(_Printf_format_string_ const wchar_t* format, ...)
    {
           va_list args;
           va_start(args, format);
           int ret = vwprintf(format, args);
           va_end(args);
           return ret;
    }
    ```

- `_Scanf_format_string_`指示参数是要在`scanf`表达式中使用的格式字符串。

     **示例**

    ```cpp
    int MyScanF(_Scanf_format_string_ const wchar_t* format, ...)
    {
           va_list args;
           va_start(args, format);
           int ret = vwscanf(format, args);
           va_end(args);
           return ret;
    }
    ```

- `_Scanf_s_format_string_`指示参数是要在`scanf_s`表达式中使用的格式字符串。

     **示例**

    ```cpp
    int MyScanF_s(_Scanf_s_format_string_ const wchar_t* format, ...)
    {
           va_list args;
           va_start(args, format);
           int ret = vwscanf_s(format, args);
           va_end(args);
           return ret;
    }
    ```

## <a name="other-common-annotations"></a>其他常见批注

**批注和说明**

- `_In_range_(low, hi)`

     `_Out_range_(low, hi)`

     `_Ret_range_(low, hi)`

     `_Deref_in_range_(low, hi)`

     `_Deref_out_range_(low, hi)`

     `_Deref_inout_range_(low, hi)`

     `_Field_range_(low, hi)`

     参数、字段或结果的范围 (包含) 从`low`到到。 `hi`  等效于应用于批注对象的,以及相应的前置状态或后状态条件。`_Satisfies_(_Curr_ >= low && _Curr_ <= hi)`

    > [!IMPORTANT]
    > 尽管名称包含 "in" 和 "out", 但`_In_`和的语义并`_Out_`不适用于这些注释。

- `_Pre_equal_to_(expr)`

     `_Post_equal_to_(expr)`

     带批注的值是`expr`准确的。  等效于应用于批注对象的,以及相应的前置状态或后状态条件。`_Satisfies_(_Curr_ == expr)`

- `_Struct_size_bytes_(size)`

     适用于结构或类声明。  指示该类型的有效对象可能大于声明的类型, 以及给定`size`的字节数。  例如：

     `typedef _Struct_size_bytes_(nSize) struct MyStruct {    size_t nSize;    ... };`

     然后, 将类型`pM` `MyStruct *`为的参数的缓冲区大小 (以字节为单位) 为:

     `min(pM->nSize, sizeof(MyStruct))`

## <a name="related-resources"></a>相关资源

[代码分析团队博客](http://go.microsoft.com/fwlink/?LinkId=251197)

## <a name="see-also"></a>请参阅

- [使用 SAL 批注以减少 C/C++ 代码缺陷](../code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects.md)
- [了解 SAL](../code-quality/understanding-sal.md)
- [对函数行为进行批注](../code-quality/annotating-function-behavior.md)
- [批注结构和类](../code-quality/annotating-structs-and-classes.md)
- [对锁定行为进行批注](../code-quality/annotating-locking-behavior.md)
- [指定何时以及在何处应用批注](../code-quality/specifying-when-and-where-an-annotation-applies.md)
- [内部函数](../code-quality/intrinsic-functions.md)
- [最佳做法和示例](../code-quality/best-practices-and-examples-sal.md)