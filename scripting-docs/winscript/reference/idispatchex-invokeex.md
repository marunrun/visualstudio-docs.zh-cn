---
title: IDispatchEx：： InvokeEx |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.InvokeEx
apilocation:
- scrobj.dll
helpviewer_keywords:
- InvokeEx method
ms.assetid: d90783e6-4b89-4423-8a56-a9c8b4b2c813
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8a15acb3211c0d3dd19c0d262efb6cbd3327ab9a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575319"
---
# <a name="idispatchexinvokeex"></a>IDispatchEx::InvokeEx
提供对 `IDispatchEx` 对象公开的属性和方法的访问。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT InvokeEx(  
   DISPID id,  
   LCID lcid,  
   WORD wFlags,  
   DISPARAMS *pdp,  
   VARIANT *pVarRes,   
   EXCEPINFO *pei,   
   IServiceProvider *pspCaller   
);  
```  
  
#### <a name="parameters"></a>参数  
 `id`  
 标识成员。 使用 `GetDispID` 或 `GetNextDispID` 获取调度标识符。  
  
 `lcid`  
 要在其中解释自变量的区域设置上下文。 @No__t_0 传递给 `InvokeEx`，以允许对象解释特定于区域设置的参数。  
  
 `wFlags`  
 @No__t_0 的合法值为：  
  
 DISPATCH_PROPERTYGET &#124; DISPATCH_METHOD &#124; DISPATCH_PROPERTYPUT &#124; DISPATCH_PROPERTYPUTREF &#124; DISPATCH_CONSTRUCT  
  
 描述 `InvokeEx` 调用的上下文的标志：  
  
|“值”|含义|  
|-----------|-------------|  
|DISPATCH_METHOD|成员作为方法进行调用。 如果属性具有相同的名称，则可以同时设置此标志和 DISPATCH_PROPERTYGET 标志（由 `IDispatch` 定义）。|  
|DISPATCH_PROPERTYGET|成员作为属性或数据成员进行检索（由 `IDispatch` 定义）。|  
|DISPATCH_PROPERTYPUT|成员将更改为属性或数据成员（由 `IDispatch` 定义）。|  
|DISPATCH_PROPERTYPUTREF|通过引用赋值而不是值赋值来更改成员。 仅当属性接受对对象（由 `IDispatch` 定义）的引用时，此标志才有效。|  
|DISPATCH_CONSTRUCT|正在将该成员用作构造函数。 （这是由 `IDispatchEx` 定义的新值）。 @No__t_0 的合法值为：<br /><br /> DISPATCH_PROPERTYGET DISPATCH_METHOD DISPATCH_PROPERTYPUT DISPATCH_PROPERTYPUTREF DISPATCH_CONSTRUCT|  
  
 `pdp`  
 指向一个结构的指针，该结构包含一个参数数组、一个命名参数的 DISPID 参数数组和数组中元素数的计数。 有关 DISPPARAMS 结构的完整说明，请参阅 `IDispatch` 文档。  
  
 `pVarRes`  
 指向要存储结果的位置的指针; 如果调用方不需要任何结果，则为 Null。 如果指定了 DISPATCH_PROPERTYPUT 或 DISPATCH_PROPERTYPUTREF，则忽略此参数。  
  
 `pei`  
 指向一个包含异常信息的结构的指针。 如果返回 `DISP_E_EXCEPTION`，则应填写此结构。 可以为 Null。 有关 `EXCEPINFO` 结构的完整说明，请参阅 `IDispatch` 文档。  
  
 `pspCaller`  
 一个指针，指向由调用方提供的服务提供程序对象，该对象允许对象获取调用方提供的服务。 可以为 Null。  
  
 `IDispatchEx::InvokeEx` 提供 `IDispatch::Invoke` 的所有相同功能，并添加了一些扩展：  
  
|||  
|-|-|  
|DISPATCH_CONSTRUCT|指示该项正用作构造函数。|  
|`pspCaller`|@No__t_0 允许对象访问调用方提供的服务。 特定服务可由调用方自身处理或委托给调用链中的调用方。 例如，如果浏览器内的脚本引擎对外部对象进行 `InvokeEx` 调用，则该对象可以跟随 `pspCaller` 链来从脚本引擎或浏览器中获取服务。 （请注意，调用链不同于创建链，也称为容器链或站点链。 可以通过某些其他机制（如 `IObjectWithSite`）来使用创建链。|  
|`this` 指针|如果在 `wFlags` 中设置 DISPATCH_METHOD，则 "this" 值可能有 "命名参数"。 DISPID 将为 DISPID_THIS，它必须是第一个命名参数。|  
  
 @No__t_1 中未使用的 `riid` 参数已被移除。  
  
 @No__t_1 中的 `puArgArr` 参数已被移除。  
  
 请参阅 `IDispatch::Invoke` 文档以了解以下示例：  
  
 "调用不带参数的方法"  
  
 "获取和设置属性"  
  
 "传递参数"  
  
 "索引属性"  
  
 "在调用期间引发异常"  
  
 "返回错误"  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|DISP_E_BADPARAMCOUNT|提供给 DISPPARAMS 的元素数不同于方法或属性接受的参数数量。|  
|DISP_E_BADVARTYPE|@No__t_0 中的一个参数不是有效的 variant 类型。|  
|DISP_E_EXCEPTION|应用程序需要引发异常。 在这种情况下，应填写 `pei` 中传递的结构。|  
|DISP_E_MEMBERNOTFOUND|请求的成员不存在，或对 `InvokeEx` 的调用尝试设置只读属性的值。|  
|DISP_E_NONAMEDARGS|@No__t_0 的这一实现不支持命名参数。|  
|DISP_E_OVERFLOW|@No__t_0 中的某个参数无法强制转换为指定的类型。|  
|DISP_E_PARAMNOTFOUND|实参之一不对应于方法的形参。|  
|DISP_E_TYPEMISMATCH|一个或多个参数无法被强制。|  
|DISP_E_UNKNOWNLCID|被调用的成员将根据 LCID 解释字符串参数，且 LCID 无法识别。 如果不需要 LCID 来解释参数，则不应返回此错误。|  
|DISP_E_PARAMNOTOPTIONAL|省略了必需的参数。|  
  
## <a name="example"></a>示例  
  
```cpp
VARIANT var;  
   BSTR bstrName;  
   DISPID dispid;  
   IDispatchEx *pdex;  
   DISPPARAMS dispparamsNoArgs = {NULL, NULL, 0, 0};  
  
   // Assign to pdex and bstrName  
   if (SUCCEEDED(pdex->GetDispID(bstrName, fdexNameCaseSensitive, &dispid)))  
   {  
      pdex->InvokeEx(dispid, LOCALE_USER_DEFAULT,  
         DISPATCH_PROPERTYGET, &dispparamsNoArgs,   
         &var, NULL, NULL);  
   }  
```  
  
## <a name="see-also"></a>请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx：： GetDispID](../../winscript/reference/idispatchex-getdispid.md)    
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)