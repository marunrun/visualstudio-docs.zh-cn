---
title: 查看调试器中的数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], inspecting programs
- debugger, viewing data
ms.assetid: 13e1105f-f987-402e-9108-ec6ac12be042
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1ade6c38a8edd73c181a3f135dd5e967901bf63f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68178930"
---
# <a name="viewing-data-in-the-debugger"></a>查看调试器中的数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 调试器提供了各种用于检查和修改程序状态的工具。 这些工具中的大多数仅在中断模式下有效。  
  
## <a name="datatips"></a>数据提示  
 数据提示是用于在调试过程中查看程序中的变量和对象的有关信息的最方便工具之一。 在调试器处于中断模式时，可以在当前范围内查看变量的值，方法是将鼠标指针置于源窗口中的变量上。 有关详细信息，请参阅[查看数据提示中的数据值](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)。  
  
## <a name="visualizers"></a>可视化工具  
 可视化工具是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 调试器的新组件，通过它可以以有意义的方式查看对象或变量的内容。 例如，可以使用 HTML 可视化工具来查看 HTML 字符串，因为这样可以解释该字符串并在浏览器中显示出来。 你可以通过数据提示、 **“监视”** 窗口、 **“自动”** 窗口、 **“局部变量”** 窗口或 **“快速监视”** 对话框来访问可视化工具。 有关详细信息，请参阅[创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)。  
  
## <a name="see-also"></a>请参阅  
 [Debugger Basics](../debugger/debugger-basics.md) （调试器基础知识）  
 [“命令”窗口](../ide/reference/command-window.md)   
 [调试器安全](../debugger/debugger-security.md)
