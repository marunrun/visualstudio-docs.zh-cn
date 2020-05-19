---
title: 如何：在本机代码中设置线程名称 | Microsoft Docs
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
ms.openlocfilehash: 1e719563c831c50cc325d70d0de431f4be1bf514
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911426"
---
# <a name="how-to-set-a-thread-name-in-native-code"></a>如何：在本机代码中设置线程名称
在 Visual Studio 的任何版本中都可以使用线程命名功能。 调试正在运行的进程时，线程命名对于在“线程”窗口中标识感兴趣的线程来说非常有用。 通过故障转储检查执行事后调试以及使用各种工具分析性能捕获时，具有高度可识别的线程名称也可能会有所帮助。

## <a name="ways-to-set-a-thread-name"></a>设置线程名称的方法

可通过两种方法设置线程名称。 第一种方法是通过 [SetThreadDescription](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-setthreaddescription) 函数设置。 第二种方法是在将 Visual Studio 调试器附加到进程时引发特定异常来进行设置。 每种方法都有各自的优点和注意事项。 从 Windows 10 版本 1607 或 Windows Server 2016 开始，支持使用 `SetThreadDescription`。

值得注意的是，如果需要，两种方法可以一起使用，因为它们的工作机制彼此独立。

### <a name="set-a-thread-name-by-using-setthreaddescription"></a>通过使用 `SetThreadDescription` 设置线程名称

优点：
* 在 Visual Studio 中进行调试时，无论调试器是否已在调用 SetThreadDescription 时附加到进程，线程名称都是可见的。
* 通过在 Visual Studio 中加载故障转储执行事后调试时，线程名称是可见的。
* 使用其他工具（如 [WinDbg](/windows-hardware/drivers/debugger/debugger-download-tools) 调试器和 [Windows 性能分析器](/windows-hardware/test/wpt/windows-performance-analyzer)性能分析器）时，线程名称也是可见的。

注意：
* 线程名称仅在 Visual Studio 2017 版本 15.6 及更高版本中可见。
* 对故障转储文件进行事后调试时，仅当故障是在 Windows 10 版本 1607、Windows Server 2016 或更高版本的 Windows 上创建时，线程名称才可见。

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

在程序中设置线程名称的另一种方法是，通过引发专门配置的异常，将所需的线程名称传达给 Visual Studio 调试器。

优点：
* 适用于所有版本的 Visual Studio。

注意：
* 仅在使用基于异常的方法时附加了调试器的情况下才起作用。
* 使用此方法设置的线程名称在转储或性能分析工具中将不可用。

*示例：*

下面显示的 `SetThreadName` 函数展示了此基于异常的方法。 请注意，线程名称将自动复制到线程，以便 `threadName` 参数的内存可在 `SetThreadName` 调用完成后释放。

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
