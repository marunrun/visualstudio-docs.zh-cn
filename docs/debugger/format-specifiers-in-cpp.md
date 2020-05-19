---
title: 调试器中的格式说明符 (C++) | Microsoft Docs
ms.date: 3/11/2019
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- C++
helpviewer_keywords:
- QuickWatch dialog box, format specifiers in C++
- variables [debugger], watch variable symbols
- symbols, watch variable formatting
- QuickWatch dialog box, using format specifiers
- expressions [C++], format specifiers
- specifiers, watch variable format
- specifiers
- Watch window, format specifiers in C++
- watch variable symbols
- format specifiers, debugger
- debugger, format specifiers recognized by
ms.assetid: 0f6f3b7c-ce2c-4b4d-b14f-7589dbed5444
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 8e6be79bc38e9283493bf5b7428a21c17cf9d3e0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896615"
---
# <a name="format-specifiers-for-c-in-the-visual-studio-debugger"></a>Visual Studio 调试器中的 C++ 格式说明符
你可以使用格式说明符更改在“监视”、“自动”和“局部变量”窗口中显示的值所用的格式。

还可在“即时”窗口、“命令”窗口、[跟踪点](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)甚至源窗口中使用格式说明符。 如果将鼠标悬停在这些窗口中的某个表达式上，结果将在[数据提示](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)中显示。 “数据提示”显示格式说明符。

> [!NOTE]
> 在 Visual Studio 本机调试器更改为新的调试引擎时，添加了一些新的格式说明符，并删除了一些旧的格式说明符。 当你使用 C++/CLI 进行互操作（混合本机和托管）调试时，仍使用较早的调试器。

## <a name="set-format-specifiers"></a>设置格式说明符
我们将使用以下示例代码：

```C++
int main() {
    int my_var1 = 0x0065;
    int my_var2 = 0x0066;
    int my_var3 = 0x0067;
}
```

调试期间，将 `my_var1` 变量添加到“监视”窗口，“调试” > “窗口” > “监视” > “监视 1”。 接下来，右键单击变量，然后选择“十六进制显示”。 现在，“监视”窗口显示值 0x0065。 若要查看以字符而不是整数形式表达的此值，请先右键单击并取消选择“十六进制显示”。 然后，在“名称”列的变量名称之后添加字符格式说明符“, c”。 现在，“值”列显示“101 'e'”。

![WatchFormatCPlus1](../debugger/media/watchformatcplus1.png "WatchFormatCPlus1")

::: moniker range=">= vs-2019" 
可以通过将逗号 (,) 追加到“监视”窗口中的值来查看可用格式说明符列表并从中进行选择。 

![WatchFormatSpecDropdown](../debugger/media/vs-2019/format-specs-cpp.png "FormatSpecCpp")

::: moniker-end

## <a name="format-specifiers"></a><a name="BKMK_Visual_Studio_2012_format_specifiers"></a>格式说明符
下表介绍可以在 Visual Studio 中使用的格式说明符。 仅新调试器支持加粗的说明符，但 C++/CLI 的互操作调试不支持。

::: moniker range=">= vs-2019" 

|说明符|格式|原始监视值|显示的值|
|---------------|------------|--------------------------|---------------------|
|d|十进制整数|0x00000066|102|
|o|无符号的八进制整数|0x00000066|000000000146|
|x<br /><br /> **h**|十六进制整数|102|0xcccccccc|
|X<br /><br /> **H**|十六进制整数|102|0xcccccccc|
|xb<br /><br /> **hb**|十六进制整数（没有前导 0x）|102|cccccccc|
|Xb<br /><br /> **Hb**|十六进制整数（没有前导 0x）|102|CCCCCCCC|
|b|无符号二进制整数|25|0b00000000000000000000000000011001|
|bb|无符号二进制整数（没有前导 0b）|25|00000000000000000000000000011001|
|e|科学记数法|25000000|2.500000e+07|
|g|科学记数或浮点（以较短者为准）|25000000|2.5e+07|
|c|单个字符|0x0065, c|101 'e'|
|s|const char* 字符串（加引号）|\<location> "hello world"|"hello world"|
|**sb**|const char * 字符串（无引号）|\<location> "hello world"|hello world|
|s8|UTF-8 字符串|\<location> "This is a UTF-8 coffee cup â˜•"|"This is a UTF-8 coffee cup ☕"|
|**s8b**|UTF-8 字符串（无引号）|\<location> "hello world"|hello world|
|su|Unicode（UTF-16 编码）字符串（加引号）|\<location> L"hello world"|L"hello world"<br /><br /> u"hello world"|
|sub|Unicode（UTF-16 编码）字符串（无引号）|\<location> L"hello world"|hello world|
|bstr|BSTR 二进制字符串（加引号）|\<location> L"hello world"|L"hello world"|
|env|环境块（双空终止字符串）|\<location> L"=::=::\\\\"|L"=::=::\\\\\\0=C:=C:\\\\windows\\\\system32\\0ALLUSERSPROFILE=...|
|**s32**|UTF-32 字符串（加引号）|\<location> U"hello world"|u"hello world"|
|**s32b**|UTF-32 string (no quotation marks)|\<location> U"hello world"|hello world|
|**en**|enum|Saturday(6)|星期六|
|**hv**|指针类型 - 指示被检查的指针值是数组的堆分配的结果，如 `new int[3]`。|\<location>{\<first member>}|\<location>{\<first member>, \<second member>, ...}|
|**na**|取消指向对象的指针的内存地址。|\<location>, {member=value...}|{member=value...}|
|**nd**|仅显示基类信息，忽略派生的类|`(Shape*) square` 包括基类和派生类信息|仅显示基类信息|
|hr|HRESULT 或 Win32 错误代码。 HRESULT 不再需要此说明符，因为调试器会自动对其进行解码。|S_OK|S_OK|
|wc|窗口类标志|0x0010|WC_DEFAULTCHAR|
|wm|Windows 消息数字|16|WM_CLOSE|
|nr|取消“原始视图”项|
|nvo|仅为数字值显示“原始视图”项|
|!|原始格式，忽略任何数据类型视图自定义项|\<customized representation>|4|

::: moniker-end

::: moniker range="vs-2017" 

|说明符|格式|原始监视值|显示的值|
|---------------|------------|--------------------------|---------------------|
|d|十进制整数|0x00000066|102|
|o|无符号的八进制整数|0x00000066|000000000146|
|x<br /><br /> **h**|十六进制整数|102|0xcccccccc|
|X<br /><br /> **H**|十六进制整数|102|0xcccccccc|
|c|单个字符|0x0065, c|101 'e'|
|s|const char* 字符串（加引号）|\<location> "hello world"|"hello world"|
|**sb**|const char * 字符串（无引号）|\<location> "hello world"|hello world|
|s8|UTF-8 字符串|\<location> "This is a UTF-8 coffee cup â˜•"|"This is a UTF-8 coffee cup ☕"|
|**s8b**|UTF-8 字符串（无引号）|\<location> "hello world"|hello world|
|su|Unicode（UTF-16 编码）字符串（加引号）|\<location> L"hello world"|L"hello world"<br /><br /> u"hello world"|
|sub|Unicode（UTF-16 编码）字符串（无引号）|\<location> L"hello world"|hello world|
|bstr|BSTR 二进制字符串（加引号）|\<location> L"hello world"|L"hello world"|
|env|环境块（双空终止字符串）|\<location> L"=::=::\\\\"|L"=::=::\\\\\\0=C:=C:\\\\windows\\\\system32\\0ALLUSERSPROFILE=...|
|**s32**|UTF-32 字符串（加引号）|\<location> U"hello world"|u"hello world"|
|**s32b**|UTF-32 string (no quotation marks)|\<location> U"hello world"|hello world|
|**en**|enum|Saturday(6)|星期六|
|**hv**|指针类型 - 指示被检查的指针值是数组的堆分配的结果，如 `new int[3]`。|\<location>{\<first member>}|\<location>{\<first member>, \<second member>, ...}|
|**na**|取消指向对象的指针的内存地址。|\<location>, {member=value...}|{member=value...}|
|**nd**|仅显示基类信息，忽略派生的类|`(Shape*) square` 包括基类和派生类信息|仅显示基类信息|
|hr|HRESULT 或 Win32 错误代码。 HRESULT 不再需要此说明符，因为调试器会自动对其进行解码。|S_OK|S_OK|
|wc|窗口类标志|0x0010|WC_DEFAULTCHAR|
|wm|Windows 消息数字|16|WM_CLOSE|
|!|原始格式，忽略任何数据类型视图自定义项|\<customized representation>|4|

::: moniker-end

> [!NOTE]
> 如果存在 hv 格式说明符，调试器会尝试确定缓冲区的长度并显示相应的元素数。 由于调试器并非总是可以查找确切的数组缓冲区大小，只要可能时，就应该使用大小说明符 `(pBuffer,[bufferSize])` 。 当缓冲区大小尚不可用时，hv 格式说明符很有用。

### <a name="size-specifiers-for-pointers-as-arrays"></a><a name="BKMK_Size_specifiers_for_pointers_as_arrays_in_Visual_Studio_2012"></a> 指针的大小说明符作为数组
如果有一个指针指向要看做数组形式的对象，则可以使用一个整数或表达式来指定数组中元素的数量。

|说明符|格式|原始监视值|显示的值|
|---------------|------------|---------------------------|---------------------|
|n|十进制或 **十六进制** 整数|pBuffer,[32]<br /><br /> pBuffer，“[0x20]”|将 `pBuffer` 显示为一个 32 元素的数组。|
|**[exp]**|计算结果为一个整数的有效的 C++ 表达式。|pBuffer,[bufferSize]|将 pBuffer 显示为 `bufferSize` 元素的一个数组。|
|**expand(n)**|计算结果为一个整数的有效的 C++ 表达式。|pBuffer, expand(2)|显示  `pBuffer`的第三个元素|

## <a name="format-specifiers-for-interop-debugging-with-ccli"></a><a name="BKMK_Format_specifiers_for_interop_debugging_and_C___edit_and_continue"></a> 使用 C++/CLI 的互操作调试的格式说明符
**粗体** 的说明符仅支持本地调试和 C++/CLI 代码。

|说明符|格式|原始监视值|显示的值|
|---------------|------------|--------------------------|---------------------|
|**d**<br /><br />**i**|有符号的十进制整数|0xF000F065|-268373915|
|**u**|无符号的十进制整数|0x0065|101|
|o|无符号的八进制整数|0xF065|0170145|
|x<br /><br />X|十六进制整数|61541|0x0000f065|
|**l**<br /><br />**h**|用于 d、i、u、o、x、X 的 long 或 short 前缀|00406042|0x0c22|
|**f**|带符号的浮点|(3./2.), f|1.500000|
|**e**|有符号的科学计数法|(3.0/2.0)|1.500000e+000|
|**g**|带符号的浮点或有符号的科学计数法，<br/> 取其中较短者|(3.0/2.0)|1.5|
|c|单个字符|\<location>|101 'e'|
|s|const char*（加引号）|\<location>|"hello world"|
|su|const wchar_t*<br /><br /> const char16_t\*（加引号）|\<location>|L"hello world"|
|sub|const wchar_t*<br /><br /> const char16_t\*|\<location>|hello world|
|s8|const char*（加引号）|\<location>|"hello world"|
|hr|HRESULT 或 Win32 错误代码。<br/>HRESULT 不再需要此说明符，因为调试器会自动对其进行解码。|S_OK|S_OK|
|wc|窗口类标志|0x00000040,|WC_DEFAULTCHAR|
|wm|Windows 消息数字|0x0010|WM_CLOSE|
|!|原始格式，忽略任何数据类型视图自定义项|\<customized representation>|4|

### <a name="format-specifiers-for-memory-locations-in-interop-debugging-with-ccli"></a><a name="BKMK_Format_specifiers_memory_locations_in_interop_debugging_and_C___edit_and_continue"></a>C++/CLI 互操作调试中的内存位置格式说明符
下表介绍用于内存位置的格式化符号。 可以使用带有计算为位置的任何值或表达式的内存位置说明符。

|符号|格式|原始监视值|显示的值|
|------------|------------|--------------------------|---------------------|
|**ma**|64 个 ASCII 字符|0x0012ffac|0x0012ffac .4...0...".0W&.......1W&.0.:W..1...."..1.JO&.1.2.."..1...0y....1|
|**m**|以十六进制表示的 16 个字节，后跟 16 个 ASCII 字符|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|
|**mb**|以十六进制表示的 16 个字节，后跟 16 个 ASCII 字符|0x0012ffac|0x0012ffac B3 34 CB 00 84 30 94 80 FF 22 8A 30 57 26 00 00 .4...0...".0W&amp;.|
|**mw**|8 个字|0x0012ffac|0x0012ffac 34B3 00CB 3084 8094 22FF 308A 2657 0000|
|**md**|4 个双字|0x0012ffac|0x0012ffac 00CB34B3 80943084 308A22FF 00002657|
|**mq**|2 个双字|0x0012ffac|0x0012ffac 7ffdf00000000000 5f441a790012fdd4|
|**mu**|双字节字符 (Unicode)|0x0012ffac|0x0012ffac 8478 77f4 ffff ffff 0000 0000 0000 0000|

### <a name="size-specifier-for-pointers-as-arrays-in-interop-debugging-with-ccli"></a><a name="BKMK_Size_specifier_for_pointers_as_arrays_in_interop_debugging_and_C___edit_and_continue"></a> 指针的大小说明符，并且指针在使用 C++/CLI 进行的互操作调试中作为数组存在
如果有一个指针指向要看做数组形式的对象，则可以使用一个整数来指定数组中元素的数量。

|说明符|格式|表达式|显示的值|
|---------------|------------|----------------|---------------------|
|n|十进制整数|pBuffer[32]|将 `pBuffer` 显示为 32 个元素的数组。|