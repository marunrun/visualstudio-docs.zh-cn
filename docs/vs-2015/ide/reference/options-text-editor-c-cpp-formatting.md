---
title: 选项，文本编辑器，C/C++，格式设置 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.C%2fC%2b%2b.Formatting.General
dev_langs:
- C++
helpviewer_keywords:
- Text Editor Options dialog box, formatting
ms.assetid: cb6f1cbb-5305-48da-a8e8-33fd70775d46
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 66adcdeca1aa794649b42f4ae153d9b2f879deff
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697142"
---
# <a name="options-text-editor-cc-formatting"></a>选项，文本编辑器，C/C++，格式设置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

允许你在使用 C 或 C++ 编程时更改代码编辑器的默认行为。  
  
 若要访问此页，请在“选项”对话框的左窗格中，展开“文本编辑器”，再展开“C/C++”，然后单击“格式设置”。  
  
> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## <a name="cc-options"></a>C/C++ 选项  
 **启用自动快速信息工具提示**  
 启用或禁用快速信息 IntelliSense 功能。  
  
## <a name="inactive-code"></a>非活动代码  
 **显示非活动代码块**  
 由于 `#ifdef` 声明而处于不活动状态的代码以颜色区分，帮助你识别此类代码。  
  
 **禁用非活动代码透明**  
 可以通过使用颜色（而非透明度）来识别非活动代码。  
  
 **非活动代码透明度百分比**  
 可以自定义非活动代码块的不透明度。  
  
## <a name="indentation"></a>缩进  
 **缩进大括号**  
 可以配置在你开始一个代码块（例如函数或 `for` 循环）之后按下 Enter 键时大括号的对齐方式。 大括号可以与该代码块的第一个字符对齐或缩进。  
  
 **遇 Tab 时自动缩进**  
 可以配置当你按下 Tab 键时当前代码执行的操作。 缩进行或插入制表符。  
  
## <a name="miscellaneous"></a>杂项  
 **枚举“任务列表”窗口中的注释**  
 编辑器可以在打开的源文件中扫描注释中的预设词。 它在“任务列表”窗口中为找到的任何关键字创建一个条目。  
  
 **突出显示匹配的标记**  
 当光标位于大括号旁边时，编辑器可以突出显示匹配的大括号，以便你更容易看到包含的代码。  
  
## <a name="outlining"></a>大纲显示  
 **打开文件时进入大纲模式**  
 在文本编辑器中打开一个文件时，可以启用大纲显示功能。 有关详细信息，请参阅[大纲显示](../../ide/outlining.md)。 选择此选项后，打开文件时将启用大纲显示功能。  
  
 **#Pragma 区域块的自动大纲显示**  
 选择此选项时，将对[杂注指令](https://msdn.microsoft.com/library/9867b438-ac64-4e10-973f-c3955209873f)启用自动大纲显示。 这使你可以在大纲模式中展开或折叠杂注区域块。  
  
 **语句块的自动大纲显示**  
 选择此选项时，将对下列语句构造启用自动大纲显示：  
  
- [if-else](https://msdn.microsoft.com/library/d9a1d562-8cf5-4bd4-9ba7-8ad970cd25b2)  
  
- [switch 语句 (C++)](https://msdn.microsoft.com/library/6c3f3ed3-5593-463c-8f4b-b33742b455c6)  
  
- [While 语句 (C++)](https://msdn.microsoft.com/library/358dbe76-5e5e-4af5-b575-c2293c636899)  
  
## <a name="see-also"></a>请参阅  
 [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)   
 [使用 IntelliSense](../../ide/using-intellisense.md)
