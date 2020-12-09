---
title: 计算局部变量 |Microsoft Docs
description: 了解 Visual Studio 如何访问内存中包含本地值的位置，该位置取决于程序的当前状态。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], evaluating locals
- expression evaluation, evaluating locals
ms.assetid: 7d1ed528-4e7a-4d8f-87b4-162440644a75
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5d9c25c9b7b32b69983aeec4a1e533cbb927a11
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915630"
---
# <a name="evaluate-locals"></a>计算局部变量
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)可获取本地的值，以及本地的名称和类型。 由于本地的值依赖于程序的当前状态，因此必须从内存中获取本地的值。 [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)对象用于将表示本地的[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象绑定到内存中包含该值的适当位置。 内存中的此位置由 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) 对象表示。

检索本地的值的此功能封装在执行以下任务的 helper 函数中：

1. 将 `IDebugField` 对象绑定到内存以获取 `IDebugObject` 对象。

2. 从内存中获取值。 此值表示为一系列字节。

3. 根据本地的类型设置值的格式。

4. 返回一个包含本地值的泛型对象。 在 c # 中，这是一个 `object` ，而在 c + + 中，它是一个 `VARIANT` 。

## <a name="managed-code"></a>托管代码
 这是在托管代码中检索本地的值的函数的实现。

```csharp
namespace EEMC
{
    internal class Field
    {
        internal static object GetValue(
            IDebugBinder binder,
            IDebugField field,
            Type t,
            uint size)
        {
            if (t == null || size == 0)  return null;

            IDebugObject debugObject = null;
            binder.Bind(null, field, out debugObject);

            byte[] buffer = new byte[size];
            for (int i = 0; i < size; i++)  buffer[i] = 0;

            debugObject.GetValue(buffer, size);

            if (t == typeof(sbyte)) return (sbyte) buffer[0];
            if (t == typeof(short)) return BitConverter.ToInt16(buffer, 0);
            if (t == typeof(int))   return BitConverter.ToInt32(buffer, 0);
            if (t == typeof(long))  return BitConverter.ToInt64(buffer, 0);
            if (t == typeof(byte))  return buffer[0];
            if (t == typeof(char))  return BitConverter.ToChar(buffer, 0);
            if (t == typeof(uint))  return BitConverter.ToUInt32(buffer, 0);
            if (t == typeof(ulong)) return BitConverter.ToUInt64(buffer, 0);
            if (t == typeof(float)) return BitConverter.ToSingle(buffer, 0);
            if (t == typeof(double))  return BitConverter.ToDouble(buffer, 0);
            if (t == typeof(bool))  return BitConverter.ToBoolean(buffer, 0);
            if (t == typeof(string))  return BitConverter.ToString(buffer, 0);
            return null;
        }
    }
}
```

## <a name="unmanaged-code"></a>非托管代码
 这是在非托管代码中检索局部值的函数的实现。 `FieldGetType` 在 [获取本地值](../../extensibility/debugger/getting-local-values.md)时显示。

```cpp
HRESULT FieldGetPrimitiveValue(
    in  IDebugBinder* pbinder,
    in  IDebugField*  pfield,
    out VARIANT*      pvarValue
    )
{
    if (pvarValue == NULL)
        return E_INVALIDARG;
    else
        *pvarValue = 0;

    if (pfield == NULL)
        return E_INVALIDARG;

    if (pbinder == NULL)
        return E_INVALIDARG;

    HRESULT hr;
    UINT          valueSize = 0;
    BYTE*         pvalueBits = NULL;
    IDebugObject* pobject    = NULL;

    //get the value as bits
    hr = pbinder->Bind( NULL, pfield, &pobject );
    if (FAILED(hr))
        return hr;

    hr = pobject->GetSize( &valueSize );
    if (FAILED(hr))
    {
        pobject->Release();
        return hr;
    }

    pvalueBits = reinterpret_cast<BYTE *>(malloc(valueSize * sizeof(BYTE)));
    if (!pvalueBits)
    {
        pobject->Release();
        return E_OUTOFMEMORY;
    }

    hr = pobject->GetValue( pvalueBits, valueSize );
    pobject->Release();
    if (FAILED(hr))
    {
        free(pvalueBits);
        return hr;
    }

    //get the type
    VARIANT     valueType;

    hr = FieldGetType( pfield, &valueType );
    if (FAILED(hr))
    {
        free(pvalueBits);
        return hr;
    }

    //copy a primitive value
    switch (valueType.vt)
    {
    case VT_BSTR:
        {
            pvarValue->vt = VT_BSTR;
            if (valueSize == 0)
                pvarValue->bstrVal = SysAllocString( OLE("") );
            else
                pvarValue->bstrVal =
                    SysAllocStringByteLen( reinterpret_cast<char*>(pvalueBits),
                                           valueSize );
        }

    case VT_BOOL:
    case VT_I1:
    case VT_I2:
    case VT_I4:
    case VT_I8:
    case VT_UI1:
    case VT_UI2:
    case VT_UI4:
    case VT_UI8:
    case VT_R4:
    case VT_R8:
        pvarValue->vt = valueType.vt;

        if (valueSize > 8)
            valueSize = 8;
        memcpy( &(pvarValue->iVal), pvalueBits, valueSize );
        break;

    case VT_VOID:
    case VT_EMPTY:
        pvarValue->vt = valueType.vt;
        break;

    default:
        //not a primitive type
        VariantClear(&valueType);
        free(pvalueBits);
        return E_FAIL;
    }

    free(pvalueBits);
    VariantClear(&valueType);
    return S_OK;
}
```

## <a name="see-also"></a>另请参阅
- [局部变量的示例实现](../../extensibility/debugger/sample-implementation-of-locals.md)
- [获取本地值](../../extensibility/debugger/getting-local-values.md)
- [计算上下文](../../extensibility/debugger/evaluation-context.md)
