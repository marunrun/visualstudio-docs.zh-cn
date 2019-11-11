---
title: 演练：向自定义编辑器添加功能 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5fa926b21171c3e09b5a0f4d74e9415da090bf2f
ms.sourcegitcommit: 97623fd6190c43fed0d2ee7af92b01c375282622
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73569080"
---
# <a name="walkthrough-add-features-to-a-custom-editor"></a>演练：向自定义编辑器添加功能
创建自定义编辑器后，可以向其添加更多功能。

## <a name="to-create-an-editor-for-a-vspackage"></a>为 VSPackage 创建编辑器

1. 使用 Visual Studio 包项目模板创建自定义编辑器。

     有关详细信息，请参阅[演练：创建自定义编辑器](../extensibility/walkthrough-creating-a-custom-editor.md)。

2. 决定您是否希望您的编辑器支持一个或多个视图。

     支持**新的窗口**命令或具有窗体视图和代码视图的编辑器需要单独的文档数据对象和文档视图对象。 在仅支持一个视图的编辑器中，可以在同一对象上实现文档数据对象和文档视图对象。

     有关多个视图的示例，请参阅[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

3. 通过设置 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> 接口实现编辑器工厂。

     有关详细信息，请参阅[编辑器工厂](../extensibility/editor-factories.md)。

4. 决定您是否希望编辑器使用就地激活或简化嵌入来管理文档视图对象窗口。

     简化的嵌入编辑器窗口承载标准文档视图，而就地激活编辑器窗口承载 ActiveX 控件或其他活动对象作为其文档视图。 有关详细信息，请参阅[简化的嵌入](../extensibility/simplified-embedding.md)和[就地激活](/visualstudio/misc/in-place-activation?view=vs-2015)。

5. 实现用于处理命令的 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口。

6. 提供文档持久性和对外部文件更改的响应：

    1. 若要保存文件，请在编辑器的文档数据对象上实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>。

    2. 若要响应外部文件更改，请在编辑器的文档数据对象上实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>。

        > [!NOTE]
        > 对 <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> 调用 `QueryService`，以获取指向 `IVsFileChangeEx`的指针。

7. 用源代码管理协调文档编辑事件。 请执行这些步骤：

    1. 通过对 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>调用 `QueryService` 来获取指向 `IVsQueryEditQuerySave2` 的指针。

    2. 第一个编辑事件发生时，调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 方法。

         如果文件尚未签出，此方法会提示用户签出文件。务必处理 "未签出的文件" 条件以避免出现错误。

    3. 同样，在保存文件之前，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> 方法。

         如果文件尚未保存或自上次保存后发生更改，则此方法将提示用户保存该文件。

8. 启用 "**属性**" 窗口，以显示在编辑器中选定的文本的属性。 请执行这些步骤：

    1. <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 每次文本选择更改时调用，并传入 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>的实现。

    2. 对 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> 服务调用 `QueryService`，以获取指向 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>的指针。

9. 使用户能够在编辑器和**工具箱**之间，或在外部编辑器（如 Microsoft Word）和**工具箱**之间拖放项。 请执行这些步骤：

    1. 在编辑器上实现 `IDropTarget`，以提醒 IDE 编辑器是拖放目标。

    2. 在视图上实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser> 接口，以便您的编辑器能够启用和禁用 "**工具箱**" 中的项。

    3. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A> 并对 <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> 服务调用 `QueryService` 以获取指向 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> 接口的指针。

         这些步骤使你的 VSPackage 可以将新项添加到 "**工具箱**"。

10. 确定是否要为编辑器提供任何其他可选功能。

    - 如果希望编辑器支持 "查找和替换" 命令，请实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>。

    - 如果要在编辑器中使用文档大纲工具窗口，请实现 `IVsDocOutlineProvider`。

    - 如果要在编辑器中使用状态栏，请实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> 并为 <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> 调用 `QueryService` 以获取指向 `IVsStatusBar`的指针。

         例如，编辑器可以显示行/列信息、选择模式（流/框）和插入模式（insert/替换）。

    - 如果希望编辑器支持 `Undo` 命令，推荐的方法是使用 OLE 撤消管理器模型。 作为替代方法，您可以让编辑器直接处理 `Undo` 命令。

11. 创建注册表信息，包括 VSPackage 的 Guid、菜单、编辑器和其他功能。

     下面是一个一般的代码示例，你可以将其放入 *.rgs*文件脚本以演示如何正确注册编辑器。

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

12. 实现区分上下文的帮助支持。

     此步骤允许您在编辑器中为项提供 F1 帮助和动态帮助窗口支持。 有关详细信息，请参阅[如何：为编辑器提供上下文](/visualstudio/extensibility/how-to-provide-context-for-editors?view=vs-2015)。

13. 通过实现 `IDispatch` 接口，从编辑器中公开自动化对象模型。

     有关详细信息，请参阅 [Contributing to the Automation Model](../extensibility/internals/contributing-to-the-automation-model.md)。

## <a name="robust-programming"></a>可靠编程

- 编辑器实例是在 IDE 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 方法时创建的。 如果编辑器支持多个视图，`CreateEditorInstance` 将同时创建文档数据和文档视图对象。 如果文档数据对象已打开，则将一个非 null `punkDocDataExisting` 值传递到 `IVsEditorFactory::CreateEditorInstance`。 您的编辑器工厂实现必须通过查询其上的相应接口来确定现有文档数据对象是否兼容。 有关详细信息，请参阅[支持多个文档视图](../extensibility/supporting-multiple-document-views.md)。

- 如果使用简化的嵌入方法，则实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 接口。

- 如果决定使用就地激活，请实现以下接口：

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>

   <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>

  > [!NOTE]
  > `IOleInPlaceComponent` 接口用于避免 OLE 2 菜单合并。

   `IOleCommandTarget` 实现处理**剪切**、**复制**和**粘贴**等命令。 在实现 `IOleCommandTarget`时，确定编辑器是否需要 *.vsct*文件来定义其自己的命令菜单结构，或者是否可以实现 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]定义的标准命令。 通常，编辑器使用和扩展 IDE 的菜单，并定义自己的工具栏。 但是，除了使用 IDE 的标准命令集外，编辑器还需要定义自己的特定命令。 编辑器必须声明它使用的标准命令，然后在 *.vsct*文件中定义任何新命令、上下文菜单、顶级菜单和工具栏。 如果创建就地激活编辑器，请在 *.vsct*文件中实现 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> 并为编辑器定义菜单和工具栏，而不是使用 OLE 2 菜单合并。

- 若要在 UI 中阻止菜单命令 crowding，应在发明新命令之前使用 IDE 中的现有命令。 共享命令在*SharedCmdDef. .vsct*和*ShellCmdDef*中定义。 默认情况下，这些文件安装在 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 安装的 VisualStudioIntegration\Common\Inc 子目录中。

- `ISelectionContainer` 可以表达单个和多个选择。 每个所选对象均作为 `IDispatch` 对象实现。

- IDE 将 `IOleUndoManager` 作为可从 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> 访问的服务，或实现为可通过 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>实例化的对象。 编辑器实现每个 `Undo` 操作的 `IOleUndoUnit` 接口。

- 自定义编辑器可以使用以下两个位置公开自动化对象：

  - `Document.Object`

  - `Window.Object`

## <a name="see-also"></a>请参阅

- [参与自动化模型](../extensibility/internals/contributing-to-the-automation-model.md)