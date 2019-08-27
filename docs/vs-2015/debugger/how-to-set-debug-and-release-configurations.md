---
title: 如何：设置调试和发布配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.builds
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
- configurations, release
- build configurations, release
- projects [Visual Studio], release configurations
- debugging [Visual Studio], release configurations
- release builds, changing settings
- debug builds
- debug builds, switching to release build
- debug builds, changing configuration settings
- debugging [Visual Studio], debug configurations
- projects [Visual Studio], debug configurations
- build configurations, debug
- debug configurations
- release builds, switching to debug build
- Visual Basic projects, debug and release builds
ms.assetid: 57b6bbb7-f2af-48f7-8773-127d75034ed2
caps.latest.revision: 48
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4984355c12a92529a943fe6778740ac2d7f522f8
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703641"
---
# <a name="how-to-set-debug-and-release-configurations"></a>如何：设置调试和发布配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 项目具有针对你的程序的单独发布和调试配置。 顾名思义，生成调试版本的目的是用于调试，而生成发布版本的目的是用于最终发布分发。  
  
 程序的调试配置使用完整符号调试信息编译，且不进行优化。 优化会使调试复杂化，因为源代码和生成的指令之间的关系更加复杂。  
  
 程序的发布配置进行了完全优化，且不包含任何符号调试信息。 根据使用的编译器选项，可在 PDB 文件中生成调试信息。 如果以后还必须调试发行版本，创建 PDB 文件就非常有用。  
  
 有关生成配置的详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。  
  
 你可以将生成配置从**生成**菜单中的，从工具栏中，或在项目属性页。 项目属性页是特定于语言的。 下面的过程演示如何从菜单和工具栏更改生成配置。 有关如何在使用不同语言的项目中更改生成配置的详细信息，请参阅下面的“相关主题”一节。  
  
### <a name="to-change-the-build-configuration"></a>更改生成配置  
  
1. 从生成菜单： 单击**生成 / Configuration Manager**，然后选择**调试**或**发行**。  
  
2. 在工具栏中，选择**调试**或**发行**从**解决方案配置**列表框。  
  
     ![工具栏生成配置](../debugger/media/toolbarbuildconfiguration.png "ToolbarBuildConfiguration")  
  
     Express 版中不提供此工具栏。 可以使用**生成解决方案 F6**并**启动调试 F5**菜单项来选择配置。  
  
## <a name="see-also"></a>请参阅  
 [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)   
 [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)   
 [调试和发布项目配置](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e)
