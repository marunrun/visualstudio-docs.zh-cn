---
title: 如何：生成并运行 LinqToXmlDataBinding 示例
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d53f8d08222eb35660f7a4454164d6b821a976d9
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714833"
---
# <a name="how-to-build-and-run-the-linqtoxmldatabinding-example"></a>如何：生成并运行 LinqToXmlDataBinding 示例

本主题演示如何创建和生成 LinqToXmlDataBinding Visual Studio 项目以及如何运行生成的 LinqToXmlDataBinding Windows Presentation Foundation (WPF) 示例程序。

有关 Visual Studio 的详细信息，请参阅 [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)。

## <a name="create-the-project"></a>创建项目

1. 打开 Visual Studio 并创建一个名为 LinqToXmlDataBinding 的 C# WPF 应用。  

   该项目应面向 .NET Framework 3.5（或更高版本）。

1. 为以下 .NET 程序集添加项目引用（如果尚不存在）：

    - System.Data

    - System.Data.DataSetExtensions

    - System.Xml

    - System.Xml.Linq

1. 按 Ctrl+Shift+B 生成解决方案，然后按 F5 运行该解决方案     。 该项目应正确编译而不出错，并作为一般 WPF 应用程序运行。

## <a name="add-code-to-the-project"></a>将代码添加到项目

1. 在解决方案资源管理器中，将源文件 Window1.xaml 重命名为“L2XDBForm.xaml    。 依赖源文件 Window1.xaml.cs 应该会自动重命名为 L2XDBForm.xaml.cs   。

1. 用 [L2DBForm.xaml 源代码](../designers/l2dbform-xaml-source-code.md)主题中的代码节替换 L2XDBForm.xaml 文件中的源代码  。 使用 XAML 源视图来处理此文件。

1. 同样，用 [L2DBForm.xaml.cs 源代码](../designers/l2dbform-xaml-cs-source-code.md)中的代码替换 L2XDBForm.xaml.cs 中的源代码  。

1. 在 App.xaml 文件中，用 `L2XDBForm.xaml` 替换 `Window1.xaml` 字符串的所有匹配项  。

1. 按 Ctrl+Shift+B 生成解决方案    。

## <a name="run-the-program"></a>运行程序

LinqToXmlDataBinding 程序可以让用户查看和操作以嵌入式 XML 元素形式存储的书籍的列表。

### <a name="to-run-the-program-and-view-the-book-list"></a>运行程序并查看书籍列表

按 F5（开始调试）或 Ctrl+F5（启动而不调试）运行 LinqToXmlDataBinding      。 显示标题为“使用 LINQ to XML 的 WPF 数据绑定”的程序窗口  。

- 请注意，UI 的顶部区域将显示表示书籍列表的原始 **XML**。 它使用 WPF <xref:System.Windows.Controls.TextBlock> 控件来显示，该控件不启用通过鼠标或键盘交互。

- 标记为“书籍列表”  的第二个垂直区域以排序的纯文本列表形式显示书籍。 它使用启用通过鼠标或键盘进行选择的 <xref:System.Windows.Controls.ListBox> 控件。

### <a name="to-add-and-delete-books-from-the-list"></a>在列表中添加和删除书籍

- 若要向列表中添加新书籍，请向最后一个区域”添加新书籍“的“ID”和“值” <xref:System.Windows.Controls.TextBox> 控件中输入值，然后单击“添加书籍”按钮     。 请注意，这会向书籍列表和 XML 列表中追加该书籍。 此程序不验证输入值。

- 若要从列表中删除现有书籍，请在“书籍列表”  区域选择该书籍，然后单击“移除所选书籍”  按钮。 请注意，这会从书籍列表和原始 XML 源列表中移除该书籍条目。

### <a name="to-edit-an-existing-book-entry"></a>编辑现有书籍条目

1. 在第二个“书籍列表”  区域中选择书籍条目。 其当前值应该显示在第三个区域“编辑所选书籍”  中。

1. 使用键盘编辑值。 只要任一 <xref:System.Windows.Controls.TextBox> 控件失去焦点，更改就会自动传播到 XML 源和书籍列表。

## <a name="see-also"></a>请参阅

- [使用 LINQ to XML 的 WPF 数据绑定示例](../designers/wpf-data-binding-using-linq-to-xml-example.md)
- [演练：LinqToXmlDataBinding 示例](../designers/walkthrough-linqtoxmldatabinding-example.md)
- [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)