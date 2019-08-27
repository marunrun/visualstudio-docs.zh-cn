---
title: CA1901:-Invoke 声明应为可移植 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1901
- PInvokeDeclarationsShouldBePortable
helpviewer_keywords:
- CA1901
- PInvokeDeclarationsShouldBePortable
ms.assetid: 90361812-55ca-47f7-bce9-b8775d3b8803
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ccbbc3178a9f65c15d11a27dee1a625cca729240
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203068"
---
# <a name="ca1901-pinvoke-declarations-should-be-portable"></a>CA1901:P/Invoke 声明应为可移植声明
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PInvokeDeclarationsShouldBePortable|
|CheckId|CA1901|
|类别|Microsoft.Portability|
|是否重大更改|是-如果 P/Invoke 是程序集外部可见。 否-如果 P/Invoke 不是程序集外部可见。|

## <a name="cause"></a>原因
 此规则计算每个参数的大小和 P/Invoke 的返回值，并验证它们的大小，封送到 32 位和 64 位平台上的非托管代码时正确。 此规则的最常见的冲突是传递需要依赖于平台的指针大小的变量的固定大小的整数。

## <a name="rule-description"></a>规则说明
 以下任一情况与此规则冲突发生：

- 返回值或参数的类型为固定大小的整数类型应为`IntPtr`。

- 返回值或参数被类型化为`IntPtr`时它的类型应为固定大小的整数。

## <a name="how-to-fix-violations"></a>如何解决冲突
 您可以通过使用来解决此冲突`IntPtr`或`UIntPtr`来表示句柄而不是`Int32`或`UInt32`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不应取消显示此警告。

## <a name="example"></a>示例
 下面的示例演示了此规则的冲突。

```csharp
internal class NativeMethods
{
    [DllImport("shell32.dll", CharSet=CharSet.Auto)]
    internal static extern IntPtr ExtractIcon(IntPtr hInst,
        string lpszExeFileName, IntPtr nIconIndex);
}
```

 在此示例中，`nIconIndex`参数声明为`IntPtr`，这是 32 位平台和 8 个字节宽，在 64 位平台上宽度为 4 个字节。 在后面的非托管声明，您可以看到，`nIconIndex`是在所有平台上的 4 字节无符号的整数。

```csharp
HICON ExtractIcon(HINSTANCE hInst, LPCTSTR lpszExeFileName,
    UINT nIconIndex);
```

## <a name="example"></a>示例
 若要解决冲突，请将声明更改为以下：

```csharp
internal class NativeMethods{
    [DllImport("shell32.dll", CharSet=CharSet.Auto)] 
    internal static extern IntPtr ExtractIcon(IntPtr hInst,
        string lpszExeFileName, uint nIconIndex);
}
```

## <a name="see-also"></a>请参阅
 [Portability Warnings](../code-quality/portability-warnings.md)
