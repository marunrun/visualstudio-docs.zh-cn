---
title: 在 Windows 窗体中嵌入图表
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3e81a5ff10cd6e309ffbf17e40ffbaa9ec88f185
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547623"
---
# <a name="embed-a-diagram-in-a-windows-form"></a>在 Windows 窗体中嵌入图表

可以在显示在 Visual Studio 窗口中的 Windows 控件中嵌入 DSL 关系图。

## <a name="embed-a-dsl-diagram-in-a-windows-control"></a>在 Windows 控件中嵌入 DSL 关系图

1. 向 DslPackage 项目添加一个新的 **用户控件** 文件。

2. 向用户控件添加 Panel 控件。 此面板将包含 DSL 关系图。

     添加所需的其他控件。

     设置控件的定位点属性。

3. 在解决方案资源管理器中，右键单击用户控件文件，然后单击 " **查看代码**"。 将此构造函数和变量添加到代码中：

    ```csharp
    internal UserControl1(MyDSLDocView docView, Control content)
      : this()
    {
      panel1.Controls.Add(content);
      this.docView = docView;
    }
    private MyDSLDocView docView;
    ```

4. 向 DslPackage 项目添加一个新文件，其中包含以下内容：

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

5. 若要测试 DSL，请按 **F5** 并打开示例模型文件。 关系图显示在控件内。 工具箱和其他功能正常工作。

## <a name="update-the-form-using-store-events"></a>使用存储事件更新窗体

1. 在窗体设计器中，添加一个名为的 **ListBox** `listBox1` 。 这将显示模型中元素的列表。 它使用 *存储事件*与模型同步。 有关详细信息，请参阅 [事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

2. 在自定义代码文件中，重写 DocView 类的其他方法：

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

3. 在用户控件后面的代码中，插入用于侦听添加和删除的元素的方法：

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

4. 若要测试 DSL，请按 **F5** ，然后在 Visual Studio 的实验实例中，打开示例模型文件。

     请注意，列表框显示模型中元素的列表，并且在任何添加或删除之后以及在撤消和重做之后都是正确的。

## <a name="see-also"></a>另请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
