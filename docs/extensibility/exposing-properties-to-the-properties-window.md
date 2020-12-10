---
title: 将属性公开到 "属性" 窗口 |Microsoft Docs
description: 了解对象的公共属性。 对这些属性所做的更改将反映在属性窗口中。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6f2668f8410b6e5f18b23c82202c1d33f8c67b4d
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994688"
---
# <a name="expose-properties-to-the-properties-window"></a>向属性窗口公开属性

本演练将对象的公共属性公开给 " **属性** " 窗口。 对这些属性所做的更改将反映在 " **属性** " 窗口中。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="expose-properties-to-the-properties-window"></a>向属性窗口公开属性

在本部分中，将创建一个自定义工具窗口，并在 " **属性** " 窗口中显示关联的窗口窗格对象的公共属性。

### <a name="to-expose-properties-to-the-properties-window"></a>向属性窗口公开属性

1. 每个 Visual Studio 扩展都从一个 VSIX 部署项目开始，该项目将包含扩展资产。 创建一个 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 名为的 VSIX 项目 `MyObjectPropertiesExtension` 。 可以通过搜索 "vsix" 在 " **新建项目** " 对话框中找到 VSIX 项目模板。

2. 通过添加一个名为的自定义工具窗口项模板来添加工具窗口 `MyToolWindow` 。 在 **解决方案资源管理器** 中，右键单击项目节点，然后选择 "**添加**  >  **新项**"。 在 "**添加新项" 对话框** 中，切换到 " **Visual c # 项目**  >  **扩展性**" 并选择 "**自定义工具窗口**"。 在对话框底部的 " **名称** " 字段中，将文件名更改为 *MyToolWindow.cs*。 有关如何创建自定义工具窗口的详细信息，请参阅 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

3. 打开 *MyToolWindow.cs* 并添加以下 using 语句：

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. 现在，将以下字段添加到 `MyToolWindow` 类中。

   ```csharp
   private ITrackSelection trackSel;
   private SelectionContainer selContainer;

   ```

5. 将以下代码添加到 `MyToolWindow` 类。

   ```csharp
   private ITrackSelection TrackSelection
   {
       get
       {
           if (trackSel == null)
               trackSel =
                  GetService(typeof(STrackSelection)) as ITrackSelection;
           return trackSel;
       }
   }

   public void UpdateSelection()
   {
       ITrackSelection track = TrackSelection;
       if (track != null)
           track.OnSelectChange((ISelectionContainer)selContainer);
   }

   public void SelectList(ArrayList list)
   {
       selContainer = new SelectionContainer(true, false);
       selContainer.SelectableObjects = list;
       selContainer.SelectedObjects = list;
       UpdateSelection();
   }

   public override void OnToolWindowCreated()
   {
       ArrayList listObjects = new ArrayList();
       listObjects.Add(this);
       SelectList(listObjects);
   }
   ```

    `TrackSelection`属性使用 `GetService` 来获取 `STrackSelection` 提供接口的服务 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 。 `OnToolWindowCreated`事件处理程序和 `SelectList` 方法一起创建仅包含工具窗口窗格对象本身的选定对象的列表。 `UpdateSelection`方法通知 "**属性**" 窗口显示工具窗口窗格的公共属性。

6. 生成项目并启动调试。 应显示 Visual Studio 的实验实例。

7. 如果 " **属性** " 窗口不可见，请按 **F4** 打开它。

8. 打开 " **MyToolWindow** " 窗口。 可以在 **查看**  >  **其他窗口** 中找到它。

    窗口随即打开，并在 " **属性** " 窗口中显示 "窗口" 窗格的公共属性。

9. 将 "**属性**" 窗口中的 "**标题**" 属性更改为 **"我的对象属性**"。

     MyToolWindow 窗口标题会相应地更改。

## <a name="expose-tool-window-properties"></a>公开工具窗口属性

在本部分中，你将添加一个工具窗口并公开其属性。 对属性所做的更改将反映在 " **属性** " 窗口中。

### <a name="to-expose-tool-window-properties"></a>公开工具窗口属性

1. 打开 *MyToolWindow.cs*，并将公共布尔属性 IsChecked 添加到 `MyToolWindow` 类。

    ```csharp
    [Category("My Properties")]
    [Description("MyToolWindowControl properties")]
    public bool IsChecked
    {
        get {
            if (base.Content == null)  return false;
            return (bool)(( MyToolWindowControl) base.Content).checkBox.IsChecked;
        }
        set {
            ((MyToolWindowControl) base.Content).checkBox.IsChecked = value;
        }
    }
    ```

     此属性将从您稍后创建的 WPF 复选框中获取其状态。

2. 打开 *MyToolWindowControl.xaml.cs* ，并将 MyToolWindowControl 构造函数替换为以下代码。

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     这将提供对 `MyToolWindowControl` 窗格的访问权限 `MyToolWindow` 。

3. 在 *MyToolWindow.cs* 中，按如下所示更改 `MyToolWindow` 构造函数：

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. 更改为 MyToolWindowControl 的设计视图。

5. 删除按钮，并将 " **工具箱** " 中的复选框添加到左上角。

6. 添加选中和未选中的事件。 在 "设计" 视图中选择该复选框。 在 " **属性** " 窗口中，单击 " **属性** " 窗口右上角 (的 "事件处理程序" 按钮) 。 在文本框中查找 **选中** 内容并键入 **checkbox_Checked** ，然后查找 " **未选中** " 并在文本框中键入 **checkbox_Unchecked** 。

7. 添加复选框事件处理程序：

    ```csharp
    private void checkbox_Checked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = true;
        pane.UpdateSelection();
    }
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = false;
        pane.UpdateSelection();
    }
    ```

8. 生成项目并启动调试。

9. 在实验实例中，打开 " **MyToolWindow** " 窗口。

     在 " **属性** " 窗口中查找窗口的属性。 **IsChecked** 属性将显示在窗口底部的 "**我的属性**" 类别下。

10. 选中 " **MyToolWindow** " 窗口中的复选框。 "**属性**" 窗口中的 **IsChecked** 更改为 **True**。 清除 **MyToolWindow** 窗口中的复选框。 "**属性**" 窗口中的 **IsChecked** 更改为 **False**。 在 "**属性**" 窗口中更改 " **IsChecked** " 的值。 **MyToolWindow** 窗口中的复选框将发生更改以匹配新值。

    > [!NOTE]
    > 如果必须释放 " **属性** " 窗口中显示的对象，请 `OnSelectChange` `null` 先使用选择容器调用。 释放属性或对象后，可以更改为已更新和列表的选择容器 <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A> <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A> 。

## <a name="change-selection-lists"></a>更改选择列表

 在本部分中，将为基本属性类添加一个选择列表，并使用工具窗口界面选择要显示的选择列表。

### <a name="to-change-selection-lists"></a>更改选择列表

1. 打开 *MyToolWindow.cs* 并添加一个名为的公共类 `Simple` 。

    ```csharp
    public class Simple
    {
        private string someText = "";

        [Category("My Properties")]
        [Description("Simple Properties")]
        [DisplayName("My Text")]
        public string SomeText
        {
            get { return someText; }
            set { someText = value; }
        }

        [Category("My Properties")]
        [Description("Read-only property")]
        public bool ReadOnly
        {
            get { return false; }
        }
    }
    ```

2. 将 `SimpleObject` 属性添加到 `MyToolWindow` 类，再加上两种方法，用于在窗口窗格和对象之间切换 " **属性** " 窗口的选择 `Simple` 。

    ```csharp
    private Simple simpleObject = null;
    public Simple SimpleObject
    {
        get
        {
            if (simpleObject == null) simpleObject = new Simple();
            return simpleObject;
        }
    }

    public void SelectSimpleList()
    {
        ArrayList listObjects = new ArrayList();
        listObjects.Add(SimpleObject);
        SelectList(listObjects);
    }

    public void SelectThisList()
    {
        ArrayList listObjects = new ArrayList();
        listObjects.Add(this);
        SelectList(listObjects);
    }
    ```

3. 在 *MyToolWindowControl.cs* 中，将复选框处理程序替换为以下代码行：

    ```csharp
    private void checkbox_Checked(object sender, RoutedEventArgs e)
     {
        pane.IsChecked = true;
        pane.SelectSimpleList();
        pane.UpdateSelection();
    }
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = false;
        pane.SelectThisList();
        pane.UpdateSelection();
    }
    ```

4. 生成项目并启动调试。

5. 在实验实例中，打开 " **MyToolWindow** " 窗口。

6. 选中 " **MyToolWindow** " 窗口中的复选框。 " **属性** " 窗口显示 `Simple` 对象属性 **SomeText** 和 **ReadOnly**。 清除该复选框。 窗口的公共属性将显示在 " **属性** " 窗口中。

    > [!NOTE]
    > **SomeText** 的显示名称为 **"我的文本**"。

## <a name="best-practice"></a>最佳做法

在本演练中， <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 将实现，以便可以选择的对象集合和所选的对象集合为同一集合。 仅所选对象将显示在 "属性浏览器" 列表中。 有关更完整的 ISelectionContainer 实现，请参阅 ToolWindow 示例。

Visual Studio 工具窗口在 Visual Studio 会话之间保持不变。 有关保持工具窗口状态的详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 。

## <a name="see-also"></a>另请参阅

- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)
