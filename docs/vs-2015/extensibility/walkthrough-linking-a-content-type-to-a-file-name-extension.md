---
title: 演练：将内容类型链接到的文件扩展名 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: beae9d0526cb9f2f294f2267a8da52d3ce3d8c08
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201997"
---
# <a name="walkthrough-linking-a-content-type-to-a-file-name-extension"></a>演练：将内容类型链接到文件扩展名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以定义您自己的内容类型，并使用编辑器 Managed Extensibility Framework (MEF) 扩展链接到它的文件扩展名。 在某些情况下，文件扩展名已定义由语言服务;不过，若要将它与 MEF 使用您仍必须将其链接到内容类型。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-mef-project"></a>创建 MEF 项目  
  
1. 创建一个 C# VSIX 项目。 (在**新的项目**对话框中，选择**Visual C# / 可扩展性**，然后**VSIX 项目**。)将解决方案命名为 `ContentTypeTest`。  
  
2. 在中**source.extension.vsixmanifest**文件中，转到**资产**选项卡，并将**类型**字段**Microsoft.VisualStudio.MefComponent**，则**源**字段**当前解决方案中的项目**，和**项目**字段的项目的名称。  
  
## <a name="defining-the-content-type"></a>定义的内容类型  
  
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
  
## <a name="linking-a-file-name-extension-to-a-content-type"></a>将文件扩展名为链接到内容类型  
  
- 若要将此内容类型映射到的文件扩展名，将导出<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition>的具有扩展名".hid"且内容类型"隐藏"。  
  
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
  
## <a name="adding-the-content-type-to-an-editor-export"></a>将内容类型添加到编辑器导出  
  
1. 创建编辑器扩展。 例如，可以使用中所述的边距标志符号扩展[演练：创建边缘字形](../extensibility/walkthrough-creating-a-margin-glyph.md)。  
  
2. 添加在此过程中定义的类。  
  
3. 在导出的扩展类时，将添加<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>的"隐藏"到它的类型。  
  
    ```csharp  
    [Export]  
    [ContentType("hid")]  
    ```  
  
## <a name="see-also"></a>请参阅  
 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
