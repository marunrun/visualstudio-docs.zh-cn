---
title: 使用修改独立 Shell。.Vsct 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, isolated mode%2C .vsct file
ms.assetid: 6d147c2d-10e9-400e-b8ce-5566287b41ba
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8c106a04e809e772ac3b8a77192fb2f101161e9c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194229"
---
# <a name="modifying-the-isolated-shell-by-using-the-vsct-file"></a>通过使用 .Vsct 文件修改独立 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 独立 shell 项目的 UI 项目包含 .vsct 文件，该文件可用于指定应用程序中可用的应用程序组和各个命令。 下面是 .vsct 文件中的摘录。  
  
```  
<!-- <Define name="No_WindowListCommand"/> -->  
<!-- <Define name="No_MoreWindowsCommand"/> -->  
<!-- <Define name="No_PaneNextPaneCommand"/> -->  
<!-- <Define name="No_PanePrevPaneCommand"/> -->  
```  
  
 默认情况下，包括大多数命令和命令组。 若要排除命令或命令组，只需取消注释该命令或组。  
  
 例如，若要删除下一个窗格和上一个窗格命令，请取消注释 `No_PaneNextPaneCommand` 和 `No_PanePrevPaneCommand` 条目：  
  
```  
  
<Define name="No_PaneNextPaneCommand"/> <Define name="No_PanePrevPaneCommand"/>  
  
```  
  
 有关这些自定义的更详细示例，请参阅 [演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
## <a name="referenced-files"></a>引用的文件  
 应用程序的默认 .vsct 文件引用以下文件。 这些文件位于 Visual Studio SDK 安装目录的 \VisualStudioIntegration\Common\Inc\ 子目录中。  
  
|文件|说明|  
|----------|-----------------|  
|wbids|Web 浏览包的 UI 标识。|  
|AppIDCmdUsed. .vsct|适用于主 Visual Studio UI 元素的命令表。|  
|EmulatorCmdUsed. .vsct|用于 Emacs 和 Brief 编辑器模拟 UI 元素的命令表。|  
|Vsdebugguids|定义 "命令、选项" 页和 Visual Studio 调试器的其他功能的 Guid。|  
|VsDbgCmdUsed. .vsct|调试器的命令表。|  
  
 AppIDCmdUsed. .vsct 文件包含 Visual Studio UI 元素，这些元素基于 .vsct 文件中定义的符号。  
  
 有关详细信息，请参阅 [设计 XML 命令表 (。.Vsct) 文件](../extensibility/internals/designing-xml-command-table-dot-vsct-files.md) 和 [.Vsct XML 架构参考](../extensibility/vsct-xml-schema-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 独立 Shell](../extensibility/visual-studio-isolated-shell.md)
