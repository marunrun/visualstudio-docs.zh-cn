---
title: 使用调试器管理异常 | Microsoft Docs
ms.custom: seodec18
ms.date: 10/09/2018
ms.topic: how-to
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
ms.openlocfilehash: ff28944a36d338230a17cd533a4832452e42885b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348452"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>在 Visual Studio 中使用调试器管理异常

异常是执行程序时发生的错误状态的指示。 你可以告知调试器在遇到哪些异常或异常集合时中断，以及希望调试器在哪个时间点中断（即在调试器中暂停）。 调试器中断时，会显示引发异常的位置。 你还可以添加或删除异常。 在 Visual Studio 中打开一个解决方案后，使用“调试”>“Windows”>“异常设置”打开异常设置”窗口   。

提供响应最重要异常的处理器。 如果需要知道如何为异常添加处理器，请参阅[通过编写更好的 C# 代码来修复 bug](../debugger/write-better-code-with-visual-studio.md)。 此外，还可了解如何将调试器配置为在引发某些异常时始终中断执行。

异常发生时，调试程序将一条异常消息写入到“输出”窗口  。 它可能会在以下情况下中断执行：

- 引发未处理的异常。
- 调试器配置为在调用任何处理器之前中断执行。
- 你设置了[仅我的代码](../debugger/just-my-code.md)，并且调试器配置为引发任何未在用户代码中进行处理的异常时中断。

> [!NOTE]
> ASP.NET 有一个顶级异常处理程序，可以在浏览器中显示错误页。 除非启用“仅我的代码”，否则它不会中断执行  。 有关示例，请参阅下面的[告知调试器在遇到用户未处理的异常时继续执行](#BKMK_UserUnhandled)。

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> 在 Visual Basic 应用程序中，调试程序将所有错误作为异常进行管理，即使使用出错时样式错误处理程序也是如此。

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>告知调试器在引发异常时中断。

调试器可能会在引发异常时中断执行，这让你有机会在调用处理器之前对异常进行检查。

在“异常设置”窗口中（“调试”>“Windows”>“异常设置”），展开一个异常类别的节点，例如“公共语言运行时异常”    。 然后选中该类别中特定异常的复选框，如 System.AccessViolationException  。 还可以选择整个类别的异常。

![已选中 AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")

> [!TIP]
> 可以使用“异常设置”工具栏中的“搜索”窗口查找特定异常，也可以使用搜索筛选特定命名空间（例如 System.IO）    。

如果在“异常设置”窗口中选择异常，则调试器会在引发异常（无论是否已处理）时中断执行  。 此时，该异常被称为第一次机会异常。 以下是几个应用场景示例：

- 在下面的 C# 控制台应用程序中，Main 方法在 `try/catch` 块内引发“AccessViolationException”  。

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

  如果在“异常设置”中选中了 AccessViolationException，则在调试器中运行此代码时将在 `throw` 行上中断执行   。 然后可以继续执行。 控制台应显示这两行：

  ```cmd
  caught exception
  goodbye
  ```

  但它没有显示 `here` 行。

- C# 控制台应用程序引用了一个类库，该类库中的类具有两个方法。 一个方法引发异常并对其进行处理，而另一个方法引发同一异常但不处理。

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

  如果在“异常设置”中选中了AccessViolationException，则在调试器中运行此代码时将在 ThrowHandledException() 和 ThrowUnhandledException() 中的 `throw` 行上中断执行     。

要将异常设置还原为默认值，请选择“将列表还原为默认设置”按钮  ：

![还原“异常设置”中的默认值](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")

## <a name="tell-the-debugger-to-continue-on-user-unhandled-exceptions"></a><a name="BKMK_UserUnhandled"></a>告知调试器在遇到用户未处理的异常时继续执行

如果使用[仅我的代码](../debugger/just-my-code.md)调试 .NET 或 JavaScript 代码，则可以告知调试器在遇到未在用户代码中进行处理但在其他地方进行了处理的异常时不要执行中断操作。

1. 在“异常设置”窗口中，右键单击列标签打开快捷菜单，然后选择“显示列”>“其他操作”   。 （如果已禁用“仅我的代码”，将看不到此命令。  ）将显示名为“其他操作”的第三列  。

   ![“其他操作”列](../debugger/media/additionalactionscolumn.png "AdditionalActionsColumn")

   对于在此列中显示“在遇到未在用户代码中进行处理的异常时继续执行”的异常，如果调试器遇到未在用户代码中进行处理但在其他地方进行了处理的异常，则将继续执行  。

2. 要更改特定异常的此设置，请选择异常，右键单击以显示快捷菜单，然后选择“在遇到未在用户代码中进行处理的异常时继续执行”  。 你还可以更改整个异常类别的设置，如整个“公共语言运行时”异常。

   ![“在遇到未在用户代码中进行处理的异常时继续执行”设置](../debugger/media/continuewhenunhandledinusercodesetting.png "ContinueWhenUnhandledInUserCodeSetting")

例如，ASP.NET Web 应用程序通过将异常转换为 HTTP 500 状态代码来处理异常（[ASP.NET Web API 中的异常处理](/aspnet/web-api/overview/error-handling/exception-handling)），该方法可能无法帮助你确定异常的来源。 在下面的示例中，用户代码对引发 `String.Format()` 的 <xref:System.FormatException>进行调用。 异常中断如下所示：

![在遇到用户未处理的异常中断](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")

## <a name="add-and-delete-exceptions"></a>添加和删除异常

可以添加和删除异常。 要从某个类别中删除某一异常类型，请选择该异常，然后在“异常设置”工具栏上，选择“从列表中删除所选异常”按钮（减号）   。 你也可以右键单击异常，然后从快捷菜单中选择“删除”  。 删除异常与取消选中异常的效果一样，即调试器在引发该异常时不会中断。

要添加异常，请执行以下操作：

1. 在“异常设置”窗口中，选择其中一个异常类别（例如“公共语言运行时”）   。

2. 选择“向所选类别添加异常”按钮（加号）  。

   ![“向所选类别添加异常”按钮](../debugger/media/addanexceptiontotheselectedcategorybutton.png "AddAnExceptionToTheSelectedCategoryButton")

3. 键入异常的名称（例如 System.UriTemplateMatchException  ）。

   ![键入异常名称](../debugger/media/typetheexceptionname.png "TypeTheExceptionName")

   异常随即添加到列表（按字母顺序），并自动选中。

要向“GPU 内存访问异常”、“JavaScript 运行时异常”或“Win32 异常”类别添加异常，请包括错误代码和说明。

> [!TIP]
> 请检查你的拼写！ “异常设置”窗口不会检查是否存在添加的异常  。 因此，如果键入 Sytem.UriTemplateMatchException，则将获得该异常的条目（而不是“System.UriTemplateMatchException”的条目）   。

异常设置保留在解决方案的 .suo 文件中，因此适用于特定解决方案。 无法跨解决方案重用特定异常设置。 此时，仅保留添加的异常，而不保留删除的异常。 你可以添加一个异常，然后关闭并重新打开解决方案，该异常仍然存在。 但是，如果删除一个异常，然后关闭/重新打开解决方案，异常将消失。

**“异常设置”** 窗口在 C# 中支持通用异常类型，但在 Visual Basic 中不支持。 要对类似 `MyNamespace.GenericException<T>`的异常执行中断操作，则必须将异常作为 **MyNamespace.GenericException`1**添加。 也就是说，如果已经创建了类似以下代码的异常：

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

则可以按照上一个过程将异常添加到“异常设置”窗口  ：

![添加常见异常](../debugger/media/addgenericexception.png "AddGenericException")

## <a name="add-conditions-to-an-exception"></a>向异常添加条件

使用“异常设置”窗口对异常设置条件  。 当前支持的条件包括要包括在异常中或排除在异常外的模块名称。 通过将模块名称设置为条件，可以选择仅在某些代码模块遇到异常时中断执行。 你还可以选择在特定的模块遇到异常时不要中断执行。

> [!NOTE]
> 从 [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] 开始，支持向异常添加条件。

要添加异常条件，请执行以下操作：

1. 在“异常设置”窗口中选择“编辑条件”按钮，或右键单击异常并选择“编辑条件”   。

   ![异常的条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

2. 要向异常添加额外的所需条件，请为每个新条件选择“添加条件”  。 将显示其他条件行。

   ![异常的额外条件](../debugger/media/extraconditionsforanexception.png "ExtraConditionsForAnException")

3. 对于每个条件行，键入模块的名称，然后将比较运算符列表更改为“等于”或“不等于”   。 你可以在名称中指定通配符 (\\\*)，以指定多个模块  。

4. 如果需要删除条件，请选择条件行末尾的 X  。

## <a name="see-also"></a>请参阅

- [在出现异常后继续执行](../debugger/continuing-execution-after-an-exception.md)<br/>
- [如何：在发生异常后检查系统代码](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [如何：使用本机运行时检查](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [使用运行时检查（不用 C 运行时库）](../debugger/using-run-time-checks-without-the-c-run-time-library.md)<br/>
- [初探调试器](../debugger/debugger-feature-tour.md)
