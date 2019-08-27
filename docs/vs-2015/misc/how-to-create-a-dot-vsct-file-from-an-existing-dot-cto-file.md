---
title: 如何：创建。从现有的 Vsct 文件。首席技术官文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, creating based on a .cto file
ms.assetid: 847717c9-477d-4ac9-8b2c-2da878912478
caps.latest.revision: 11
manager: jillfra
ms.openlocfilehash: 83608d768940158dcdab427a557577677e56f7c8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822433"
---
# <a name="how-to-create-a-vsct-file-from-an-existing-cto-file"></a>如何：创建。从现有的 Vsct 文件。首席技术官文件
可从现有的二进制 .cto 文件创建一个基于 XML 的 .vsct 文件。 这样既可充分利用新的命令表编译器格式。 即使 .cto 文件是从 .ctc 文件编译而来，此过程仍然有效。 你可以编辑 .vsct 文件并将其编译到其他 .cto 文件。  
  
### <a name="to-create-a-vsct-file-from-a-cto-file"></a>从 .cto 文件创建 .Vsct 文件  
  
1. 获取 .cto 文件及其对应 .ctsym 文件的副本。  
  
2. 将文件与 vsct.exe 编译器放在同一目录中。  
  
3. 在 Visual Studio 命令提示符处，转到包含 .cto 和 .ctsym 文件的目录。  
  
4. 类型 **vsct.exe** _ctofilename_**.cto** _vsctfilename_**.vsct -S**_symfilename_**.ctsym**。  
  
     `ctofilename` 是 .cto 文件的名称，`vsctfilename` 是要创建的 vsct 文件的名称，而 `symfilename` 是 .ctsym 文件的名称。  
  
     此过程可创建新的 .vsct XML 命令表编译器文件。 可像任何其他 .vsct 文件一样，使用 vsct.exe（vsct 编译器）来编辑和编译此文件。  
  
## <a name="see-also"></a>请参阅  
 [如何：创建。Vsct 文件](../extensibility/internals/how-to-create-a-dot-vsct-file.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)