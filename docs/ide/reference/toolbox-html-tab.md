---
title: 工具箱，“HTML”选项卡
ms.date: 06/21/2017
ms.topic: reference
f1_keywords:
- vs.toolbox.html
helpviewer_keywords:
- Toolbox, HTML tab
- HTML Designer, setting options
- HTML tab in Toolbox
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0489f534466149a437384d4f21e34f1fa9e98c5b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596432"
---
# <a name="toolbox-html-tab"></a>“工具箱”->“HTML”选项卡

“工具箱”的“HTML”  选项卡提供可用于网页和 Web 窗体的组件。 若要查看此选项卡，首先在 HTML 设计器中打开要编辑的文档。 在“视图”  菜单上，单击“工具箱”  ，然后单击“工具箱”的“HTML”  选项卡。

若要在“HTML”  选项卡上创建工具的实例，可以双击此工具将其添加到文档中的当前插入点，或选择该工具并将其拖动到编辑图面上所需的位置。

## <a name="ui-elements"></a>UI 元素

默认情况下，“HTML”选项卡提供下列工具。

**指针**

![ASP.NET 移动设计器 HTML 页指针](../../ide/reference/media/vxpointer.gif)

打开任一工具箱选项卡时，此工具默认处于选中状态。 无法删除此工具。 使用指针可将对象拖动到“设计”视图图面上、调整其大小，并在页面或窗体中对其重新定位。 有关详细信息，请参阅[工具箱](../../ide/reference/toolbox.md)。

**Input (Button)**

![HTML 网页按钮](../../ide/reference/media/vxbutton.gif)

插入 `input` 的一个 `type="button"` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个按钮，插入 `id="Button1"`，对于第二个按钮，插入 `id="Button2"`，以此类推。

将“Input (Button)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="Button1" type="button" value="Button" name="Button1">
```

**Input (Reset)**

![HTMLpageResetButton 屏幕快照](../../ide/reference/media/vxreset.gif)

插入 `input` 的一个 `type="reset"` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个重置按钮，插入 `id="Reset1"`，对于第二个重置按钮，插入 `id="Reset2"`，以此类推。

将“Input (Reset)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="Reset1" type="reset" value="Reset" name="Reset1">
```

**Input (Submit)**

![HTMLpageToolbarSubmitButton 屏幕快照](../../ide/reference/media/vxsubmit.gif)

插入 `input` 的一个 `type="submit"` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个提交按钮，插入 `id="Submit1"`，对于第二个提交按钮，插入 `id="Submit2"`，以此类推。

将“Input (Submit)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="Submit1" type="submit" value="Submit" name="Submit1">
```

**Input (Text)**

![HTMLpageToolbarTextField 屏幕快照](../../ide/reference/media/vxtextfield.gif)

在文档中插入 `input` 的一个 `type="text"` 元素。 若要更改显示的默认文本，请编辑 `value` 特性。 默认情况下，对于第一个文本字段，插入 `id="Text1"`，对于第二个文本字段，插入 `id="Text2"`，以此类推。

将“Input (Text)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="Text1" TYPE="text" value="Text Field" name="Text1">
```

> [!IMPORTANT]
>建议对所有用户输入进行验证。 有关详细信息，请参阅[在 ASP.NET 网页 (Razor) 站点中验证用户输入](/aspnet/web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites)。

**Input (File)**

![HTML 页文件字段](../../ide/reference/media/vxfilefield.gif)

在文档中插入 `input` 的一个 `type="file"` 元素。 默认情况下，对于第一个文件字段，插入 `id="File1"`，对于第二个文件字段，插入 `id="File2"`，以此类推。

将“Input (File)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="File1" type="file" name="File1">
```

> [!IMPORTANT]
> 建议对所有用户输入进行验证。 有关详细信息，请参阅[在 ASP.NET 网页 (Razor) 站点中验证用户输入](/aspnet/web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites)。

**Input (Password)**

![Visual Studio 密码字段](../../ide/reference/media/vxpassword.gif)

插入 `input` 的一个 `type="password"` 元素。 默认情况下，对于第一个密码字段，插入 `id="Password1"`，对于第二个密码字段，插入 `id="Password2"`，以此类推。

将“Input (Password)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="Password1" type="password" name="Password1">
```

> [!IMPORTANT]
> 如果应用程序传输用户名和密码，则应配置网站使用安全套接字层 (SSL) 对传输进行加密。 有关详细信息，请参阅[保护连接](/previous-versions/tn-archive/bb418917(v=technet.10))。 此外，建议对所有用户输入进行验证。 有关详细信息，请参阅[在 ASP.NET 网页 (Razor) 站点中验证用户输入](/aspnet/web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites)。

**Input (Check box)**

![HTML 网页工具箱复选框选项](../../ide/reference/media/vxcheckbox.gif)

插入 `input` 的一个 `type="checkbox"` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个复选框，插入 `id="Checkbox1"`，对于第二个复选框，插入 `id="Checkbox2"`，以此类推。

将“Input (Check box)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="Checkbox1" type="checkbox" name="Checkbox1">
```

**Input (Radio)**

![VisualStudioHTMLpageRadioButton 屏幕快照](../../ide/reference/media/vxradio.gif)

插入 `input` 的一个 `type="radio"` 元素。 若要更改显示的文本，请编辑 `name` 属性。 默认情况下，对于第一个单选按钮，插入 `id="Radio1"`，对于第二个单选按钮，插入 `id="Radio2"`，以此类推。

将“Input (Radio)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="Radio1" type="radio" name="Radio1">
```

**Input (Hidden)**

![HTML 页隐藏项](../../ide/reference/media/vxhidden.gif)

插入 `input` 的一个 `type="hidden"` 元素。 默认情况下，对于第一个隐藏字段，插入 `id="Hidden1"`，对于第二个隐藏字段，插入 `id="Hidden2"`，以此类推。

将“Input (Hidden)”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<input id="Hidden1" type="hidden" name="Hidden1">
```

**Textarea**

![HTML 页工具栏文本区域](../../ide/reference/media/vxtextarea.gif)

插入一个 `textarea` 元素。 可以调整文本区域的大小，或使用其滚动条查看延伸到显示区域外的文本。 若要更改显示的默认文本，请编辑 `value` 特性。 默认情况下，对于第一个文本区域，插入 `id="textarea1"`，对于第二个文本区域，插入 `id=" textarea 2"`，以此类推。

将“Textarea”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<textarea id=" textarea 1 name=" textarea 1" rows=2 cols=20></textarea>
```

> [!IMPORTANT]
> 建议对所有用户输入进行验证。 有关详细信息，请参阅[在 ASP.NET 网页 (Razor) 站点中验证用户输入](/aspnet/web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites)。

**Table**

![HTMLpageToolbarTable 屏幕快照](../../ide/reference/media/vxtable.gif)

插入一个 `table` 元素。

将“Table”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<table cellspacing="1" width="75%" border=1> <tr><td></td></tr></table>
```

**Image**

![HTML 页图像项](../../ide/reference/media/vximage.gif)

插入一个 `img` 元素。 编辑此元素可指定其 `src` 和 `alt` 文本。

将“Image”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<img alt="" src="">
```

**选择**

![HTML 页工具箱下拉列表](../../ide/reference/media/vxdropdown.gif)

插入一个下拉 `select` 元素（不含 `size` 特性）。 默认情况下，对于第一个列表框，插入 `id="select1"`，对于第二个列表框，插入 `id="select2"`，以此类推。

将“Select”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<select id="select1" name="select1"><option selected></option></select>
```

通过增加 size 属性的值可以创建多行 `select` 元素。

**Horizontal Rule**

![HTML 页水平标尺项](../../ide/reference/media/vxhorizontal.gif)

插入一个 `hr` 元素。 若要增大线条的粗细，请编辑 `size` 特性。

将“Horizontal Rule”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<hr width="100%" size=1>
```

**Div**

![HTML 页标签](../../ide/reference/media/vxlabel.gif)

插入一个 `div` 元素，该元素包括一个 `ms_positioning="FlowLayout"` 特性。 除宽度和高度之外，该项与“流布局面板”相同。 若要设置 `div` 元素中所含文本的格式，请在开始标记中添加 `class="stylename"` 特性。

将“Div”  拖动到“设计”视图图面上时，会在文档中插入类似如下的 HTML 标记：

```html
<div ms_positioning="FlowLayout" style="width: 70px; position: relative; height: 15px">Label</div>
```

## <a name="see-also"></a>另请参阅

- [工具箱](../../ide/reference/toolbox.md)
