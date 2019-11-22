---
title: 使用编码的 UI 测试来测试 SharePoint 2010 应用程序 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 51b53778-469c-4cc9-854c-4e4992d6389b
caps.latest.revision: 32
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 73dd0e406e8e0a00260d922e38dee70135c3645d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298006"
---
# <a name="testing-sharepoint-2010-applications-with-coded-ui-tests"></a>使用编码的 UI 测试来测试 SharePoint 2010 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过在 SharePoint 应用程序中包含编码的 UI 测试，您可以验证整个应用程序（包括其 UI 控件）是否正常工作。 编码的 UI 测试还可以验证 UI 中的值和逻辑。

 **惠?**

- Visual Studio Enterprise

## <a name="what-else-should-i-know-about-coded-ui-tests"></a>还应当编码的 UI 测试了解什么?
 若要详细了解使用编码的 UI 测试的相关好处，请参阅[使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)和[使用 Visual Studio 2012 测试持续交付 - 第 5 章：实现系统测试的自动化](https://go.microsoft.com/fwlink/?LinkID=255196)。

 **注意**

- ![Prerequsite](../test/media/prereq.png "Prereq") Coded UI tests for SharePoint applications are supported only with SharePoint 2010.

- ![Prerequsite](../test/media/prereq.png "Prereq") Support for Visio and PowerPoint 2010 controls in your SharePoint application is not supported.

## <a name="creating-a-coded-ui-test-for-your-sharepoint-app"></a>为您的 SharePoint 应用程序创建编码的 UI 测试
 为 SharePoint 2010 应用程序[创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate) ，与为其他类型的应用程序创建测试相同。 支持对 Web 编辑界面上的所有控件进行录制和播放。 选择类别和 Web 部件的接口都是标准 Web 控件。

 ![SharePoint web parts](../test/media/cuit-sharepoint.png "CUIT_SharePoint")

> [!NOTE]
> 如果要录制操作，请在生成代码前验证操作。 因为有多种行为与鼠标悬停操作相关联，所以它在默认情况下处于开启状态。 注意从编码的 UI 测试中移除冗余的悬停操作。 为此，您可以编辑测试的代码，或者使用 [编码的 UI 测试编辑器](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)。

## <a name="including-testing-of-office-2010-controls-within-your-sharepoint-app"></a>在 SharePoint 应用程序中包括 Office 2010 控件的测试
 若要对 SharePoint 应用中的某些 office 2010 Web 部件实现自动化，您必须作出一些细微的代码修改。

> [!WARNING]
> 不支持对 Visio 和 PowerPoint 2010 控件的支持。

### <a name="excel-2010-cell-controls"></a>Excel 2010 单元格控件
 若要包括 Excel 单元格控件，则必须在编码的 UI 测试代码中做一些更改。

> [!WARNING]
> 如果在任何 Excel 单元格中输入文本，然后进行箭头键操作，将无法正确进行录制。 使用鼠标选择单元格。

 如果要录制对空单元格的操作，则必须双击该单元格，然后执行设置文本操作，以此修改代码。 这是必需的，因为如果单击单元格，然后进行任何键盘操作，将会激活单元格内的 `textarea` 。 如果只是录制对空单元格的 `setvalue` ，将会搜索直到单击单元格后才会显示的 `editbox` 。 例如:

```csharp
Mouse.DoubliClick(uiItemCell,new Point(31,14));
uiGridKeyboardInputEdit.Text=value;
```

 如果要录制对非空单元格的操作，则稍微有些复杂，因为在向单元格添加文本时，将会添加一个新的 \<div> 控件作为此单元格的子项。 新的 \<div> 控件包含刚才输入的文本。 记录器需要录制对新 \<div> 控件的操作；但是，它无法进行录制，因为新 \<div> 控件直到进入测试后才会存在。 您必须手动对代码做出以下更改，才能解决这一问题。

1. 转到单元格初始化，将 `RowIndex` 和 `ColumnIndex` 作为主要属性：

    ```csharp
    this.mUIItemCell.SearchProperties[HtmlCell.PropertyNames. RowIndex] = "3";
    this.mUIItemCell.SearchProperties[HtmlCell.PropertyNames. ColumnIndex] = "3";
    ```

2. 找到单元格的 `HtmlDiv` 子项：

    ```csharp
    private UITestControl getControlToDoubleClick(HtmlCell cell)
    {
         if (String.IsNullOrEmpty(cell.InnerText)) return cell;
         HtmlDiv pane = new HtmlDiv(cell);
         pane.FilterProperties[HtmlDiv.PropertyNames.InnerText] = cell.InnerText;
         // Class is an important property in finding pane
         pane.FilterProperties[HtmlDiv.PropertyNames.Class] = "cv-nwr";
         UITestControlCollection panes = pane.FindMatchingControls();
         return panes[0];
    }

    ```

3. 添加 `HtmlDiv`鼠标双击操作的代码：

    ```csharp
    Mouse.DoubleClick(uIItemPane, new Point(31, 14)); )
    ```

4. 添加 `TextArea`设置文本操作的代码：

    ```csharp
    uIGridKeyboardInputEdit.Text = value; }
    ```

## <a name="enabling-coded-ui-testing-of-silverlight-web-parts-in-your-sharepoint-2010-app"></a>在 SharePoint 2010 应用程序中启用 Silverlight Web 部件的编码 UI 测试
 Visual Studio 2012 和更高版本中不支持 Silverlight 测试。 但是，如果要对 SharePoint 2010 应用中的 Silverlight Web 部件进行测试，可以从 Visual Studio 库安装单独的 Silverlight 插件。

#### <a name="setting-up-your-machine"></a>设置您的计算机

1. 确保安装了 Visual Studio 2012.1 或更高版本。

2. 安装 [用于 Silverlight 的 Microsoft Visual Studio UI 测试插件](https://marketplace.visualstudio.com/items?itemName=PrachiBoraMSFT.MicrosoftVisualStudioUITestPluginforSilverlight)。

3. 安装 [Fiddler](http://www.fiddler2.com/fiddler2/)。 这只是一个用来捕获和记录 HTTP 流量的工具。

4. 下载 [fiddlerXap 项目](https://40jajy3iyl373v772m19fybm-wpengine.netdna-ssl.com/wp-content/uploads/sites/6/2019/02/FiddlerXapProxy.zip)。 解压并生成该项目，然后运行“CopySLHelper.bat”脚本，以便安装使用 Fiddler 工具测试 Silverlight Web 部件时所需的帮助程序 DLL。

   在设置计算机后，若要开始测试包含 Silverlight Web 部件的 SharePoint 2010 应用，请执行以下步骤：

#### <a name="testing-silverlight-web-parts"></a>测试 Silverlight Web 部件

1. 启动 Fiddler。

2. 清除浏览器缓存。 这是必需的，因为 XAP 文件（包含 Silverlight UI 自动化帮助程序 DLL）通常会被缓存。 我们必须确保选择修改后的 XAP 文件，因此需要清除浏览器缓存。

3. 打开网页。

4. 启动记录器并生成代码，就像常规 Web 应用程序测试一样。

5. 您应确认生成的代码引用 Microsoft.VisualStudio.TestTools.UITest.Extension.Silverlight.dll。

     有关详细信息，请参见 [使用 Visual Studio 2012 对 SharePoint 2010 进行 UI 测试](https://devblogs.microsoft.com/devops/ui-testing-sharepoint-2010-with-visual-studio-2012/)

## <a name="external-resources"></a>外部资源

### <a name="blogs"></a>博客
 [使用 Visual Studio 2012 对 SharePoint 2010 进行 UI 测试](https://devblogs.microsoft.com/devops/ui-testing-sharepoint-2010-with-visual-studio-2012/)

 [了解编码的 UI 测试中的 Silverlight 控件的搜索逻辑](https://tapas-techsnips.blogspot.com/)

 [获取 Silverlight 控件的属性](https://tapas-techsnips.blogspot.com/)

 [编码的 UI 测试的内容索引](https://blogs.msdn.microsoft.com/mathew_aniyan/2013/02/18/content-index-for-coded-ui-test/)

### <a name="guidance"></a>指导
 [使用 Visual Studio 2012 测试持续交付 - 第 5 章：实现系统测试的自动化](https://go.microsoft.com/fwlink/?LinkID=255196)

### <a name="forum"></a>论坛
 [Visual Studio ALM + Team Foundation Server 博客](https://go.microsoft.com/fwlink/?LinkID=254496)

## <a name="see-also"></a>请参阅
 [Use UI Automation To Test Your Code](../test/use-ui-automation-to-test-your-code.md) [Web performance and load testing SharePoint 2010 and 2013 applications](https://msdn.microsoft.com/library/20c2e469-0e4e-4296-a739-c0e8fff36e54) [Create SharePoint Solutions](https://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631) [Verifying and Debugging SharePoint Code](https://msdn.microsoft.com/library/b5f3bce2-6a51-41b1-a292-9e384bae420c) [Building and Debugging SharePoint Solutions](https://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae) [Profiling the Performance of SharePoint Applications](https://msdn.microsoft.com/library/61ae02e7-3f37-4230-bae1-54a498c2fae8)
