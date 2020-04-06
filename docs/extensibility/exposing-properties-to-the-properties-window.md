---
title: 向属性窗口公开属性 |微软文档
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
ms.openlocfilehash: f84962628ae550676e2c2eeb10c0f3baeca1bb58
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711830"
---
# <a name="expose-properties-to-the-properties-window"></a>向"属性"窗口公开属性

本演练将对象的公共属性公开到 **"属性"** 窗口。 对这些属性所做的更改将反映在 **"属性"** 窗口中。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="expose-properties-to-the-properties-window"></a>向"属性"窗口公开属性

在本节中，您将创建一个自定义工具窗口，并在 **"属性"** 窗口中显示关联的窗口窗格对象的公共属性。

### <a name="to-expose-properties-to-the-properties-window"></a>向"属性"窗口公开属性

1. 每个 Visual Studio 扩展都从 VSIX 部署项目开始，该项目将包含扩展资产。 创建[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]名为 的`MyObjectPropertiesExtension`VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 通过添加名为 的`MyToolWindow`自定义工具窗口项模板来添加工具窗口。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在 **"添加新项目"对话框**中，转到**可视化 C# 项** > **扩展性**并选择 **"自定义工具窗口**"。 在对话框底部的 **"名称"** 字段中，将文件名更改为*MyToolWindow.cs*。 有关如何创建自定义工具窗口的详细信息，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

3. 打开*MyToolWindow.cs*并添加以下使用语句：

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. 现在向`MyToolWindow`类添加以下字段。

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

    属性`TrackSelection`用于`GetService`获取提供`STrackSelection`<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>接口的服务。 事件`OnToolWindowCreated`处理程序和方法`SelectList`共同创建仅包含工具窗口窗格对象本身的选定对象的列表。 该方法`UpdateSelection`告诉 **"属性"** 窗口显示工具窗口窗格的公共属性。

6. 生成项目并启动调试。 应出现视觉工作室的实验实例。

7. 如果**属性**窗口不可见，则通过按**F4**打开它。

8. 打开 **"我的工具窗口"窗口**。 您可以在 **"查看** > **其他窗口**"中找到它。

    窗口将打开，窗口窗格的公共属性将显示在 **"属性"** 窗口中。

9. 将 **"属性**"窗口中**的标题**属性更改为 **"我的对象属性**"。

     "MyTool 窗口"窗口标题会相应地更改。

## <a name="expose-tool-window-properties"></a>公开工具窗口属性

在本节中，添加工具窗口并公开其属性。 对属性所做的更改将反映在 **"属性"** 窗口中。

### <a name="to-expose-tool-window-properties"></a>公开工具窗口属性

1. 打开*MyToolWindow.cs*，并将公共布尔属性"是检查"添加到类`MyToolWindow`中。

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

     此属性从稍后将创建的 WPF 复选框中获取其状态。

2. 打开*MyToolWindowControl.xaml.cs，* 并将 MyToolWindowControl 构造函数替换为以下代码。

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     这允许`MyToolWindowControl`访问`MyToolWindow`窗格。

3. 在*MyToolWindow.cs*中，`MyToolWindow`更改构造函数如下所示：

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. 更改为 MyToolWindowControl 的设计视图。

5. 删除该按钮，并将复选框从 **"工具"框**添加到左上角。

6. 添加选中和未选中的事件。 选择设计视图中的复选框。 在"**属性"** 窗口中，单击事件处理程序按钮（在 **"属性"** 窗口的右上角）。 在文本框中查找 **"已选中****"并键入checkbox_Checked，** 然后在文本框中查找 **"未选中**"并键入**checkbox_Unchecked。**

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

9. 在实验例中，打开**MyTool 窗口**。

     在 **"属性"** 窗口中查找窗口的属性。 **"IsChecked"** 属性显示在窗口底部，"**我的属性**"类别下。

10. 选中 **"MyTool 窗口"窗口中**的复选框。 **在****"属性"** 窗口中选中更改为**True**。 清除 **"MyTool 窗口"窗口中**的复选框。 **在****"属性"** 窗口中选中更改为**False**。 在 **"属性"** 窗口中更改 **"已检查"** 的值。 **"MyToolWindow"窗口中**的复选框将更改以匹配新值。

    > [!NOTE]
    > 如果必须释放"**属性"** 窗口中显示的对象，请先使用`OnSelectChange``null`选择容器进行调用。 处理属性或对象后，可以更改为已更新<xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A>并<xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A>列出的选择容器。

## <a name="change-selection-lists"></a>更改选择列表

 在本节中，您可以为基本属性类添加选择列表，并使用工具窗口界面选择要显示的选择列表。

### <a name="to-change-selection-lists"></a>更改选择列表

1. 打开*MyToolWindow.cs*并添加名为 的公共`Simple`类。

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

2. `MyToolWindow`向类`SimpleObject`添加属性，以及两个在窗口窗格和`Simple`对象之间切换 **"属性**"窗口选择的方法。

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

3. 在*MyToolWindowControl.cs*中，将复选框处理程序替换为以下代码行：

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

5. 在实验例中，打开**MyTool 窗口**。

6. 在 **"MyTool 窗口"窗口中**选择复选框。 属性**窗口**显示`Simple`对象属性"**某些文本**"和 **"只读"。** 清除复选框。 窗口的公共属性将显示在 **"属性"** 窗口中。

    > [!NOTE]
    > **某些文本**的显示名称是 **"我的文本**"。

## <a name="best-practice"></a>最佳做法

在本演练中，<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>实现可选择的对象集合和所选对象集合是同一集合。 只有所选对象显示在属性浏览器列表中。 有关更完整的 I选择容器实现，请参阅参考.ToolWindow 示例。

可视化工作室工具窗口在可视化工作室会话之间保留。 有关保留工具窗口状态的详细信息，请参阅<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>。

## <a name="see-also"></a>请参阅

- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)
