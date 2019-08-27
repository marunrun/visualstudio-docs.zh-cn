---
title: 演练：将功能添加到自定义编辑器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
caps.latest.revision: 39
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1d14fb36298518409df34302f9346e186f0b0263
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825166"
---
# <a name="walkthrough-adding-features-to-a-custom-editor"></a>演练：在自定义编辑器中添加功能
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建自定义编辑器后，您可以向其添加更多的功能。  
  
### <a name="to-create-an-editor-for-a-vspackage"></a>若要创建 VSPackage 的编辑器  
  
1. 使用 Visual Studio 包项目模板创建自定义编辑器。  
  
     有关详细信息，请参见[演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)。  
  
2. 决定您编辑器来支持单个视图或多个视图。  
  
     支持的编辑器**新的窗口**命令，或具有窗体视图和代码视图，需要单独的文档数据对象和文档视图对象。 在一个编辑器，支持单个视图，文档数据对象和文档视图对象可以实现对同一个对象。  
  
     多个视图的示例，请参阅[Supporting Multiple Document Views](../extensibility/supporting-multiple-document-views.md)。  
  
3. 编辑器工厂实现通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>接口。  
  
     有关详细信息，请参阅[编辑器工厂](../extensibility/editor-factories.md)。  
  
4. 决定是否希望在使用就地激活编辑器或简化的嵌入来管理文档视图对象窗口。  
  
     简化的嵌入编辑器窗口承载标准文档视图中，而在就地激活编辑器窗口承载 ActiveX 控件或其他活动作为其文档视图对象。 有关详细信息，请参阅[简化的嵌入](../extensibility/simplified-embedding.md)并[就地激活](../misc/in-place-activation.md)。  
  
5. 实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口以处理命令。  
  
6. 通过执行以下操作来提供文档暂留和响应的外部文件更改：  
  
    1. 若要保存该文件，实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>和<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>编辑器的文档的数据对象。  
  
    2. 若要对外部文件的更改做出响应，实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>编辑器的文档的数据对象。  
  
        > [!NOTE]
        > 调用`QueryService`上<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>若要获取的指针`IVsFileChangeEx`。  
  
7. 协调与源代码管理的文档编辑事件。 具体方法为：  
  
    1. 获取一个指向`IVsQueryEditQuerySave2`通过调用`QueryService`上<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>。  
  
    2. 第一个编辑事件发生时，调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>方法。  
  
         这会提示用户签出该文件，如果未签出。请务必处理要避免出现错误"未签出文件"条件  
  
    3. 同样，保存该文件之前, 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>方法。  
  
         此方法会提示用户保存文件，如果尚未保存，或自上次保存以来已更改。  
  
8. 启用**属性**窗口中显示的文本在编辑器中选择的属性。 具体方法为：  
  
    1. 调用<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>每个时间文本选择发生更改，传递的实现中<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>。  
  
    2. 调用`QueryService`上<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>服务，以获取一个指向<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>。  
  
9. 使用户能够拖放到编辑器之间的项和**工具箱**，或之间外部编辑器 （如 Microsoft Word) 和**工具箱**。 具体方法为：  
  
    1. 实现`IDropTarget`上您的编辑器来提醒你的编辑器是拖放目标的 IDE。  
  
    2. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>使您的编辑器可以启用和禁用中的项在视图上的接口**工具箱**。  
  
    3. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A>，并调用`QueryService`上<xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox>服务，以获取指向的指针<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3>接口。  
  
         这样，若要添加新项目添加到你的 VSPackage**工具箱**。  
  
10. 确定编辑器是否需要任何其他可选功能。  
  
    - 如果你想您编辑器来支持查找和替换命令，实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>。  
  
    - 如果你想要使用文档大纲工具窗口在编辑器中的，实现`IVsDocOutlineProvider`。  
  
    - 如果你想要在编辑器中使用一个状态栏，实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>，并调用`QueryService`有关<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>若要获取的指针`IVsStatusBar`。  
  
         例如，编辑器可以显示行 / 列信息、 选择模式 （流式传输 / 框），并插入模式 （插入 / 重叠）。  
  
    - 如果希望支持您编辑器`Undo`命令时，建议的方法是使用 OLE 撤消管理器模型。 或者，可以使编辑器处理`Undo`直接命令。  
  
11. 创建注册表信息，包括 VSPackage、 菜单、 编辑器和其他功能的 Guid。  
  
     下面是代码的一般示例将放入.rgs 文件脚本中用于演示如何正确注册编辑器。  
  
    ```  
    NoRemove Editors  
    {  
          ForceRemove {...guidEditor...} = s 'RTF Editor'  
          {  
             val Package = s '{...guidVsPackage...}'  
             ForceRemove Extensions  
             {  
                val rtf = d 50  
             }  
          }  
    }  
    NoRemove Menus  
    {  
          val {...guidVsPackage...} = s ',203,11'  
    }  
    ```  
  
12. 实现上下文相关帮助支持。  
  
     这使您可以提供 F1 帮助和动态帮助窗口支持在编辑器中的项。 有关这方面的详细信息，请参阅[如何：为编辑器提供的上下文](../extensibility/how-to-provide-context-for-editors.md)。  
  
13. 通过实现公开自动化对象模型从你的编辑器`IDispatch`接口。  
  
     有关详细信息，请参阅 [Contributing to the Automation Model](../extensibility/internals/contributing-to-the-automation-model.md)。  
  
## <a name="robust-programming"></a>可靠编程  
  
- IDE 调用时将创建编辑器实例<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法。 如果编辑器支持多个视图`CreateEditorInstance`创建文档的数据和文档视图对象。 如果文档数据对象已打开，非 null`punkDocDataExisting`值传递给`IVsEditorFactory::CreateEditorInstance`。 编辑器工厂实现必须确定现有的文档数据对象是否通过查询在其上的相应接口兼容。 有关详细信息，请参阅[Supporting Multiple Document Views](../extensibility/supporting-multiple-document-views.md)。  
  
- 如果您使用简化的嵌入方法，实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>接口。  
  
- 如果您决定使用就地激活，实现以下接口：  
  
     <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>  
  
     <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>  
  
     <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>  
  
    > [!NOTE]
    > `IOleInPlaceComponent`接口用于避免 OLE 2 菜单合并。  
  
     你`IOleCommandTarget`实现处理命令，如**剪切**，**副本**，并且**粘贴**。 在实现时`IOleCommandTarget`，确定编辑器是否需要其自己的.vsct 文件来定义其自己的命令菜单结构，或如果它可以实现定义的标准命令[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 通常情况下，编辑器使用和扩展 IDE 的菜单并定义其自己的工具栏。 但是，它通常有必要为一个编辑器，用于定义其自己特定的命令，除了使用 IDE 的标准命令集。 若要执行此操作，你的编辑器必须声明其使用，然后在.vsct 文件中定义任何新的命令、 上下文菜单中，顶级菜单和工具栏的标准命令。 如果您创建就地激活编辑器，然后实现<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>，并为而不是使用 OLE 2 菜单合并的.vsct 文件中的编辑器中定义的菜单和工具栏。  
  
- 若要防止出现拥挤的 UI 中的菜单命令，您应使用现有的命令在 IDE 中创建新的命令之前。 共享的命令 SharedCmdDef.vsct 和 ShellCmdDef.vsct 中定义。 这些文件安装的 VisualStudioIntegration\Common\Inc 子目录中的默认情况下你[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]安装。  
  
- `ISelectionContainer` 可以表示单个和多个选择。 每个所选的对象作为`IDispatch`对象。  
  
- IDE 实现`IOleUndoManager`作为一项服务可从访问<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>或作为一个对象，可以通过实例化<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>。 编辑器实现`IOleUndoUnit`为每个接口`Undo`操作。  
  
- 有两个位置的自定义编辑器可以公开自动化对象：  
  
  - `Document.Object`  

  - `Window.Object`  
  
## <a name="see-also"></a>请参阅  
 [参与自动化模型](../extensibility/internals/contributing-to-the-automation-model.md)   
 [如何：为编辑器提供上下文](../extensibility/how-to-provide-context-for-editors.md)
