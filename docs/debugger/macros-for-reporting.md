---
title: 用于报告的宏 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.macros
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- macros, CRT reporting macros
- macros, debugging with
- _RPTFn macro
- CRT, reporting macros
- debugging [CRT], reporting macros
- _RPTn macro
ms.assetid: f2085314-a3a8-4caf-a5a4-2af9ad5aad05
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c2129db98293cef678527fb331992c6c5960d8f9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72731387"
---
# <a name="macros-for-reporting"></a>用于报告的宏
可以使用在 CRTDBG.H 中定义的 _RPTn 和 _RPTFn 宏替换 `printf` 语句进行调试 。 未定义 _DEBUG 时，不必将它们括在 #ifdef 内，因为它们会在发布版本中自动消失 。

|宏|描述|
|-----------|-----------------|
|_RPT0、_RPT1、_RPT2、_RPT3、_RPT4    |向四个自变量输出一个消息字符串和零。 对于从 _RPT1 到 _RPT4，消息字符串作为参数的 printf 样式的格式化字符串。|
|_RPTF0、_RPTF1、_RPTF2、_RPTF4   |与 _RPTn 相同，但这些宏还输出其所在的文件名和行号。|

 请看下面的示例：

```cpp
#ifdef _DEBUG
    if ( someVar > MAX_SOMEVAR )
        printf( "OVERFLOW! In NameOfThisFunc( ),
               someVar=%d, otherVar=%d.\n",
               someVar, otherVar );
#endif
```

 该代码将 `someVar` 和 `otherVar` 的值输出到 stdout。 可以使用以下对 `_RPTF2` 的调用报告同样的值另加文件名和行号：

```cpp
if (someVar > MAX_SOMEVAR) _RPTF2(_CRT_WARN, "In NameOfThisFunc( ), someVar= %d, otherVar= %d\n", someVar, otherVar );
```

可能会发现某特定应用程序需要调试报告，而 C 运行时库提供的宏不提供该报告。 对于这些情况，你可以编写专门设计的宏来满足自己的需求。 例如，可以在其中一个头文件中包含以下代码来定义名为 ALERT_IF2 的宏：

```cpp
#ifndef _DEBUG                  /* For RELEASE builds */
#define  ALERT_IF2(expr, msg, arg1, arg2)  do {} while (0)
#else                           /* For DEBUG builds   */
#define  ALERT_IF2(expr, msg, arg1, arg2) \
    do { \
        if ((expr) && \
            (1 == _CrtDbgReport(_CRT_ERROR, \
                __FILE__, __LINE__, msg, arg1, arg2))) \
            _CrtDbgBreak( ); \
    } while (0)
#endif
```

 调用一次 ALERT_IF2 可以执行 printf 代码的所有函数 ：

```cpp
ALERT_IF2(someVar > MAX_SOMEVAR, "OVERFLOW! In NameOfThisFunc( ),
someVar=%d, otherVar=%d.\n", someVar, otherVar );
```

 你可以轻松更改自定义宏，以便向不同目标报告更多或更少的信息。 当调试需求不断变化时，此方法特别有用。

## <a name="see-also"></a>请参阅
- [CRT 调试方法](../debugger/crt-debugging-techniques.md)
