---
title: 用调试器管理异常 |Microsoft Docs
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
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911509"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>在 Visual Studio 中管理调试器的异常

异常是执行程序时发生的错误状态的指示。 您可以告知调试器要中断的异常或异常的集合，以及希望调试器中断的位置（即，在调试器中暂停）。 调试器中断时，会显示引发异常的位置。 你还可以添加或删除异常。 在 Visual Studio 中打开解决方案后，使用 "**调试 > Windows > 异常设置**" 打开 "**异常设置**" 窗口。

提供响应最重要异常的处理程序。 如果需要知道如何添加异常处理程序，请参阅[通过编写更好C#的代码修复 bug](../debugger/write-better-code-with-visual-studio.md)。 此外，还将了解如何将调试器配置为始终中断某些异常的执行。

异常发生时，调试程序将一条异常消息写入到“输出”窗口。 在以下情况下，它可能会在以下情况下中断执行：

- 引发了不处理的异常。
- 调试器配置为在调用任何处理程序之前中断执行。
- 您已设置[仅我的代码](../debugger/just-my-code.md)，并且调试器配置为在用户代码中未处理的任何异常上中断。

> [!NOTE]
> ASP.NET 有一个顶级异常处理程序，可以在浏览器中显示错误页。 除非打开**仅我的代码**，否则它不会中断执行。 有关示例，请参阅下面的[通知调试器继续执行用户未经处理的异常](#BKMK_UserUnhandled)。

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> 在 Visual Basic 应用程序中，调试程序将所有错误作为异常进行管理，即使使用出错时样式错误处理程序也是如此。

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>通知调试器在引发异常时中断

调试器可以在引发异常的位置中断执行，因此您可以在调用处理程序之前检查异常。

在 "**异常设置**" 窗口（"**调试" > Windows > "异常设置**"）中，展开 "异常" 类别（如 "**公共语言运行时异常**"）的节点。 然后选中该类别内特定异常的复选框，如**AccessViolationException**。 还可以选择整个类别的异常。

![已检查 AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")

> [!TIP]
> 您可以使用 "**异常设置**" 工具栏中的 "**搜索**" 窗口查找特定异常，或使用 "搜索" 来筛选特定命名空间（如**System.IO**）。

如果在 "**异常设置**" 窗口中选择异常，则调试器执行会在引发异常的任何位置中断，无论是否已处理。 现在，例外称为第一次机会异常。 以下是几个应用场景示例：

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

  如果已签入 "**异常设置**" **AccessViolationException** ，则在调试器中运行此代码时，执行将在 `throw` 行中断。 然后可以继续执行。 控制台应显示这两行：

  ```cmd
  caught exception
  goodbye
  ```

  但它不会显示 `here` 行。

- C#控制台应用程序引用具有具有两个方法的类的类库。 一个方法引发异常并对其进行处理，而另一个方法引发同一异常但不处理它。

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

  如果已签入 "**异常设置**" **AccessViolationException** ，则在调试程序中运行此代码时，执行将在**throw （）** 和**ThrowUnhandledException （）** 的 `throw` 行中断。

若要将异常设置还原为默认值，请选择 "将**列表还原到默认设置**" 按钮：

![还原异常设置中的默认值](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")

## <a name="BKMK_UserUnhandled"></a>通知调试器在用户未经处理的异常上继续

如果正在通过[仅我的代码](../debugger/just-my-code.md)调试 .Net 或 JavaScript 代码，则可以告知调试器阻止不在用户代码中处理但在其他地方处理的异常。

1. 在 "**异常设置**" 窗口中，右键单击列标签打开快捷菜单，然后选择 "**显示列 > 其他操作**"。 （如果已关闭**仅我的代码**，则不会显示此命令。）将显示名为 "**附加操作**" 的第三列。

   ![其他操作列](../debugger/media/additionalactionscolumn.png "AdditionalActionsColumn")

   对于在此列中的**用户代码未处理时**显示 "继续" 的异常，如果未在用户代码中处理此异常，则调试器将继续，但会在外部处理。

2. 若要更改特定异常的此设置，请选择异常，右键单击以显示快捷菜单，然后选择 "**在用户代码中未经处理时继续**"。 您还可以更改整个类别的异常（如整个公共语言运行时异常）的设置。

   ![* * 在用户代码中未经处理时继续操作 * * 设置](../debugger/media/continuewhenunhandledinusercodesetting.png "ContinueWhenUnhandledInUserCodeSetting")

例如，ASP.NET web 应用程序通过将异常转换为 HTTP 500 状态代码来处理异常（[ASP.NET Web API 中的异常处理](/aspnet/web-api/overview/error-handling/exception-handling)），这可能不会帮助你确定异常的源。 在下面的示例中，用户代码对引发 `String.Format()` 的 <xref:System.FormatException>进行调用。 异常中断如下所示：

![用户&#45;未经处理的异常中断](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")

## <a name="add-and-delete-exceptions"></a>添加和删除异常

可以添加和删除异常。 若要从类别中删除异常类型，请选择该异常，然后在 "**异常设置**" 工具栏上选择 "**从列表中删除所选异常**" 按钮（减号）。 或者，您可以右键单击异常并从快捷菜单中选择 "**删除**"。 删除异常与取消选中异常的效果相同，即调试器在引发时不会中断。

添加异常：

1. 在 "**异常设置**" 窗口中，选择其中一个异常类别（例如，**公共语言运行时**）。

2. 选择 "**向所选类别添加例外**" 按钮（加号）。

   ![* * 向选定类别添加例外 * * 按钮](../debugger/media/addanexceptiontotheselectedcategorybutton.png "AddAnExceptionToTheSelectedCategoryButton")

3. 键入异常的名称（例如**sytem.uritemplatematchexception**）。

   ![键入异常名称](../debugger/media/typetheexceptionname.png "TypeTheExceptionName")

   异常会添加到列表（按字母顺序），并自动选中。

若要将异常添加到 GPU 内存访问异常、JavaScript 运行时异常或 Win32 异常类别，请包括错误代码和说明。

> [!TIP]
> 请检查你的拼写！ “异常设置”窗口不会检查是否存在添加的异常。 因此，如果键入 Sytem.UriTemplateMatchException，则将获得该异常的条目（而不是“System.UriTemplateMatchException”的条目）。

异常设置保留在解决方案的 .suo 文件中，因此适用于特定解决方案。 无法跨解决方案重用特定异常设置。 现在仅保存添加的异常。删除的异常不是。 您可以添加一个异常，然后关闭并重新打开该解决方案，并且该异常将仍然存在。 但是，如果删除一个异常，然后关闭/重新打开解决方案，异常将消失。

**“异常设置”** 窗口在 C# 中支持通用异常类型，但在 Visual Basic 中不支持。 要对类似 `MyNamespace.GenericException<T>`的异常执行中断操作，则必须将异常作为 **MyNamespace.GenericException`1**添加。 也就是说，如果你创建了类似于以下代码的异常：

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

您可以使用前面的过程将异常添加到**异常设置**：

![添加一般异常](../debugger/media/addgenericexception.png "AddGenericException")

## <a name="add-conditions-to-an-exception"></a>向异常添加条件

使用 "**异常设置**" 窗口设置异常条件。 当前支持的条件包括要包括或排除在异常中的模块名称。 通过将模块名称设置为条件，可以选择仅对某些代码模块中断异常。 您还可以选择避免中断特定的模块。

> [!NOTE]
> 从 [!include[vs_dev15](../misc/includes/vs_dev15_md.md)]开始，支持将条件添加到异常中。

添加条件异常：

1. 选择 "异常设置" 窗口中的 "**编辑条件**" 按钮，或右键单击异常并选择 "**编辑条件**"。

   ![异常条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

2. 若要向异常添加额外的所需条件，请选择 "为每个新条件**添加条件**"。 将显示其他条件行。

   ![异常的额外条件](../debugger/media/extraconditionsforanexception.png "ExtraConditionsForAnException")

3. 对于每个条件行，键入模块的名称，并将 "比较运算符" 列表更改为 "**等于**" 或 "**不等于**"。 您可以在名称中指定通配符（ **\\\*** ），以指定多个模块。

4. 如果需要删除条件，请选择条件行末尾的**X** 。

## <a name="see-also"></a>请参阅

- [在出现异常后继续执行](../debugger/continuing-execution-after-an-exception.md)<br/>
- [如何：在发生异常后检查系统代码](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [如何：使用本机运行时检查](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [使用运行时检查（不用 C 运行时库）](../debugger/using-run-time-checks-without-the-c-run-time-library.md)<br/>
- [初探调试器](../debugger/debugger-feature-tour.md)
