---
title: 用于报告的宏 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.macros
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- macros, CRT reporting macros
- macros, debugging with
- _RPTFn macro
- CRT, reporting macros
- debugging [CRT], reporting macros
- _RPTn macro
ms.assetid: f2085314-a3a8-4caf-a5a4-2af9ad5aad05
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e4aee33d571f95e24a359fa2bc7e12ae8d64eae0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62431623"
---
# <a name="macros-for-reporting"></a>用于报告的宏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用 **_RPTn**，并 **_RPTFn**在 CRTDBG 中定义的宏。H、 要替换的使用`printf`语句进行调试。 这些宏自动不会显示在你的发布生成何时 **_DEBUG**未定义，因此无需将它们括在 **#ifdef**s。  
  
|宏|描述|  
|-----------|-----------------|  
|_RPT0、_RPT1、_RPT2、_RPT3、_RPT4|向四个自变量输出一个消息字符串和零。 对于从 _RPT1 到 _RPT4，消息字符串作为参数的 printf 样式的格式化字符串。|  
|**_RPTF0**, **_RPTF1**, **,_RPTF2**, **_RPTF4**|与相同 **_RPTn** ，但这些宏还输出宏所在的位置的文件名称和行号。|  
  
 请看下面的示例：  
  
```  
#ifdef _DEBUG  
    if ( someVar > MAX_SOMEVAR )  
        printf( "OVERFLOW! In NameOfThisFunc( ),  
               someVar=%d, otherVar=%d.\n",  
               someVar, otherVar );  
#endif  
```  
  
 该代码将 `someVar` 和 `otherVar` 的值输出到 stdout。 可以使用以下对 `_RPTF2` 的调用报告同样的值另加文件名和行号：  
  
```  
if (someVar > MAX_SOMEVAR) _RPTF2(_CRT_WARN, "In NameOfThisFunc( ), someVar= %d, otherVar= %d\n", someVar, otherVar );  
```  
  
 如果发现某特定应用程序需要调试报告，而 C 运行库提供的宏不提供该报告，则可以编写专门设计的宏来符合您自己的需求。 例如，可以在其中一个头文件中包含以下代码来定义名为 ALERT_IF2 的宏：  
  
```  
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
  
 调用一次**ALERT_IF2**无法执行的所有功能**printf**在本主题开头的代码：  
  
```  
ALERT_IF2(someVar > MAX_SOMEVAR, "OVERFLOW! In NameOfThisFunc( ),   
someVar=%d, otherVar=%d.\n", someVar, otherVar );  
```  
  
 因为可以方便地更改自定义宏，以便向不同目标报告或多或少的信息（取决于怎样更方便），所以该方法在调试要求不断发展时尤其有用。  
  
## <a name="see-also"></a>请参阅  
 [CRT 调试方法](../debugger/crt-debugging-techniques.md)
