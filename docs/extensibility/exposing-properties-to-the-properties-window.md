---
title: 公开属性设置为属性窗口 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2cd1f44342199c26506cceb4c77378b13aefd566
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341230"
---
# <a name="expose-properties-to-the-properties-window"></a>公开属性设置为属性窗口

本演练中公开的对象的公共属性**属性**窗口。 对这些属性进行的更改会反映在**属性**窗口。

## <a name="prerequisites"></a>系统必备

从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="expose-properties-to-the-properties-window"></a>公开属性设置为属性窗口

在本部分中，创建自定义工具窗口并显示关联的窗口窗格对象中的公共属性**属性**窗口。

### <a name="to-expose-properties-to-the-properties-window"></a>若要公开属性设置为属性窗口

1. 每个 Visual Studio 扩展开始于 VSIX 部署项目，它将包含扩展资产。 创建[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSIX 项目名为`MyObjectPropertiesExtension`。 您可以发现中的 VSIX 项目模板**新的项目**通过搜索"vsix"对话框。

2. 通过添加一个名为的自定义工具窗口项模板添加工具窗口`MyToolWindow`。 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 在中**添加新项对话框**，请转到**Visual C# 项** > **扩展性**，然后选择**自定义工具窗口**。 在中**名称**在对话框底部字段中，将文件名称更改为*MyToolWindow.cs*。 有关如何创建自定义工具窗口的详细信息，请参阅[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

3. 打开*MyToolWindow.cs*并添加以下 using 语句：

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. 现在，添加以下字段以`MyToolWindow`类。

   ```csharp
   private ITrackSelection trackSel;
   private SelectionContainer selContainer;

   ```

5. 向 `MyToolWindow` 类添加下面的代码。

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

    `TrackSelection`属性使用`GetService`来获取`STrackSelection`服务，提供了<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>接口。 `OnToolWindowCreated`事件处理程序和`SelectList`方法一起创建了包含仅的工具窗口窗格对象本身所选对象的列表。 `UpdateSelection`方法会示意**属性**窗口中显示的工具窗口窗格的公共属性。

6. 生成项目并启动调试。 应显示 Visual Studio 的实验实例。

7. 如果**属性**窗口不可见，请按打开**F4**。

8. 打开**MyToolWindow**窗口。 你可以找到它在**视图** > **其他 Windows**。

    打开相应的窗口和窗口窗格中的公共属性显示在**属性**窗口。

9. 更改**标题**属性中的**属性**窗口**我的对象属性**。

     MyToolWindow 窗口标题也会相应更改。

## <a name="expose-tool-window-properties"></a>公开工具窗口属性

在本部分中，添加工具窗口，并公开其属性。 对属性所做的更改反映在**属性**窗口。

### <a name="to-expose-tool-window-properties"></a>若要公开工具窗口属性

1. 打开*MyToolWindow.cs*，并添加公共的布尔属性 IsChecked 到`MyToolWindow`类。

    ```csharp
    [Category("My Properties")]
    [Description("MyToolWindowControl properties")]
    public bool IsChecked
    {
        get {
            if (base.Content == null)  return false;
            return (bool)(( MyToolWindowControl) base.Content).checkBox.IsChecked;
        }
        set {
            ((MyToolWindowControl) base.Content).checkBox.IsChecked = value;
        }
    }
    ```

     此属性获取其状态从稍后将创建的 WPF 复选框。

2. 打开*MyToolWindowControl.xaml.cs*和 MyToolWindowControl 构造函数替换为以下代码。

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     这样`MyToolWindowControl`访问`MyToolWindow`窗格。

3. 在中*MyToolWindow.cs*，更改`MyToolWindow`构造函数，如下所示：

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. 将更改为 MyToolWindowControl 的设计视图。

5. 删除按钮并添加一个复选框，从**工具箱**到左上角。

6. Checked 和 Unchecked 事件添加。 在设计视图中选择相应的复选框。 中**属性**窗口中，单击事件处理程序按钮 (右上角**属性**窗口)。 查找**Checked**并键入**checkbox_Checked**在文本框中，然后找到**选中此项**并键入**checkbox_Unchecked**在文本框中。

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

9. 在实验实例中，打开**MyToolWindow**窗口。

     窗口的属性中查找**属性**窗口。 **IsChecked**属性下显示在窗口的底部**我的属性**类别。

10. 选中该复选框**MyToolWindow**窗口。 **IsChecked**中**属性**窗口更改为**True**。 清除中的复选框**MyToolWindow**窗口。 **IsChecked**中**属性**窗口更改为**False**。 更改的值**IsChecked**中**属性**窗口。 中的复选框**MyToolWindow**窗口更改以匹配新值。

    > [!NOTE]
    > 如果必须显示在对象的 dispose**属性**窗口中，调用`OnSelectChange`与`null`选择容器第一个。 后释放该属性或对象，您可以更改为已更新的选择容器<xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A>和<xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A>列出。

## <a name="change-selection-lists"></a>更改所选内容列表

 在本部分中，添加选择列表的基本属性类并使用工具窗口界面选择要显示的选择列表。

### <a name="to-change-selection-lists"></a>若要更改的选择列表

1. 打开*MyToolWindow.cs*并添加一个名为的公共类`Simple`。

    ```csharp
    public class Simple
    {
        private string someText = "";

        [Category("My Properties")]
        [Description("Simple Properties")]
        [DisplayName("My Text")]
        public string SomeText
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

2. 添加`SimpleObject`属性设置为`MyToolWindow`类，以及两种方法来切换**属性**窗口窗格之间的窗口选定内容和`Simple`对象。

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

3. 在中*mytoolwindowcontrol.cs*，复选框处理程序替换为以下代码行：

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

5. 在实验实例中，打开**MyToolWindow**窗口。

6. 选择中的复选框**MyToolWindow**窗口。 **属性**窗口将显示`Simple`对象属性， **SomeText**并**ReadOnly**。 清除复选框。 在窗口的公共属性显示在**属性**窗口。

    > [!NOTE]
    > 显示名称**SomeText**是**我的文本**。

## <a name="best-practice"></a>最佳做法

在此演练中，<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>实现，以便可选择对象集合和所选的对象集合是相同的集合。 仅所选的对象显示在属性浏览器列表。 有关更完整的 ISelectionContainer 实现，请参阅 Reference.ToolWindow 示例。

Visual Studio 会话之间持久保存 visual Studio 工具窗口。 有关保留工具窗口状态的详细信息，请参阅<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>。

## <a name="see-also"></a>请参阅

- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)