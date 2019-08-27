---
title: CA1063:正确实现 IDisposable |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ImplementIDisposableCorrectly
- CA1063
helpviewer_keywords:
- CA1063
- ImplementIDisposableCorrectly
ms.assetid: 12afb1ea-3a17-4a3f-a1f0-fcdb853e2359
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 90f218165c0543c1881857191efd202717c6e372
ms.sourcegitcommit: 51dad3e11d7580567673e0d426ab3b0a17584319
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66820883"
---
# <a name="ca1063-implement-idisposable-correctly"></a>CA1063:正确实现 IDisposable
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ImplementIDisposableCorrectly|
|CheckId|CA1063|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 `IDisposable` 未正确实现。 此处列出了此问题的一些原因：

- 在类中重新实现 IDisposable。

- 完成重新中被重写。

- 重写 dispose。

- Dispose （） 不是公共的密封的或名为 Dispose。

- Dispose （bool） 不受保护、 虚拟或未密封。

- 在未密封类型中，dispose （） 必须调用 dispose （true）。

- 对于非密封类型 Finalize 实现不会调用一个或两个 dispose （bool） 或事例类终结器。

  这些模式的任何一个冲突将触发此警告。

  每个未密封的根 IDisposable 类型都必须提供其自己受保护的虚拟 void dispose （bool） 方法。 Dispose （） 应调用 dispose （true） 和 Finalize 应调用 dispose （false）。 如果要创建未密封的根 IDisposable 类型，必须定义 dispose （bool），调用它。 有关详细信息，请参阅[清理了非托管资源](https://msdn.microsoft.com/library/a17b0066-71c2-4ba4-9822-8e19332fc213)中[Framework 设计准则](https://msdn.microsoft.com/library/5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b).NET Framework 文档的部分。

## <a name="rule-description"></a>规则说明
 所有的 IDisposable 类型都应当正确实现 Dispose 模式。

## <a name="how-to-fix-violations"></a>如何解决冲突
 检查你的代码并确定哪些以下解决方法将修复此冲突。

- 从由实现的接口列表中移除 IDisposable {0} ，而是重写 Dispose 基类实现。

- 从类型中移除终结器{0}、 重写 Dispose (bool disposing)，和其中 disposing 为 false 的代码路径中加入终结逻辑。

- 删除{0}、 重写 Dispose (bool disposing)，和其中 disposing 为 true 的代码路径中加入释放逻辑。

- 确保{0}声明为 public 和密封的。

- 重命名{0}为 Dispose，并确保它被声明为 public 和 sealed。

- 请确保{0}声明为受保护，虚拟的并为其未密封的。

- 修改{0}，以便它将调用 dispose （true），然后调用 GC。当前对象实例上的 SuppressFinalize (this 或 Me [!INCLUDE[vbprvb](../includes/vbprvb-md.md)])，然后返回。

- 修改{0}，以便它调用 dispose （false），然后返回。

- 如果你正在编写一个未密封的根 IDisposable 类，请确保 IDisposable 实现遵循本部分前面所述的模式。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="pseudo-code-example"></a>伪代码示例
 下面的伪代码提供了应如何使用托管的类中实现 dispose （bool） 和本机资源的常规示例。

```
public class Resource : IDisposable
{
    private IntPtr nativeResource = Marshal.AllocHGlobal(100);
    private AnotherResource managedResource = new AnotherResource();

// Dispose() calls Dispose(true)
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }
    // NOTE: Leave out the finalizer altogether if this class doesn't
    // own unmanaged resources itself, but leave the other methods
    // exactly as they are.
    ~Resource()
    {
        // Finalizer calls Dispose(false)
        Dispose(false);
    }
    // The bulk of the clean-up code is implemented in Dispose(bool)
    protected virtual void Dispose(bool disposing)
    {
        if (disposing)
        {
            // free managed resources
            if (managedResource != null)
            {
                managedResource.Dispose();
                managedResource = null;
            }
        }
        // free native resources if there are any.
        if (nativeResource != IntPtr.Zero)
        {
            Marshal.FreeHGlobal(nativeResource);
            nativeResource = IntPtr.Zero;
        }
    }
}
```
