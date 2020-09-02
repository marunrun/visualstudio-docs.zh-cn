---
title: 命令处理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - command handling
ms.assetid: 78f67d92-77f7-45cb-ad75-6e3346379cc3
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 563f38cd2dc3854918fe637fdc11afe1d1a49b64
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184378"
---
# <a name="command-handling"></a>命令处理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编辑器可以定义新命令。 命令通常显示在菜单、工具栏或上下文菜单中。  
  
 有关定义命令和菜单的详细信息，请参阅 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。  
  
 语言服务可以通过截获枚举来控制在编辑器中显示哪些上下文菜单 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 。 或者，您可以根据每个标记来控制上下文菜单。 有关详细信息，请参阅 [语言服务筛选器的重要命令](../extensibility/internals/important-commands-for-language-service-filters.md)。  
  
## <a name="adding-commands-to-the-editor-context-menu"></a>将命令添加到编辑器上下文菜单  
 若要将命令添加到上下文菜单，必须先定义一组属于特定组的菜单命令。 下面的示例摘自作为演练演练的一部分生成的 .vsct 文件：向 [自定义编辑器添加功能](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)：  
  
 \<Menu guid="guidCustomEditorCmdSet" id="IDMX_RTF" priority="0x0000" type="Context">  
  
 \<Parent guid="guidCustomEditorCmdSet" id="0"/>  
  
 \<Strings>  
  
 \<ButtonText>CustomEditor 上下文菜单\</ButtonText>  
  
 \<CommandName>CustomEditorContextMenu\</CommandName>  
  
 \</Strings>  
  
 \</Menu>  
  
 \</Menus>  
  
 以上文本会添加一个上下文菜单命令，其中包含文本 **CustomEditor 上下文菜单**。 菜单 GUID 是用此编辑器创建的命令集的 GUID，而类型为 "Context"。  
  
 你还可以使用不需要在 .vsct 文件中定义的预定义命令。 例如，如果检查 Visual Studio 包模板生成的 EditorPane.cs 文件，会发现一组预定义的命令（如定义的命令） <xref:Microsoft.VisualStudio.VSConstants.VSStd97CmdID> <xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> 在命令处理程序（如 onSelectAll 方法）中进行处理。  
  
## <a name="see-also"></a>另请参阅  
 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
