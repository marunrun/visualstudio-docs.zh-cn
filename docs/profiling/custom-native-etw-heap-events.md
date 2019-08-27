---
title: 自定义本机 ETW 堆事件 | Microsoft Docs
ms.date: 02/24/2017
ms.topic: conceptual
ms.assetid: 668a6603-5082-4c78-98e6-f3dc871aa55b
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- C++
ms.workload:
- cplusplus
ms.openlocfilehash: 1bb6f906cbfb715d67f6e10ddcecf094bc25821f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62552929"
---
# <a name="custom-native-etw-heap-events"></a>自定义本机 ETW 堆事件

Visual Studio 包含本机内存探查器等各种[分析和诊断工具](../profiling/profiling-feature-tour.md)。  此探查器与堆提供程序中的 [ETW 事件](/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)挂钩，并分析如何分配和使用内存。  默认情况下，此工具仅可以分析从标准的 Windows 堆进行的分配，不会显示此本机堆以外的任何分配。

在很多情况下，你可能想要用自己的自定义堆，并避免标准堆的分配开销。  例如，可以使用 [VirtualAlloc](/windows/desktop/api/memoryapi/nf-memoryapi-virtualalloc) 在应用或游戏的开头分配大量内存，然后管理该列表中属于自己的块。  在此方案中，内存探查器工具只会看到初始分配，并且看不到在内存块内执行的自定义管理。  但是，通过使用自定义本机堆 ETW 提供程序，可让工具了解你在标准堆外进行的分配。

例如，在类似下面的项目中（其中 `MemoryPool` 为自定义堆），你将只能在 Windows 堆上看到一个分配：

```cpp
class Foo
{
public:
    int x, y;
};

...

// MemoryPool is a custom managed heap, which allocates 8192 bytes
// on the standard Windows Heap named "Windows NT"
MemoryPool<Foo, 8192> mPool;

// the "allocate" method requests memory from the pool created above
// and is cast to an object of type Foo, shown above
Foo* pFoo1 = (Foo*)mPool.allocate();
Foo* pFoo2 = (Foo*)mPool.allocate();
Foo* pFoo3 = (Foo*)mPool.allocate();
```

在不含自定义堆跟踪的[内存使用情况](../profiling/memory-usage.md)工具的快照中，仅显示一个 8192 字节分配，池未进行任何自定义分配：

![Windows 堆分配](media/heap-example-windows-heap.png)

通过执行以下步骤，我们可以使用同一工具跟踪自定义堆中的内存使用情况。

## <a name="how-to-use"></a>使用方法

可以在 C 和 C++ 中轻松使用此库。

1. 包括自定义堆 ETW 提供程序的标头：

   ```cpp
   #include <VSCustomNativeHeapEtwProvider.h>
   ```

1. 将 `__declspec(allocator)` 装饰器添加到自定义堆管理器的任何函数中，该函数向新分配的堆内存返回指针。  使用此装饰器可正确标识将返回的内存类型。  例如:

   ```cpp
   __declspec(allocator) void *MyMalloc(size_t size);
   ```

   > [!NOTE]
   > 此修饰器将告知编译器该函数是对某分配器的调用。  每次调用函数都将输出调用点的地址、调用指令的大小和新的 `S_HEAPALLOCSITE` 符号的新对象的 typeId。  分配调用堆栈后，Windows 会发出具有此信息的 ETW 事件。  内存探查器工具浏览调用堆栈以查找匹配 `S_HEAPALLOCSITE` 符号的返回地址，并且符号中的 typeId 信息用于显示分配的运行时类型。
   >
   > 简言之，这表示类似 `(B*)(A*)MyMalloc(sizeof(B))` 的调用将显示在该工具中，且类型为 `B`，而不是 `void`，也不是 `A`。

1. 对于 C++，创建 `VSHeapTracker::CHeapTracker` 对象，提供堆名称，这将显示在分析工具中：

   ```cpp
   auto pHeapTracker = std::make_unique<VSHeapTracker::CHeapTracker>("MyCustomHeap");
   ```

   如果使用 C，请改用 `OpenHeapTracker` 函数。  调用其他跟踪函数时，此函数将返回你将使用的句柄：

   ```C
   VSHeapTrackerHandle hHeapTracker = OpenHeapTracker("MyHeap");
   ```

1. 使用自定义函数分配内存时，调用 `AllocateEvent` (C++) 或 `VSHeapTrackerAllocateEvent` (C) 方法，传入指向内存及其大小的指针，以跟踪分配：

   ```cpp
   pHeapTracker->AllocateEvent(memPtr, size);
   ```

   or

   ```C
   VSHeapTrackerAllocateEvent(hHeapTracker, memPtr, size);
   ```

   > [!IMPORTANT]
   > 别忘了使用前面所述的 `__declspec(allocator)` 修饰器标记自定义分配器函数。

1. 使用自定义函数释放内存时，调用 `DeallocateEvent` (C++) 或 `VSHeapTracerDeallocateEvent` (C) 函数，传入指向内存的指针，以跟踪释放：

   ```cpp
   pHeapTracker->DeallocateEvent(memPtr);
   ```

   或：

   ```C
   VSHeapTrackerDeallocateEvent(hHeapTracker, memPtr);
   ```

1. 使用自定义函数重新分配内存时，调用 `ReallocateEvent` (C++) 或 `VSHeapReallocateEvent` (C) 方法，传入指向新内存、分配大小的指针以及指向旧内存的指针：

   ```cpp
   pHeapTracker->ReallocateEvent(memPtrNew, size, memPtrOld);
   ```

   或：

   ```C
   VSHeapTrackerReallocateEvent(hHeapTracker, memPtrNew, size, memPtrOld);
   ```

1. 最后，若要关闭并清除 C++ 中的自定义堆跟踪器，请通过手动或通过标准作用域规则或 C 中的 `CloseHeapTracker` 函数使用 `CHeapTracker` 析构函数：

   ```cpp
   delete pHeapTracker;
   ```

   或：

   ```C
   CloseHeapTracker(hHeapTracker);
   ```

## <a name="track-memory-usage"></a>跟踪内存使用情况
随着这些调用就位，现可使用 Visual Studio 中的标准**内存使用量**工具跟踪自定义堆使用情况。  有关如何使用此工具的详细信息，请参阅[内存使用量](../profiling/memory-usage.md)文档。 确保已通过快照启用堆分析，否则你的自定义堆使用情况将不会显示。

![启用堆分析](media/heap-enable-heap.png)

若要查看自定义堆跟踪，请使用位于“快照”窗口右上角的“堆”下拉菜单，将视图从“NT 堆” 更改为之前已命名的自己的堆。

![堆选择](media/heap-example-custom-heap.png)

通过上面的代码示例，当 `MemoryPool` 创建 `VSHeapTracker::CHeapTracker` 对象，并且我们自己的 `allocate` 方法在调用 `AllocateEvent` 方法时，你可以查看该自定义分配的结果，结果显示三个实例，合计 24 个字节，均为类型 `Foo`。

默认的 NT 堆看起来与前面的相同，同时添加了 `CHeapTracker` 对象。

![带跟踪器的 NT 堆](media/heap-example-windows-heap.png)

如[内存使用量](../profiling/memory-usage.md)文档中所述，与标准的 Windows 堆一样，你还可使用此工具比较快照，并查找自定义堆中的泄漏和损坏。

> [!TIP]
> Visual Studio 在性能分析工具集中还包含内存使用情况工具，可在“调试” > “性能探查器”菜单选项或通过 Alt+F2 组合键启用该工具。  此功能不包含堆跟踪，并且不会按如下所述显示你的自定义堆。  只有“诊断工具”窗口包含此功能，可通过选择“调试” > “Windows” > “显示诊断工具”菜单或 Ctrl+Alt+F2 组合键来启用此窗口。

## <a name="see-also"></a>请参阅
[首先了解分析工具](../profiling/profiling-feature-tour.md)
[内存使用情况](../profiling/memory-usage.md)
