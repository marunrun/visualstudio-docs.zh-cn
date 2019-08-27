---
title: 获取局部属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, getting local properties
- debugging [Debugging SDK], local properties
- expression evaluation, local properties
ms.assetid: 6c3a79e8-1ba1-4863-97c3-0216c3d9f092
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b174af9e107c13c3d8a79f00493fe5dbdd180ec6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436400"
---
# <a name="getting-local-properties"></a>获取局部属性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 Visual Studio 调用[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)来获取[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象，它提供对要在中显示的所有局部变量的访问**局部变量**窗口。 Visual Studio 然后调用[下一步](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)来获取要为每个本地显示的信息。 在此示例中，该类`CEnumPropertyInfo`实现`IEnumDebugPropertyInfo2`接口。  
  
 此实现`IEnumDebugPropertyInfo2::Next`执行下列任务：  
  
1. 清除其中的信息是要存储的数组。  
  
2. 调用[下一步](../../extensibility/debugger/reference/ienumdebugfields-next.md)对于每个本地存储返回[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)中要返回的数组。 [IEnumDebugFields](../../extensibility/debugger/reference/ienumdebugfields.md)提供对象时这`CEnumPropertyInfo`类实例化。  
  
## <a name="managed-code"></a>托管代码  
 此示例演示一种实现`IEnumDebugPropertyInfo2::EnumChildren`在托管代码中的方法的局部变量。  
  
```csharp  
namespace EEMC  
{  
    public class CEnumMethodField : IEnumDebugFields  
    {  
        public HRESULT Next(  
                uint                  count,  
                DEBUG_PROPERTY_INFO[] properties,  
            out uint                  fetched)  
        {  
            if (count > properties.Length)  
                throw new COMException();  
  
            // Zero out the array.  
            for (int i= 0; i < count; i++)  
            {  
                properties[i].bstrFullName = "";  
                properties[i].bstrName = "";  
                properties[i].bstrType = "";  
                properties[i].bstrValue = "";  
                properties[i].dwAttrib = 0;  
                properties[i].dwFields = 0;  
                properties[i].pProperty = null;  
            }  
            fetched = 0;  
  
            // COM interop.  
            HRESULT hr;  
            uint innerFetched;  
            IDebugField[] field = new IDebugField[1];  
  
            while (fetched < count)  
            {  
                field[0] = null;  
                innerFetched = 0;  
  
                // Get next field.  
                if (fetched < fieldCount)  
                    hr = fields.Next(1, field, ref innerFetched);  
                // No more fields.  
                else return COM.S_FALSE;  
  
                if (hr != COM.S_OK || innerFetched != 1 || field[0] == null)  
                    throw new COMException("CEnumPropertyInfo.Next");  
  
                // Get property from field.  
                CFieldProperty fieldProperty =   
                    new CFieldProperty(provider, address, binder, field[0]);  
  
                DEBUG_PROPERTY_INFO[] property =  
                                new DEBUG_PROPERTY_INFO[1];  
                fieldProperty.GetPropertyInfo((uint) infoFlags, radix, 0, null, 0, property);  
                properties[fetched++] = property[0];  
            }  
            return COM.S_OK;  
        }  
    }  
}  
```  
  
## <a name="unmanaged-code"></a>非托管代码  
 此示例演示一种实现`IEnumDebugPropertyInfo2::EnumChildren`非托管代码中的方法的局部变量。  
  
```cpp#  
STDMETHODIMP CEnumPropertyInfo::Next(  
    in  ULONG                count,  
    out DEBUG_PROPERTY_INFO* pelements,   
    out ULONG*               pfetched )  
{  
    if (pfetched)  
        *pfetched = 0;  
    if (!pelements)  
        return E_INVALIDARG;  
    else  
        memset( pelements, 0, count * sizeof(DEBUG_PROPERTY_INFO));  
  
    HRESULT hr  = S_OK;  
    ULONG   idx = 0;  
    while (idx < count)  
    {  
        ULONG        fetchedFields;  
        IDebugField* pfield;  
  
        //get the next field  
        hr = m_fields->Next( 1, &pfield, &fetchedFields );  
        if (FAILED(hr))  
            return hr;  
        if (fetchedFields != 1)  
            return E_FAIL;  
        idx++;  
  
        //create a CFieldProperty to retrieve the DEBUG_PROPERTY_INFO  
        CFieldProperty* pproperty =  
            new CFieldProperty( m_provider, m_address, m_binder, pfield );  
        pfield->Release();  
        if (!pproperty)  
            return E_OUTOFMEMORY;  
  
        hr = pproperty->Init();  
        if (FAILED(hr))  
        {  
            pproperty->Release();  
            return hr;  
        }  
  
        hr = pproperty->GetPropertyInfo( m_infoFlags,  
                                         m_radix,  
                                         0,  
                                         NULL,  
                                         0,  
                                         pelements + idx - 1);  
        pproperty->Release();  
        if (FAILED(hr))  
            return hr;  
    }  
  
    if (pfetched)  
        *pfetched = idx;  
    return hr;  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [局部的实现示例](../../extensibility/debugger/sample-implementation-of-locals.md)   
 [枚举局部](../../extensibility/debugger/enumerating-locals.md)
