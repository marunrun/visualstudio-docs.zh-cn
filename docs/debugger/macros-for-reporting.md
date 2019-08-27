---
title: 用于报告的宏 |Microsoft Docs
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
ms.openlocfilehash: 2c92424275a1dff69863b81fbf8567fbc4b84499
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62905550"
---
# <a name="macros-for-reporting"></a>用于报告的宏
对于调试，你可以使用 **_RPTn**并 **_RPTFn**在 CRTDBG 中定义的宏。H、 要替换的使用`printf`语句。 无需在 inclose **#ifdef**s，因为它们自动不会显示在你的发布生成时 **_DEBUG**并不定义。

|宏|描述|
|-----------|-----------------|
|_RPT0、_RPT1、_RPT2、_RPT3、_RPT4|向四个自变量输出一个消息字符串和零。 对于从 _RPT1 到 _RPT4，消息字符串作为参数的 printf 样式的格式化字符串。|
|_RPTF0、_RPTF1、_RPTF2、_RPTF4|与 _RPTn 相同，但这些宏还输出其所在的文件名和行号。|

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

您可能会发现特定应用程序需要调试报告功能，它不提供用 C 运行库提供的宏。 对于这些情况下，可以编写专门为适合你自己的需求而设计的宏。 例如，可以在其中一个头文件中包含以下代码来定义名为 ALERT_IF2 的宏：

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

 调用一次**ALERT_IF2**可以执行的所有函数**printf**代码：

```cpp
ALERT_IF2(someVar > MAX_SOMEVAR, "OVERFLOW! In NameOfThisFunc( ),
someVar=%d, otherVar=%d.\n", someVar, otherVar );
```

 您可以轻松更改自定义的宏来增加或减少报告到不同的目标的信息。 随着在调试需求的发展，这种方法是特别有用。

## <a name="see-also"></a>请参阅
- [CRT 调试方法](../debugger/crt-debugging-techniques.md)
