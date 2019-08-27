---
title: 如何：生成并运行 LinqToXmlDataBinding 示例 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 3943deaf-80e2-4968-ac04-d3ef56cfad6c
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bebaeba2cc6f74a3ddbf059ca802252ad0bab6cf
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696159"
---
# <a name="how-to-build-and-run-the-linqtoxmldatabinding-example"></a>如何：生成并运行 LinqToXmlDataBinding 示例
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题演示如何创建和生成 LinqToXmlDataBinding Visual Studio 项目以及如何运行生成的 LinqToXmlDataBinding Windows Presentation Foundation (WPF) 示例程序。  
  
 有关使用 Visual Studio 创建项目的详细信息，请参阅 [Visual Studio 中的应用程序开发](https://msdn.microsoft.com/97490c1b-a247-41fb-8f2c-bc4c201eff68)。  
  
## <a name="creating-and-populating-the-project"></a>创建和填充项目  
  
#### <a name="to-create-the-starting-project"></a>创建起始项目  
  
1. 启动 Visual Studio 并创建一个名为 LinqToXmlDataBinding 的 C# WPF 应用程序。 该项目必须使用 .NET Framework 3.5（或更高版本）。  
  
2. 为以下 .NET 程序集添加项目引用（如果尚不存在）：  
  
    - System.Data  
  
    - System.Data.DataSetExtensions  
  
    - System.Xml  
  
    - System.Xml.Linq  
  
3. 按“Ctnrl+Shift+B”生成解决方案，然后按“F5”运行该解决方案。 该项目应正确编译而不出错，并作为一般 WPF 应用程序运行。  
  
#### <a name="to-add-custom-code-to-the-project"></a>对项目添加自定义代码  
  
1. 在解决方案资源管理器中，将源文件 Window1.xaml 重命名为 L2XDBForm.xaml。 依赖源文件 Window1.xaml.cs 应该会自动重命名为 L2XDBForm.xaml.cs。  
  
2. 用 [L2DBForm.xaml 源代码](../designers/l2dbform-xaml-source-code.md)主题中的代码节替换 L2XDBForm.xaml 文件中的源代码。 （使用 XAML 源视图来处理此文件。）  
  
3. 同样，用 [L2DBForm.xaml.cs 源代码](../designers/l2dbform-xaml-cs-source-code.md)中的代码替换 L2XDBForm.xaml.cs 中的源代码。  
  
4. 在 App.xaml 文件中，用“L2XDBForm.xaml”替换“Window1.xaml”字符串的所有匹配项。  
  
5. 按“Ctrl+Shift+B”生成解决方案。  
  
## <a name="running-the-program"></a>运行程序  
 LinqToXmlDataBinding 程序可以让用户查看和操作以嵌入式 XML 元素形式存储的书籍的列表。  
  
#### <a name="to-run-the-program-and-view-the-book-list"></a>运行程序并查看书籍列表  
  
1. 按“F5”（“启动调试”）或“Ctrl+F5”（“开始执行(不调试)”）运行 LinqToXmlDataBinding。 应显示标题为“使用 LINQ to XML 的 WPF 数据绑定”的程序窗口。  
  
2. 请注意，UI 的顶部区域将显示表示书籍列表的原始 **XML**。 它使用 WPF <xref:System.Windows.Controls.TextBlock> 控件来显示，该控件不启用通过鼠标或键盘交互。  
  
3. 标记为“书籍列表”的第二个垂直区域以排序的纯文本列表形式显示书籍。 它使用启用通过鼠标或键盘进行选择的 <xref:System.Windows.Controls.ListBox> 控件。  
  
#### <a name="to-add-and-delete-books-from-the-list"></a>在列表中添加和删除书籍  
  
1. 若要从列表中删除现有书籍，请在“书籍列表”区域选择该书籍，然后单击“移除所选书籍”按钮。 请注意，这会从书籍列表和原始 XML 源列表中移除该书籍条目。  
  
2. 若要向列表中添加新书籍，请向最后一个区域”添加新书籍“的“ID”和“值” <xref:System.Windows.Controls.TextBox> 控件中输入值，然后单击“添加书籍”按钮。 请注意，这会向书籍列表和 XML 列表中追加该书籍。 此程序不验证输入值。  
  
#### <a name="to-edit-an-existing-book-entry"></a>编辑现有书籍条目  
  
1. 在第二个“书籍列表”区域中选择书籍条目。 其当前值应该显示在第三个区域“编辑所选书籍”中。  
  
2. 使用键盘编辑值。 只要任一 <xref:System.Windows.Controls.TextBox> 控件失去焦点，更改就会自动传播到 XML 源和书籍列表。  
  
## <a name="see-also"></a>请参阅  
 [使用 LINQ to XML 的 WPF 数据绑定示例](../designers/wpf-data-binding-using-linq-to-xml-example.md)   
 [演练：LinqToXmlDataBinding 示例](../designers/walkthrough-linqtoxmldatabinding-example.md)   
 [Visual Studio 中的应用程序开发](https://msdn.microsoft.com/97490c1b-a247-41fb-8f2c-bc4c201eff68)
