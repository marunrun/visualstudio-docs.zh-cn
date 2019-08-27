---
title: CA2000:丢失范围之前释放对象
ms.date: 05/14/2019
ms.topic: reference
f1_keywords:
- CA2000
- Dispose objects before losing scope
- DisposeObjectsBeforeLosingScope
helpviewer_keywords:
- CA2000
- DisposeObjectsBeforeLosingScope
ms.assetid: 0c3d7d8d-b94d-46e8-aa4c-38df632c1463
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 732b3d683802c50042ee40fee1549a9d247e2470
ms.sourcegitcommit: 283f2dbce044a18e9f6ac6398f6fc78e074ec1ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65804979"
---
# <a name="ca2000-dispose-objects-before-losing-scope"></a>CA2000:丢失范围之前释放对象

|||
|-|-|
|TypeName|DisposeObjectsBeforeLosingScope|
|CheckId|CA2000|
|类别|Microsoft.Reliability|
|是否重大更改|非换行|

## <a name="cause"></a>原因

一个本地对象<xref:System.IDisposable>创建类型，但未对该对象的所有引用超出范围之前释放对象。

## <a name="rule-description"></a>规则说明

如果不显式释放可释放的对象，对它的所有引用超出范围之前，将在垃圾回收器运行终结器对象的某些不确定时间释放该对象。 因为可能会发生异常事件，将阻止终结器运行的对象，该对象应改为显式释放。

### <a name="special-cases"></a>特殊情况

即使未释放对象 CA2000 规则不会引发以下类型的本地对象：

- <xref:System.IO.Stream?displayProperty=nameWithType>
- <xref:System.IO.TextReader?displayProperty=nameWithType>
- <xref:System.IO.TextWriter?displayProperty=nameWithType>
- <xref:System.Resources.IResourceReader?displayProperty=nameWithType>

将其中一种类型的对象传递给构造函数，然后将其分配给字段指示*释放所有权的转移*为新构造的类型。 也就是说，现负责释放的对象的新构造的类型。 如果你的代码将的其中一种类型的对象传递给构造函数，即使该对象未被释放之前对它的所有引用也会发生 CA2000 规则的无冲突不在作用域。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请调用<xref:System.IDisposable.Dispose%2A>上对它的所有引用超出范围之前的对象。

可以使用[`using`语句](/dotnet/csharp/language-reference/keywords/using-statement)([ `Using` ](/dotnet/visual-basic/language-reference/statements/using-statement)在 Visual Basic 中) 来包装实现的对象<xref:System.IDisposable>。 结束时自动释放对象的包装在这种方式`using`块。 但是，在以下情况下不应该或不能与处理`using`语句：

- 若要返回的可释放对象，该对象必须构造中`try/finally`块外部`using`块。

- 未初始化的构造函数中的可释放对象的成员`using`语句。

- 当只有一个异常处理程序的受保护的构造函数都嵌套在[采集一部分`using`语句](/dotnet/csharp/language-reference/language-specification/statements#the-using-statement)，外部构造函数中的失败可能会导致永远不会创建嵌套的构造函数的对象正在关闭。 在下面的示例中的故障<xref:System.IO.StreamReader>构造函数可能会导致<xref:System.IO.FileStream>对象永远不会关闭。 CA2000 这种情况下标记规则的冲突。

   ```csharp
   using (StreamReader sr = new StreamReader(new FileStream("C:\myfile.txt", FileMode.Create)))
   { ... }
   ```

- 动态对象应使用卷影对象来实现 dispose 模式的<xref:System.IDisposable>对象。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

除非不禁止显示此规则的警告：

- 已在您调用的对象上调用方法`Dispose`，如 <xref:System.IO.Stream.Close%2A>
- 引发警告返回的方法<xref:System.IDisposable>包装您的对象的对象
- 正在分配的方法不具有 dispose 所有权;也就是说，负责释放对象传输到另一个对象或方法中创建并返回到调用方的包装器

## <a name="related-rules"></a>相关的规则

- [CA2213：应释放可释放的字段](../code-quality/ca2213-disposable-fields-should-be-disposed.md)
- [CA2202:多次未释放对象](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)

## <a name="example"></a>示例

如果要实现返回一个可释放对象的方法，使用 try/finally 块没有 catch 块来确保释放对象。 通过使用 try/finally 块，则允许异常引发的故障点，并确保释放该对象。

在 OpenPort1 方法中，打开 ISerializable 对象 SerialPort 的调用或对 SomeMethod 的调用可能会失败。 此实现会引发 CA2000 警告。

在 OpenPort2 方法中，两个 SerialPort 对象是声明并且已设置为 null:

- `tempPort`用于测试方法操作成功。

- `port`用于该方法的返回值。

`tempPort`构造，以打开`try`块中，和任何其他所需的工作都在相同`try`块。 在末尾`try`块中，打开的端口分配给`port`将返回的对象和`tempPort`对象设置为`null`。

`finally`块检查的值`tempPort`。 如果不为 null，该方法中的操作已失败，并`tempPort`关闭以确保释放任何资源。 如果该方法的操作成功，则如果操作失败，则将为 null，则返回的端口对象将包含打开的 SerialPort 对象。

```csharp
public SerialPort OpenPort1(string portName)
{
   SerialPort port = new SerialPort(portName);
   port.Open();  //CA2000 fires because this might throw
   SomeMethod(); //Other method operations can fail
   return port;
}

public SerialPort OpenPort2(string portName)
{
   SerialPort tempPort = null;
   SerialPort port = null;
   try
   {
      tempPort = new SerialPort(portName);
      tempPort.Open();
      SomeMethod();
      //Add any other methods above this line
      port = tempPort;
      tempPort = null;

   }
   finally
   {
      if (tempPort != null)
      {
         tempPort.Close();
      }
   }
   return port;
}
```

```vb
Public Function OpenPort1(ByVal PortName As String) As SerialPort

   Dim port As New SerialPort(PortName)
   port.Open()    'CA2000 fires because this might throw
   SomeMethod()   'Other method operations can fail
   Return port

End Function

Public Function OpenPort2(ByVal PortName As String) As SerialPort

   Dim tempPort As SerialPort = Nothing
   Dim port As SerialPort = Nothing

   Try
      tempPort = New SerialPort(PortName)
      tempPort.Open()
      SomeMethod()
      'Add any other methods above this line
      port = tempPort
      tempPort = Nothing

   Finally
      If Not tempPort Is Nothing Then
         tempPort.Close()
      End If

   End Try

   Return port

End Function
```

## <a name="example"></a>示例

默认情况下，Visual Basic 编译器的溢出检查的所有算术运算符。 因此，任何 Visual Basic 算术运算可能会引发<xref:System.OverflowException>。 这可能导致的规则，如 CA2000 意外冲突。 例如，以下 CreateReader1 函数将生成 CA2000 冲突，因为 Visual Basic 编译器发出溢出检查的加法运算的可能会引发异常会导致无法释放 StreamReader 的指令。

若要解决此问题，可以禁用你的项目中的 Visual Basic 编译器发出溢出检查，或您可以修改代码，如以下 CreateReader2 函数中所示。

若要禁用溢出检查的发送元组，右键单击解决方案资源管理器中的项目名称，然后依次**属性**。 单击**编译**，单击**高级编译选项**，然后选中**整数溢出检查**。

[!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../code-quality/codesnippet/VisualBasic/ca2000-dispose-objects-before-losing-scope-vboverflow_1.vb)]

## <a name="see-also"></a>请参阅

- <xref:System.IDisposable>
- [Dispose 模式](/dotnet/standard/design-guidelines/dispose-pattern)