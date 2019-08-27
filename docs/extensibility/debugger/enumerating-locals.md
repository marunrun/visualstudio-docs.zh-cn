---
title: 枚举局部 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], enumerating locals
- expression evaluation, enumerating locals
ms.assetid: 254a88e7-d3a7-447a-bd0c-8985e73d85cf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 32700d32b65503cf696b180793e0d9d471571b0a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315462"
---
# <a name="enumerate-locals"></a>枚举局部变量
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

Visual Studio 何时可以来填充**局部变量**窗口中，它将调用[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)上[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)从返回的对象[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) (请参阅[实现 GetMethodProperty](../../extensibility/debugger/implementing-getmethodproperty.md))。 `IDebugProperty2::EnumChildren` 返回[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象。

实现`IDebugProperty2::EnumChildren`执行下列任务：

1. 可确保这表示一种方法。

2. 使用`guidFilter`参数以确定哪种方法要对其调用[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md)对象。 如果`guidFilter`等于：

    1. `guidFilterLocals`调用[EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)来获取[IEnumDebugFields](../../extensibility/debugger/reference/ienumdebugfields.md)对象。

    2. `guidFilterArgs`调用[EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)若要获取`IEnumDebugFields`对象。

    3. `guidFilterLocalsPlusArgs`从结果进行组合的枚举合成`IDebugMethodField::EnumLocals`和`IDebugMethodField::EnumArguments`。 类表示此合成`CEnumMethodField`。

3. 实例化一个类 (称为`CEnumPropertyInfo`在此示例中)，它实现`IEnumDebugPropertyInfo2`接口并包含`IEnumDebugFields`对象。

4. 返回`IEnumDebugProperty2Info2`接口从`CEnumPropertyInfo`对象。

## <a name="managed-code"></a>托管代码
此示例演示一种实现`IDebugProperty2::EnumChildren`在托管代码中。

```csharp
namespace EEMC
{
    public class CFieldProperty : IDebugProperty2
    {
        public HRESULT EnumChildren (
                uint                    dwFields,
                uint                    radix,
            ref Guid                    guidFilter,
                ulong                   attribFilter,
                string                  nameFilter,
                uint                    timeout,
            out IEnumDebugPropertyInfo2 properties)
        {
            properties = null;
            IEnumDebugFields fields = null;

            // If this field is a method...
            if (0 != ((uint) fieldKind & (uint) FIELD_KIND.FIELD_TYPE_METHOD))
            {
                IDebugMethodField methodField = (IDebugMethodField) field;

                // Enumerate parameters.
                if (guidFilter == FilterGuids.guidFilterArgs)
                {
                    methodField.EnumParameters(out fields);
                }
                // Enumerate local variables.
                else if (guidFilter == FilterGuids.guidFilterLocals)
                {
                    methodField.EnumLocals(address, out fields);
                }
                // Enumerate all local variables, including invisible compiler temps.
                else if (guidFilter == FilterGuids.guidFilterAllLocals)
                {
                    methodField.EnumAllLocals(address, out fields);
                }
                // Enumerate "this", if any, and all parameters and local variables.
                else if (guidFilter == FilterGuids.guidFilterLocalsPlusArgs)
                {
                    IDebugClassField fieldThis  = null;
                    IEnumDebugFields parameters = null;
                    IEnumDebugFields locals     = null;

                    methodField.GetThis(out fieldThis);
                    methodField.EnumParameters(out parameters);
                    methodField.EnumLocals(address, out locals);

                    CEnumMethodField enumMethodField =
                        new CEnumMethodField(fieldThis, parameters, locals);
                    fields = (IEnumDebugFields) enumMethodField;
                }
                // Enumerate only "this".
                else if (guidFilter == FilterGuids.guidFilterThis)
                {
                    IDebugClassField fieldThis = null;
                    methodField.GetThis(out fieldThis);

                    CEnumMethodField enumMethodField =
                        new CEnumMethodField(fieldThis, null, null);
                    fields = (IEnumDebugFields) enumMethodField;
                }
                else throw new COMException();// E_FAIL
            }
            // Wrap a property enumerator around the field enumerator.
            CEnumPropertyInfo propertiesInfo =
                new CEnumPropertyInfo(provider, address, binder, radix, fields,
                (DEBUGPROP_INFO_FLAGS) dwFields);

            properties = (IEnumDebugPropertyInfo2) propertiesInfo;
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>非托管的代码
 此示例演示一种实现`IDebugProperty2::EnumChildren`非托管代码中。

```cpp
STDMETHODIMP CFieldProperty::EnumChildren(
        in DEBUGPROP_INFO_FLAGS        infoFlags,
        in DWORD                       radix,
        in REFGUID                     guidFilter,
        in DBG_ATTRIB_FLAGS            attribFilter,
        in LPCOLESTR                   pszNameFilter,
        in DWORD                       timeout,
        out IEnumDebugPropertyInfo2 ** ppchildren )
{
    if (ppchildren == NULL)
        return E_INVALIDARG;
    else
        *ppchildren = 0;

    //get enumeration
    HRESULT hr;
    IEnumDebugFields*     pfields    = NULL;

    if (m_fieldKind & FIELD_TYPE_METHOD)
    {
        //-----------------------------------------------------
        // A Method

        IDebugMethodField*  pmethod    = NULL;

        //enumerate the requested properties
        hr = m_field->QueryInterface( IID_IDebugMethodField,
            reinterpret_cast<void**>(&pmethod) );
        if (FAILED(hr))
            return hr;

        if (guidFilter == guidFilterArgs)
        {
            hr = pmethod->EnumParameters( &pfields );
        }
        else if (guidFilter == guidFilterLocals)
        {
            hr = pmethod->EnumLocals( m_address, &pfields );
        }
        else if (guidFilter == guidFilterAllLocals)
        {
            hr = pmethod->EnumAllLocals( m_address, &pfields );
        }
        else if (guidFilter == guidFilterLocalsPlusArgs)
        {
            //we create a special enumerator for this
            IDebugClassField* pfieldThis  = NULL;
            IEnumDebugFields* pparameters = NULL;
            IEnumDebugFields* plocals     = NULL;

            pmethod->GetThis( &pfieldThis );
            pmethod->EnumParameters( &pparameters );
            pmethod->EnumLocals( m_address, &plocals );

            CEnumMethodField* penumMethodField =
                new CEnumMethodField( pfieldThis, pparameters, plocals );
            if (pfieldThis != NULL)
                pfieldThis->Release();
            if (pparameters != NULL)
                pparameters->Release();
            if (plocals != NULL)
                plocals->Release();
            if (!penumMethodField)
            {
                hr = E_OUTOFMEMORY;
            }
            else
            {
                hr = penumMethodField->QueryInterface( IID_IEnumDebugFields,
                        reinterpret_cast<void**>(&pfields) );
                penumMethodField->Release();
            }
        }
        else if (guidFilter == guidFilterThis )
        {
            IDebugClassField* pfieldThis = NULL;

            hr = pmethod->GetThis( &pfieldThis );
            if (SUCCEEDED(hr))
            {
                CEnumMethodField* penumMethodField =
                    new CEnumMethodField( pfieldThis, NULL, NULL );
                pfieldThis->Release();
                if (!penumMethodField)
                {
                    hr = E_OUTOFMEMORY;
                }
                else
                {
                    hr = penumMethodField->QueryInterface( IID_IEnumDebugFields,
                        reinterpret_cast<void**>(&pfields) );
                    penumMethodField->Release();
                }
            }
        }
        else
        {
            hr = E_FAIL;
        }

        pmethod->Release();
        if (hr != S_OK)
            return hr;
    }

    //create a property info enumeration around the field enumerator
    CEnumPropertyInfo* pproperties =
        new CEnumPropertyInfo( m_provider, m_address, m_binder,
                               radix, pfields, infoFlags );
    if (pfields != NULL)
        pfields->Release();
    if (pproperties == NULL)
        return E_OUTOFMEMORY;

    hr = pproperties->QueryInterface( IID_IEnumDebugPropertyInfo2,
        reinterpret_cast<void**>(ppchildren) );
    pproperties->Release();

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [局部的实现示例](../../extensibility/debugger/sample-implementation-of-locals.md)
- [实现 GetMethodProperty](../../extensibility/debugger/implementing-getmethodproperty.md)
- [评估上下文](../../extensibility/debugger/evaluation-context.md)
