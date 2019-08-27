---
title: 如何：从 DLL 项目进行调试 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- DLL projects, debugging
- debugging DLLs
- DLLs, debugging projects
- debugging [Visual Studio], DLLs
ms.assetid: 40a94339-d3f7-4ab9-b8a1-b8cf82942f44
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6496d38e753d2338966916d1d7855abca77ace34
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438487"
---
# <a name="how-to-debug-from-a-dll-project"></a>如何：从 DLL 项目进行调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

要开始调试 DLL 项目，必须在项目属性中指定调用应用程序。 C++ 属性页的布局和内容与 C# 和 Visual Basic 属性页的不同。  
  
 如果本机代码调用了托管 DLL，而你想对这两者进行调试，则可以在项目属性中指定此项。 有关详细信息，请参阅[如何：在混合模式下调试](../debugger/how-to-debug-in-mixed-mode.md)。  
  
> [!NOTE]
> 不能在 Visual Studio 的 Express 版本中指定外部调用应用程序。 相反，你需要向解决方案添加一个可执行项目，将其设置为启动项目，然后从该可执行项目调用 DLL 中的方法。  
  
### <a name="to-specify-the-calling-application-in-a-c-project"></a>在 C++ 项目中指定调用应用程序  
  
1. 右键单击项目节点中的**解决方案资源管理器**，然后选择**属性**。 转到**调试**选项卡。  
  
2. 确保窗口顶部的“配置”字段设置为“调试”。  
  
3. 转到**配置属性 / 调试**。  
  
4. 在中**要启动的调试器**列表中，选择**本地 Windows 调试器**或**远程 Windows 调试器**。  
  
5. 在中**命令**或**远程命令**框中，添加该应用程序的完全限定路径名称。  
  
6. 向“命令参数”框添加任何必要的程序参数。  
  
### <a name="to-specify-the-calling-application-in-a-c-or-visual-basic-project"></a>在 C# 或 Visual Basic 项目中指定调用应用程序  
  
1. 右键单击项目节点中的**解决方案资源管理器**，然后选择**属性**。 转到**调试**选项卡。  
  
     选择**启动外部程序**，并添加要运行的程序的完全限定的路径名称。  
  
     如果你需要添加外部程序的命令行自变量，将其添加到**命令行参数**字段。  
  
2. 你还可以将应用程序作为 URL 调用。 (如果你正在调试由本地 ASP.NET 应用程序使用的托管 DLL，则可能想要执行此操作。)  
  
     下**启动操作**，选择**URL 启动浏览器：** 单选按钮，并填写 URL。  
  
### <a name="to-start-debugging-from-the-dll-project"></a>从 DLL 项目启动调试  
  
1. 根据需要设置断点。  
  
2. 开始调试 (按 F5，单击绿色箭头，或单击**调试 / 启动调试**)。  
  
## <a name="see-also"></a>请参阅  
 [调试 DLL 项目](../debugger/debugging-dll-projects.md)   
 [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)
