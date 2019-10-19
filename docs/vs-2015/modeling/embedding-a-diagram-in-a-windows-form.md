---
title: 在 Windows 窗体中嵌入关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: fa6cd040-7c88-4329-b9c3-2a80b312610f
caps.latest.revision: 3
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 487105350fe5c62a9451bccc5713c6506c76bf1f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669691"
---
# <a name="embedding-a-diagram-in-a-windows-form"></a>在 Windows 窗体中嵌入图表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在 "[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]" 窗口中显示的 Windows 控件中嵌入 DSL 关系图。

## <a name="embedding-a-diagram"></a>嵌入关系图

#### <a name="to-embed-a-dsl-diagram-in-a-windows-control"></a>在 Windows 控件中嵌入 DSL 关系图

1. 向 DslPackage 项目添加一个新的**用户控件**文件。

2. 向用户控件添加 Panel 控件。 此面板将包含 DSL 关系图。

     添加所需的其他控件。

     设置控件的定位点属性。

3. 在解决方案资源管理器中，右键单击用户控件文件，然后单击 "**查看代码**"。 将此构造函数和变量添加到代码中：

    ```csharp

    internal UserControl1(MyDSLDocView docView, Control content)
      : this()
    {
      panel1.Controls.Add(content);
      this.docView = docView;
    }
    private MyDSLDSLDocView docView;

    ```

4. 向 DslPackage 项目添加一个新文件，其中包含以下内容：

    ```
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

5. 若要测试 DSL，请按 F5 并打开示例模型文件。 关系图显示在控件内。 工具箱和其他功能正常工作。

#### <a name="updating-the-form-using-store-events"></a>使用存储事件更新窗体

1. 在窗体设计器中，添加名为 `listBox1` 的**ListBox** 。 这将显示模型中元素的列表。 它将使用*存储事件*与模型一起保留在 synchronism 中。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

2. 在自定义代码文件中，重写 DocView 类的其他方法：

    ```

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

    ```

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

4. 若要测试 DSL，请按 F5，然后在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中，打开示例模型文件。

     请注意，列表框显示模型中元素的列表，并且在任何添加或删除之后以及在撤消和重做之后都是正确的。

## <a name="see-also"></a>请参阅
 [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)[编写代码以定制域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
