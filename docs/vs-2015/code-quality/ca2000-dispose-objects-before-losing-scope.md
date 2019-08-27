---
title: CA2000:范围前释放对象 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 975e1eee68911f8d9d0942e73275fcf521979772
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681506"
---
# <a name="ca2000-dispose-objects-before-losing-scope"></a>CA2000:丢失范围之前释放对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 若要修复此规则的冲突，请调用<xref:System.IDisposable.Dispose%2A>上对它的所有引用超出范围之前的对象。  
  
 请注意，可以使用`using`语句 (`Using`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 来包装实现的对象`IDisposable`。 在这种方式中包装的对象将自动释放在结束时的`using`块。  
  
 以下是某些情况下，使用语句不足以保护 IDisposable 对象，并可以导致 CA2000 发生。  
  
- 返回可释放的对象需要外使用 try/finally 块中构造对象块。  
  
- 初始化可释放对象的成员不应在构造函数中使用的语句。  
  
- 嵌套只能通过一个异常处理程序保护的构造函数。 例如，应用于对象的  
  
    ```  
    using (StreamReader sr = new StreamReader(new FileStream("C:\myfile.txt", FileMode.Create)))  
    { ... }  
    ```  
  
     导致 CA2000 发生，因为在 StreamReader 对象的构造中的失败可能会导致永远不会关闭该 FileStream 对象。  
  
- 动态对象应使用卷影对象实现 IDisposable 的对象的释放模式。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 不要禁止显示此规则发出的警告，除非您对您的对象调用了一个方法，而该方法调用 `Dispose`，例如 <xref:System.IO.Stream.Close%2A>；或者，如果引发警告的方法返回一个包装您的对象的 IDisposable 对象。  
  
## <a name="related-rules"></a>相关的规则  
 [CA2213：应释放可释放的字段](../code-quality/ca2213-disposable-fields-should-be-disposed.md)  
  
 [CA2202:多次未释放对象](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)  
  
## <a name="example"></a>示例  
 如果要实现返回一个可释放对象的方法，使用 try/finally 块没有 catch 块来确保释放对象。 通过使用 try/finally 块，则允许异常引发的故障点，并确保释放该对象。  
  
 在 OpenPort1 方法中，打开 ISerializable 对象 SerialPort 的调用或对 SomeMethod 的调用可能会失败。 此实现会引发 CA2000 警告。  
  
 在 OpenPort2 方法中，两个 SerialPort 对象是声明并且已设置为 null:  
  
- `tempPort`用于测试方法操作成功。  
  
- `port`用于该方法的返回值。  
  
  `tempPort`构造，以打开`try`块中，和任何其他所需的工作都在相同`try`块。 在末尾`try`块中，打开的端口分配给`port`将返回的对象和`tempPort`对象设置为`null`。  
  
  `finally`块检查的值`tempPort`。 如果不为 null，该方法中的操作已失败，并`tempPort`关闭以确保释放任何资源。 如果该方法的操作成功，则如果操作失败，则将为 null，则返回的端口对象将包含打开的 SerialPort 对象。  
  
  [!code-csharp[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/cs/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.cs#1)]
  [!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/vb/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.vb#1)]
  [!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/vb/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.vboverflow.vb#1)]  
  
## <a name="example"></a>示例  
 默认情况下，[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]编译器具有溢出检查的所有算术运算符。 因此，任何 Visual Basic 算术运算可能会引发<xref:System.OverflowException>。 这可能导致的规则，如 CA2000 意外冲突。 例如，以下 CreateReader1 函数将生成 CA2000 冲突，因为 Visual Basic 编译器发出溢出检查的加法运算的可能会引发异常会导致无法释放 StreamReader 的指令。  
  
 若要解决此问题，可以禁用你的项目中的 Visual Basic 编译器发出溢出检查，或您可以修改代码，如以下 CreateReader2 函数中所示。  
  
 若要禁用溢出检查的发送元组，右键单击解决方案资源管理器中的项目名称，然后依次**属性**。 单击**编译**，单击**高级编译选项**，然后选中**整数溢出检查**。  
  
<!-- TODO: review snippet reference  [!CODE [FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope.VBOverflow#1](FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope.VBOverflow#1)]  -->  
  
## <a name="see-also"></a>请参阅  
 <xref:System.IDisposable>   
 [Dispose 模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)