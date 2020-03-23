---
title: 使用调试器管理异常 |微软文档
ms.custom: seodec18
ms.date: 10/09/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.exceptions
- vs.debug.exceptions.find
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- run-time errors
- exception handling, during debugging
- errors [debugger]
- debugger, runtime errors
- On Error-style error handlers
- exceptions, Win32
- run-time errors, debugging
- Win32, exceptions
- run time, exceptions
- error handling
- debugging [Visual Studio], exception handling
- common language runtime, exceptions
- native run-time checks
- exceptions, debugging
ms.assetid: 43a77fa8-37d0-4c98-a334-0134dbca4ece
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 00ad5b41dd0a11661d281f24474b7673ea0a342c
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301121"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>使用可视化工作室中的调试器管理异常

异常是执行程序时发生的错误状态的指示。 您可以告诉调试器要打开哪些异常或异常集，以及此时您希望调试器中断（即在调试器中暂停）。 当调试器中断时，它会显示异常被抛出的位置。 您还可以添加或删除异常。 在 Visual Studio 中打开解决方案后，请使用**调试> Windows >异常设置**来打开 **"例外设置"** 窗口。

提供响应最重要异常的处理程序。 如果需要知道如何添加异常处理程序，请参阅[编写更好的 C# 代码来修复 Bug。](../debugger/write-better-code-with-visual-studio.md) 此外，了解如何将调试器配置为始终中断某些异常的执行。

发生异常时，调试器将异常消息写入**输出**窗口。 在下列情况下，它可能会中断执行：

- 引发未处理的异常。
- 调试器配置为在调用任何处理程序之前中断执行。
- 您已设置["仅我的代码](../debugger/just-my-code.md)"，调试器配置为在用户代码中未处理的任何异常时中断。

> [!NOTE]
> ASP.NET 有一个顶级异常处理程序，可以在浏览器中显示错误页。 除非启用 **"我的代码"，** 否则不会中断执行。 例如，请参阅[告诉调试器继续处理用户未处理的异常](#BKMK_UserUnhandled)。

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> 在 Visual Basic 应用程序中，调试程序将所有错误作为异常进行管理，即使使用出错时样式错误处理程序也是如此。

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>告诉调试器在引发异常时中断

调试器可以在引发异常时中断执行，因此您可以在调用处理程序之前检查异常。

在 **"异常设置**"窗口中（**调试> Windows >异常设置**），展开异常类别（如**通用语言运行时异常）的**节点。 然后，选择该类别中特定异常的复选框，如**System.Access"异常**"。 还可以选择整个类别的异常。

![已选中 AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "异常设置检查访问")

> [!TIP]
> 您可以使用 **"异常设置"** 工具栏中的 **"搜索**"窗口查找特定异常，或使用搜索来筛选特定命名空间（如**System.IO**）。

如果在 **"异常设置"** 窗口中选择异常，则调试器将在引发异常的位置中断，无论是否处理。 现在，异常称为第一次机会异常。 以下是几个应用场景示例：

- 在以下 C# 控制台应用程序中，Main 方法在`try/catch`块内引发**Access"冲突异常**"。

  ```csharp
  static void Main(string[] args)
  {
      try
      {
          throw new AccessViolationException();
          Console.WriteLine("here");
      }
      catch (Exception e)
      {
          Console.WriteLine("caught exception");
      }
      Console.WriteLine("goodbye");
  }
  ```

  如果在 **"异常设置"** 中选中**了 Access"冲突异常**"，则`throw`当您在调试器中运行此代码时，将在行上执行。 然后可以继续执行。 控制台应显示这两行：

  ```cmd
  caught exception
  goodbye
  ```

  但它不显示线条`here`。

- C# 控制台应用程序引用具有两种方法的类库。 一种方法引发异常并处理它，而第二个方法引发相同的异常，但不处理它。

  ```csharp
  public class Class1
  {
      public void ThrowHandledException()
      {
          try
          {
              throw new AccessViolationException();
          }
          catch (AccessViolationException ave)
          {
              Console.WriteLine("caught exception" + ave.Message);
          }
      }

      public void ThrowUnhandledException()
      {
          throw new AccessViolationException();
      }
  }
  ```

  以下是控制台应用程序的 Main() 方法：

  ```csharp
  static void Main(string[] args)
  {
      Class1 class1 = new Class1();
      class1.ThrowHandledException();
      class1.ThrowUnhandledException();
  }
  ```

  如果在 **"异常设置"** 中选中**了 Access"异常"，** 则当您`throw`在调试器中运行此代码时，执行将在**ThrowHandledException（）** 和 **"Throw Unhandled异常"** 中执行。

要将异常设置还原到默认值，请选择"**将列表还原到默认设置**"按钮：

![还原异常设置中的默认值](../debugger/media/restoredefaultexceptions.png "还原默认异常")

## <a name="tell-the-debugger-to-continue-on-user-unhandled-exceptions"></a><a name="BKMK_UserUnhandled"></a>告诉调试器继续处理用户未处理的异常

如果使用["我的代码](../debugger/just-my-code.md)"调试 .NET 或 JavaScript 代码，则可以告诉调试器，以防止在用户代码中处理但在其他地方处理的异常。

1. 在 **"例外设置"** 窗口中，通过右键单击列标签打开快捷菜单，然后选择 **"显示列>其他操作**"。 （如果您已关闭 **"仅我的代码"，** 则看不到此命令。将显示名为 **"其他操作"的第**三列。

   ![其他操作列](../debugger/media/additionalactionscolumn.png "其他操作栏")

   对于在此列**中用户代码中未处理时显示"继续"** 的异常，如果该异常未在用户代码中处理，而是外部处理，则调试器将继续。

2. 要更改特定异常的此设置，请选择异常，右键单击以显示快捷菜单，然后选择"**用户代码 中未处理时继续**"。 您还可以更改整个异常类别（如整个通用语言运行时异常）的设置。

   ![[在用户代码中未处理时继续]](../debugger/media/continuewhenunhandledinusercodesetting.png "在用户代码设置中未处理时继续")

例如，ASP.NET Web 应用程序通过将异常转换为 HTTP 500 状态代码[（ASP.NET Web API 中的异常处理](/aspnet/web-api/overview/error-handling/exception-handling)）来处理异常，这可能无助于您确定异常的来源。 在下面的示例中，用户代码对引发 `String.Format()` 的 <xref:System.FormatException>进行调用。 异常中断如下所示：

![用户&#45;未处理异常的中断](../debugger/media/exceptionunhandledbyuser.png "异常未按用户处理")

## <a name="add-and-delete-exceptions"></a>添加和删除异常

可以添加和删除异常。 要从类别中删除异常类型，请选择异常，然后从 **"例外设置"** 工具栏上的列表按钮（减号）**中选择"删除所选异常**"。 或者，您可以右键单击异常并选择"从快捷菜单**中删除**"。 删除异常的效果与取消选中异常的效果相同，即调试器在引发异常时不会中断。

要添加异常：

1. 在 **"例外设置"** 窗口中，选择一个异常类别（例如，**通用语言运行时**）。

2. 选择"**向所选类别添加异常**"按钮（加号）。

   ![[向所选类别添加异常] 按钮](../debugger/media/addanexceptiontotheselectedcategorybutton.png "添加"异常"到所选类别按钮")

3. 键入异常的名称（例如，**系统.UriTemplate 匹配异常**）。

   ![键入异常名称](../debugger/media/typetheexceptionname.png "键入异常名称")

   异常将添加到列表中（按字母顺序排列），并自动选中。

要向 GPU 内存访问异常添加异常，JavaScript 运行时异常或 Win32 异常类别包括错误代码和说明。

> [!TIP]
> 请检查你的拼写！ **"例外设置"** 窗口不检查是否存在添加的异常。 因此，如果您键入**Sytem.UriTemplateMatchException，** 您将获得该异常的条目（而不是**针对 System.UriTemplate 匹配异常**）。

异常设置保留在解决方案的 .suo 文件中，因此适用于特定解决方案。 无法跨解决方案重用特定异常设置。 现在只保留添加的异常;删除的异常不是。 您可以添加异常，关闭并重新打开解决方案，并且该异常仍将存在。 但是，如果删除一个异常，然后关闭/重新打开解决方案，异常将消失。

**“异常设置”** 窗口在 C# 中支持通用异常类型，但在 Visual Basic 中不支持。 要对类似 `MyNamespace.GenericException<T>`的异常执行中断操作，则必须将异常作为 **MyNamespace.GenericException`1**添加。 也就是说，如果您创建了如下所示的异常：

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

您可以使用前面的过程将异常添加到**异常设置**：

![添加常见异常](../debugger/media/addgenericexception.png "添加通用异常")

## <a name="add-conditions-to-an-exception"></a>向异常添加条件

使用 **"例外设置"** 窗口设置异常条件。 当前支持的条件包括要包括或排除异常的模块名称。 通过将模块名称设置为条件，您可以选择仅在某些代码模块上为异常设置中断。 您也可以选择避免中断特定模块。

> [!NOTE]
> 支持从 中[!include[vs_dev15](../misc/includes/vs_dev15_md.md)]开始向异常添加条件。

要添加条件异常：

1. 在"异常设置"窗口中选择 **"编辑条件**"按钮，或右键单击异常并选择 **"编辑条件**"。

   ![异常的条件](../debugger/media/dbg-conditional-exception.png "Dbg条件异常")

2. 要向异常添加额外的必需条件，请选择为每个新条件**添加条件**。 将显示其他条件行。

   ![异常的额外条件](../debugger/media/extraconditionsforanexception.png "例外的外附加条件")

3. 对于每个条件行，键入模块的名称，并将比较运算符列表更改为**等于**或不**等于**。 您可以在名称中指定通配**\\**符 （ ） 以指定多个模块。

4. 如果需要删除条件，请选择条件行末尾的**X。**

## <a name="see-also"></a>另请参阅

- [异常后继续执行](../debugger/continuing-execution-after-an-exception.md)<br/>
- [如何：在异常后检查系统代码](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [如何：使用本机运行时检查](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [使用没有 C 运行时库的运行时检查](../debugger/using-run-time-checks-without-the-c-run-time-library.md)<br/>
- [初探调试器](../debugger/debugger-feature-tour.md)
