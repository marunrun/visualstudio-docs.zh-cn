---
title: 演练：将内容类型链接到的文件扩展名 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e402979dc5b76b8693a4be7a80a3d5d98f889616
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66320674"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>演练：将内容类型链接到的文件扩展名
您可以定义您自己的内容类型和使用的编辑器 Managed Extensibility Framework (MEF) 扩展链接到它的文件扩展名。 在某些情况下，文件扩展名已由语言服务定义。 但是，若要使用 MEF 中使用它，你必须仍将其链接到内容类型。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，不要从下载中心安装 Visual Studio SDK。 它包含作为 Visual Studio 安装程序中的可选功能。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建一个 C# VSIX 项目。 (在**新的项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名为 `ContentTypeTest`。

2. 在中**source.extension.vsixmanifest**文件中，转到**资产**选项卡，并将**类型**字段**Microsoft.VisualStudio.MefComponent**，则**源**字段**当前解决方案中的项目**，和**项目**字段的项目的名称。

## <a name="define-the-content-type"></a>将内容类型定义

1. 添加一个类文件并将其命名为 `FileAndContentTypes`。

2. 添加对下列程序集的引用：

    1. System.ComponentModel.Composition

    2. Microsoft.VisualStudio.Text.Logic

    3. Microsoft.VisualStudio.CoreUtility

3. 以下代码添加到`using`指令。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Utilities;

    ```

4. 声明一个静态类，包含的定义。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {. . .}
    ```

5. 在此类中，导出<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>名为"隐藏"，并声明其基本定义为"text"。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
        [Export]
        [Name("hid")]
        [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;
    }
    ```

## <a name="link-a-file-name-extension-to-a-content-type"></a>链接到内容类型的文件扩展名

- 若要将此内容类型映射到的文件扩展名，将导出<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>具有扩展名 *.hid*和内容类型"隐藏"。

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

## <a name="add-the-content-type-to-an-editor-export"></a>将内容类型添加到编辑器导出

1. 创建编辑器扩展。 例如，可以使用中所述的边距标志符号扩展[演练：创建边缘字形](../extensibility/walkthrough-creating-a-margin-glyph.md)。

2. 添加在此过程中定义的类。

3. 在导出的扩展类时，将添加<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"隐藏"到它的类型。

    ```csharp
    [Export]
    [ContentType("hid")]
    ```

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)