---
title: 演练：创建代码片段
ms.date: 06/10/2019
ms.topic: conceptual
helpviewer_keywords:
- code snippets, creating
- code snippets, shortcut
- code snippets, template
- code snippets, replacements
- code snippets, references
- code snippets, imports
ms.assetid: 0dcaae11-39cf-4463-9c90-2494321251c2
author: jillre
ms.author: jillfra
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: fb76fd61cb06b2877ebe0cd1714610b25845ebc0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72647136"
---
# <a name="walkthrough-create-a-code-snippet"></a>演练：创建代码片段

只需几步操作即可创建代码片段。 你需要做的就是创建一个 XML 文件，填写适当的元素，并向其中添加代码。 可以选择使用替换参数和项目引用。 在“代码片段管理器”（“工具” > “代码片段管理器”）中使用“导入”按钮向 Visual Studio 的安装导入代码片段     。

## <a name="snippet-template"></a>代码片段模板

以下 XML 是基本代码片段模板：

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
    <CodeSnippet Format="1.0.0">
        <Header>
            <Title></Title>
        </Header>
        <Snippet>
            <Code Language="">
                <![CDATA[]]>
            </Code>
        </Snippet>
    </CodeSnippet>
</CodeSnippets>
```

## <a name="create-a-code-snippet"></a>创建代码片段

1. 在 Visual Studio 中创建新的 XML 文件，然后添加如上所示的模板。

2. 在 Title 元素中填写代码片段的标题  。 使用标题 Square Root  。

3. 在 Code  元素的“语言”  属性中填写代码片段的语言。 对于 C#，使用 CSharp，对于 Visual Basic，使用 VB   。

   > [!TIP]
   > 要查看所有可用语言值，请浏览[代码片段架构引用](code-snippets-schema-reference.md)页上的[代码元素属性部分](code-snippets-schema-reference.md#attributes)。

4. 在 Code 元素中的 CDATA 部分内添加代码片段   。

   对于 C#：

   ```xml
   <Code Language="CSharp">
       <![CDATA[double root = Math.Sqrt(16);]]>
   </Code>
   ```

   或者，对于 Visual Basic：

   ```xml
   <Code Language="VB">
       <![CDATA[Dim root = Math.Sqrt(16)]]>
   </Code>
   ```

   > [!NOTE]
   > 无法指定如何对代码片段 CDATA 部分中的代码行执行缩进或格式设置。  插入后，语言服务将自动设置所插入代码的格式。

5. 将代码片段保存为 SquareRoot.snippet（可将其保存在任何位置）  。

## <a name="import-a-code-snippet"></a>导入代码片段

1. 可以使用“代码片段管理器”将代码片段导入到 Visual Studio 安装  。 通过选择“工具” > “代码片段管理器”打开它   。

2. 单击“导入”按钮  。

3. 请转到在前面的过程中保存代码片段的位置，选择该位置，然后单击“打开”  。

4. “导入代码片段”对话框随即打开，要求从右窗格中提供的选项中选择代码片段的添加位置  。 其中一个选项应为“我的代码片段”  。 选择它，单击“完成”，然后单击“确定”   。

5. 代码片段会复制到以下某一位置，具体取决于代码语言：

   ::: moniker range="vs-2017"

   *%USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\Visual C#\My Code Snippets*
    *%USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\Visual Basic\My Code Snippets*

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   *%USERPROFILE%\Documents\Visual Studio 2019\Code Snippets\Visual C#\My Code Snippets*
    *%USERPROFILE%\Documents\Visual Studio 2019\Code Snippets\Visual Basic\My Code Snippets*

   ::: moniker-end

6. 通过打开 C# 或 Visual Basic 项目来测试代码片段。 在编辑器中打开一个代码文件之后，依次选择右键单击菜单中的“代码片段” > “插入代码片段”，再选择“我的代码片段”    。 应看到一个名为 Square Root 的代码片段  。 双击该选项。

   该代码片段代码已插入代码文件中。

## <a name="description-and-shortcut-fields"></a>“说明”和“快捷方式”字段

::: moniker range="vs-2017"

1. 在“代码片段管理器”中查看“说明”字段时，可以获得有关代码片段的详细信息。 快捷方式是用户为插入代码片段而键入的标记。 通过打开文件 %USERPROFILE%\Documents\Visual Studio 2017\Code Snippets\\[Visual C# 或 Visual Basic]\My Code Snippet\SquareRoot.snippet，编辑已添加的代码片段  。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在“代码片段管理器”中查看“说明”字段时，可以获得有关代码片段的详细信息。 快捷方式是用户为插入代码片段而键入的标记。 通过打开文件 %USERPROFILE%\Documents\Visual Studio 2019\Code Snippets\\[Visual C# 或 Visual Basic]\My Code Snippet\SquareRoot.snippet，编辑已添加的代码片段  。

::: moniker-end

   > [!TIP]
   > 由于要编辑在其中放置 Visual Studio 的目录中的文件，因此无需重新将其导入到 Visual Studio。

2. 将 Author  和 Description  元素添加到 Header  元素，并填写。

3. Header  元素应该类似于以下形式：

   ```xml
   <Header>
       <Title>Square Root</Title>
       <Author>Myself</Author>
       <Description>Calculates the square root of 16.</Description>
   </Header>
   ```

4. 打开“代码片段管理器”  并选择代码片段。 在右窗格中，注意“说明”和“创建者”字段现在已填充   。

   ![代码片段管理器中的代码片段说明](media/code-snippet-description-author.png)

5. 要添加快捷方式，请在 Header 元素中添加 Shortcut 元素   ：

   ```xml
   <Header>
      <Title>Square Root</Title>
      <Author>Myself</Author>
      <Description>Calculates the square root of 16.</Description>
      <Shortcut>sqrt</Shortcut>
    </Header>
   ```

6. 再次保存代码片段文件。

7. 要测试快捷方式，请打开之前使用的项目，在编辑器中键入 sqrt 并按 Tab（Visual Basic 按一次，C# 按两次）   。

   代码片段代码已插入。

## <a name="replacement-parameters"></a>替换参数

你可能希望用户替换部分代码片段。 例如，可能希望用户将变量名称替换为其当前项目中的某个名称。 可以提供两种类型的替换：文本和对象。 使用 [Literal 元素](code-snippets-schema-reference.md#literal-element)标识整体包含在代码片段中、但在插入到代码中后可能会进行自定义的代码部分的替换对象（例如字符串或数值）。 使用 [Object 元素](code-snippets-schema-reference.md#object-element)标识代码片段所需的、但可能是在代码片段外部定义的项（例如对象实例或控件）。

1. 要使用户可以轻松替换数字以计算平方根，请按如下所示修改 SquareRoot.snippet 文件的 Snippet 元素   ：

   ```xml
   <Snippet>
     <Code Language="CSharp">
       <![CDATA[double root = Math.Sqrt($Number$);]]>
     </Code>
     <Declarations>
       <Literal>
         <ID>Number</ID>
         <ToolTip>Choose the number you want the square root of.</ToolTip>
         <Default>16</Default>
       </Literal>
     </Declarations>
   </Snippet>
   ```

   请注意，文本替换是给定的 ID (`Number`)。 此 ID 在代码片段中引用，用 `$` 字符括起来：

   ```xml
   <![CDATA[double root = Math.Sqrt($Number$);]]>
   ```

2. 保存片段文件。

3. 打开项目，并插入片段。

   已插入代码片段，并且突出显示要替换的可编辑文本。 将鼠标悬停在替换参数上，以查看该值的工具提示。

   ![Visual Studio 中的代码片段替换参数工具提示](media/snippet-replacement-parameter-tooltip.png)

   > [!TIP]
   > 如果片段中有多个可替换的参数，可按 Tab，从一个参数导航到另一个参数，以更改值  。

## <a name="import-a-namespace"></a>导入命名空间

可通过包含 [Imports 元素](code-snippets-schema-reference.md#imports-element)，使用代码片段添加 `using` 指令 (C#) 或 `Imports` 语句 (Visual Basic)。 对于 .NET Framework 项目，还可以通过使用 [References 元素](code-snippets-schema-reference.md#references-element)将引用添加到项目。

以下 XML 显示在 System.IO 命名空间中使用 `File.Exists` 方法的代码片段，因此可定义 Imports 元素，以导入 System.IO 命名空间  。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippets xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
  <CodeSnippet Format="1.0.0">
    <Header>
      <Title>File Exists</Title>
      <Shortcut>exists</Shortcut>
    </Header>
    <Snippet>
      <Code Language="CSharp">
        <![CDATA[var exists = File.Exists("C:\\Temp\\Notes.txt");]]>
      </Code>
      <Imports>
        <Import>
          <Namespace>System.IO</Namespace>
        </Import>
      </Imports>
    </Snippet>
  </CodeSnippet>
</CodeSnippets>
```

## <a name="see-also"></a>请参阅

- [代码片段架构参考](../ide/code-snippets-schema-reference.md)
