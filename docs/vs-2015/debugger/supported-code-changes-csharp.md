---
title: " (c # ) 支持的代码更改 |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue [C#], supported code changes
ms.assetid: c7a48ea9-5a7f-4328-a9d7-f0e76fac399d
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6fc02c11a4ebceea431fc06a1bd1cfdb1063097d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "67823541"
---
# <a name="supported-code-changes-c"></a>受支持的代码更改 (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“编辑并继续”处理方法体内的大多数类型的代码更改。 但是，方法体外的大多数更改以及方法体内的小部分更改在调试期间不能应用。 若要应用这些不受支持的更改，您必须停止调试，重新开始新版本的代码。  
  
 在调试会话期间，不能对 C# 代码应用下列更改：  
  
- 对当前语句或任何其他活动语句的更改。  
  
     活动语句包括为转至当前语句而调用过的任何语句（位于调用堆栈的函数中）。  
  
     当前语句在源窗口中以黄色背景标记。 其他活动语句以阴影背景标记，并且是只读的。 可在“选项”对话框中更改这些默认颜色。  
  
- 更改类型的签名。  
  
- 添加匿名方法，该方法捕获之前未被捕获的变量。  
  
- 添加、移除或更改特性。  
  
- 添加、移除或更改 `using` 指令。  
  
- 在活动语句前后添加 `foreach`、`using` 或 `lock`。  
  
## <a name="unsafe-code"></a>不安全代码  
 对不安全代码的更改与对安全代码的更改具有相同的限制，但它还包含一条附加限制：“编辑并继续”不支持更改存在于包含 `stackalloc` 运算符的方法内的不安全代码。  
  
## <a name="exceptions"></a>例外  
 “编辑并继续”支持对 `catch` 和 `finally` 块的更改，除了不允许在活动语句周围添加 `catch` 或`finally` 块以外。  
  
## <a name="unsupported-scenarios"></a>不支持的方案  
 在以下调试方案中，“编辑并继续”不可用：  
  
- 在某些情况下调试 LINQ 代码。 有关详细信息，请参阅 [Debugging LINQ](../debugger/debugging-linq.md)（调试 LINQ）。  
  
  - 捕获之前尚未捕获的变量。  

  - 更改查询表达式的类型 (例如，选择 a => 选择 new {A = a}; )   

  - 删除包含活动语句的 `where`。  

  - 删除包含活动语句的 `let`。  

  - 删除包含活动语句的 `join`。  

  - 删除包含活动语句的 `orderby`。  
  
- 混合模式（本机/托管）调试。  
  
- SQL 调试。  
  
- 调试 Dr.Watson 转储。  
  
- 在未选择 "**在未经处理的异常上展开调用堆栈**" 选项的情况下，在未处理的异常之后编辑代码。  
  
- 调试嵌入式运行时应用程序。  
  
- 通过从 "**调试**" 菜单中选择 "**启动**"，调试**附加到**的应用程序，而不是运行该应用程序。  
  
- 调试优化后的代码。  
  
- 如果由于生成错误无法生成新版本的代码，则对旧版本的代码进行调试。  
  
## <a name="see-also"></a>另请参阅  
 ["编辑并继续" (Visual c # ) ](../debugger/edit-and-continue-visual-csharp.md)   
 [如何：使用“编辑并继续”(C#)](../debugger/how-to-use-edit-and-continue-csharp.md)
