---
title: 如何：在本机代码中设置线程名称 |Microsoft Docs
ms.date: 12/17/2018
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- debugging [C++], threads
- SetThreadName function
- threading [Visual Studio], names
- thread names
- debugging [Visual Studio], threads
ms.assetid: c85d0968-9f22-4d69-87f4-acca2ae777b8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: d37a028fb5af099484d81374e52cfd12af727f94
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62847533"
---
# <a name="how-to-set-a-thread-name-in-native-code"></a>如何：在本机代码中设置线程名称
在 Visual Studio 的任何版本中都可以使用线程命名功能。 线程命名功能可用于标识的感兴趣的线程**线程**窗口调试正在运行的进程时。 具有 recognizably 名为线程也会有所帮助时执行事后调试通过崩溃转储检查和分析性能捕获使用各种工具。

## <a name="ways-to-set-a-thread-name"></a>如何设置线程名称

有两种方法来设置线程名称。 第一种是通过[SetThreadDescription](https://docs.microsoft.com/windows/desktop/api/processthreadsapi/nf-processthreadsapi-setthreaddescription)函数。 第二个是通过 Visual Studio 调试器附加到进程时引发特定异常。 每种方法都有优点和需要注意的问题。

值得注意的是_同时_方法可以一起使用，如果需要，因为它们的工作所依据的机制是相互独立。

### <a name="set-a-thread-name-by-using-setthreaddescription"></a>通过设置线程名称 `SetThreadDescription`

优点：
* 在 Visual Studio 中，而不考虑在调试器已附加到进程调用 SetThreadDescription 时进行调试时，线程名称是可见的。
* 执行事后通过加载 Visual Studio 中的故障转储调试时，线程名称是可见的。
* 线程名称也是可见时使用其他工具，如[WinDbg](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)调试器并[Windows Performance Analyzer](https://docs.microsoft.com/windows-hardware/test/wpt/windows-performance-analyzer)性能分析器。

注意：
* 线程名称将仅显示在 Visual Studio 2017 版本 15.6 及更高版本。
* 事后调试崩溃转储文件，线程名称时，仅在 Windows 10 版本 1607年中，Windows Server 2016 或更高版本的 Windows 上创建在崩溃时可见。

*示例：*

```C++
#include <windows.h>
#include <processthreadsapi.h>

int main()
{
    HRESULT r;
    r = SetThreadDescription(
        GetCurrentThread(),
        L"ThisIsMyThreadName!"
    );

    return 0;
}
```

### <a name="set-a-thread-name-by-throwing-an-exception"></a>通过引发异常来设置线程名称

若要在程序中设置线程名称的另一种方法是通过引发专门配置异常到 Visual Studio 调试器通信所需的线程名称。

优点：
* 所有版本的 Visual Studio 中的工作原理。

注意：
* 仅适用于将调试器附加于的基于异常的方法的时间。
* 使用此方法设置线程名称在转储或性能分析工具中将不可用。

*示例：*

`SetThreadName`函数如下所示演示此基于异常的方法。 请注意，线程名称将自动复制到线程，以便为内存`threadName`参数可以释放后`SetThreadName`调用完成。

```C++
//
// Usage: SetThreadName ((DWORD)-1, "MainThread");
//
#include <windows.h>
const DWORD MS_VC_EXCEPTION = 0x406D1388;
#pragma pack(push,8)
typedef struct tagTHREADNAME_INFO
{
    DWORD dwType; // Must be 0x1000.
    LPCSTR szName; // Pointer to name (in user addr space).
    DWORD dwThreadID; // Thread ID (-1=caller thread).
    DWORD dwFlags; // Reserved for future use, must be zero.
} THREADNAME_INFO;
#pragma pack(pop)
void SetThreadName(DWORD dwThreadID, const char* threadName) {
    THREADNAME_INFO info;
    info.dwType = 0x1000;
    info.szName = threadName;
    info.dwThreadID = dwThreadID;
    info.dwFlags = 0;
#pragma warning(push)
#pragma warning(disable: 6320 6322)
    __try{
        RaiseException(MS_VC_EXCEPTION, 0, sizeof(info) / sizeof(ULONG_PTR), (ULONG_PTR*)&info);
    }
    __except (EXCEPTION_EXECUTE_HANDLER){
    }
#pragma warning(pop)
}
```

## <a name="see-also"></a>请参阅
- [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
- [如何：在托管代码中设置线程名称](../debugger/how-to-set-a-thread-name-in-managed-code.md)
