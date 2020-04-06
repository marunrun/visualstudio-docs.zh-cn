---
title: 演练：向自定义编辑器添加功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b145dd4d82887122009553afd883abb6cade849e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697790"
---
# <a name="walkthrough-add-features-to-a-custom-editor"></a>演练：向自定义编辑器添加功能
创建自定义编辑器后，可以向其添加更多功能。

## <a name="to-create-an-editor-for-a-vspackage"></a>为 VS 包创建编辑器

1. 使用可视化工作室包项目模板创建自定义编辑器。

     有关详细信息，请参阅[演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)。

2. 确定是希望编辑器支持单个视图还是多个视图。

     支持 **"新建窗口"** 命令或具有窗体视图和代码视图的编辑器需要单独的文档数据对象和文档视图对象。 在仅支持单个视图的编辑器中，文档数据对象和文档视图对象可以在同一对象上实现。

     有关多个视图的示例，请参阅[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

3. 通过设置<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>接口实现编辑器工厂。

     有关详细信息，请参阅[编辑器工厂](../extensibility/editor-factories.md)。

4. 确定是希望编辑器使用就地激活还是简化嵌入来管理文档视图对象窗口。

     简化的嵌入编辑器窗口承载标准文档视图，而就地激活编辑器窗口将 ActiveX 控件或其他活动对象作为文档视图。 有关详细信息，请参阅[简化嵌入](../extensibility/simplified-embedding.md)和[就地激活](/visualstudio/misc/in-place-activation?view=vs-2015)。

5. 实现接口<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>来处理命令。

6. 提供文档持久性和对外部文件更改的响应：

    1. 要保留该文件，请实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>编辑器<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>的文档数据对象。

    2. 要响应外部文件更改，请实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx>编辑器<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>的文档数据对象并在其上实现。

        > [!NOTE]
        > 调用`QueryService`<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>以获取指向`IVsFileChangeEx`的指针。

7. 使用源代码控制协调文档编辑事件。 执行以下步骤:

    1. 通过调用`IVsQueryEditQuerySave2``QueryService`<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>获取指向 的指针。

    2. 当发生第一个编辑事件时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>调用 方法。

         此方法会提示用户签出该文件（如果该文件尚未签出）。请务必处理"文件未签出"条件以避免错误。

    3. 同样，在保存文件之前，调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A>方法。

         此方法会提示用户保存文件（如果该文件尚未保存或自上次保存以来已更改）。

8. 使 **"属性"** 窗口能够显示编辑器中选择的文本的属性。 执行以下步骤:

    1. 每次<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A>文本选择更改时调用 ，传入您的实现<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>中。

    2. 调用`QueryService`服务<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>以获取指向<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>的指针。

9. 允许用户在编辑器和**工具箱**之间，或在外部编辑器（如 Microsoft Word）和**工具箱**之间拖放项目。 执行以下步骤:

    1. 在`IDropTarget`编辑器上实现，以提醒 IDE 编辑器是放置目标。

    2. 在视图<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>上实现界面，以便编辑器可以启用和禁用**工具箱**中的项目。

    3. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A>并调用`QueryService`<xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox>服务以获取指向<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3>接口的指针。

         这些步骤使 VSPackage 能够将新项目添加到**工具箱**。

10. 决定是否需要编辑器的任何其他可选功能。

    - 如果希望编辑器支持查找和替换命令，请实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>。

    - 如果要在编辑器中使用文档大纲工具窗口，请实现`IVsDocOutlineProvider`。

    - 如果要在<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>编辑器中使用状态栏，请实现和调用`QueryService`<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>以获取指向`IVsStatusBar`的指针。

         例如，编辑器可以显示行/列信息、选择模式（流/框）和插入模式（插入/过度击）。

    - 如果希望编辑器支持该`Undo`命令，建议的方法是使用 OLE 撤消管理器模型。 作为替代方法，您可以让编辑器直接处理该`Undo`命令。

11. 创建注册表信息，包括 VSPackage 的 GUID、菜单、编辑器和其他功能。

     下面是一个通用代码示例，您将在 *.rgs*文件脚本中放置这些代码，以演示如何正确注册编辑器。

    ```csharp
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

12. 实施上下文相关的帮助支持。

     此步骤允许您为编辑器中的项目提供 F1 帮助和动态帮助窗口支持。 有关详细信息，请参阅[如何：为编辑器提供上下文](/visualstudio/extensibility/how-to-provide-context-for-editors?view=vs-2015)。

13. 通过实现接口，`IDispatch`从编辑器中公开自动化对象模型。

     有关详细信息，请参阅 [Contributing to the Automation Model](../extensibility/internals/contributing-to-the-automation-model.md)。

## <a name="robust-programming"></a>可靠编程

- 当 IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A>方法时，将创建编辑器实例。 如果编辑器支持多个视图，`CreateEditorInstance`则同时创建文档数据和文档视图对象。 如果文档数据对象已打开，则将一个非空`punkDocDataExisting`值传递给`IVsEditorFactory::CreateEditorInstance`。 编辑器工厂实现必须通过查询现有文档数据对象上的相应接口来确定其是否兼容。 有关详细信息，请参阅[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

- 如果使用简化的嵌入方法，则<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>实现接口。

- 如果您决定使用就地激活，实现以下接口：

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>

   <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>

  > [!NOTE]
  > 该`IOleInPlaceComponent`接口用于避免 OLE 2 菜单合并。

   您的`IOleCommandTarget`实现处理命令，如**剪切**、**复制**和**粘贴**。 实现`IOleCommandTarget`时，决定编辑器是否需要自己的 *.vsct*文件来定义自己的命令菜单结构，或者是否可以实现 定义的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]标准命令。 通常，编辑人员使用并扩展 IDE 的菜单并定义自己的工具栏。 但是，编辑器除了使用 IDE 的标准命令集外，通常还需要定义自己的特定命令。 编辑器必须声明它使用的标准命令，然后在 *.vsct*文件中定义任何新命令、上下文菜单、顶级菜单和工具栏。 如果创建就地激活编辑器，请实现<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>和定义 *.vsct*文件中编辑器的菜单和工具栏，而不是使用 OLE 2 菜单合并。

- 为了防止菜单命令在 UI 中拥挤，在发明新命令之前，应使用 IDE 中的现有命令。 共享命令在*SharedCmdDef.vsct*和*ShellCmdDef.vsct 中*定义。 这些文件默认安装在安装[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]的 VisualStudio 集成_Common_Inc 子目录中。

- `ISelectionContainer`可以同时表示单选和多个选择。 每个选定的对象都作为对象`IDispatch`实现。

- IDE 实现`IOleUndoManager`为可从<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>或 作为对象可实例化的对象的服务<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>。 编辑器实现每个`Undo`操作`IOleUndoUnit`的接口。

- 自定义编辑器可以公开自动化对象，有两个位置：

  - `Document.Object`

  - `Window.Object`

## <a name="see-also"></a>请参阅

- [为自动化模型做出贡献](../extensibility/internals/contributing-to-the-automation-model.md)
