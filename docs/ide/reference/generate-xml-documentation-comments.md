---
title: 插入 XML 文档注释
ms.date: 01/22/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 20381dd78f169e2b549e077992ac0d1dc1b5c44c
ms.sourcegitcommit: 6375001ab26786af8d4d449f5846f8a49779ed18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2020
ms.locfileid: "76892126"
---
# <a name="how-to-insert-xml-comments-for-documentation-generation"></a>如何：为文档生成项插入 XML 注释

Visual Studio 可自动生成标准的 XML 文档注释结构，进而帮助记录类和方法等代码元素。 在编译时，可生成一个包含文档注释的 XML 文件。

> [!TIP]
> 若要了解如何配置已生成 XML 文件的名称和位置，请参阅[使用 XML 注释将代码文档化（C# 指南）](/dotnet/csharp/codedoc)。

可随附 .NET 程序集一并分发编译器生成的 XML 文件，让 Visual Studio 和其他 IDE 能够快速显示类型和成员信息。 此外，可以通过 [DocFX](https://dotnet.github.io/docfx/) 和 [Sandcastle](https://www.microsoft.com/download/details.aspx?id=10526) 等工具运行 XML 文件，由此生成 API 引用网站。

> [!NOTE]
> 可在 [C#](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments) 和 [Visual Basic](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation) 中使用自动插入 XML 文档注释的“插入注释”命令  。 但可在 C++ 文件中手动插入 [XML 文档注释](/cpp/build/reference/xml-documentation-visual-cpp)，这样仍可在编译时生成 XML 文档文件。

## <a name="to-insert-xml-comments-for-a-code-element"></a>若要为代码元素插入 XML 注释

1. 将文本光标放在要记录的元素上（例如，一种方法）。

2. 执行下列操作之一：

   - 在 C# 中键入 `///` 或在 Visual Basic 中键入 `'''`

   - 在“编辑”菜单上，选择“IntelliSense” > “插入注释”   

   - 在代码元素上或其正上方的右键单击或上下文菜单中，选择“代码段” > “插入代码段”  

   随即基于代码元素生成 XML 模板。 例如，对方法进行注释时，它会生成 \<summary\> 元素，针对每个参数生成一个 \<param\> 元素，并生成一个记录返回值的 \<returns\> 元素    。

   ![XML 注释模板 - C#](media/doc-preview-cs.png)

   ![XML 注释模板 - Visual Basic](media/doc-preview-vb.png)

3. 为每个 XML 元素输入说明以完整记录代码元素。

   ![完成的注释](media/doc-result-cs.png)

你可以在 XML 注释中使用样式，将鼠标悬停在元素上时这些样式将在“快速信息”中呈现。 这些样式包括：斜体、粗体、项目符号和可单击的链接。

   ![完成的注释](media/doc-styles-cs.png) 

> [!NOTE]
> 在 C# 中键入`///`（或在 Visual Basic 中键入 `'''`）后，可[选择](../../ide/reference/options-text-editor-csharp-advanced.md)切换 XML 文档注释。 在菜单栏中，选择“工具” > “选项”以打开“选项”对话框    。 然后，导航到“文本编辑器” > “C#”或导航到“基本” > “高级”     。 在“编辑器帮助”部分，查找“生成 XML 文档注释”选项   。

## <a name="see-also"></a>请参阅

- [XML 文档注释（C# 编程指南）](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [使用 XML 注释来记录代码（C# 指南）](/dotnet/csharp/codedoc)
- [如何：创建 XML 文档 (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation)
- [C++ 注释](/cpp/cpp/comments-cpp)
- [XML 文档 (C++)](/cpp/build/reference/xml-documentation-visual-cpp)
- [代码生成](../code-generation-in-visual-studio.md)
