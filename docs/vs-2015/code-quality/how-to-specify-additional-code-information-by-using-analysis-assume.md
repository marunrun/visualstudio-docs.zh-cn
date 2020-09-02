---
title: 如何：使用 __analysis_assume 指定其他代码信息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- __analysis_assume
helpviewer_keywords:
- __analysis_assume
ms.assetid: 51205d97-4084-4cf4-a5ed-3eeaf67deb1b
caps.latest.revision: 12
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: f2f18c9284ec96de7a7b8663aff485962d194282
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "77277970"
---
# <a name="how-to-specify-additional-code-information-by-using-__analysis_assume"></a>如何：使用 __analysis_assume 指定其他代码信息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以为 C/c + + 代码的代码分析工具提供提示，以帮助分析过程并减少警告。 若要提供其他信息，请使用以下函数：  
  
 `__analysis_assume(`  `expr`  `)`  
  
 `expr` -假定为 true 的任何表达式。  
  
 代码分析工具假定表达式所表示的条件在函数显示的点处为 true，并在更改表达式（例如，通过赋值给变量时）时保持为 true。  
  
> [!NOTE]
> `__analysis_assume` 不会影响代码优化。 在代码分析工具外部， `__analysis_assume` 定义为 "无操作"。  
  
## <a name="example"></a>示例  
 下面的代码使用 `__analysis_assume` 来更正代码分析警告 [C6388](../code-quality/c6388.md)：  
  
```  
#include<windows.h>  
#include<codeanalysis\sourceannotations.h>  
  
using namespace vc_attributes;  
  
// calls free and sets ch to null  
void FreeAndNull(char* ch);  
  
//requires pc to be null  
void f([Pre(Null=Yes)] char* pc);  
  
void test( )  
{  
  char *pc = (char*)malloc(5);  
  FreeAndNull(pc);  
  __analysis_assume(pc == NULL);   
  f(pc);  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [__assume](https://msdn.microsoft.com/library/d8565123-b132-44b1-8235-5a8c8bff85a7)
