---
title: 使用 CRT 库查找内存泄漏  |Microsoft Docs
ms.date: 10/04/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- breakpoints, on memory allocation
- _CrtMemState
- _CrtMemCheckpoint
- memory leaks
- _CrtMemDifference
- memory leaks, detecting and isolating
- _CrtDumpMemoryLeaks
- _CrtSetBreakAlloc
- _crtBreakAlloc
- _CrtSetReportMode
- memory, debugging
- _CrtMemDumpStatistics
- debugging memory leaks
- _CRTDBG_MAP_ALLOC
- _CrtSetDbgFlag
ms.assetid: cf6dc7a6-cd12-4283-b1b6-ea53915f7ed1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e7fdfedbb2f632bdb0fcaa05c7f0fb282a8fcd2b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62849967"
---
# <a name="find-memory-leaks-with-the-crt-library"></a>使用 CRT 库查找内存泄漏

内存泄漏是 C/C++ 应用程序中最微妙、最难以发现的 bug 。 内存泄漏是由于之前分配的内存未能正确解除分配而导致的。 最开始的少量内存泄漏可能没被发现，但随时间推移，会导致各种问题，从性能变差到程序由于内存不足而崩溃。 内存泄漏的应用会耗尽全部可用内存，导致其它程序崩溃，从而让人难以分辨是哪个程序引发问题。 即使无害的内存泄漏也可能表明存在其他应纠正的问题。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]调试器和 C 运行时库 (CRT) 可以帮助你检测和识别内存泄漏。

## <a name="enable-memory-leak-detection"></a>启用内存泄漏检测

检测内存泄漏的主要工具是 C/C++ 调试器和 C 运行时库 (CRT) 调试堆函数。

若要启用调试堆的所有函数，在 C++ 程序中，按以下顺序包含以下语句：

```cpp
#define _CRTDBG_MAP_ALLOC
#include <stdlib.h>
#include <crtdbg.h>
```

`#define` 语句将 CRT 堆函数的基础版本映射到对应的调试版本。 如果您忽略`#define`语句，为内存泄漏转储[不够详尽](#interpret-the-memory-leak-report)。

包括 *crtdbg.h* 将映射到 `malloc`和`free` 函数的调试版本 [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg) 和 [_free_dbg](/cpp/c-runtime-library/reference/free-dbg)，它们分别跟踪内存分配和解除分配。 此映射只在包含 `_DEBUG`的调试版本中发生。 发布版本使用普通的 `malloc` 和 `free` 函数。

使用上面的语句启用调试堆函数后，在应用出口点之前放置 [_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks) 以在应用退出时显示内存泄漏报告。

```cpp
_CrtDumpMemoryLeaks();
```

如果你的应用程序有多个出口点，无需在每个出口点手动设置`_CrtDumpMemoryLeaks`。 若要自动在每个退出点调用 `_CrtDumpMemoryLeaks` ，使用此处所示的位字段在应用程序开头调用 `_CrtSetDbgFlag` ：

```cpp
_CrtSetDbgFlag ( _CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF );
```

默认情况下，`_CrtDumpMemoryLeaks` 将内存泄漏报告输出到输出窗口的调试窗格中。 如果使用库，该库可能会将输出重置到另一位置。 

可以使用 `_CrtSetReportMode` 将报告重定向到其他位置，或返回到 **输出** 窗口，如下所示：

```cpp
_CrtSetReportMode( _CRT_ERROR, _CRTDBG_MODE_DEBUG );
```

## <a name="interpret-the-memory-leak-report"></a>解释内存泄漏报告

如果应用没有定义 `_CRTDBG_MAP_ALLOC` ， [_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks)显示如下所示的内存泄漏报告：

```cmd
Detected memory leaks!
Dumping objects ->
{18} normal block at 0x00780E80, 64 bytes long.
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD
Object dump complete.
```

如果您的应用程序定义`_CRTDBG_MAP_ALLOC`，内存泄漏报告如下所示：

```cmd
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\leaktest\leaktest.cpp(20) : {18}
normal block at 0x00780E80, 64 bytes long.
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD
Object dump complete.
```

第二个报告显示首次分配泄漏的内存的文件名和行号。

该值指示是否定义`_CRTDBG_MAP_ALLOC`，内存泄漏报告将显示：

- 内存分配编号，在示例中为 `18`
- 块类型，在示例中为 `normal` 。
- 十六进制内存位置，在示例中为 `0x00780E80`。
- 块的大小，在示例中为 `64 bytes`。
- 块中前 16 个字节的数据（十六进制形式）。

内存块的类型包括”普通”、”客户端”或 *CRT*。 “普通块”是由程序分配的普通内存。 “客户端块”是由 MFC 程序针对需要析构函数的对象而使用的特殊类型内存块。 MFC `new` 运算符根据正在创建的对象创建普通块或客户端块。

“CRT 块”是由 CRT 库为自己使用而分配的内存块。  CRT 库处理这些块的解除分配，因此 CRT 块不会显示在内存泄漏报告中，除非 CRT 库存在严重问题。

另外两种类型的内存块绝不会出现在内存泄漏报告中。 *释放的块*是已经释放的内存块，从定义上说不是泄漏的内存。 *忽略的块*是已明确标记要从内存泄漏报告中排除的内存。

以前的技术使用标准 CRT`malloc`函数确定存在内存泄漏的内存分配。 但是，如果你的程序使用 c + +`new`运算符分配内存，可能只能在内存泄漏报告中看到`operator new`调用`_malloc_dbg`的文件名和行号。 若要创建更有用的内存泄漏报告，可以编写如下所示来报告进行分配的行的宏：

```cpp
#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif
```

现在可以在代码中使用`DBG_NEW`宏来替换`new`运算符。 在调试版本中，`DBG_NEW`使用全局重载`operator new`，它采用块类型、文件和行号的附加参数。 重载`new` 调用 `_malloc_dbg` 以记录额外信息。 内存泄漏报告显示分配了泄漏对象的文件名和行号。 发行版本仍然使用默认的`new`。 下面是该技巧的示例：

```cpp
// debug_new.cpp
// compile by using: cl /EHsc /W4 /D_DEBUG /MDd debug_new.cpp
#define _CRTDBG_MAP_ALLOC
#include <cstdlib>
#include <crtdbg.h>

#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif

struct Pod {
    int x;
};

void main() {
    Pod* pPod = DBG_NEW Pod;
    pPod = DBG_NEW Pod; // Oops, leaked the original pPod!
    delete pPod;

    _CrtDumpMemoryLeaks();
}
```

在 Visual Studio 调试器中运行此代码时，调用 `_CrtDumpMemoryLeaks` 之后，**输出**窗口中生成的报告类似于如下所示：

```Output
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\debug_new\debug_new.cpp(20) : {75}
 normal block at 0x0098B8C8, 4 bytes long.
 Data: <    > CD CD CD CD
Object dump complete.
```

此输出报告，泄露的分配位于 *debug_new.cpp* 的第 20 行。

>[!NOTE]
>我们不建议创建名为`new`或任何其他语言关键字的预处理器宏。

## <a name="set-breakpoints-on-a-memory-allocation-number"></a>内存分配编号上设置断点

分配了泄漏内存块时，内存分配编号会提示你。 例如，分配编号为 18 的块内存是应用程序运行期间分配的第 18 块内存。 CRT 报告统计运行期间所有的内存块分配情况，其中包括 CRT 库库和 MFC 等其他库的分配。 因此，分配块编号是 18 的内存可能不是代码分配的第 18 个内存块。

可以使用分配编号在内存分配位置设置断点。

**使用“监视”窗口设置内存分配断点：**

1. 在应用程序的起点附近设置断点并开始调试。

1. 当应用程序在断点处暂停时，选择 **调试** > **窗口** > **监视 1**（或**监视 2**、**监视 3**、**监视 4**）打开 **监视** 窗口。

1. 在**监视**窗口的**名称** 列中键入`_crtBreakAlloc`。

   如果你使用的是 CRT 库的多线程 DLL 版本（/MD 选项），添加上下文运算符： `{,,ucrtbased.dll}_crtBreakAlloc`

1. 按 **Enter**。

   调试器将计算调用，并将结果放入”值”列。 如果你尚未在内存分配上设置任何断点，此值将为 **-1** 。

1. 在**值**列中，将该值替换为调试程序要中断处的内存分配的分配编号。

内存分配编号上设置断点后，继续调试。 请确保在相同条件下运行，这样内存分配编号就不会更改。 当应用程序在指定的内存分配处中断时，使用**调用堆栈**窗口和其他调试器窗口来确定分配内存时的情况。 然后，可以继续执行程序以观察对象会发生什么情况，并确定为什么它不正确释放。

在对象上设置数据断点可能也有帮助。 有关详细信息，请参阅[使用断点](../debugger/using-breakpoints.md)。

你也可以在代码中设置内存分配断点。 可以这样设置：

```cpp
_crtBreakAlloc = 18;
```

 或：

```cpp
_CrtSetBreakAlloc(18);
```

## <a name="compare-memory-states"></a>比较内存状态
 另一种找出内存泄漏的技术是在关键位置对应用程序的内存状态创建快照。 若要在应用程序的给定位置创建内存状态的快照，创建 `_CrtMemState` 结构并将其传递给`_CrtMemCheckpoint` 函数。

```cpp
_CrtMemState s1;
_CrtMemCheckpoint( &s1 );
```

`_CrtMemCheckpoint`函数用当前内存状态的快照填充该结构。

若要输出`_CrtMemState`结构的内容，请将该结构传递给`_ CrtMemDumpStatistics`函数：

```cpp
_CrtMemDumpStatistics( &s1 );
```

`_ CrtMemDumpStatistics` 输出内存状态转储，如下所示：

```cmd
0 bytes in 0 Free Blocks.
0 bytes in 0 Normal Blocks.
3071 bytes in 16 CRT Blocks.
0 bytes in 0 Ignore Blocks.
0 bytes in 0 Client Blocks.
Largest number used: 3071 bytes.
Total allocations: 3764 bytes.
```

若要确定代码的某个部分是否发生了内存泄漏，可以对这部分之前和之后的内存状态创建快照，然后使用 `_ CrtMemDifference` 比较两个状态：

```cpp
_CrtMemCheckpoint( &s1 );
// memory allocations take place here
_CrtMemCheckpoint( &s2 );

if ( _CrtMemDifference( &s3, &s1, &s2) )
   _CrtMemDumpStatistics( &s3 );
```

`_CrtMemDifference` 比较内存状态`s1`和`s2`，并在 (`s3`) 中返回结果，它是 `s1` 与 `s2` 之间的差异。

查找内存泄漏的一项技术是首先在你的应用程序开头和结尾放置 `_CrtMemCheckpoint`，然后使用`_CrtMemDifference` 比较结果。 如果`_CrtMemDifference` 显示内存已泄漏，可以添加更多`_CrtMemCheckpoint`调用使用二进制搜索来划分程序，直到你找到泄漏源。

## <a name="false-positives"></a>误报
 如果一个库将内部分配的内存块标记为普通块而不是 CRT 块或客户端块，则 `_CrtDumpMemoryLeaks` 会给出错误的内存泄漏指示。 在这种情况下， `_CrtDumpMemoryLeaks` 无法区分用户和内部库分配的内存块。 如果库分配的全局析构函数在你调用`_CrtDumpMemoryLeaks`之后运行，则每个内部库分配都会报告为内存泄漏。 版本早于 Visual Studio.NET 的标准模板库可能导致 `_CrtDumpMemoryLeaks` 误报。

## <a name="see-also"></a>请参阅
- [CRT 调试堆详细信息](../debugger/crt-debug-heap-details.md)
- [调试器安全](../debugger/debugger-security.md)
- [调试本机代码](../debugger/debugging-native-code.md)
