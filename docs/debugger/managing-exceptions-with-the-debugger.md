---
title: 管理调试器的异常 |Microsoft Docs
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
ms.openlocfilehash: b83cb026bec6d33490517e5703a042b4a8e2434c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62846457"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>管理 Visual Studio 中调试器的异常

异常是执行程序时发生的错误状态的指示。 哪些异常或异常执行中断，组可以让调试程序并想要调试器中断的位置 （即，在调试器中暂停）。 调试器中断，它会显示引发异常的位置。 您还可以添加或删除的异常。 使用 Visual Studio 中打开的解决方案中，使用**调试 > Windows > 异常设置**以打开**异常设置**窗口。

提供响应最重要的异常处理程序。 如果您需要知道如何添加异常的处理程序，请参阅[通过编写更好地修复 bugC#代码](../debugger/write-better-code-with-visual-studio.md)。 此外，了解如何配置调试器始终中断执行的一些异常。

异常发生时，调试程序将一条异常消息写入到“输出”窗口。 它可能会中断执行，在以下情况下，当：

- 是引发未处理异常。
- 将调试器配置为中断执行之前调用任何处理程序。
- 已设置[仅我的代码](../debugger/just-my-code.md)，并将调试器配置为在用户代码中未处理任何异常发生时中断。

> [!NOTE]
> ASP.NET 有一个顶级异常处理程序，可以在浏览器中显示错误页。 它不会中断执行，除非**仅我的代码**处于开启状态。 有关示例，请参阅[让调试程序在用户未经处理的异常时继续](#BKMK_UserUnhandled)下面。

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> 在 Visual Basic 应用程序中，调试程序将所有错误作为异常进行管理，即使使用出错时样式错误处理程序也是如此。

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>让调试器在引发异常时中断

调试器可以在引发异常的点处中断执行，以便调用处理程序之前，可能会检查该异常。

在中**异常设置**窗口 (**调试 > Windows > 异常设置**)，展开的节点，一个类别的异常，例如**公共语言运行时异常**. 然后选择该类别中的特定异常的复选框，如**System.AccessViolationException**。 还可以选择整个类别的异常。

![选中 AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")

> [!TIP]
> 你可以通过使用查找特定异常**搜索**中的窗口**异常设置**工具栏中或使用搜索筛选特定命名空间 (如**System.IO**)。

如果选择中的异常**异常设置**窗口中，引发异常，无论是否对其进行处理的任何位置调试程序执行将中断。 现在该异常被称为第一次异常。 以下是几个应用场景示例：

- 在下面的 C# 控制台应用程序中，Main 方法在 `try/catch` 块内引发“AccessViolationException”。

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

  如果有**AccessViolationException**签入**异常设置**，将中断执行`throw`行时在调试器中运行此代码。 然后可以继续执行。 控制台应显示这两行：

  ```cmd
  caught exception
  goodbye
  ```

  但它不会显示`here`行。

- C# 控制台应用程序引用具有两种方法的类的类库。 一种方法引发异常，并处理它，而第二种方法会引发同一异常但不会进行处理。

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

  如果有**AccessViolationException**签入**异常设置**，将中断执行`throw`在这两行**ThrowHandledException()** 和**ThrowUnhandledException()** 在调试器中运行此代码时。

若要将异常设置还原为默认值，请选择**将列表恢复到默认设置**按钮：

![还原异常设置中的默认值](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")

## <a name="BKMK_UserUnhandled"></a>让调试器在用户未经处理的异常时继续

如果你正在调试.NET 或 JavaScript 代码与[仅我的代码](../debugger/just-my-code.md)，可以让调试器在阻止的不在用户代码中处理但在处理其他地方异常中断的。

1. 在中**异常设置**窗口中，右键单击一个列标签中，打开快捷菜单，然后选择**显示列 > 其他操作**。 (如果已关闭**仅我的代码**，不会看到此命令。)名为的第三个列**其他操作**出现。

   ![其他操作列](../debugger/media/additionalactionscolumn.png "AdditionalActionsColumn")

   为异常，并显示**在用户代码中未经处理时继续**在本专栏中，调试器会继续该异常如果未在用户代码中进行处理，但从外部进行的。

2. 若要更改此设置为特定异常，请选择异常，右键单击以显示快捷菜单，然后选择**未经处理时继续在用户代码中**。 您可能还更改的设置为整个类别的异常，如整个公共语言运行时异常）。

   ![* * 未经处理时继续在用户代码 * * 设置](../debugger/media/continuewhenunhandledinusercodesetting.png "ContinueWhenUnhandledInUserCodeSetting")

例如，ASP.NET web 应用程序通过将它们转换为 HTTP 500 状态代码处理异常 ([ASP.NET Web API 中的异常处理](http://www.asp.net/web-api/overview/error-handling/exception-handling))，这可能无法帮助你确定异常的来源。 在下面的示例中，用户代码对引发 `String.Format()` 的 <xref:System.FormatException>进行调用。 异常中断如下所示：

![将在用户处中断&#45;未经处理的异常](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")

## <a name="add-and-delete-exceptions"></a>添加和删除异常

可以添加和删除异常。 若要从类别中删除一个异常类型，选择异常，并选择**从列表中删除所选的异常**（减号） 按钮**异常设置**工具栏。 或者，可以右键单击异常，选择**删除**从快捷菜单。 删除异常具有相同的效果为具有异常未选中状态，这是调试程序不会被引发时中断。

若要添加一个例外：

1. 在中**异常设置**窗口中，选择其中一个异常类别 (例如，**公共语言运行时**)。

2. 选择**将异常添加到所选类别**按钮 （加号）。

   ![* * 将异常添加到所选类别 * * 按钮](../debugger/media/addanexceptiontotheselectedcategorybutton.png "AddAnExceptionToTheSelectedCategoryButton")

3. 键入异常的名称 (例如， **System.UriTemplateMatchException**)。

   ![键入异常名称](../debugger/media/typetheexceptionname.png "TypeTheExceptionName")

   异常是添加到列表 （按字母顺序），并自动选中。

若要将异常添加到 GPU 内存访问异常、 JavaScript 运行时异常或 Win32 异常类别，包括错误代码和说明。

> [!TIP]
> 请检查你的拼写！ “异常设置”窗口不会检查是否存在添加的异常。 因此，如果键入 Sytem.UriTemplateMatchException，则将获得该异常的条目（而不是“System.UriTemplateMatchException”的条目）。

异常设置保留在解决方案的 .suo 文件中，因此适用于特定解决方案。 无法跨解决方案重用特定异常设置。 现在将会保留添加的异常;不是删除的异常。 您可能会添加一个异常，关闭并重新打开解决方案，以及异常仍在那里。 但是，如果删除一个异常，然后关闭/重新打开解决方案，异常将消失。

**“异常设置”** 窗口在 C# 中支持通用异常类型，但在 Visual Basic 中不支持。 要对类似 `MyNamespace.GenericException<T>`的异常执行中断操作，则必须将异常作为 **MyNamespace.GenericException`1**添加。 也就是说，如果你已创建如下所示代码的异常：

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

您可以将异常添加到**异常设置**使用前面的过程：

![添加常见异常](../debugger/media/addgenericexception.png "AddGenericException")

## <a name="add-conditions-to-an-exception"></a>将条件添加到异常

使用**异常设置**窗口设置异常条件。 当前支持的条件包括模块名称要包括或排除异常。 通过设置模块名称作为条件，您可以选择仅在某些代码模块上异常中断。 此外可以选择以避免中断特定模块的问题。

> [!NOTE]
> 将条件添加到异常从开始支持[!include[vs_dev15](../misc/includes/vs_dev15_md.md)]。

若要添加条件的异常：

1. 选择**编辑条件**按钮在异常设置窗口中，或右键单击异常并选择**编辑条件**。

   ![异常的条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

2. 若要将需要更多条件添加到异常，请选择**添加条件**对每个新条件。 另一个条件的行显示。

   ![异常的额外条件](../debugger/media/extraconditionsforanexception.png "ExtraConditionsForAnException")

3. 对于每个条件行中，键入模块的名称并更改到的比较运算符列表**等于**或**不等于**。 你可以指定通配符 (**\\\***) 中指定多个模块的名称。

4. 如果你需要删除条件，请选择**X**条件行尾。

## <a name="see-also"></a>请参阅

- [在出现异常后继续执行](../debugger/continuing-execution-after-an-exception.md)<br/>
- [如何：在发生异常后检查系统代码](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [如何：使用本机运行时检查](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [使用运行时检查（不用 C 运行时库）](../debugger/using-run-time-checks-without-the-c-run-time-library.md)<br/>
- [初探调试器](../debugger/debugger-feature-tour.md)
