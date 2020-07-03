---
title: 演练：将内容类型链接到文件扩展名 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b4e5ba3cd82090b5fad76d48c4600e0814bd91eb
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904686"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>演练：将内容类型链接到文件扩展名
您可以定义自己的内容类型，并使用编辑器 Managed Extensibility Framework （MEF）扩展将文件扩展名链接到该类型。 在某些情况下，文件扩展名已由语言服务定义。 但是，若要将其与 MEF 一起使用，还必须将其链接到内容类型。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 c # VSIX 项目。 （在 "**新建项目**" 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。）命名解决方案 `ContentTypeTest` 。

2. 在**source.extension.vsixmanifest**文件中，中转到 "**资产**" 选项卡，并将 "**类型**" 字段设置为 " **microsoft.visualstudio.mefcomponent**"，将 "**源**" 字段设置为**当前解决方案中的项目**，将 "**项目**" 字段设置为项目的名称。

## <a name="define-the-content-type"></a>定义内容类型

1. 添加一个类文件并将其命名为 `FileAndContentTypes`。

2. 添加对下列程序集的引用：

    1. System.ComponentModel.Composition

    2. VisualStudio。

    3. VisualStudio. CoreUtility

3. 添加以下 `using` 指令。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Utilities;

    ```

4. 声明一个包含定义的静态类。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {. . .}
    ```

5. 在此类中，导出 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> 名为 "hid" 的，并将其基本定义声明为 "text"。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
        [Export]
        [Name("hid")]
        [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;
    }
    ```

## <a name="link-a-file-name-extension-to-a-content-type"></a>将文件扩展名链接到内容类型

- 若要将此内容类型映射到文件扩展名，请导出 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> 扩展名为*hid*和内容类型为 "hid" 的。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
         [Export]
         [Name("hid")]
         [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;

         [Export]
         [FileExtension(".hid")]
         [ContentType("hid")]
        internal static FileExtensionToContentTypeDefinition hiddenFileExtensionDefinition;
    }
    ```

## <a name="add-the-content-type-to-an-editor-export"></a>向编辑器导出添加内容类型

1. 创建编辑器扩展。 例如，可以使用[演练：创建边距标志符号](../extensibility/walkthrough-creating-a-margin-glyph.md)中所述的边距标志符号扩展。

2. 添加您在此过程中定义的类。

3. 导出扩展类时，请向其添加 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 类型为 "hid" 的。

    ```csharp
    [Export]
    [ContentType("hid")]
    ```

## <a name="see-also"></a>另请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
