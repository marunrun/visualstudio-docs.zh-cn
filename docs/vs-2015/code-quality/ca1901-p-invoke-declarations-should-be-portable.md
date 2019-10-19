---
title: CA1901： P-Invoke 声明应为可移植性 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d1b4c0c5bcf22db6558f156fd1acd0be94026b08
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661062"
---
# <a name="ca1901-pinvoke-declarations-should-be-portable"></a>CA1901：P/Invoke 声明应为可移植声明
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PInvokeDeclarationsShouldBePortable|
|CheckId|CA1901|
|类别|Microsoft 可移植性|
|是否重大更改|如果在程序集外部可见，则为。 否-如果 P/Invoke 在程序集外部不可见，则为。|

## <a name="cause"></a>原因
 此规则将评估每个参数的大小和 P/Invoke 的返回值，并验证在对32位和64位平台上的非托管代码进行封送处理时，其大小是否正确。 此规则最常见的冲突是传递固定大小的整数，其中需要使用平台相关的指针大小变量。

## <a name="rule-description"></a>规则说明
 以下任何一种情况都会违反此规则：

- 返回值或参数类型为固定大小的整数（当它应类型化为 `IntPtr` 时）。

- 返回值或参数的类型应为固定大小的整数 `IntPtr`。

## <a name="how-to-fix-violations"></a>如何解决冲突
 可以通过使用 `IntPtr` 或 `UIntPtr` 来表示句柄而不是 `Int32` 或 `UInt32` 来解决此冲突。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不应禁止显示此警告。

## <a name="example"></a>示例
 下面的示例演示违反此规则的情况。

```csharp
internal class NativeMethods
{
    [DllImport("shell32.dll", CharSet=CharSet.Auto)]
    internal static extern IntPtr ExtractIcon(IntPtr hInst,
        string lpszExeFileName, IntPtr nIconIndex);
}
```

 在此示例中，将 `nIconIndex` 参数声明为 `IntPtr`，这在32位平台上为4个字节宽，64位平台上为8个字节。 在下面的非托管声明中，可以看到 `nIconIndex` 是所有平台上的4字节无符号整数。

```csharp
HICON ExtractIcon(HINSTANCE hInst, LPCTSTR lpszExeFileName,
    UINT nIconIndex);
```

## <a name="example"></a>示例
 若要解决此冲突，请将声明更改为以下内容：

```csharp
internal class NativeMethods{
    [DllImport("shell32.dll", CharSet=CharSet.Auto)]
    internal static extern IntPtr ExtractIcon(IntPtr hInst,
        string lpszExeFileName, uint nIconIndex);
}
```

## <a name="see-also"></a>请参阅
 [可迁移性警告](../code-quality/portability-warnings.md)
