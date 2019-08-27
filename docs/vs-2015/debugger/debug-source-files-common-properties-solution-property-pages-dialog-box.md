---
title: 调试通用属性解决方案属性页源对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.options.FindSource
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- SQL
- VB
- CSharp
- C++
helpviewer_keywords:
- Debug Source Files property page
- debugging [Visual Studio], specifying source and symbol files
- source files, specifying in debugger
- debugger, source files
ms.assetid: 0af11464-eeb1-4d0b-87a6-0cc96779afb1
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 47fb2511e39153753a2c27483dd6ac96c26c9e83
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143032"
---
# <a name="debug-source-files-common-properties-solution-property-pages-dialog-box"></a>“解决方案属性页”对话框 ->“通用属性”->“调试源文件”
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

该属性页指定调试器调试解决方案时查找源文件的位置。  
  
 若要访问“调试源文件”属性页，请在“解决方案资源管理器”中右键单击你的解决方案，并从快捷菜单中选择“属性”    。 展开“公共属性”文件夹并单击“调试源文件”页   。  
  
 **包含源代码的目录**  
 包含在调试解决方案时调试器搜索源文件的目录的列表。 还可搜索指定目录的子目录。  
  
 **不查找这些源文件**  
 输入不希望调试器读取的任何文件的名称。 如果调试器在以上指定的某个目录中找到这些文件之一，它将忽略该文件。 如果调试时出现“查找源”对话框，并点击“取消”，正在搜索的文件会被添加到此列表中，以使调试器不会再搜索该文件   。  
  
## <a name="see-also"></a>请参阅  
 [调试器安全](../debugger/debugger-security.md)   
 [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
