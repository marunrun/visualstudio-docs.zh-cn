---
title: 从后台线程更新 UML 模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 42c06b0b-b681-4e19-b5f3-6116dd2a4072
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9e6626faa09f1e38506c2d205d13caa9a3707fc0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659466"
---
# <a name="update-a-uml-model-from-a-background-thread"></a>从后台线程中更新 UML 模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有时它在后台线程中对模型进行更改时有用。 例如，如果你正在从速度较慢的外部资源加载信息，你可以使用后台线程来监督更新。 这允许用户在更新进行时查看每个更新。

 但请注意，该 UML 存储区并不是线程安全的。 以下预防措施非常重要：

- 每次对模型或关系图进行更新，必须在用户界面 (UI) 线程中进行。 必须使用后台线程 <xref:System.Windows.Forms.Control.Invoke%2A> 或 `Dispatcher.`<xref:System.Windows.Threading.Dispatcher.Invoke%2A> 来使 UI 线程执行实际更新。

- 如果将一系列更改集合成单个事务，我们建议你在事务进行时避免让用户编辑模型。 否则，用户所做的任何编辑都将成为在同一事务的一部分。 你可以通过模式对话框来避免用户进行更改。 如果你愿意，可以在对话框中提供“取消”按钮。 用户可以在发生更改时看到他们。

## <a name="example"></a>示例
 此示例使用后台线程对模型进行几项更改。 使用了一个对话框来在运行该线程时排除用户。 在此简单示例中，该对话框中未提供“取消”按钮。 不过，添加此功能很容易。

#### <a name="to-run-the-example"></a>运行示例

1. 在C#项目中创建一个命令处理程序，如在[建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)中所述。

2. 确保该项目包含对这些程序集的引用：

   - Microsoft.VisualStudio.ArchitectureTools.Extensibility

   - Microsoft.VisualStudio.Modeling.Sdk.[版本号]

   - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]

   - Microsoft.VisualStudio.Uml.Interfaces

   - System.ComponentModel.Composition

   - System.Windows.Forms

3. 向项目添加一个名为**ProgressForm**的 Windows 窗体。 此窗体应显示一条指示正在进行更新的消息。 它不必包含任何其他控件。

4. 添加一个 C# 文件，其中包含步骤 7 后显示的代码。

5. 生成并运行该项目。

    一个新的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实例将以实验模式打开。

6. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实验实例中创建或打开一个 UML 类关系图。

7. 右键单击 UML 类图中的任意位置，然后单击 "**添加多个 UML 类**"。

   关系图中将以半秒的时间间隔接连显示若干新的类框。

```csharp
using System;
using System.ComponentModel;
using System.ComponentModel.Composition;
using System.Threading;
using System.Windows.Forms;

using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using Microsoft.VisualStudio.Uml.Classes;

namespace BackgroundThreadProgressUI // CHANGE TO YOUR NAMESPACE
{
  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  class UmlClassAdderCommand : ICommandExtension
  {

    [Import]
    IDiagramContext context { get; set; }

    [Import]
    ILinkedUndoContext linkedUndoContext { get; set; }

    // Called when the user runs the command.
    public void Execute(IMenuCommand command)
    {
      // The form that will exclude the user.
      ProgressForm form = new ProgressForm();

      // System.ComponentModel.BackgroundWorker is a
      // convenient way to run a background thread.
      BackgroundWorker worker = new BackgroundWorker();
      worker.WorkerSupportsCancellation = true;

      worker.DoWork += delegate(object sender, DoWorkEventArgs args)
      {
        // This block will be executed in a background thread.

        IClassDiagram diagram = context.CurrentDiagram as IClassDiagram;
        IModelStore store = diagram.ModelStore;
        const int CLASSES_TO_CREATE = 15;

        // Group all the changes together.
        using (ILinkedUndoTransaction transaction = linkedUndoContext.BeginTransaction("Background Updates"))
        {
          for (int i = 1; i < CLASSES_TO_CREATE; i++)
          {
            if (worker.CancellationPending)
               return; // No commit - undo all.

            // Create model elements using the UI thread by using
            // the Invoke method on the progress form. Always
            // modify the model and diagrams from a UI thread.
            form.Invoke((MethodInvoker)(delegate
            {
              IClass newClass = store.Root.CreateClass();
              newClass.Name = string.Format("NewClass{0}", i);
              diagram.Display(newClass);
            }));

            // Sleep briefly so that we can watch the updates.
            Thread.Sleep(500);
          }

          // Commit the transaction or it will be rolled back.
          transaction.Commit();
        }
      };

      // Close the form when the thread completes.
      worker.RunWorkerCompleted += delegate(object sender, RunWorkerCompletedEventArgs args)
      {
        form.Close();
      };

      // Start the thread before showing the modal progress dialog.
      worker.RunWorkerAsync();

      // Show the form modally, parented on VS.
      // Prevents the user from making changes while in progress.
      form.ShowDialog();
    }

    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled = command.Visible = true;
    }

    public string Text
    {
      get { return "Add several classes"; }
    }
  }
}
```

#### <a name="to-allow-the-user-to-cancel-the-thread-in-the-example"></a>允许用户取消示例中的线程

1. 向进程对话框添加一个“取消”按钮。

2. 向进程对话框添加下列代码：

     `public event MethodInvoker Cancel;`

     `private void CancelButton_Click(object sender, EventArgs e)`

     `{`

     `Cancel();`

     `}`

3. 在 Execute() 方法中，在窗体构造后插入此行：

     `form.Cancel += delegate() { worker.CancelAsync(); };`

### <a name="other-methods-of-accessing-the-ui-thread"></a>访问 UI 线程的其他方法
 如果不需要创建对话框，则可以访问显示关系图的控件：

 `DiagramView uiThreadHolder = context.CurrentDiagram.GetObject<Diagram>().ActiveDiagramView;`

 可以使用 `uiThreadHolder.Invoke()` 在 UI 线程中执行操作。

## <a name="see-also"></a>请参阅
 [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)在[建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)
