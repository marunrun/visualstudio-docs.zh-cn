---
title: 演练：使用带有编辑器扩展的快捷键 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 651598c0dbe746a9a26a6d60ce72b02853f98d47
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697154"
---
# <a name="walkthrough-use-a-shortcut-key-with-an-editor-extension"></a>演练：使用带有编辑器扩展的快捷键
您可以响应编辑器扩展中的快捷键。 以下演练演示如何使用快捷键向文本视图添加视图修饰。 本演练基于视口修饰编辑器模板，它允许您使用 + 字符添加修饰。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建托管扩展框架 （MEF） 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`KeyBindingTest`。

2. 向项目添加编辑器文本修饰项模板并将其`KeyBindingTest`命名。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 添加以下引用并将**CopyLocal**设置为`false`：

    微软.VisualStudio.编辑器

    微软.VisualStudio.OLE.Interop

    微软.VisualStudio.shell.14.0

    微软.VisualStudio.文本管理器.互通

   在 KeyBindingTest 类文件中，将类名称更改为紫色CornerBox。 使用左侧边距中显示的灯泡进行其他适当的更改。 在构造函数中，将修饰图层的名称从**键绑定测试**更改为**紫色CornerBox：**

```csharp
this.layer = view.GetAdornmentLayer("PurpleCornerBox");
```

在KeyBindingTestTextViewCreationListener.cs类文件中，将修饰层的名称从**键绑定测试**更改为**紫色CornerBox：**

```csharp
[Export(typeof(AdornmentLayerDefinition))]
[Name("PurpleCornerBox")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
public AdornmentLayerDefinition editorAdornmentLayer;
```

## <a name="handle-typechar-command"></a>处理 TYPECHAR 命令
在 Visual Studio 2017 版本 15.6 之前，在编辑器扩展中处理命令<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>的唯一方法是实现基于命令筛选器。 Visual Studio 2017 版本 15.6 引入了一种基于编辑器命令处理程序的现代简化方法。 接下来的两节演示如何使用旧式方法和现代方法处理命令。

## <a name="define-the-command-filter-prior-to-visual-studio-2017-version-156"></a>定义命令筛选器（在 Visual Studio 2017 版本 15.6 之前）

 命令筛选器是 的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>实现，它通过实例化修饰来处理命令。

1. 添加一个类文件并将其命名为 `KeyBindingCommandFilter`。

2. 使用指令添加以下内容。

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Text.Editor;

    ```

3. 名为 KeyBinding命令筛选器的类应从<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>继承。

    ```csharp
    internal class KeyBindingCommandFilter : IOleCommandTarget
    ```

4. 为文本视图、命令链中的下一个命令添加私有字段，以及一个标志，以表示是否已添加命令筛选器。

    ```csharp
    private IWpfTextView m_textView;
    internal IOleCommandTarget m_nextTarget;
    internal bool m_added;
    internal bool m_adorned;
    ```

5. 添加设置文本视图的构造函数。

    ```csharp
    public KeyBindingCommandFilter(IWpfTextView textView)
    {
        m_textView = textView;
        m_adorned = false;
    }
    ```

6. 实现方法`QueryStatus()`如下。

    ```csharp
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
    {
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);
    }
    ```

7. 实现该方法`Exec()`，以便在键入加号 （**+**） 字符时向视图添加紫色框。

    ```csharp
    int IOleCommandTarget.Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)
    {
        if (m_adorned == false)
        {
            char typedChar = char.MinValue;

            if (pguidCmdGroup == VSConstants.VSStd2K && nCmdID == (uint)VSConstants.VSStd2KCmdID.TYPECHAR)
            {
                typedChar = (char)(ushort)Marshal.GetObjectForNativeVariant(pvaIn);
                if (typedChar.Equals('+'))
                {
                    new PurpleCornerBox(m_textView);
                    m_adorned = true;
                }
            }
        }
        return m_nextTarget.Exec(ref pguidCmdGroup, nCmdID, nCmdexecopt, pvaIn, pvaOut);
    }

    ```

## <a name="add-the-command-filter-prior-to-visual-studio-2017-version-156"></a>添加命令筛选器（在 Visual Studio 2017 版本 15.6 之前）
 修饰提供程序必须向文本视图添加命令筛选器。 在此示例中，提供程序实现<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>侦听文本视图创建事件。 此修饰提供程序还导出修饰层，该层定义修饰的 Z 顺序。

1. 在键绑定测试文本视图创建侦听器文件中，使用指令添加以下内容：

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio.Utilities;
    using Microsoft.VisualStudio.Editor;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.TextManager.Interop;

    ```

2. 要获取文本视图适配器，必须导入<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>。

    ```csharp
    [Import(typeof(IVsEditorAdaptersFactoryService))]
    internal IVsEditorAdaptersFactoryService editorFactory = null;

    ```

3. 更改<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>方法以便添加 。 `KeyBindingCommandFilter`

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));
    }
    ```

4. 处理程序`AddCommandFilter`获取文本视图适配器并添加命令筛选器。

    ```csharp
    void AddCommandFilter(IWpfTextView textView, KeyBindingCommandFilter commandFilter)
    {
        if (commandFilter.m_added == false)
        {
            //get the view adapter from the editor factory
            IOleCommandTarget next;
            IVsTextView view = editorFactory.GetViewAdapter(textView);

            int hr = view.AddCommandFilter(commandFilter, out next);

            if (hr == VSConstants.S_OK)
            {
                commandFilter.m_added = true;
                 //you'll need the next target for Exec and QueryStatus
                if (next != null)
                commandFilter.m_nextTarget = next;
            }
        }
    }
    ```

## <a name="implement-a-command-handler-starting-in-visual-studio-2017-version-156"></a>实现命令处理程序（从 Visual Studio 2017 版本 15.6 开始）

首先，更新项目的 Nuget 引用以引用最新的编辑器 API：

1. 右键单击项目并选择 **"管理 Nuget 包**"。

2. 在**Nuget 包管理器**中，选择"**更新**"选项卡，**选择"选择所有包**"复选框，然后选择 **"更新**"。

命令处理程序是 的<xref:Microsoft.VisualStudio.Commanding.ICommandHandler%601>实现，它通过实例化修饰来处理命令。

1. 添加一个类文件并将其命名为 `KeyBindingCommandHandler`。

2. 使用指令添加以下内容。

   ```csharp
   using Microsoft.VisualStudio.Commanding;
   using Microsoft.VisualStudio.Text.Editor;
   using Microsoft.VisualStudio.Text.Editor.Commanding.Commands;
   using Microsoft.VisualStudio.Utilities;
   using System.ComponentModel.Composition;
   ```

3. 名为 KeyBindingCommandHandler 的类应`ICommandHandler<TypeCharCommandArgs>`从 继承，并将其<xref:Microsoft.VisualStudio.Commanding.ICommandHandler>导出为 ：

   ```csharp
   [Export(typeof(ICommandHandler))]
   [ContentType("text")]
   [Name("KeyBindingTest")]
   internal class KeyBindingCommandHandler : ICommandHandler<TypeCharCommandArgs>
   ```

4. 添加命令处理程序的显示名称：

   ```csharp
   public string DisplayName => "KeyBindingTest";
   ```

5. 实现方法`GetCommandState()`如下。 由于此命令处理程序处理核心编辑器 TYPECHAR 命令，因此可以将启用该命令委派给核心编辑器。

   ```csharp
   public CommandState GetCommandState(TypeCharCommandArgs args)
   {
       return CommandState.Unspecified;
   }
   ```

6. 实现该方法`ExecuteCommand()`，以便在键入加号 （**+**） 字符时向视图添加紫色框。

   ```csharp
   public bool ExecuteCommand(TypeCharCommandArgs args, CommandExecutionContext executionContext)
   {
       if (args.TypedChar == '+')
       {
           bool alreadyAdorned = args.TextView.Properties.TryGetProperty(
               "KeyBindingTextAdorned", out bool adorned) && adorned;
           if (!alreadyAdorned)
           {
               new PurpleCornerBox((IWpfTextView)args.TextView);
               args.TextView.Properties.AddProperty("KeyBindingTextAdorned", true);
           }
       }

       return false;
   }
   ```

   7. 将修饰图层定义从*KeyBindingTestTextViewCreationListener.cs*文件复制到*KeyBindingCommandHandler.cs，* 然后删除*KeyBindingTestTextViewCreationListener.cs*文件：

   ```csharp
   /// <summary>
   /// Defines the adornment layer for the adornment. This layer is ordered
   /// after the selection layer in the Z-order.
   /// </summary>
   [Export(typeof(AdornmentLayerDefinition))]
   [Name("PurpleCornerBox")]
   [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
   private AdornmentLayerDefinition editorAdornmentLayer;
   ```

## <a name="make-the-adornment-appear-on-every-line"></a>使修饰出现在每行上

原始修饰出现在文本文件中的每个字符"a"上。 现在，我们更改了代码以添加修饰以响应**+** 该字符，它仅在键入字符的**+** 行上添加修饰。 我们可以更改修饰代码，以便修饰再次出现在每个"a"上。

在*KeyBindingTest.cs*文件中，更改`CreateVisuals()`方法以遍转视图中的所有行以修饰"a"字符。

```csharp
private void CreateVisuals(ITextViewLine line)
{
    IWpfTextViewLineCollection textViewLines = this.view.TextViewLines;

    foreach (ITextViewLine textViewLine in textViewLines)
    {
        if (textViewLine.ToString().Contains("a"))
        {
            // Loop through each character, and place a box around any 'a'
            for (int charIndex = textViewLine.Start; charIndex < textViewLine.End; charIndex++)
            {
                if (this.view.TextSnapshot[charIndex] == 'a')
                {
                    SnapshotSpan span = new SnapshotSpan(this.view.TextSnapshot, Span.FromBounds(charIndex, charIndex + 1));
                    Geometry geometry = textViewLines.GetMarkerGeometry(span);
                    if (geometry != null)
                    {
                        var drawing = new GeometryDrawing(this.brush, this.pen, geometry);
                        drawing.Freeze();

                        var drawingImage = new DrawingImage(drawing);
                        drawingImage.Freeze();

                        var image = new Image
                        {
                            Source = drawingImage,
                        };

                        // Align the image with the top of the bounds of the text geometry
                        Canvas.SetLeft(image, geometry.Bounds.Left);
                        Canvas.SetTop(image, geometry.Bounds.Top);

                        this.layer.AddAdornment(AdornmentPositioningBehavior.TextRelative, span, null, image, null);
                    }
                }
            }
        }
    }
}
```

## <a name="build-and-test-the-code"></a>生成和测试代码

1. 构建密钥绑定测试解决方案并在实验实例中运行它。

2. 创建或打开文本文件。 键入一些包含字符"a"的单词，然后在文本**+** 视图中键入任意位置。

     文件中的每个"a"字符上都应出现紫色方块。
