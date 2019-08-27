---
title: 通过使用修改独立的 Shell。Vsct 文件 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194229"
---
# <a name="modifying-the-isolated-shell-by-using-the-vsct-file"></a>通过使用修改独立的 Shell。Vsct 文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 独立的 shell 项目的 UI 项目包含可以指定应用程序中提供了哪些应用程序组和单个命令在.vsct 文件。 以下是未修改的.vsct 文件的摘录。  
  
```  
<!-- <Define name="No_WindowListCommand"/> -->  
<!-- <Define name="No_MoreWindowsCommand"/> -->  
<!-- <Define name="No_PaneNextPaneCommand"/> -->  
<!-- <Define name="No_PanePrevPaneCommand"/> -->  
```  
  
 默认情况下，会包含大多数命令和命令组。 若要排除的命令或命令组，只需取消注释该命令或组。  
  
 例如，若要删除的下一个窗格和上一窗格命令，取消注释`No_PaneNextPaneCommand`和`No_PanePrevPaneCommand`条目：  
  
```  
  
<Define name="No_PaneNextPaneCommand"/> <Define name="No_PanePrevPaneCommand"/>  
  
```  
  
 有关更详细的示例这些自定义，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
## <a name="referenced-files"></a>引用的文件  
 为应用程序的默认.vsct 文件引用以下文件。 这些文件位于 Visual Studio SDK 安装目录的 \VisualStudioIntegration\Common\Inc\ 子目录中。  
  
|文件|描述|  
|----------|-----------------|  
|wbids.h|Web 浏览包的 UI 标识。|  
|AppIDCmdUsed.vsct|命令表的主 Visual Studio UI 元素。|  
|EmulatorCmdUsed.vsct|Emacs 和简述编辑器仿真 UI 元素的命令表。|  
|Vsdebugguids.h|定义命令、 选项页上，在 Visual Studio 调试器的其他功能的 Guid。|  
|VsDbgCmdUsed.vsct|调试器的命令表。|  
  
 AppIDCmdUsed.vsct 文件包括基于应用程序.vsct 文件中定义的符号的 Visual Studio UI 元素。  
  
 有关详细信息，请参阅[设计 XML 命令表 (。Vsct) 文件](../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)并[VSCT XML 架构参考](../extensibility/vsct-xml-schema-reference.md)。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 独立 Shell](../extensibility/visual-studio-isolated-shell.md)
