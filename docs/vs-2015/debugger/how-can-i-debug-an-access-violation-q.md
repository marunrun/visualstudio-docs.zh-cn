---
title: 如何调试访问冲突？ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.access
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- access violation debugging
- debugging [Visual Studio], access violations
ms.assetid: 9311d754-0ce9-4145-b147-88b6ca77ba63
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 073fc84d15cb31b4f7a4cc635524ab08a724911e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147851"
---
# <a name="how-can-i-debug-an-access-violation"></a>如何调试访问冲突？
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

问题描述  
 我的程序产生了访问冲突。 如何调试它？  
  
## <a name="solution"></a>解决方案  
 如果在取消引用多个指针的代码行上出现访问冲突，则可能很难辨别引起访问冲突的指针。 从 Visual Studio 2015 Update 1 起，异常对话框现对导致访问冲突的指针进行显式命名。  
  
 例如，以下代码中，将出现访问冲突：  
  
```cpp  
#include <iostream>  
using namespace std;  
  
class ClassB {  
public:  
      ClassC* C;  
      ClassB() {  
            C = new ClassC();  
      }  
     void printHello() {  
            cout << "hello world";  
      }  
};  
  
class ClassA {  
public:  
    ClassB* B;  
    ClassA() {  
            B = nullptr;  
      }  
};  
  
int main() {  
    ClassA* A = new ClassA();  
    A->B->printHello();  
}  
```  
  
 如果在 Visual Studio 2015 Update 1 中运行此代码，你将看到以下异常对话框：  
  
 ![AccessViolationCPlus](../debugger/media/accessviolationcplus.png "AccessViolationCPlus")  
  
 如果无法确定该指针为何导致访问冲突，请对代码进行跟踪，以确保导致该问题的指针被正确处理。  如果它作为参数传递，请确保正确传递且未意外创建 [浅表副本](http://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy)。 然后验证未由于创建数据断点而在程序中某些位置无意更改了所述指针的值，以确保没有在程序中其他位置对其进行修改。 有关数据断点的详细信息，请参阅 [使用断点](../debugger/using-breakpoints.md)中的数据断点部分。  
  
## <a name="see-also"></a>请参阅  
 [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)
