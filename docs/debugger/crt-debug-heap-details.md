---
title: CRT 调试堆详细信息 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debug heap, accessing
- heap functions
- _CRTDBG_CHECK_ALWAYS_DF macro
- _CrtMemDumpStatistics function
- debugging [C++], debug heap
- _CRT_BLOCK macro
- DBGINT.H file
- _CrtMemDumpAllObjectsSince function
- _crtBreakAlloc global variable
- _CrtMemState function
- _CLIENT_BLOCK macro
- _FREE_BLOCK block
- _CrtMemBlockHeader function
- heap state reporting functions
- _CRTDBG_ALLOC_MEM_DF macro
- _CrtSetBreakAlloc function
- memory blocks, allocation types on debug heap
- debugging [C++], CRT debug support
- debug heap, tracking heap allocation requests
- memory allocation, debug heap
- _NORMAL_BLOCK block
- crtBreakAlloc global variable
- _CrtDoForAllClientObjects function
- new operator, using debug heap from C++
- _CrtSetDumpClient function
- debugging [CRT], heap-related problems
- debug heap, solving memory allocation problems
- _CrtMemCheckpoint function
- debug builds, linking to debug heap
- _IGNORE_BLOCK block
- _crtDbgFlag function
- client blocks, specifying subtypes
- memory leaks, tracking
- _CrtSetDbgFlag function
- nBlockUse method
- memory leaks, CRT debug library functions
- _CRTDBG_DELAY_FREE_MEM_DF macro
- allocation request numbers
- _CRTDBG_LEAK_CHECK_DF macro
- debug heap
- memory, debugging
- _CrtReportBlockType function
- _CrtDumpMemoryLeaks function
- _CrtCheckMemory function
- debug heap, CRT
- memory blocks, free
- _BLOCK_TYPE macro
- debug heap, memory blocks
- heap allocation, debug
- debugging memory leaks
- _BLOCK_SUBTYPE macro
- debug heap, using from C++
- _CrtMemDifference function
- heap allocation, tracking requests
- debugging [Visual Studio], debug heap
- delete operator, using debug heap from C++
- blocks, types of on the debug heap
- _CRTDBG_CHECK_CRT_DF macro
- debug heap, reporting functions
ms.assetid: bf78ace6-28e4-4a04-97c6-39e0cdd00ba4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f55bd71b2174a03fb44b4512f04997e48d636d12
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62563751"
---
# <a name="crt-debug-heap-details"></a>CRT 调试堆详细信息
本主题详细描述了 CRT 调试堆。

## <a name="BKMK_Contents"></a> 内容
[利用调试堆查找缓冲区溢出](#BKMK_Find_buffer_overruns_with_debug_heap)

[调试堆中的块类型](#BKMK_Types_of_blocks_on_the_debug_heap)

[检查堆完整性和内存泄漏](#BKMK_Check_for_heap_integrity_and_memory_leaks)

[配置调试堆](#BKMK_Configure_the_debug_heap)

[C++ 调试堆中的 new、delete 和 _CLIENT_BLOCK](#BKMK_new__delete__and__CLIENT_BLOCKs_in_the_C___debug_heap)

[堆状态报告函数](#BKMK_Heap_State_Reporting_Functions)

[跟踪堆分配请求](#BKMK_Track_Heap_Allocation_Requests)

## <a name="BKMK_Find_buffer_overruns_with_debug_heap"></a> 利用调试堆查找缓冲区溢出
程序员遇到的两种最常见而又难处理的问题是，覆盖已分配缓冲区的末尾以及内存泄漏（未能在不再需要某些分配后将其释放）。 调试堆提供功能强大的工具来解决这类内存分配问题。

堆函数的“调试”版本调用“发布”版本中使用的标准版本或基版本。 请求内存块时，调试堆管理器从基堆分配略大于所请求的块的内存块，并返回指向该块中属于你的部分的指针。 例如，假定应用程序包含调用：`malloc( 10 )`。 在发布版本中，[malloc](/cpp/c-runtime-library/reference/malloc) 将调用基堆分配例程以请求分配 10 个字节。 但在调试版本中，`malloc`将调用 [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg)，它随后将调用基堆分配例程以请求分配 10 个字节加上大约 36 个字节的额外内存。 调试堆中产生的所有内存块在单个链接列表中连接起来，按照分配时间排序。

调试堆例程分配的附加内存的用途为：存储簿记信息，存储将调试内存块链接在一起的指针，以及形成数据两侧的小缓冲区（用于捕捉已分配区域的覆盖）。

当前，用于存储调试堆的簿记信息的块头结构在 DBGINT.H 头文件中声明如下：

```cpp
typedef struct _CrtMemBlockHeader
{
// Pointer to the block allocated just before this one:
    struct _CrtMemBlockHeader *pBlockHeaderNext;
// Pointer to the block allocated just after this one:
    struct _CrtMemBlockHeader *pBlockHeaderPrev;
    char *szFileName;    // File name
    int nLine;           // Line number
    size_t nDataSize;    // Size of user block
    int nBlockUse;       // Type of block
    long lRequest;       // Allocation number
// Buffer just before (lower than) the user's memory:
    unsigned char gap[nNoMansLandSize];
} _CrtMemBlockHeader;

/* In an actual memory block in the debug heap,
 * this structure is followed by:
 *   unsigned char data[nDataSize];
 *   unsigned char anotherGap[nNoMansLandSize];
 */
```

块的用户数据区两侧的 `NoMansLand` 缓冲区当前大小为 4 字节，并填充有调试堆例程用于验证用户内存块的限制是否未被覆盖的已知字节值。 调试堆还使用已知值填充新的内存块。 若选择将释放的块保留在堆的链接列表中（如下文所述），则这些释放的块也会填充一个已知的值。 当前，所用的实际字节值如下所示：

在应用程序使用的内存的任何一侧上的"NoMansLand"缓冲区当前 0xFD 填充 NoMansLand (0xFD)。

已释放的块 (0xDD) 已释放的块保留在调试堆中未使用的链接列表时`_CRTDBG_DELAY_FREE_MEM_DF`标志设置当前用 0xDD 填充。

这些对象用 0xcd 填充分配时填充新对象 (0xCD) 新对象。

![返回页首](../debugger/media/pcs_backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)

## <a name="BKMK_Types_of_blocks_on_the_debug_heap"></a> 调试堆中的块类型
调试堆中的每个内存块都被分配给五种分配类型之一。 出于泄漏检测和状态报告的目的，对这些类型进行了不同的跟踪和报告。 可以通过使用对调试堆分配函数之一（如 [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg)的直接调用来分配块，从而指定块的类型。 调试堆中五种类型的内存块（在 _ CrtMemBlockHeader 结构的 nBlockUse 成员中设置）如下：

**_NORMAL_BLOCK**调用[malloc](/cpp/c-runtime-library/reference/malloc)或[calloc](/cpp/c-runtime-library/reference/calloc)创建普通块。 如果只打算使用普通块，而不需要客户端块，则可能需要定义 [_CRTDBG_MAP_ALLOC](/cpp/c-runtime-library/crtdbg-map-alloc)，这将导致所有堆分配调用映射到其调试版本中的调试等效项。 这将允许将关于每个分配调用的文件名和行号信息存储到对应的块头中。

`_CRT_BLOCK` 许多运行时库函数在内部分配的内存块被标记为 CRT 块，这样就可以单独处理它们了。 结果，泄漏检测和其他操作不需要受这些块影响。 分配永不可以分配、重新分配或释放任何 CRT 类型的块。

`_CLIENT_BLOCK` 出于调试目的，应用程序可以专门跟踪一组给定的分配，具体方法是使用对调试堆函数的显式调用，将它们作为此类型的内存块进行分配。 例如，MFC 将所有 Cobject 分配为客户端块；其他应用程序可能会在客户端块中保留不同的内存对象。 还可以指定客户端块的子类型，使跟踪粒度更大。 若要指定客户端块的子类型，请将该数字向左移 16 位，并使用 `_CLIENT_BLOCK` 对其进行 `OR` 运算。 例如:

```cpp
#define MYSUBTYPE 4
freedbg(pbData, _CLIENT_BLOCK|(MYSUBTYPE<<16));
```

客户端提供的挂钩函数（用于转储在“客户端”块中存储的对象）可以使用 [_CrtSetDumpClient](/cpp/c-runtime-library/reference/crtsetdumpclient) 进行安装，然后，每当调试函数转储“客户端”块时均会调用该挂钩函数。 同样，对于调试堆中的每个“客户端”块，可以使用 [_CrtDoForAllClientObjects](/cpp/c-runtime-library/reference/crtdoforallclientobjects) 来调用应用程序提供的给定函数。

**_FREE_BLOCK**通常情况下，从列表中删除也将释放的块。 为了检查并未仍在向已释放的内存写入数据，或为了模拟内存不足情况，可以选择在链接列表上保留已释放块，将其标记为“可用”，并用已知字节值（当前为 0xDD）填充。

**_IGNORE_BLOCK**就可以关闭调试堆操作的一段时间。 在该时间段内，内存块保留在列表上，但被标记为“忽略”块。

若要确定给定块的类型和子类型，请使用 [_CrtReportBlockType](/cpp/c-runtime-library/reference/crtreportblocktype) 函数以及 _BLOCK_TYPE 和 _BLOCK_SUBTYPE 宏。 宏的定义（在 crtdbg.h 中）如下所示：

```cpp
#define _BLOCK_TYPE(block)          (block & 0xFFFF)
#define _BLOCK_SUBTYPE(block)       (block >> 16 & 0xFFFF)
```

![返回页首](../debugger/media/pcs_backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)

## <a name="BKMK_Check_for_heap_integrity_and_memory_leaks"></a> 检查堆完整性和内存泄漏
许多调试堆功能必须从代码内访问。 下一节描述其中一些功能以及如何使用这些功能。

`_CrtCheckMemory` 例如，可使用对 [_CrtCheckMemory](/cpp/c-runtime-library/reference/crtcheckmemory) 的调用来检查堆在任意点的完整性。 该函数检查堆中的每个内存块，验证内存块头信息有效，并确认尚未修改缓冲区。

`_CrtSetDbgFlag` 可控制调试堆如何使用内部标志 [_crtDbgFlag](/cpp/c-runtime-library/crtdbgflag) 跟踪分配，此标志可以使用 [_CrtSetDbgFlag](/cpp/c-runtime-library/reference/crtsetdbgflag) 函数进行读取和设置。 通过更改该标志，可以指示调试堆在程序退出时检查内存泄漏，并报告检测到的所有泄漏。 同样，可以指定释放的内存块不从链接列表中删除，从而模拟内存不足的情况。 检查堆时，会对这些释放的块进行整体检查，确保它们未受到干扰。

_crtDbgFlag 标志包含下列位域：

|位域|默认<br /><br /> 值|描述|
|---------------|-----------------------|-----------------|
|**_CRTDBG_ALLOC_MEM_DF**|On|打开调试分配。 当该位为 off 时，分配仍链接在一起，但它们的块类型为 _IGNORE_BLOCK。|
|**_CRTDBG_DELAY_FREE_MEM_DF**|Off|防止实际释放内存，与模拟内存不足情况相同。 当该位为 on 时，已释放块保留在调试堆的链接列表中，但标记为 _FREE_BLOCK，并用特殊字节值填充。|
|**_CRTDBG_CHECK_ALWAYS_DF**|Off|导致每次分配和释放时均调用 _CrtCheckMemory。 这将减慢执行，但可快速捕捉错误。|
|**_CRTDBG_CHECK_CRT_DF**|Off|导致将标记为 _CRT_BLOCK 类型的块包括在泄漏检测和状态差异操作中。 当该位为 off 时，在这些操作期间将忽略由运行库内部使用的内存。|
|**_CRTDBG_LEAK_CHECK_DF**|Off|导致在程序退出时通过调用 _CrtDumpMemoryLeaks 来执行泄漏检查。 如果应用程序未能释放其所分配的所有内存，将生成错误报告。|

![返回页首](../debugger/media/pcs_backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)

## <a name="BKMK_Configure_the_debug_heap"></a> 配置调试堆
对堆函数（例如 `malloc`、`free`、`calloc`、`realloc`、`new` 和 `delete`）的所有调用均解析为这些函数在调试堆中运行的调试版本。 释放内存块时，调试堆自动检查已分配区域两侧的缓冲区的完整性，并在发生覆盖时发出错误报告。

**使用调试堆**

- 用 C 运行库的调试版本链接应用程序的调试版本。

  更改一个或多个 _crtDbgFlag 位域并创建标志的新状态

1. 在 `_CrtSetDbgFlag` 参数设置为 `newFlag` 的情况下调用 `_CRTDBG_REPORT_FLAG`（以获取当前的 `_crtDbgFlag` 状态），并在一个临时变量中存储返回值。

2. 打开的任何位`OR`-ing (按位&#124;符号) 带相应位屏蔽 （在应用程序代码中由清单常量显示） 的临时变量。

3. 关闭其他位`AND`-ing (按位 & 符号) 与变量`NOT`(按位 ~ 符号) 的相应位屏蔽。

4. 在 `_CrtSetDbgFlag` 参数设置为临时变量中存储的值的情况下调用 `newFlag`，以创建 `_crtDbgFlag` 的新状态。

   例如，下列代码行打开自动泄漏检测，关闭检查 `_CRT_BLOCK` 类型的块：

```cpp
// Get current flag
int tmpFlag = _CrtSetDbgFlag( _CRTDBG_REPORT_FLAG );

// Turn on leak-checking bit.
tmpFlag |= _CRTDBG_LEAK_CHECK_DF;

// Turn off CRT block checking bit.
tmpFlag &= ~_CRTDBG_CHECK_CRT_DF;

// Set flag to the new value.
_CrtSetDbgFlag( tmpFlag );
```

![返回页首](../debugger/media/pcs_backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)

## <a name="BKMK_new__delete__and__CLIENT_BLOCKs_in_the_C___debug_heap"></a> C++ 调试堆中的 new、delete 和 _CLIENT_BLOCK
C 运行库的调试版本包含 C++ `new` 和 `delete` 运算符的调试版本。 如果使用 `_CLIENT_BLOCK` 分配类型，则必须直接调用 `new` 运算符的调试版本，或者创建可在调试模式中替换 `new` 运算符的宏，如下面的示例所示：

```cpp
/* MyDbgNew.h
 Defines global operator new to allocate from
 client blocks
*/

#ifdef _DEBUG
   #define DEBUG_CLIENTBLOCK   new( _CLIENT_BLOCK, __FILE__, __LINE__)
#else
   #define DEBUG_CLIENTBLOCK
#endif // _DEBUG

/* MyApp.cpp
        Use a default workspace for a Console Application to
 *      build a Debug version of this code
*/

#include "crtdbg.h"
#include "mydbgnew.h"

#ifdef _DEBUG
#define new DEBUG_CLIENTBLOCK
#endif

int main( )   {
    char *p1;
    p1 =  new char[40];
    _CrtMemDumpAllObjectsSince( NULL );
}
```

`delete` 运算符的“Debug”版本可用于所有块类型，并且编译“Release”版本时程序中不需要任何更改。

![返回页首](../debugger/media/pcs_backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)

## <a name="BKMK_Heap_State_Reporting_Functions"></a> 堆状态报告函数
 **_CrtMemState**

 若要捕获给定时刻堆状态的摘要快照，请使用 CRTDBG.H 中定义的 _CrtMemState 结构：

```cpp
typedef struct _CrtMemState
{
    // Pointer to the most recently allocated block:
    struct _CrtMemBlockHeader * pBlockHeader;
    // A counter for each of the 5 types of block:
    size_t lCounts[_MAX_BLOCKS];
    // Total bytes allocated in each block type:
    size_t lSizes[_MAX_BLOCKS];
    // The most bytes allocated at a time up to now:
    size_t lHighWaterCount;
    // The total bytes allocated at present:
    size_t lTotalCount;
} _CrtMemState;
```

此结构保存指向调试堆的链接列表中的第一个（最近分配的）块的指针。 然后，在两个数组中，它记录该列表中每种类型的内存块（_NORMAL_BLOCK、`_CLIENT_BLOCK`、_FREE_BLOCK 等）的数量，以及在每种类型的块中分配的字节数。 最后，它记录到那时为止在整个堆中分配的最高字节数，以及当前分配的字节数。

**其他 CRT 报告函数**

下列函数报告堆的状态和内容，并使用这些信息帮助检测内存泄漏及其他问题：

|函数|描述|
|--------------|-----------------|
|[_CrtMemCheckpoint](/cpp/c-runtime-library/reference/crtmemcheckpoint)|在应用程序提供的 _CrtMemState 结构中保存堆的快照。|
|[_CrtMemDifference](/cpp/c-runtime-library/reference/crtmemdifference)|比较两个内存状态结构，在第三个状态结构中保存二者之间的差异，如果两个状态不同，则返回 TRUE。|
|[_CrtMemDumpStatistics](/cpp/c-runtime-library/reference/crtmemdumpstatistics)|转储给定的 _CrtMemState 结构。 该结构可能包含给定时刻调试堆状态的快照或两个快照之间的差异。|
|[_CrtMemDumpAllObjectsSince](/cpp/c-runtime-library/reference/crtmemdumpallobjectssince)|转储有关在堆的给定快照之后，或是从执行开始时起，分配的所有对象的信息。 如果已使用 _CrtSetDumpClient 安装挂钩函数，则每次它转储 _CLIENT_BLOCK 块时，都会调用应用程序所提供的挂钩函数。|
|[_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks)|确定自程序开始执行以来是否发生过内存泄漏，如果发生过，则转储所有已分配对象。 如果已使用 _CrtSetDumpClient 安装挂钩函数，则每次 _CrtDumpMemoryLeaks 转储 _CLIENT_BLOCK 块时，都会调用应用程序所提供的挂钩函数。|

![返回页首](../debugger/media/pcs_backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)

## <a name="BKMK_Track_Heap_Allocation_Requests"></a> 跟踪堆分配请求
尽管查明在其中执行断言或报告宏的源文件名和行号对于定位问题原因常常很有用，对于堆分配函数却可能不是这样。 虽然可在应用程序的逻辑树中的许多适当点插入宏，但分配经常隐藏在特殊例程中，该例程会在很多不同时刻从很多不同位置进行调用。 问题通常并不在于如何确定哪行代码进行了错误分配，而在于如何确定该行代码进行的上千次分配中的哪一次是错误分配以及原因。

**唯一分配请求编号和 _crtBreakAlloc**

识别出错的特定堆分配调用的最简单方法是利用与调试堆中的每个块相关联的唯一分配请求编号。 当某个转储函数报告了有关某个块的信息时，此分配请求编号将括在大括号中（例如，“{36}”）。

知道了分配不当的块的分配请求编号后，就可以将该编号传递给 [_CrtSetBreakAlloc](/cpp/c-runtime-library/reference/crtsetbreakalloc) 以创建断点。 执行将在分配块之前中断，你可以回溯，确定哪个例程导致了错误调用。 若要避免重新编译，可在调试器中通过将 _crtBreakAlloc 设置为所得知的分配请求编号来完成同样的操作。

**创建分配例程的“Debug”版本**

比较复杂方法是创建自己的分配例程的调试版本，与[堆分配函数](../debugger/debug-versions-of-heap-allocation-functions.md)的 _dbg 版本相当。 然后，可将源文件和行号参数传递给基础堆分配例程，便可立即了解错误分配的出处。

例如，假定您的应用程序包含与下面类似的常用例程：

```cpp
int addNewRecord(struct RecStruct * prevRecord,
                 int recType, int recAccess)
{
    // ...code omitted through actual allocation...
    if ((newRec = malloc(recSize)) == NULL)
    // ... rest of routine omitted too ...
}
```

在头文件中，可以添加如下代码：

```cpp
#ifdef _DEBUG
#define  addNewRecord(p, t, a) \
            addNewRecord(p, t, a, __FILE__, __LINE__)
#endif
```

接下来，可以如下更改记录创建例程中的分配：

```cpp
int addNewRecord(struct RecStruct *prevRecord,
                int recType, int recAccess
#ifdef _DEBUG
               , const char *srcFile, int srcLine
#endif
    )
{
    /* ... code omitted through actual allocation ... */
    if ((newRec = _malloc_dbg(recSize, _NORMAL_BLOCK,
            srcFile, scrLine)) == NULL)
    /* ... rest of routine omitted too ... */
}
```

在其中调用 `addNewRecord` 的源文件名和行号将存储在产生的每个块中（这些块是在调试堆中分配的），并将在检查该块时进行报告。

![返回页首](../debugger/media/pcs_backtotop.png "PCS_BackToTop") [目录](#BKMK_Contents)

## <a name="see-also"></a>请参阅
[调试本机代码](../debugger/debugging-native-code.md)
