---
title: 演练：在编辑器扩展中使用快捷键 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
caps.latest.revision: 33
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5c9cb20bafa552c47a2f599d12e6b66fdb2bde59
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201947"
---
# <a name="walkthrough-using-a-shortcut-key-with-an-editor-extension"></a>演练：在编辑器扩展中使用快捷键
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以在编辑器扩展中响应快捷键。 下面的演练演示如何使用快捷键将视图修饰添加到文本视图。 本演练基于视口修饰编辑器模板，它允许您使用 + 字符添加修饰。  
  
## <a name="prerequisites"></a>必备条件  
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目  
  
1. 创建 c # VSIX 项目。  (在 " **新建项目** " 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。 ) 将解决方案命名为 `KeyBindingTest` 。  
  
2. 将编辑器文本修饰项模板添加到项目并将其命名为 `KeyBindingTest` 。 有关详细信息，请参阅 [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。  
  
3. 添加以下引用，并将 **CopyLocal** 设置为 `false` ：  
  
    VisualStudio  
  
    VisualStudio。  
  
    VisualStudio。14。0  
  
    VisualStudio. TextManager  
  
   在 KeyBindingTest 类文件中，将类名称更改为 PurpleCornerBox。 使用左侧空白处显示的灯泡来进行其他适当的更改。 在构造函数中，将修饰层的名称从 " **KeyBindingTest** " 更改为 " **PurpleCornerBox**"：  
  
```csharp  
this.layer = view.GetAdornmentLayer("PurpleCornerBox");  
```  
  
## <a name="defining-the-command-filter"></a>定义命令筛选器  
 命令筛选器是的实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ，它通过实例化修饰来处理命令。  
  
1. 添加一个类文件并将其命名为 `KeyBindingCommandFilter`。  
  
2. 添加下面的 using 语句。  
  
    ```csharp  
    using System;  
    using System.Runtime.InteropServices;  
    using Microsoft.VisualStudio.OLE.Interop;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Text.Editor;  
  
    ```  
  
3. 名为 KeyBindingCommandFilter 的类应继承自 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。  
  
    ```csharp  
    internal class KeyBindingCommandFilter : IOleCommandTarget  
    ```  
  
4. 为文本视图、命令链中的下一个命令添加私有字段，并添加一个标志来表示是否已添加命令筛选器。  
  
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
  
6. 实现 `QueryStatus()` 方法，如下所示。  
  
    ```vb  
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)  
    {  
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);  
    }  
    ```  
  
7. 实现 `Exec()` 方法，以便在键入 + 字符时将紫色框添加到视图中。  
  
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
  
## <a name="adding-the-command-filter"></a>添加命令筛选器  
 修饰提供程序必须向文本视图添加命令筛选器。 在此示例中，提供程序实现 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> 以侦听文本视图创建事件。 此修饰提供程序还导出修饰层，修饰层定义修饰的 Z 顺序。  
  
1. 在 KeyBindingTestTextViewCreationListener 文件中，添加以下 using 语句：  
  
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
  
2. 在修饰层定义中，将 AdornmentLayer 的名称从 **KeyBindingTest** 更改为 **PurpleCornerBox**。  
  
    ```csharp  
    [Export(typeof(AdornmentLayerDefinition))]  
    [Name("PurpleCornerBox")]  
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
    public AdornmentLayerDefinition editorAdornmentLayer;  
    ```  
  
3. 若要获取文本视图适配器，必须导入 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> 。  
  
    ```csharp  
    [Import(typeof(IVsEditorAdaptersFactoryService))]  
    internal IVsEditorAdaptersFactoryService editorFactory = null;  
  
    ```  
  
4. 更改 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> 方法，使其添加 `KeyBindingCommandFilter` 。  
  
    ```csharp  
    public void TextViewCreated(IWpfTextView textView)  
    {  
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));  
    }  
    ```  
  
5. `AddCommandFilter`处理程序获取文本视图适配器并添加命令筛选器。  
  
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
  
## <a name="making-the-adornment-appear-on-every-line"></a>使修饰出现在每一行上  
 原始修饰出现在文本文件中的每个字符 "a" 上。 现在，我们已更改代码以添加修饰以响应 "+" 字符，它只会在类型为 "+" 的行中添加修饰。 我们可以更改修饰代码，以便修饰每个 "a" 上出现一次。  
  
 在 KeyBindingTest.cs 文件中，更改问题解答 ( # A1 方法，以循环访问视图中的所有行来修饰 "a" 字符。  
  
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
  
## <a name="building-and-testing-the-code"></a>生成和测试代码  
  
1. 生成 KeyBindingTest 解决方案并在实验实例中运行它。  
  
2. 创建或打开一个文本文件。 键入包含字符 "a" 的一些字词，然后在文本视图中的任意位置键入 "+"。  
  
     文件中的每个 "a" 字符上都应出现紫色正方形。
