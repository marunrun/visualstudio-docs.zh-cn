---
title: 调试 c + + 访问冲突 | Microsoft Docs
description: 如果有多个指针是候选项，请参阅故障排除访问冲突问题的提示。 最新版本的 Visual Studio 命名错误指针。
ms.custom: SEO-VS-2020, seodec18
ms.date: 02/05/2019
ms.topic: how-to
f1_keywords:
- vs.debug.access
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- access violation debugging
- debugging [Visual Studio], access violations
ms.assetid: 9311d754-0ce9-4145-b147-88b6ca77ba63
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 1786085e2f68a1d1196158ac56a62b87b80858be
ms.sourcegitcommit: 3c571f44bfd6402efea5187af43df287bac5b6ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "97761363"
---
# <a name="how-can-i-debug-a-c-access-violation"></a>如何调试 C++ 访问冲突？

## <a name="problem-description"></a>问题描述

我的程序产生了访问冲突。 如何调试它？

## <a name="solution"></a>解决方案

如果在取消引用多个指针的代码行上出现访问冲突，则可能很难辨别引起访问冲突的指针。 从 Visual Studio 2015 Update 1 起，异常对话框现对导致访问冲突的指针进行显式命名。

例如，以下代码中，将出现访问冲突：

```C++
#include <iostream>
using namespace std;

class ClassC {
public:
  void printHello() {
    cout << "hello world";
  }
};

class ClassB {
public:
  ClassC* C;
  ClassB() {
    C = new ClassC();
  }
};

class ClassA {
public:
  ClassB* B;
  ClassA() {
    // Uncomment to fix
    // B = new ClassB();
  }
};

int main() {
  ClassA* A = new ClassA();
  A->B->C->printHello();

}
```

如果在 Visual Studio 2015 Update 1 中运行此代码，你将看到以下异常对话框：

![Microsoft Visual Studio 异常对话框的屏幕截图，其中显示“A->B 为 nullptr”的读取访问冲突。 选中了“中断”按钮。](../debugger/media/accessviolationcplus.png)

如果无法确定该指针为何导致访问冲突，请对代码进行跟踪，以确保导致该问题的指针被正确处理。  如果它作为参数传递，请确保正确传递且未意外创建[浅表副本](https://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy)。 然后为有问题的指针创建一个数据断点，以确保它没有在程序的其他地方被修改，从而验证这些值没有在程序的某个地方被无意地更改。 有关数据断点的详细信息，请参阅 [使用断点](../debugger/using-breakpoints.md)中的数据断点部分。

## <a name="see-also"></a>请参阅
- [调试本机代码常见问题解答](../debugger/debugging-native-code-faqs.md)