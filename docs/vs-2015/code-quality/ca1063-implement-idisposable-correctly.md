---
title: CA1063：正确实现 IDisposable |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1fe2982ab9e1b3951583b268eadb44c97c8e4805
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663639"
---
# <a name="ca1063-implement-idisposable-correctly"></a>CA1063：正确实现 IDisposable
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ImplementIDisposableCorrectly|
|CheckId|CA1063|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 未正确实现 `IDisposable`。 此问题的一些原因如下所示：

- IDisposable 是在类中重新实现的。

- Finalize 重新被重写。

- Dispose 被重写。

- Dispose （）不是公共、密封或名为 Dispose。

- Dispose （bool）未受保护、虚拟或未密封。

- 在未密封的类型中，Dispose （）必须调用 Dispose （true）。

- 对于未密封类型，Finalize 实现不会调用 Dispose （bool）或 case 类终结器。

  违反上述任何一种模式都将触发此警告。

  每个未密封的根 IDisposable 类型都必须提供其自己的受保护虚拟 void Dispose （bool）方法。 Dispose （）应调用 Dispose （true），Finalize 应调用 Dispose （false）。 如果要创建未密封的根 IDisposable 类型，则必须定义 Dispose （bool）并调用它。 有关详细信息，请参阅 .NET Framework 文档的[框架设计指南](https://msdn.microsoft.com/library/5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b)部分中的[清理非托管资源](https://msdn.microsoft.com/library/a17b0066-71c2-4ba4-9822-8e19332fc213)。

## <a name="rule-description"></a>规则说明
 所有的 IDisposable 类型都应当正确实现 Dispose 模式。

## <a name="how-to-fix-violations"></a>如何解决冲突
 检查你的代码并确定以下哪种解决方法将修复此冲突。

- 从 {0} 实现的接口列表中删除 IDisposable，并改为重写基类 Dispose 实现。

- 从类型 {0} 中删除终结器，重写 Dispose （bool 释放），并在 "dispose" 为 false 的代码路径中放置终止逻辑。

- 删除 {0}，替代 Dispose （bool 释放），并将 dispose 逻辑放在 "Dispose" 为 true 的代码路径中。

- 确保将 {0} 声明为 public 和 sealed。

- 将 {0} 重命名为 "Dispose"，并确保将其声明为 public 和 sealed。

- 请确保将 {0} 声明为 protected、virtual 和未密封。

- 修改 {0} 以便它调用 Dispose （true），然后调用 GC。Gc.suppressfinalize 在当前对象实例上（[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 中的 "this" 或 "Me"），然后返回。

- 修改 {0} 以便它调用 Dispose （false），然后返回。

- 如果要编写未密封的根 IDisposable 类，请确保 IDisposable 的实现遵循本部分前面所述的模式。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="pseudo-code-example"></a>伪代码示例
 下面的伪代码提供了一个示例，说明如何在使用托管资源和本机资源的类中实现 Dispose （bool）。

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
