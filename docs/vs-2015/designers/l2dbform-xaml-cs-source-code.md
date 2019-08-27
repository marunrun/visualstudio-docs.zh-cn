---
title: L2DBForm.xaml.cs 源代码 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 5a40dad3-6763-4576-b3ad-874df3f2c8d9
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ba6262ef3174428dc14c5f747c4346b5f04e35ee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62427996"
---
# <a name="l2dbformxamlcs-source-code"></a>L2DBForm.xaml.cs Source Code
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题包含文件 L2DBForm.xaml.cs 中 C# 源代码的内容和说明。 本文件中包含的 L2XDBForm 分部类可分为三个逻辑区域：数据成员、`OnRemove` 和 `OnAddBook` 按钮单击事件处理程序。  
  
## <a name="data-members"></a>数据成员  
 使用两个私有数据成员将此类与 L2DBForm.xaml 中使用的窗口资源相关联。  
  
- 命名空间变量 `myBooks` 初始化为 `"http://www.mybooks.com"`。  
  
- 用下面的行将构造函数中的成员 `bookList` 初始化为 L2DBForm.xaml 中的 CDATA 字符串：  
  
    ```  
    bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;  
    ```  
  
## <a name="onaddbook-event-handler"></a>OnAddBook 事件处理程序  
 此方法包含下面三个语句：  
  
- 第一个条件语句用于输入验证。  
  
- 第二个语句根据用户在“添加新书籍”用户界面 (UI) 区域中输入的字符串值新建 <xref:System.Xml.Linq.XElement>。  
  
- 最后一个语句将此新书籍元素添加到 L2DBForm.xaml 中的数据提供程序。 因此，动态数据绑定将用此新项自动更新 UI；不需要用户提供额外的代码。  
  
## <a name="onremove-event-handler"></a>OnRemove 事件处理程序  
 由于两个原因，`OnRemove` 处理程序比 `OnAddBook` 处理程序更复杂。 首先，由于原始 XML 包含保留的空白，因此还必须与书籍条目一起移除匹配的换行符。 其次，出于方便，对所选项进行的选择会重置为列表中以前的选择。  
  
 但是，移除所选书籍项的核心工作仅通过两个语句完成：  
  
- 首先，检索与列表框中当前所选项相关联的书籍元素：  
  
  ```  
  XElement selBook = (XElement)lbBooks.SelectedItem;   
  ```  
  
- 然后，从数据提供程序中删除此元素：  
  
  ```  
  selBook.Remove();  
  ```  
  
  此外，动态数据绑定将确保自动更新程序的 UI。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
  
### <a name="code"></a>代码  
  
```csharp  
using System;  
using System.Linq;  
using System.Collections;  
using System.Collections.Generic;  
using System.Diagnostics;  
using System.Text;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Input;  
using System.Xml;  
using System.Xml.Linq;  
  
namespace LinqToXmlDataBinding {  
    /// <summary>  
    /// Interaction logic for L2XDBForm.xaml  
    /// </summary>  
  
    public partial class L2XDBForm : System.Windows.Window   
    {  
        XNamespace mybooks = "http://www.mybooks.com";  
        XElement bookList;  
  
        public L2XDBForm()   
        {  
            InitializeComponent();  
            bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;  
        }  
  
        void OnRemoveBook(object sender, EventArgs e)   
        {  
            int index = lbBooks.SelectedIndex;  
            if (index < 0) return;  
  
            XElement selBook = (XElement)lbBooks.SelectedItem;  
            //Get next node before removing element.  
            XNode nextNode = selBook.NextNode;  
            selBook.Remove();  
  
            //Remove any matching newline node.  
            if (nextNode != null && nextNode.ToString().Trim().Equals(""))  
            { nextNode.Remove(); }  
  
            //Set selected item.   
            if (lbBooks.Items.Count > 0)  
            {  lbBooks.SelectedItem = lbBooks.Items[index > 0 ? index - 1 : 0]; }  
        }  
  
        void OnAddBook(object sender, EventArgs e)   
        {  
            if (String.IsNullOrEmpty(tbAddID.Text) ||  
                String.IsNullOrEmpty(tbAddValue.Text))  
            {  
                MessageBox.Show("Please supply both a Book ID and a Value!", "Entry Error!");  
                return;   
            }  
            XElement newBook = new XElement(  
                                mybooks + "book",  
                                new XAttribute("id", tbAddID.Text),  
                                tbAddValue.Text);  
            bookList.Add("  ", newBook, "\r\n");  
        }  
    }  
}  
  
```  
  
### <a name="comments"></a>注释  
 有关这些处理程序的关联 XAML 源，请参阅 [L2DBForm.xaml 源代码](../designers/l2dbform-xaml-source-code.md)。  
  
## <a name="see-also"></a>请参阅  
 [演练：LinqToXmlDataBinding 示例](../designers/walkthrough-linqtoxmldatabinding-example.md)   
 [L2DBForm.xaml 源代码](../designers/l2dbform-xaml-source-code.md)
