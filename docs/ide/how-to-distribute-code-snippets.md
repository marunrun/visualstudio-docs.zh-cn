---
title: 将代码片段作为扩展分发
ms.date: 03/21/2019
ms.topic: conceptual
helpviewer_keywords:
- code snippets, distributing
ms.assetid: 5f717abd-e167-47ae-818c-6b0bae100ceb
author: jillre
ms.author: jillfra
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: 3b5ae4053e97e823952118abda11f334c5ac1083
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656071"
---
# <a name="how-to-distribute-code-snippets"></a>如何：分发代码片段

可以向朋友提供代码片段，然后让他们使用代码片段管理器在自己的计算机上安装代码片段  。 但是，如果你有若干代码片段要分发或者希望进行范围更广泛的分发，则可以将代码片段文件包含到 Visual Studio 扩展中。 然后，Visual Studio 用户可安装扩展，以获得这些片段。

## <a name="prerequisites"></a>系统必备

安装“Visual Studio 扩展开发”工作负载，以访问“VSIX 项目”项目模板   。

![“Visual Studio 扩展开发”工作负载](media/vs-2019/extension-development-workload.png)

## <a name="set-up-the-extension"></a>设置扩展

在此过程中，将使用相同的 Hello World 代码片段，该代码片段创建自[演练：创建代码片段](../ide/walkthrough-creating-a-code-snippet.md)。 本文提供了片段 XML，因此无需返回创建片段。

1. 根据“空 VSIX 项目”模板创建一个新项目，并将该项目命名为 TestSnippet   。

2. 在 **TestSnippet** 项目中，添加一个新的 XML 文件，并将其命名为 *VBCodeSnippet.snippet*。 将内容替换为以下 XML：

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

### <a name="set-up-the-directory-structure"></a>设置目录结构

1. 在解决方案资源管理器中，选择项目节点，并添加一个文件夹，该文件夹的名称为想要代码片段在代码片段管理器中显示的名称   。 在本例中，名称应为 HelloWorldVB  。

2. 将 .snippet 文件移动到 HelloWorldVB 文件夹   。

3. 在解决方案资源管理器中选择 .snippet 文件，确保“属性”窗口中的“生成操作”设置为“内容”，“复制到输出目录”设置为“始终复制”，“包含在 VSIX 中”设置为“true”          。

### <a name="add-the-pkgdef-file"></a>添加 .pkgdef 文件

::: moniker range="vs-2017"

1. 将文本文件添加到 *HelloWorldVB* 文件夹，并将其命名为 *HelloWorldVB.pkgdef*。 此文件用于向注册表添加某些项。 在这种情况下，会将新子项添加到 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Languages\CodeExpansions\Basic 密钥  。

::: moniker-end

::: moniker range=">=vs-2019"

1. 将文本文件添加到 *HelloWorldVB* 文件夹，并将其命名为 *HelloWorldVB.pkgdef*。 此文件用于向注册表添加某些项。 在这种情况下，会将新子项添加到 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Languages\CodeExpansions\Basic 密钥  。

::: moniker-end

2. 向文件中添加以下行。

    ```txt
    // Visual Basic
    [$RootKey$\Languages\CodeExpansions\Basic\Paths]
    "HelloWorldVB"="$PackageFolder$"
    ```

    通过检查此项，你可以看到如何指定不同的语言。

3. 在解决方案资源管理器中，选择 .pkgdef 文件，并在“属性”窗口中确保    ：

   - 将“生成操作”设置为“内容”  
   - 将“复制到输出目录”设置为“始终复制”  
   - 将“包含在 VSIX 中”设置为“true”  

4. 将.pkgdef 文件添加为 VSIX 清单中的资产  。 在 source.extension.vsixmanifest 文件中，转到“资产”选项卡，然后单击“新建”    。

5. 在“添加新资产”  对话框中，将“类型”  设置为“Microsoft.VisualStudio.VsPackage”  ，将“源”  设置为“文件系统上的文件”  ，将“路径”  设置为“HelloWorldVB.pkgdef”  （它应显示在下拉列表中）。

### <a name="test-the-snippet"></a>测试代码片段

1. 现在，可以确保代码片段在 Visual Studio 的实验实例中的工作。 实验实例是 Visual Studio 的第二份副本，它独立于用于编写代码的副本。 它可让在扩展上工作，而不会影响你的开发环境。

2. 生成项目并启动调试。

   将出现 Visual Studio 的第二个实例。

3. 在实验实例中，请转到“工具” > “代码片段管理器”，并将“语言”设置为“Basic”     。 将看到 HelloWorldVB 显示为一个文件夹，并且应能够展开该文件夹以查看 HelloWorldVB 代码片段   。

4. 测试代码片段。 在实验实例中，打开 Visual Basic 项目，并打开一个代码文件。 将光标置于代码中的某处，右键单击，然后在上下文菜单中选择“插入片段”  。

5. 将看到 HelloWorldVB 显示为一个文件夹  。 双击该选项。 应会看到弹出窗口插入代码段：  HelloWorldVB >，其包含“HelloWorldVB”下拉列表  。 单击 HelloWorldVB 下拉列表  。

   代码文件中添加了以下行：

    ```vb
    Console.WriteLine("Hello, World!")
    ```

## <a name="see-also"></a>请参阅

- [代码片段](../ide/code-snippets.md)