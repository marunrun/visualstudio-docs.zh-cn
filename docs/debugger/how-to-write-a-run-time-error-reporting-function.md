---
title: 编写运行时错误报告函数 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- run-time errors, reporting functions
- reporting function
ms.assetid: 989bf312-5038-44f3-805f-39a34d18760e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 073943d8b6a3dbf5ee3af653a43046c3b389fbfd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85348400"
---
# <a name="how-to-write-a-run-time-error-reporting-function-c"></a>如何：编写运行时错误报告函数 (C++)
运行时错误的自定义报告函数必须具有与 `_CrtDbgReportW` 相同的声明。 它应当将值 1 返回给调试器。

下面的示例显示了如何定义自定义报告函数：

## <a name="example"></a>示例

```cpp
#include <stdio.h>
int errorhandler = 0;
void configureMyErrorFunc(int i)
{
    errorhandler = i;
}

int MyErrorFunc(int errorType, const wchar_t *filename,
                int linenumber, const wchar_t *moduleName,
                const wchar_t *format, ...)
{
    switch (errorhandler)
    {
    case 0:
    case 1:
        wprintf(L"Error type %d at %s line %d in %s",
                errorType, filename, linenumber, moduleName);
        break;
    case 2:
    case 3:
        fprintf(stderr, "Error type");
        break;
    }

    return 1;
}
```

## <a name="example"></a>示例
下面的示例显示了一个更为复杂的自定义报告函数。 在该示例中，switch 语句处理由 `reportType` 的 `_CrtDbgReportW` 参数定义的各种错误类型。 由于要替换 `_CrtDbgReportW`，因此不能使用 `_CrtSetReportMode`。 函数必须处理输出。 这个函数中的第一个变量自变量获得运行时错误号。 有关详细信息，请参阅 [_RTC_SetErrorType](/cpp/c-runtime-library/reference/rtc-seterrortype)。

```cpp
#include <windows.h>
#include <stdarg.h>
#include <rtcapi.h>
#include <malloc.h>
#pragma runtime_checks("", off)
int Catch_RTC_Failure(int errType, const wchar_t *file, int line,
                      const wchar_t *module, const wchar_t *format, ...)
{
    // Prevent re-entrance.
    static long running = 0;
    while (InterlockedExchange(&running, 1))
        Sleep(0);
    // Now, disable all RTC failures.
    int numErrors = _RTC_NumErrors();
    int *errors=(int*)_alloca(numErrors);
    for (int i = 0; i < numErrors; i++)
        errors[i] = _RTC_SetErrorType((_RTC_ErrorNumber)i, _RTC_ERRTYPE_IGNORE);

    // First, get the rtc error number from the var-arg list.
    va_list vl;
    va_start(vl, format);
    _RTC_ErrorNumber rtc_errnum = va_arg(vl, _RTC_ErrorNumber);
    va_end(vl);

    wchar_t buf[512];
    const char *err = _RTC_GetErrDesc(rtc_errnum);
    swprintf_s(buf, 512, L"%S\nLine #%d\nFile:%s\nModule:%s",
        err,
        line,
        file ? file : L"Unknown",
        module ? module : L"Unknown");
    int res = (MessageBox(NULL, buf, L"RTC Failed...", MB_YESNO) == IDYES) ? 1 : 0;
    // Now, restore the RTC errortypes.
    for(int i = 0; i < numErrors; i++)
        _RTC_SetErrorType((_RTC_ErrorNumber)i, errors[i]);
    running = 0;
    return res;
}
#pragma runtime_checks("", restore)
```

## <a name="example"></a>示例
使用 `_RTC_SetErrorFuncW` 安装自定义函数来代替 `_CrtDbgReportW`。 有关详细信息，请参阅 [_RTC_SetErrorFuncW](/cpp/c-runtime-library/reference/rtc-seterrorfuncw)。 `_RTC_SetErrorFuncW` 的返回值是前一个报告函数，如果必要，可以保存并恢复它。

```cpp
#include <rtcapi.h>
int main()
{
    _RTC_error_fnW oldfunction, newfunc;
    oldfunction = _RTC_SetErrorFuncW(&MyErrorFunc);
    // Run some code.
    newfunc = _RTC_SetErrorFuncW(oldfunction);
    // newfunc == &MyErrorFunc;
    // Run some more code.
}
```

## <a name="see-also"></a>请参阅
[本机运行时检查自定义](../debugger/native-run-time-checks-customization.md)
