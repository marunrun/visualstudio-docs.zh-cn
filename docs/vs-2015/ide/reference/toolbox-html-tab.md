---
title: “工具箱”->“HTML”选项卡 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.toolbox.html
helpviewer_keywords:
- Toolbox, HTML tab
- HTML Designer, setting options
- HTML tab in Toolbox
ms.assetid: 9bfdd3b8-f5ac-4a5f-bdbf-c2b4e97641d8
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d3d6eafbafbf9b373028a7ba052ba9e8df62511c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661602"
---
# <a name="toolbox-html-tab"></a>工具箱，“HTML”选项卡
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

“工具箱”的“HTML”  选项卡提供可用于网页和 Web 窗体的组件。 若要查看此选项卡，首先在 HTML 设计器中打开要编辑的文档。 在“视图”  菜单上，单击“工具箱”  ，然后单击“工具箱”的“HTML”  选项卡。

 若要在“HTML”  选项卡上创建工具的实例，可以双击此工具将其添加到文档中的当前插入点，或选择该工具并将其拖动到编辑图面上所需的位置。

## <a name="tasks"></a>任务

- [如何：管理“工具箱”窗口](https://msdn.microsoft.com/a022c3fe-298c-4a59-a48f-b050da90ebc2)

- [如何：操作工具箱选项卡](https://msdn.microsoft.com/21285050-cadd-455a-b1f5-a2289a89c4db)

## <a name="ui-elements"></a>UI 元素
 默认情况下，“HTML”选项卡提供下列工具。

 **指针** ![ASP.NET Mobile 设计器 html 页指针](../../ide/reference/media/vxpointer.gif "|::ref1::|")

 打开任一工具箱选项卡时，此工具默认处于选中状态。 无法删除此工具。 使用指针可将对象拖动到“设计”视图图面上、调整其大小，并在页面或窗体中对其重新定位。 有关详细信息，请参阅[如何：管理“工具箱”窗口](https://msdn.microsoft.com/a022c3fe-298c-4a59-a48f-b050da90ebc2)和[如何：操作工具箱选项卡](https://msdn.microsoft.com/21285050-cadd-455a-b1f5-a2289a89c4db)。

 **输入（按钮）** ![HTML 网页按钮](../../ide/reference/media/vxbutton.gif "|::ref2::|")

 插入 `type="button"` 的一个 `input` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个按钮，插入 `id="Button1"`，对于第二个按钮，插入 `id="Button2"`，以此类推。

 将“Input (Button)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="Button1" type="button" value="Button" name="Button1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputButton 服务器控件声明性语法](https://msdn.microsoft.com/99ccf7fb-7e2a-4ba1-bcd9-981b619a16aa)、[NIB：如何：创建脚本和编辑事件处理程序](https://msdn.microsoft.com/69d71d13-c68b-4ecd-869b-a42edf6d1f6d)、[按钮 Web 服务器控件内容映射](https://msdn.microsoft.com/library/66b3ce28-3b93-4f0a-951f-42fb5bb5fddf)、<xref:System.Web.UI.HtmlControls.HtmlInputButton>、<xref:System.Web.UI.HtmlControls.HtmlButton> 和 <xref:System.Web.UI.WebControls.Button>。

 **输入（Reset）** ![HTMLpageResetButton 屏幕快照](../../ide/reference/media/vxreset.gif "|::ref3::|")

 插入 `type="reset"` 的一个 `input` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个重置按钮，插入 `id="Reset1"`，对于第二个重置按钮，插入 `id="Reset2"`，以此类推。

 将“Input (Reset)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="Reset1" type="reset" value="Reset" name="Reset1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputFile 服务器控件声明性语法](https://msdn.microsoft.com/cfc1f1fb-d33a-464d-9bb5-204e66174979)、<xref:System.Web.UI.HtmlControls.HtmlInputButton> 和 <xref:System.Web.UI.WebControls.Button>。

 **输入（提交）** ![HTMLpageToolbarSubmitButton 屏幕快照](../../ide/reference/media/vxsubmit.gif "|::ref4::|")

 插入 `type="submit"` 的一个 `input` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个提交按钮，插入 `id="Submit1"`，对于第二个提交按钮，插入 `id="Submit2"`，以此类推。

 将“Input (Submit)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="Submit1" type="submit" value="Submit" name="Submit1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputSubmit 服务器控件声明性语法](https://msdn.microsoft.com/eef2a157-f184-4ce9-b256-d1eacc7930f2)、<xref:System.Web.UI.HtmlControls.HtmlInputButton> 和 <xref:System.Web.UI.WebControls.Button>。

 **输入（文本）** ![HTMLpageToolbarTextField 屏幕快照](../../ide/reference/media/vxtextfield.gif "|::ref5::|")

 在文档中插入 `type="text"` 的一个 `input` 元素。 若要更改显示的默认文本，请编辑 `value` 特性。 默认情况下，对于第一个文本字段，插入 `id="Text1"`，对于第二个文本字段，插入 `id="Text2"`，以此类推。

 将“Input (Text)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="Text1" TYPE="text" value="Text Field" name="Text1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputText 服务器控件声明性语法](https://msdn.microsoft.com/87060d90-a11c-434d-9fc9-b03a8487041e)、[TextBox Web 服务器控件概述](https://msdn.microsoft.com/library/ab354bc1-f23a-48fc-93d8-d4d7c1b7396f)、<xref:System.Web.UI.HtmlControls.HtmlInputText> 和 <xref:System.Web.UI.WebControls.TextBox>。

> [!IMPORTANT]
> 建议对所有用户输入进行验证。 有关详细信息，请参阅[在 ASP.NET 网页中验证用户输入](https://msdn.microsoft.com/library/4ad3dacb-89e0-4cee-89ac-40a3f2a85461)。

 **输入（文件）** ![HTML 页文件字段](../../ide/reference/media/vxfilefield.gif "|::ref6::|")

 在文档中插入 `type="file"` 的一个 `input` 元素。 默认情况下，对于第一个文件字段，插入 `id="File1"`，对于第二个文件字段，插入 `id="File2"`，以此类推。

 将“Input (File)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="File1" type="file" name="File1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputFile 服务器控件声明性语法](https://msdn.microsoft.com/a817b4a0-056f-4c17-a696-b9fdcde43db6) 和 <xref:System.Web.UI.HtmlControls.HtmlInputFile>。

> [!IMPORTANT]
> 建议对所有用户输入进行验证。 有关详细信息，请参阅[在 ASP.NET 网页中验证用户输入](https://msdn.microsoft.com/library/4ad3dacb-89e0-4cee-89ac-40a3f2a85461)。

 **输入（密码）** ![Visual Studio 密码字段](../../ide/reference/media/vxpassword.gif "|::ref7::|")

 插入 `type="password"` 的一个 `input` 元素。 默认情况下，对于第一个密码字段，插入 `id="Password1"`，对于第二个密码字段，插入 `id="Password2"`，以此类推。

 将“Input (Password)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="Password1" type="password" name="Password1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputPassword 服务器控件声明性语法](https://msdn.microsoft.com/df703dd0-1624-4e5a-a547-c97f2f331b9f)、[如何：设置 TextBox Web 服务器控件以输入密码](https://msdn.microsoft.com/library/5b5069f3-64a1-435a-aee6-da263f4e6310)和[演练：验证 Web 窗体页中的用户输入](https://msdn.microsoft.com/library/7141d6ba-34f3-410b-b5cd-2102a24cb436)。

> [!IMPORTANT]
> 如果应用程序传输用户名和密码，则应配置网站使用安全套接字层 (SSL) 对传输进行加密。 有关详细信息，请参阅 [IIS 操作指南](http://go.microsoft.com/fwlink/?linkid=47856)中的“使用 SSL 保护连接”。 此外，建议对所有用户输入进行验证。 有关详细信息，请参阅[在 ASP.NET 网页中验证用户输入](https://msdn.microsoft.com/library/4ad3dacb-89e0-4cee-89ac-40a3f2a85461)。

 **输入（复选框）** ![HTML 网页工具箱复选框选项](../../ide/reference/media/vxcheckbox.gif "|::ref8::|")

 插入 `type="checkbox"` 的一个 `input` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个复选框，插入 `id="Checkbox1"`，对于第二个复选框，插入 `id="Checkbox2"`，以此类推。

 将“Input (Check box)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="Checkbox1" type="checkbox" name="Checkbox1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputCheckBox 服务器控件声明性语法](https://msdn.microsoft.com/4a509586-89d8-4ccf-a0b8-b9160ce6e4a6)、[CheckBox 和 CheckBoxList Web 服务器控件概述](https://msdn.microsoft.com/library/3028dfd3-e2c5-451d-9150-d02c8ffb92bf)、<xref:System.Web.UI.HtmlControls.HtmlInputCheckBox> 和 <xref:System.Web.UI.WebControls.CheckBox>。

 **输入（收音机）** ![VisualStudioHTMLpageRadioButton 屏幕快照](../../ide/reference/media/vxradio.gif "|::ref9::|")

 插入 `type="radio"` 的一个 `input` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个单选按钮，插入 `id="Radio1"`，对于第二个单选按钮，插入 `id="Radio2"`，以此类推。

 将“Input (Radio)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="Radio1" type="radio" name="Radio1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputRadioButton 服务器控件声明性语法](https://msdn.microsoft.com/6e60ff63-cc57-46ef-bf96-e829e204ba33)、[RadioButton 和 RadioButtonList Web 服务器控件概述](https://msdn.microsoft.com/library/20eb383c-4b59-432b-bba3-e9d785107747)、<xref:System.Web.UI.HtmlControls.HtmlInputRadioButton> 和 <xref:System.Web.UI.WebControls.RadioButton>。

 **输入（隐藏）** ![HTML 页隐藏项](../../ide/reference/media/vxhidden.gif "|::ref10::|")

 插入 `type="hidden"` 的一个 `input` 元素。 默认情况下，对于第一个隐藏字段，插入 `id="Hidden1"`，对于第二个隐藏字段，插入 `id="Hidden2"`，以此类推。

 将“Input (Hidden)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<input id="Hidden1" type="hidden" name="Hidden1">
```

 有关详细信息，请参阅 [HTML 输入控件](https://msdn.microsoft.com/library/2ba82c6b-dff7-4b73-b1c2-9e76a48a69de)、[HtmlInputHidden 服务器控件声明性语法](https://msdn.microsoft.com/4194e44d-1d74-4bfc-9cc7-743a2e1ea5f9) 和 <xref:System.Web.UI.HtmlControls.HtmlInputHidden>。

 **Textarea** ![Html 页工具栏文本区域](../../ide/reference/media/vxtextarea.gif "|::ref11::|")

 插入一个 `textarea` 元素。 可以调整文本区域的大小，或使用其滚动条查看延伸到显示区域外的文本。 若要更改显示的默认文本，请编辑 `value` 特性。 默认情况下，对于第一个文本区域，插入 `id="textarea1"`，对于第二个文本区域，插入 `id=" textarea 2"`，以此类推。

 将“Textarea”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<textarea id=" textarea 1 name=" textarea 1" rows=2 cols=20></textarea>
```

 有关详细信息，请参阅 [HtmlTextArea 服务器控件声明性语法](https://msdn.microsoft.com/5a103ffa-235b-4452-ba2b-a4fb8ba8cb87)、<xref:System.Web.UI.HtmlControls.HtmlTextArea> 和 <xref:System.Web.UI.WebControls.TextBox>。

> [!IMPORTANT]
> 建议对所有用户输入进行验证。 有关详细信息，请参阅[在 ASP.NET 网页中验证用户输入](https://msdn.microsoft.com/library/4ad3dacb-89e0-4cee-89ac-40a3f2a85461)。

 **表** ![HTMLpageToolbarTable 屏幕快照](../../ide/reference/media/vxtable.gif "|::ref12::|")

 插入一个 `table` 元素。

 将“Table”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<table cellspacing="1" width="75%" border=1> <tr><td></td></tr></table>
```

 有关详细信息，请参阅 [HtmlTable 服务器控件声明性语法](https://msdn.microsoft.com/625b06d8-0f69-4112-a1d4-8ef2a9fbcda9)、[Table、TableRow 和 TableCell Web 服务器控件概述](https://msdn.microsoft.com/library/2fbd0582-cf69-4c8d-9e35-21f35e2cee1a)、<xref:System.Web.UI.HtmlControls.HtmlTable> 和 <xref:System.Web.UI.WebControls.Table>。

 **图像** ![HTML 页面图像项](../../ide/reference/media/vximage.gif "|::ref13::|")

 插入一个 `img` 元素。 编辑此元素可指定其 `src` 和 `alt` 文本。

 将“Image”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<img alt="" src="">
```

 有关详细信息，请参阅 [HtmlImage 服务器控件声明性语法](https://msdn.microsoft.com/528430e8-ced1-47d1-8db2-942e734a61f6)、[Image Web 服务器控件概述](https://msdn.microsoft.com/library/096a8d8d-58ee-4ee8-ab82-6594a0f3a0a9)、<xref:System.Web.UI.HtmlControls.HtmlImage>、<xref:System.Web.UI.HtmlControls.HtmlInputImage> 和 <xref:System.Web.UI.WebControls.Image>。

 **选择** ![HTML 页工具箱下拉列表](../../ide/reference/media/vxdropdown.gif "|::ref14::|")

 插入一个下拉 `select` 元素（不含 `size` 特性）。 默认情况下，对于第一个列表框，插入 `id="select1"`，对于第二个列表框，插入 `id="select2"`，以此类推。

 将“Select”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<select id="select1" name="select1"><option selected></option></select>
```

 通过增加 size 属性的值可以创建多行 `select` 元素。

 有关详细信息，请参阅 [HtmlSelect 服务器控件声明性语法](https://msdn.microsoft.com/ee93bdec-b343-441a-a8ff-56ffcafe9ae5)、[NIB：如何：创建脚本和编辑事件处理程序](https://msdn.microsoft.com/69d71d13-c68b-4ecd-869b-a42edf6d1f6d)、[DropDownList Web 服务器控件概述](https://msdn.microsoft.com/library/517dd1a4-8df3-4c9f-8c89-1549a1aee608)、[ListBox Web 服务器控件概述](https://msdn.microsoft.com/library/c08ee025-787a-408d-858e-a4a5fdb61d97)、<xref:System.Web.UI.HtmlControls.HtmlSelect> 和 <xref:System.Web.UI.WebControls.DropDownList>。

 **水平规则** ![HTML 页水平标尺项](../../ide/reference/media/vxhorizontal.gif "|::ref15::|")

 插入一个 `hr` 元素。 若要增大线条的粗细，请编辑 `size` 特性。

 将“Horizontal Rule”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<hr width="100%" size=1>
```

 有关详细信息，请参阅 [HTML 水平标尺控件](https://msdn.microsoft.com/library/bf6df0a8-9844-404d-8a9a-3455b0180f2f)。

 **Div** ![HTML 页面标签](../../ide/reference/media/vxlabel.gif "|::ref16::|")

 插入一个 `div` 元素，该元素包括一个 `ms_positioning="FlowLayout"` 特性。 除宽度和高度之外，该项与“流布局面板”相同。 若要设置 `div` 元素中所含文本的格式，请在开始标记中添加 `class="stylename"` 特性。

 将“Div”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```
<div ms_positioning="FlowLayout" style="width: 70px; position: relative; height: 15px">Label</div>
```

 有关详细信息，请参阅 [HTML Div 控件](https://msdn.microsoft.com/library/585fa702-4408-4af1-a92b-68d77ee5e995)、[Label Web 服务器控件概述](https://msdn.microsoft.com/library/990558d1-4b22-4f28-b100-78a434b3c5ac)和 <xref:System.Web.UI.WebControls.Label>。

## <a name="see-also"></a>另请参阅
 [工具箱](../../ide/reference/toolbox.md)[标准选项卡，工具箱](https://msdn.microsoft.com/library/35e9320d-fcbd-474b-8b8f-55705e9a1870) [HTML 控件](https://msdn.microsoft.com/library/83bc6f7e-a2b5-4fe9-9a34-eb34aef673be)
