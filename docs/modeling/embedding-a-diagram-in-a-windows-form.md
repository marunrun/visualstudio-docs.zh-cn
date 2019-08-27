---
title: 在 Windows 窗体中嵌入图表
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9b2ed12175e986178d43ffe5e3da8b85e2ab22e5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62994585"
---
# <a name="embed-a-diagram-in-a-windows-form"></a>在 Windows 窗体中嵌入图表

您可以在 Windows 控件，将显示在 Visual Studio 窗口中嵌入 DSL 关系图。

## <a name="embed-a-dsl-diagram-in-a-windows-control"></a>在 Windows 控件中嵌入 DSL 关系图

1. 添加一个新**用户控件**到 DslPackage 项目的文件。

2. 将在面板控件添加到用户控件。 此面板将包含 DSL 关系图。

     添加所需的其他控件。

     设置控件的定位点属性。

3. 在解决方案资源管理器，右键单击用户控件文件，然后单击**查看代码**。 将此构造函数和变量添加到代码中：

    ```csharp
    internal UserControl1(MyDSLDocView docView, Control content)
      : this()
    {
      panel1.Controls.Add(content);
      this.docView = docView;
    }
    private MyDSLDocView docView;
    ```

4. 将新文件添加到 DslPackage 项目中包含以下内容：

    ```csharp
    using System.Windows.Forms;
    namespace Company.MyDSL
    {
      partial class MyDSLDocView
      {
        private UserControl1 container;
        public override IWin32Window Window
        {
          get
          {
            if (container == null)
            {
              // Put our own form inside the DSL window:
              container = new UserControl1(this,
                (Control)base.Window);
            }
            return container;
    } } } }
    ```

5. 若要测试 DSL，按**F5**并打开示例模型文件。 该控件中显示关系图。 工具箱和其他功能会正常工作。

## <a name="update-the-form-using-store-events"></a>更新窗体使用存储事件

1. 在窗体设计器中，添加**ListBox**名为`listBox1`。 这将在模型中显示的元素的列表。 与模型使用同步*存储事件*。 有关详细信息，请参阅[事件处理程序传播更改外部模型](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

2. 在自定义代码文件中，重写进一步 DocView 类的方法：

    ```csharp
    partial class MyDSLDocView
    {
     /// <summary>
     /// Register store event listeners.
     /// This method is called when the model and diagram
     /// have completed loading.
     /// </summary>
     protected override bool LoadView()
      {
        bool result = base.LoadView();
        Store store = this.DocData.Store;
        EventManagerDirectory emd = store.EventManagerDirectory;
        DomainClassInfo componentClass = store.DomainDataDirectory.FindDomainClass(typeof(ExampleElement));
        emd.ElementAdded.Add(componentClass, new EventHandler<ElementAddedEventArgs>(AddElement));
        emd.ElementDeleted.Add(componentClass, new EventHandler<ElementDeletedEventArgs>(RemoveElement));

        // Do the initial parts list:
        container.SetUpFormFromModel();
        return result;
      }
     /// <summary>
     /// Listener method called on creation of each instance of
     /// the ExampleElement class or its subclasses.
     /// </summary>
     private void AddElement(object sender, ElementAddedEventArgs e)
     {
       container.Add(e.ModelElement as ExampleElement);
     }
     /// <summary>
     /// Listener method called after deletion of each instance of
     /// the ExampleElement class or its subclasses.
     /// </summary>
     private void RemoveElement(object sender, ElementDeletedEventArgs e)
     {
       container.Remove(e.ModelElement as ExampleElement);
     }
    ```

3. 在针对该用户控件代码中，插入方法来侦听元素中添加和删除：

    ```csharp
    public partial class UserControl1 : UserControl { ...

    private ExampleModel modelRoot;

    internal void Add(ExampleElement e) { UpdatePartsList(); }
    internal void Remove(ExampleElement e) { UpdatePartsList(); }

    internal void SetUpFormFromModel()
    {
      modelRoot = this.docView.CurrentDiagram.ModelElement as ExampleModel;
      UpdatePartsList();
    }

    private void UpdatePartsList()
    {
      StringBuilder builder = new StringBuilder();
      listBox1.Items.Clear();
      foreach (ExampleElement c in modelRoot.Elements)
      {
        listBox1.Items.Add(c.Name);
      }
    }
    ```

4. 若要测试 DSL，按**F5**并在 Visual Studio 的实验实例中，打开示例模型文件。

     请注意，列表框中显示的元素的列表在模型中，并且它是正确任何添加或删除操作，以及撤消和重做。

## <a name="see-also"></a>请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
