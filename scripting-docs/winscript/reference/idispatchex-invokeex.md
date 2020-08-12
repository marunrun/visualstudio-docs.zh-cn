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
ms.openlocfilehash: 673b3f1e64caa79dc2b21641209423d93fe0f834
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144410"
---
# <a name="idispatchexinvokeex"></a>IDispatchEx::InvokeEx
提供对对象公开的属性和方法的访问 `IDispatchEx` 。  
  
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
 要在其中解释自变量的区域设置上下文。 向 `lcid` 传递到，以 `InvokeEx` 允许对象解释特定于区域设置的参数。  
  
 `wFlags`  
 的合法值为 `wFlags` ：  
  
 DISPATCH_PROPERTYGET &#124; DISPATCH_METHOD &#124; DISPATCH_PROPERTYPUT &#124; DISPATCH_PROPERTYPUTREF &#124; DISPATCH_CONSTRUCT  
  
 描述调用的上下文的标志 `InvokeEx` ：  
  
|值|含义|  
|-----------|-------------|  
|DISPATCH_METHOD|成员作为方法进行调用。 如果某个属性具有相同的名称，则这两个标志和 DISPATCH_PROPERTYGET 标志都可以设置 (`IDispatch`) 定义。|  
|DISPATCH_PROPERTYGET|成员作为 () 定义的属性或数据成员来检索 `IDispatch` 。|  
|DISPATCH_PROPERTYPUT|成员将更改为属性或数据成员 (由 `IDispatch`) 定义。|  
|DISPATCH_PROPERTYPUTREF|通过引用赋值而不是值赋值来更改成员。 仅当属性接受对) 定义的 (对象的引用时，此标志才有效 `IDispatch` 。|  
|DISPATCH_CONSTRUCT|正在将该成员用作构造函数。  (这是) 定义的一个新值 `IDispatchEx` 。 的合法值为 `wFlags` ：<br /><br /> DISPATCH_PROPERTYGET DISPATCH_METHOD DISPATCH_PROPERTYPUT DISPATCH_PROPERTYPUTREF DISPATCH_CONSTRUCT|  
  
 `pdp`  
 指向一个结构的指针，该结构包含一个参数数组、一个命名参数的 DISPID 参数数组和数组中元素数的计数。 `IDispatch`有关 DISPPARAMS 结构的完整说明，请参阅文档。  
  
 `pVarRes`  
 指向要存储结果的位置的指针; 如果调用方不需要任何结果，则为 Null。 如果指定 DISPATCH_PROPERTYPUT 或 DISPATCH_PROPERTYPUTREF，则忽略此参数。  
  
 `pei`  
 指向一个包含异常信息的结构的指针。 如果返回，则应填写此结构 `DISP_E_EXCEPTION` 。 可以为 Null。 `IDispatch`有关结构的完整说明，请参阅文档 `EXCEPINFO` 。  
  
 `pspCaller`  
 一个指针，指向由调用方提供的服务提供程序对象，该对象允许对象获取调用方提供的服务。 可以为 Null。  
  
 `IDispatchEx::InvokeEx`提供与相同的所有功能 `IDispatch::Invoke` ，并添加几个扩展：  
  
|值|含义|
|-|-|  
|DISPATCH_CONSTRUCT|指示该项正用作构造函数。|  
|`pspCaller`|`pspCaller`允许对象访问调用方提供的服务。 特定服务可由调用方自身处理或委托给调用链中的调用方。 例如，如果浏览器内的脚本引擎对 `InvokeEx` 外部对象进行调用，则该对象可以跟随该 `pspCaller` 链接从脚本引擎或浏览器获取服务。  (请注意，调用链不同于创建链，也称为容器链或站点链。 可以通过某些其他机制（例如）来使用创建链 `IObjectWithSite` 。 ) |  
|`this` 指针|在中设置 DISPATCH_METHOD 时 `wFlags` ，"this" 值可能有 "命名参数"。 DISPID 将 DISPID_THIS，并且必须是第一个命名参数。|  
  
 中未使用的 `riid` 参数已 `IDispatch::Invoke` 被移除。  
  
 `puArgArr`中的参数已 `IDispatch::Invoke` 被移除。  
  
 请参阅 `IDispatch::Invoke` 以下示例的文档：  
  
 "调用不带参数的方法"  
  
 "获取和设置属性"  
  
 "传递参数"  
  
 "索引属性"  
  
 "在调用期间引发异常"  
  
 "返回错误"  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|值|含义|  
|-|-|  
|`S_OK`|成功。|  
|DISP_E_BADPARAMCOUNT|提供给 DISPPARAMS 的元素数不同于方法或属性接受的参数数量。|  
|DISP_E_BADVARTYPE|中的一个参数 `rgvarg` 不是有效的 variant 类型。|  
|DISP_E_EXCEPTION|应用程序需要引发异常。 在这种情况下，应填写传递的结构 `pei` 。|  
|DISP_E_MEMBERNOTFOUND|请求的成员不存在，或对的调用 `InvokeEx` 尝试设置只读属性的值。|  
|DISP_E_NONAMEDARGS|此实现 `IDispatch` 不支持命名参数。|  
|DISP_E_OVERFLOW|中的一个参数 `rgvarg` 未能强制转换为指定的类型。|  
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
  
## <a name="see-also"></a>另请参阅  
 [IDispatchEx 接口](../../winscript/reference/idispatchex-interface.md)   
 [IDispatchEx：： GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)