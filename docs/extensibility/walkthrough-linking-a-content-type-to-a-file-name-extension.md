---
title: 演练：将内容类型链接到文件名扩展名 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 328be013b5d522938cd7450fc53d4866c632abb3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697067"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>演练：将内容类型链接到文件名扩展名
您可以使用编辑器托管扩展框架 （MEF） 扩展名定义自己的内容类型并将文件名扩展名链接到该扩展名。 在某些情况下，文件名扩展名已由语言服务定义。 但是，要将其与 MEF 一起使用，您仍必须将其链接到内容类型。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 C# VSIX 项目。 （在 **"新项目"** 对话框中，选择**可视化 C# / 可扩展性**，然后选择**VSIX 项目**。命名解决方案`ContentTypeTest`。

2. 在**source.扩展.vsixmanifest 文件中**，转到 **"资产**"选项卡，并将 **"类型"** 字段设置为**Microsoft.VisualStudio.Mef组件**，**将"源**"字段设置为**当前解决方案中的项目**，并将**项目**字段设置为项目名称。

## <a name="define-the-content-type"></a>定义内容类型

1. 添加一个类文件并将其命名为 `FileAndContentTypes`。

2. 添加对下列程序集的引用：

    1. System.ComponentModel.Composition

    2. 微软.VisualStudio.文本.逻辑

    3. 微软.VisualStudio.核心实用程序

3. 添加以下`using`指令。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Utilities;

    ```

4. 声明包含定义的静态类。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {. . .}
    ```

5. 在此类中，导出名为<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition>"隐藏"并将其基本定义声明为"文本"。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
        [Export]
        [Name("hid")]
        [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;
    }
    ```

## <a name="link-a-file-name-extension-to-a-content-type"></a>将文件名扩展名链接到内容类型

- 要将此内容类型映射到文件名扩展名，导出具有<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>扩展名 *.hid*和内容类型"hid"的 。

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

1. 创建编辑器扩展。 例如，您可以使用演练中描述的边距字形扩展[：创建边距字形](../extensibility/walkthrough-creating-a-margin-glyph.md)。

2. 添加在此过程中定义的类。

3. 导出扩展类时，向其添加类型<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>为"隐藏"。

    ```csharp
    [Export]
    [ContentType("hid")]
    ```

## <a name="see-also"></a>请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
