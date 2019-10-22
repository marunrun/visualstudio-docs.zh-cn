---
title: 如何：分发代码片段 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code snippets, distributing
ms.assetid: 5f717abd-e167-47ae-818c-6b0bae100ceb
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2c080f1b5d4b36093cca44daaac644276039718e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667955"
---
# <a name="how-to-distribute-code-snippets"></a>如何：分发代码段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以只向朋友提供代码片段，然后让他们使用代码片段管理器在自己的计算机上安装代码片段。 但是，如果你有若干代码片段要分发或者希望进行范围更广泛的分发，则可以将代码片段文件包含到 Visual Studio 扩展中，用户可以安装该扩展。

 要创建 Visual Studio 扩展，你必须安装 Visual Studio SDK。 在[Visual studio 2015 下载](http://www.visualstudio.com/downloads/visual-studio-2015-downloads-vs.aspx)中查找与 visual studio 安装匹配的 VSSDK 版本。

## <a name="setting-up-the-extension"></a>设置扩展
 在此过程中，将使用在[演练：创建代码片段](../ide/walkthrough-creating-a-code-snippet.md)中创建的相同 Hello World 代码片段。 我们将提供 .snippet 文本，因此无需返回该演练并获取相关代码片段。

1. 创建名为 **TestSnippet** 的新 VSIX 项目。 （“文件”->“新建”->“项目”->“Visual C#”（或“Visual Basic”）->“扩展性”）

2. 在 **TestSnippet** 项目中，添加一个新的 XML 文件，并将其命名为 **VBCodeSnippet.snippet**。 将内容替换为以下内容：

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <CodeSnippets
        xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
      <CodeSnippet Format="1.0.0">
        <Header>
          <Title>Hello World VB</Title>
          <Shortcut>HelloWorld</Shortcut>
          <Description>Inserts code</Description>
          <Author>MSIT</Author>
          <SnippetTypes>
            <SnippetType>Expansion</SnippetType>
            <SnippetType>SurroundsWith</SnippetType>
          </SnippetTypes>
        </Header>
        <Snippet>
          <Code Language="VB">
            <![CDATA[Console.WriteLine("Hello, World!")]]>
          </Code>
        </Snippet>
      </CodeSnippet>
    </CodeSnippets>
    ```

#### <a name="setting-up-the-directory-structure"></a>设置目录结构

1. 在解决方案资源管理器中，选择项目节点，并添加一个文件夹，该文件夹的名称为你想要代码片段在代码片段管理器中显示的名称。 在本例中，应为 **HelloWorldVB**。

2. 将 .snippet 文件移动到 **HelloWorldVB** 文件夹。

3. 在“解决方案资源管理器”中选择 .snippet 文件，确保“属性”窗口中的“生成操作”设置为“内容”，“复制到输出目录”设置为“始终复制”，“包含在 VSIX 中”设置为“true”。

#### <a name="adding-the-pkgdef-file"></a>添加 .pkgdef 文件

1. 将文本文件添加到 **HelloWorldVB** 文件夹，并将其命名为 **HelloWorldVB.pkgdef**。 此文件用于向注册表添加某些项。 在本例中，它将一个新项添加到

     **HKCU\Software\Microsoft\VisualStudio\14.0\Languages\CodeExpansions\Basic**。

2. 向文件中添加以下行。

    ```
    // Visual Basic
    [$RootKey$\Languages\CodeExpansions\Basic\Paths]
    "HelloWorldVB"="$PackageFolder$"
    ```

     通过检查此项，你可以看到如何指定不同的语言。

3. 在“解决方案资源管理器”中选择 .pkgdef 文件，确保“属性”窗口中的“生成操作”设置为“内容”，“复制到输出目录”设置为“始终复制”，“包含在 VSIX 中”设置为“true”。

4. 将.pkgdef 文件添加为 VSIX 清单中的资产。 在 source.extension.vsixmanifest 文件中，转到“资产”选项卡，然后单击“新建”。

5. 在“添加新资产”对话框中，将“类型”设置为“Microsoft.VisualStudio.VsPackage”，将“类型”设置为“文件系统上的文件”，将“路径”设置为“HelloWorldVB.pkgdef”（它应显示在下拉列表中）。

### <a name="testing-the-snippet"></a>测试代码片段

1. 现在，可以确保代码片段在 Visual Studio 的实验实例中的工作。 实验实例是 Visual Studio 的第二份副本，它独立于用于编写代码的副本。 它可让在扩展上工作，而不会影响你的开发环境。

2. 生成项目并启动调试。 将显示 Visual Studio 的第二个实例。

3. 在实验实例中，请转到“工具/代码片段管理器”，并将“语言”设置为“Basic”。 将看到 HelloWorldVB 显示为一个文件夹，并且应能够展开文件夹以查看 HelloWorldVB 代码片段。

4. 测试代码片段。 在实验实例中，打开 Visual Basic 项目，并打开一个代码文件。 将光标置于代码中的某处，右键单击，然后在上下文菜单中选择“插入片段”。

5. 将看到 HelloWorldVB 显示为一个文件夹。 双击该选项。 将会看到一个弹出窗口“<插入代码片段: HellowWorldVB >”，该窗口中包含下拉列表“HelloWorldVB”。 单击 HelloWorldVB 下拉列表。 将看到添加到文件的以下行：

    ```vb
    Console.WriteLine("Hello, World!")
    ```

## <a name="see-also"></a>请参阅
 [代码片段](../ide/code-snippets.md)
