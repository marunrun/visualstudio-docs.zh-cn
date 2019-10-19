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
ms.openlocfilehash: a89dce28f33bef0ffdb13d6254b2ac6b86ac25db
ms.sourcegitcommit: 8a96a65676fd7a2a03b0803d7eceae65f3fa142b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72589024"
---
# <a name="how-to-set-a-thread-name-in-native-code"></a>如何：在本机代码中设置线程名称
在 Visual Studio 的任何版本中都可以使用线程命名功能。 当调试正在运行的进程时，线程命名有助于标识 "**线程**" 窗口中感兴趣的线程。 在通过故障转储检查并使用各种工具分析性能捕获时，具有 recognizably 命名的线程也会有所帮助。

## <a name="ways-to-set-a-thread-name"></a>设置线程名称的方法

可以通过两种方法来设置线程名称。 第一种方式是通过[SetThreadDescription](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-setthreaddescription)函数。 第二种方法是在 Visual Studio 调试器附加到进程时引发特定异常。 每种方法都有优点和注意事项。 从 Windows 10 版本1607或 Windows Server 2016 开始，支持使用 `SetThreadDescription`。

值得注意的是，_这两_种方法可以一起使用（如果需要），因为它们的工作机制彼此独立。

### <a name="set-a-thread-name-by-using-setthreaddescription"></a>使用 `SetThreadDescription` 设置线程名称

优点：
* 在 Visual Studio 中进行调试时，线程名称是可见的，无论调试程序是否已在调用 SetThreadDescription 时附加到进程。
* 在 Visual Studio 中加载故障转储后，线程名称将在执行事后调试时可见。
* 使用其他工具（如[WinDbg](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)调试器和[Windows 性能分析器](https://docs.microsoft.com/windows-hardware/test/wpt/windows-performance-analyzer)性能分析器）时，也会显示线程名称。

注意：
* 线程名称只在 Visual Studio 2017 版本15.6 及更高版本中可见。
* 当事后调试故障转储文件时，只有在 Windows 10 版本1607、Windows Server 2016 或更高版本的 Windows 上创建了崩溃后，线程名称才可见。

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

在程序中设置线程名称的另一种方法是，通过引发专门配置的异常将所需的线程名称传达给 Visual Studio 调试器。

优点：
* 适用于所有版本的 Visual Studio。

注意：
* 仅在使用基于异常的方法时附加调试器时才起作用。
* 使用此方法设置的线程名称将在转储或性能分析工具中不可用。

*示例：*

下面显示的 `SetThreadName` 函数演示了此基于异常的方法。 请注意，线程名称将自动复制到线程，以便 `threadName` 参数的内存可在 `SetThreadName` 调用完成后释放。

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
