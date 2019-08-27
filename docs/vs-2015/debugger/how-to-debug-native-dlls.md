---
title: 如何：调试本机 Dll |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.dll
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging DLLs
- DLLs, debugging
- executable files, specifying for debug sessions
ms.assetid: 76b34d15-a66d-4963-842e-c8b955c81696
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 16a533b27e619526edab71374d922e68baf0a4b0
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65702684"
---
# <a name="how-to-debug-native-dlls"></a>如何：调试本机 Dll
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在“工具”菜单上选择“导入和导出设置”。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 当调试 DLL 时，可以从以下开始调试：  
  
- 用于创建调用 DLL 的可执行文件的项目。  
  
  \- 或 -  
  
- 用于创建 DLL 本身的项目。  
  
  如果有用于创建可执行文件的项目，则从该项目开始调试。 然后可以打开 DLL 的源文件，并在该文件中设置断点，即使它不是用于创建可执行文件的项目的一部分。 有关详细信息，请参见[断点](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583)  
  
  如果从创建 DLL 的项目开始调试，则必须指定在调试 DLL 时要使用的可执行文件。  
  
### <a name="to-specify-an-executable-for-the-debug-session"></a>为调试会话指定可执行文件  
  
1. 在中**解决方案资源管理器**，选择创建 DLL 的项目。  
  
2. 从**视图**菜单中，选择**属性页**。  
  
3. 在中**属性页**对话框中，打开**配置属性**文件夹，然后选择**调试**类别。  
  
4. 在中**命令**框中，指定容器的路径名称。 例如，C:\Program Files\MyApplication\MYAPP.EXE。  
  
5. 在中**命令参数**框中，指定可执行文件的任何必需参数。  
  
   如果未指定中的可执行文件_项目_**属性页**对话框中，[调试会话对话框可执行文件](../debugger/executable-for-debugging-session-dialog-box.md)启动调试时出现。  
  
## <a name="see-also"></a>请参阅  
 [调试器安全](../debugger/debugger-security.md)   
 [在 Visual Studio 中进行调试](../debugger/debugging-in-visual-studio.md)
