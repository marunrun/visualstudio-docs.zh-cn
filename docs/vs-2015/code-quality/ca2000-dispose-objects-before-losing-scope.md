---
title: CA2000：在丢失范围之前释放对象 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2000
- Dispose objects before losing scope
- DisposeObjectsBeforeLosingScope
helpviewer_keywords:
- CA2000
- DisposeObjectsBeforeLosingScope
ms.assetid: 0c3d7d8d-b94d-46e8-aa4c-38df632c1463
caps.latest.revision: 32
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e3de3246980ead0b20d471321a9696451aed81ac
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534766"
---
# <a name="ca2000-dispose-objects-before-losing-scope"></a>CA2000:丢失范围之前释放对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DisposeObjectsBeforeLosingScope|
|CheckId|CA2000|
|类别|Microsoft 可靠性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 创建类型的本地对象 <xref:System.IDisposable> ，但在对对象的所有引用超出范围之前，不会释放对象。

## <a name="rule-description"></a>规则描述
 如果在对某个可释放对象的所有引用超出范围之前未显式释放该对象，则当垃圾回收器运行该对象的终结器时，将在某个不确定的时间释放该对象。 由于可能发生异常事件，将阻止对象的终结器运行，因此应改为显式释放对象。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请 <xref:System.IDisposable.Dispose%2A> 在对象的所有引用超出范围之前对其调用。

 请注意，可以使用 `using` 语句（ `Using` 中的 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ）来包装实现的对象 `IDisposable` 。 以这种方式包装的对象将在块关闭时自动释放 `using` 。

 在以下情况下，使用语句不足以保护 IDisposable 对象，并可能导致 CA2000 发生。

- 返回一个可释放对象需要在 using 块外的 try/finally 块中构造对象。

- 不应在 using 语句的构造函数中初始化可释放对象的成员。

- 嵌套仅受一个异常处理程序保护的构造函数。 例如，应用于对象的

    ```
    using (StreamReader sr = new StreamReader(new FileStream("C:\myfile.txt", FileMode.Create)))
    { ... }
    ```

     导致 CA2000 发生，因为 StreamReader 对象的构造失败导致不会关闭 FileStream 对象。

- 动态对象应使用影子对象来实现 IDisposable 对象的 Dispose 模式。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不要禁止显示此规则发出的警告，除非您对您的对象调用了一个方法，而该方法调用 `Dispose`，例如 <xref:System.IO.Stream.Close%2A>；或者，如果引发警告的方法返回一个包装您的对象的 IDisposable 对象。

## <a name="related-rules"></a>相关规则
 [CA2213:应释放可释放的字段](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

 [CA2202:不要多次释放对象](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)

## <a name="example"></a>示例
 如果要实现一个返回可释放对象的方法，请在没有 catch 块的情况下使用 try/finally 块来确保释放对象。 通过使用 try/finally 块，你允许在错误点引发异常，并确保对象已释放。

 在 OpenPort1 方法中，打开 ISerializable 对象 SerialPort 或对 SomeMethod 的调用可能会失败。 此实现将引发 CA2000 警告。

 在 OpenPort2 方法中，将声明两个 SerialPort 对象并将其设置为 null：

- `tempPort`，用于测试方法操作是否成功。

- `port`，用于方法的返回值。

  `tempPort`构造并在块中打开 `try` ，并在相同的块中执行任何其他所需的工作 `try` 。 在块的末尾 `try` ，将返回已打开的端口，并将 `port` `tempPort` 对象设置为 `null` 。

  `finally`块检查的值 `tempPort` 。 如果不为 null，则方法中的操作失败，并 `tempPort` 关闭以确保释放所有资源。 如果方法的操作成功，则返回的端口对象将包含打开的 SerialPort 对象; 如果操作失败，则将为 null。

  [!code-csharp[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/cs/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.cs#1)]
  [!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/vb/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.vb#1)]
  [!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/vb/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.vboverflow.vb#1)]

## <a name="example"></a>示例
 默认情况下， [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 编译器会检查溢出的所有算术运算符。 因此，任何 Visual Basic 算术运算都可能引发 <xref:System.OverflowException> 。 这可能会导致 CA2000 等规则发生意外冲突。 例如，以下 CreateReader1 函数将产生 CA2000 冲突，因为 Visual Basic 编译器发出的溢出检查指令可能会引发导致 StreamReader 无法释放的异常。

 若要解决此问题，可以在项目中禁用 Visual Basic 编译器发出溢出检查，也可以修改代码，如以下 CreateReader2 函数所示。

 若要禁用溢出检查，请在解决方案资源管理器中右键单击项目名称，然后单击 "**属性**"。 单击 "**编译**"，单击 "**高级编译选项**"，然后选中 "**删除整数溢出检查**"。

<!-- TODO: review snippet reference  [!CODE [FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope.VBOverflow#1](FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope.VBOverflow#1)]  -->

## <a name="see-also"></a>另请参阅
 <xref:System.IDisposable> [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)