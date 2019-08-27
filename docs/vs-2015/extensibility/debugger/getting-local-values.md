---
title: 获取局部值 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, local values
- debugging [Debugging SDK], local values
- expression evaluation, getting local values
ms.assetid: a10b0764-65ac-476f-bf42-b4a9c38e20de
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2c01e090ff3459d2d70281ab4fce95d3e6f68759
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436376"
---
# <a name="getting-local-values"></a>获取局部值
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 若要获取局部变量的值，Visual Studio 会调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)该本地的。 在此实现中，类`CFieldProperty`为每个本地实施 IDebugProperty2 接口。  
  
 此实现`IDebugProperty2::GetPropertyInfo`执行下列任务：  
  
1. 获取局部变量的名称、 属性和属性从[FIELD_INFO](../../extensibility/debugger/reference/field-info.md)类已实例化和初始化时填充的结构。  
  
2. 获取局部变量的类型从[IDebugField](../../extensibility/debugger/reference/idebugfield.md)对象。  
  
3. 获取局部变量的值从`IDebugField`对象。 此字段绑定到的本地使用的内存位置[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)对象和值从生成获取[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)对象。  
  
4. 返回所有请求中的属性[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)结构。  
  
## <a name="managed-code"></a>托管代码  
 此示例演示一种实现`IDebugProperty2::GetPropertyInfo`为一种方法的本地托管代码中。 它还显示一个帮助程序函数， `Field.GetType`，即用于获取字段的类型。 `Field.GetValue` 中所示[评估局部变量](../../extensibility/debugger/evaluating-locals.md)。 帮助器函数`Field.MapModifiersToAttributes`（未显示） 只需将转换的字段[FIELD_MODIFIERS](../../extensibility/debugger/reference/field-modifiers.md)到标志[DBG_ATTRIB_FLAGS](../../extensibility/debugger/reference/dbg-attrib-flags.md)值。  
  
```csharp  
namespace EEMC  
{  
    public class CFieldProperty : IDebugProperty2  
    {  
        public HRESULT GetPropertyInfo(  
            uint                  dwFields,  
            uint                  radix,  
            uint                  timeout,  
            IDebugReference2[]    refArgs,  
            uint                  argCount,   
            DEBUG_PROPERTY_INFO[] infoArray)  
        {  
            DEBUGPROP_INFO_FLAGS flags = (DEBUGPROP_INFO_FLAGS) dwFields;  
            DEBUGPROP_INFO_FLAGS infoFields = DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_NONE;  
  
            // Initialize the structure.  
            DEBUG_PROPERTY_INFO info = infoArray[0];  
            info.pProperty = null;  
  
            // Fill in the full name, if requested.   
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_FULLNAME))  
            {  
                info.bstrFullName = fieldInfo.bstrFullName;  
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_FULLNAME;   
            }  
            // Fill in the name, if requested.   
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_NAME))  
            {  
                info.bstrName = fieldInfo.bstrName;  
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_NAME;   
            }  
            // Fill in the type, if requested.  
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_TYPE))  
            {  
                if (fieldType == null)  
                    fieldType = Field.GetType(field, out fieldSize);  
                if (fieldType == null)  
                    info.bstrType = "unknown";  
                else  
                    info.bstrType = fieldType.ToString();  
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_TYPE;  
            }  
            // The property associated with this property is this property.  
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_PROP))  
            {  
                info.pProperty = this;  
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_PROP;   
            }  
            // Get the property value, if requested.  
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_VALUE))  
            {  
                if (fieldType == null)  
                    fieldType = Field.GetType(field, out fieldSize);  
                if (fieldType == null)  
                    info.bstrValue = "?";  
                else  
                {  
                    object o = Field.GetValue(binder, field, fieldType, fieldSize);  
                    if (o == null)  
                        info.bstrValue = "?";  
                    else  
                        info.bstrValue = o.ToString();  
                }  
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_VALUE;   
            }  
            // Get the property attributes, if requested.  
            if (0 != (flags & DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_ATTRIB))  
            {  
                info.dwAttrib =   
                    (ulong) Field.MapModifiersToAttributes(  
                        (FIELD_MODIFIERS) fieldInfo.dwModifiers,  
                        fieldKind);  
                infoFields |= DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_ATTRIB;   
            }  
            info.dwFields = (uint) infoFields;  
            infoArray[0] = info;  
            return COM.S_OK;  
        }  
    }  
  
//----------------------------------------------------------------------------  
  
    internal class Field  
    {  
        internal static Type GetType(IDebugField field, out uint size)  
        {  
            size = 0;  
  
            IDebugField fieldType = null;  
            field.GetType(out fieldType);  
            if (fieldType == null)  return null;  
  
            // Get field size.  
            fieldType.GetSize(out size);  
  
            // Get approximate type name.  
            FIELD_INFO[] fieldTypeInfo = new FIELD_INFO[1];  
            fieldType.GetInfo((uint) FIELD_INFO_FIELDS.FIF_NAME,  
                fieldTypeInfo);  
  
            // Map approximate name to type name.  
            switch (fieldTypeInfo[0].bstrName)  
            {  
                case "whole":  
                switch (size)  
                {  
                    case 1: return typeof(sbyte);  
                    case 2: return typeof(short);  
                    case 4: return typeof(int);  
                    case 8: return typeof(long);  
                }  
                    break;  
                case "uwhole":  
                switch (size)  
                {  
                    case 1: return typeof(byte);  
                    case 2: return typeof(char);  
                    case 4: return typeof(uint);  
                    case 8: return typeof(ulong);  
                }  
                    break;  
                case "real":  
                switch (size)  
                {  
                    case 4: return typeof(float);  
                    case 8: return typeof(double);  
                }  
                    break;  
                case "bool": return typeof(bool);  
                case "string": return typeof(string);  
            }  
            return null;  
        }  
}  
```  
  
## <a name="unmanaged-code"></a>非托管代码  
 此示例演示一种实现`IDebugProperty2::GetPropertyInfo`为一种方法的本地非托管代码中。 它还演示了两个帮助器函数`FieldGetType`和`FieldGetValue`，它们用来分别获取字段的类型和值。 请注意， `VARIANT`s 用于字段的值，然后键入作为`VARIANT`可以处理各种值类型。 在此实现中，`FieldGetValue`将返回[IDebugField](../../extensibility/debugger/reference/idebugfield.md)是更高版本的对象转换为对的调用中的值`FieldGetPrimitiveValue`(所示[评估局部变量](../../extensibility/debugger/evaluating-locals.md))。  
  
```cpp#  
STDMETHODIMP CFieldProperty::GetPropertyInfo(   
    in  DEBUGPROP_INFO_FLAGS infoFlags,  
    in  DWORD                radix,  
    in  DWORD                timeout,  
    in  IDebugReference2**   ppargs,  
    in  DWORD                argCount,  
    out DEBUG_PROPERTY_INFO* ppropertyInfo  
    )  
{  
    if (!ppropertyInfo)  
        return E_INVALIDARG;  
    else  
        memset(ppropertyInfo,0,sizeof(*ppropertyInfo));  
  
    if (infoFlags & DEBUGPROP_INFO_FULLNAME)  
    {  
        ppropertyInfo->dwFields     |= DEBUGPROP_INFO_FULLNAME;  
        ppropertyInfo->bstrFullName  = SysAllocString( m_fieldInfo.bstrFullName );  
    }  
  
    if (infoFlags & DEBUGPROP_INFO_NAME)  
    {  
        ppropertyInfo->dwFields     |= DEBUGPROP_INFO_NAME;  
        ppropertyInfo->bstrName      = SysAllocString( m_fieldInfo.bstrName );  
    }  
  
    if (infoFlags & DEBUGPROP_INFO_TYPE)  
    {  
        ppropertyInfo->dwFields     |= DEBUGPROP_INFO_TYPE;  
  
        VARIANT type;  
        if (SUCCEEDED(FieldGetType( m_field, &type )))  
        {  
            // Convert the variant's type to a string  
            VariantTypeToString( type, &(ppropertyInfo->bstrType) );  
            VariantClear(&type);  
  
        }  
        if (ppropertyInfo->bstrType == NULL)   
            ppropertyInfo->bstrType = SysAllocString( GetString(IDS_MSG_UNKNOWNTYPE) );  
    }  
  
    if (infoFlags & DEBUGPROP_INFO_PROP)  
    {  
        ppropertyInfo->dwFields     |= DEBUGPROP_INFO_PROP;  
        QueryInterface( IID_IDebugProperty2,  
                        reinterpret_cast<void**>(&(ppropertyInfo->pProperty)) );  
    }  
  
    if (infoFlags & DEBUGPROP_INFO_VALUE)  
    {  
        ppropertyInfo->dwFields   |= DEBUGPROP_INFO_VALUE;  
  
        //only show primitive values  
        VARIANT value;  
        if (SUCCEEDED(FieldGetValue(m_field, &value)))  
        {  
            VariantValueToString( radix, m_binder, value,  
                                  &(ppropertyInfo->bstrValue) );  
            VariantClear(&value);  
        }  
  
        if (ppropertyInfo->bstrValue == NULL)   
            ppropertyInfo->bstrValue = SysAllocString( GetString(IDS_MSG_UNKNOWNVALUE) );  
    }  
  
    if (infoFlags & DEBUGPROP_INFO_VALUE_AUTOEXPAND)  
    {  
    // AUTOEXPAND is ignored in this example  
    }  
  
    if (infoFlags & DEBUGPROP_INFO_ATTRIB)  
    {  
        ppropertyInfo->dwFields   |= DEBUGPROP_INFO_ATTRIB;  
  
        FIELD_MODIFIERS   modifiers = m_fieldInfo.dwModifiers;  
        DBG_ATTRIB_FLAGS  attrib    = DBG_ATTRIB_NONE;  
  
        //access      
        if (modifiers & FIELD_MOD_ACCESS_PUBLIC)  
            attrib |= DBG_ATTRIB_ACCESS_PUBLIC;  
        if (modifiers & FIELD_MOD_ACCESS_PRIVATE)  
            attrib |= DBG_ATTRIB_ACCESS_PRIVATE;  
        if (modifiers & FIELD_MOD_ACCESS_PROTECTED)  
            attrib |= DBG_ATTRIB_ACCESS_PROTECTED;  
        if (modifiers & FIELD_MOD_FINAL)  
            attrib |= DBG_ATTRIB_ACCESS_FINAL;  
  
        //constant  
        if (modifiers & FIELD_MOD_CONSTANT)  
            attrib |= DBG_ATTRIB_VALUE_READONLY;  
  
        //storage  
        if (m_fieldKind & FIELD_SYM_GLOBAL)  
            attrib |= DBG_ATTRIB_STORAGE_GLOBAL;  
        if (modifiers & FIELD_MOD_STATIC)  
            attrib |= DBG_ATTRIB_STORAGE_STATIC;  
  
        //type modifier  
        if (modifiers & FIELD_MOD_VIRTUAL)  
            attrib |= DBG_ATTRIB_TYPE_VIRTUAL;  
        if (modifiers & FIELD_MOD_CONSTANT)  
            attrib |= DBG_ATTRIB_TYPE_CONSTANT;  
        if (modifiers & FIELD_MOD_SYNCHRONIZED)  
            attrib |= DBG_ATTRIB_TYPE_SYNCHRONIZED;  
        if (modifiers & FIELD_MOD_VOLATILE)  
            attrib |= DBG_ATTRIB_TYPE_VOLATILE;  
  
        //type  
        if (m_fieldKind & FIELD_TYPE_METHOD)  
            attrib |= DBG_ATTRIB_METHOD;  
        if (m_fieldKind & FIELD_TYPE_PROP)  
            attrib |= DBG_ATTRIB_PROPERTY;  
        if (m_fieldKind & FIELD_TYPE_CLASS)  
            attrib |= DBG_ATTRIB_CLASS;  
        if (m_fieldKind & FIELD_TYPE_INTERFACE)  
            attrib |= DBG_ATTRIB_INTERFACE;  
        if (m_fieldKind & FIELD_TYPE_INNERCLASS)  
            attrib |= DBG_ATTRIB_INNERCLASS;  
        if (m_fieldKind & FIELD_KIND_SYMBOL)  
            attrib |= DBG_ATTRIB_DATA;  
  
        //set the debug attributes  
        ppropertyInfo->dwAttrib = attrib;  
    }  
  
    return S_OK;  
}  
  
//////////////////////////////////////////////////////////////////////  
// Helper functions  
  
struct PrimitiveTypeInfo  
{  
    LPCOLESTR  pszName;  
    UINT       size;  
    VARTYPE    vt;  
};  
  
PrimitiveTypeInfo primitiveTypeTable[] =  
{  
    { OLE("string"),    0,    VT_BSTR },  
    { OLE("whole"),     1,    VT_I1   },  
    { OLE("whole"),     2,    VT_I2   },  
    { OLE("whole"),     4,    VT_I4   },  
    { OLE("whole"),     8,    VT_I8   },  
    { OLE("uwhole"),    1,    VT_UI1  },  
    { OLE("uwhole"),    2,    VT_UI2  },  
    { OLE("uwhole"),    4,    VT_UI4  },  
    { OLE("uwhole"),    8,    VT_UI8  },  
    { OLE("real"),      4,    VT_R4   },  
    { OLE("real"),      8,    VT_R8   },  
    { OLE("bool"),      1,    VT_BOOL },  
    { OLE("bool"),      2,    VT_BOOL },  
    { OLE("bool"),      4,    VT_BOOL },  
  
    { OLE("System.String"),   0,  VT_BSTR },  
    { OLE("System.SByte"),    1,  VT_I1   },  
    { OLE("System.Int16"),    2,  VT_I2   },  
    { OLE("System.Int32"),    4,  VT_I4   },  
    { OLE("System.Int64"),    8,  VT_I8   },  
    { OLE("System.Byte"),     1,  VT_UI1  },  
    { OLE("System.Char"),     1,  VT_UI2  },  
    { OLE("System.UInt16"),   2,  VT_UI2  },  
    { OLE("System.UInt32"),   4,  VT_UI4  },  
    { OLE("System.UInt64"),   8,  VT_UI8  },  
    { OLE("System.Single"),   4,  VT_R4   },  
    { OLE("System.Double"),   8,  VT_R8   },  
    { OLE("System.Boolean"),  1,  VT_BOOL },  
    { OLE("System.Boolean"),  2,  VT_BOOL },  
    { OLE("System.Boolean"),  4,  VT_BOOL },  
  
    { NULL, 0, VT_EMPTY }  
};  
  
HRESULT FieldGetType( in IDebugField* pfield, out VARIANT* pvarType )  
{  
    HRESULT hr;  
  
    if (pfield == NULL)  
        return E_INVALIDARG;  
    if (pvarType == NULL)  
        return E_INVALIDARG;  
    else  
        *pvarType = 0;  
  
    //get type size and name  
    DWORD        fieldTypeSize;  
    FIELD_INFO   fieldTypeInfo;  
    IDebugField* pfieldType = NULL;  
  
    hr = pfield->GetType( &pfieldType );  
    if (FAILED(hr))  
        return hr;   
  
    hr = pfieldType->GetSize( &fieldTypeSize );  
    if (FAILED(hr))  
    {  
        pfieldType->Release();  
        return hr;  
    }  
  
    hr = pfieldType->GetInfo( FIF_NAME, &fieldTypeInfo );    
    if (FAILED(hr))  
    {  
        pfieldType->Release();  
        return hr;  
    }  
  
    //check for primitive types  
    memset( pvarType, 0, sizeof(*pvarType) );  
    VariantInit(pvarType);  
  
    for (PrimitiveTypeInfo* pprimTypeInfo = primitiveTypeTable;  
         pprimTypeInfo->pszName != NULL;  
         pprimTypeInfo++)  
    {  
        if (pprimTypeInfo->size == fieldTypeSize &&   
           (wcscmp(pprimTypeInfo->pszName,fieldTypeInfo.bstrName) == 0))  
        {  
            pvarType->vt = pprimTypeInfo->vt;  
            break;  
        }  
    }  
  
    //VT_UNKNOWN is used for all other (structured) types  
    if (pvarType->vt == VT_EMPTY)  
    {  
        pvarType->vt      = VT_UNKNOWN;  
        pvarType->punkVal = pfieldType;  
        pvarType->punkVal->AddRef();  
    }  
  
    if (fieldTypeInfo.bstrName != NULL)  
        SysFreeString(fieldTypeInfo.bstrName);  
    pfieldType->Release();  
    return S_OK;  
}  
  
//----------------------------------------------------------------------------  
  
HRESULT FieldGetValue( in IDebugField* pfield, out VARIANT* pvarValue )  
{  
    if (pvarValue == NULL)  
        return E_INVALIDARG;  
    else  
        *pvarValue = 0;  
    if (pfield == NULL)  
        return E_INVALIDARG;  
  
    //we delay getting the primitive value by just setting VT_UNKNOWN  
    pvarValue->vt      = VT_UNKNOWN;  
    pvarValue->punkVal = pfield;  
    pvarValue->punkVal->AddRef();  
  
    return S_OK;  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [局部的实现示例](../../extensibility/debugger/sample-implementation-of-locals.md)   
 [获取局部属性](../../extensibility/debugger/getting-local-properties.md)   
 [计算上下文](../../extensibility/debugger/evaluation-context.md)
