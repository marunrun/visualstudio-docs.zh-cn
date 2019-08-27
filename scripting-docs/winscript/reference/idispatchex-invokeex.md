---
title: IDispatchEx::InvokeEx | Microsoft Docs
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
ms.openlocfilehash: 33494836e463c9c2fd74acf7835d7e4630747b0e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000742"
---
# <a name="idispatchexinvokeex"></a>IDispatchEx::InvokeEx
提供对属性和方法公开的访问`IDispatchEx`对象。  
  
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
 标识成员。 使用`GetDispID`或`GetNextDispID`若要获取的调度标识符。  
  
 `lcid`  
 要在其中解释自变量的区域设置上下文。 `lcid`传递给`InvokeEx`以允许要解释特定于区域设置其参数的对象。  
  
 `wFlags`  
 的合法值为`wFlags`是：  
  
 DISPATCH_PROPERTYGET &#124; DISPATCH_METHOD &#124; DISPATCH_PROPERTYPUT &#124; DISPATCH_PROPERTYPUTREF &#124; DISPATCH_CONSTRUCT  
  
 描述的上下文的标志`InvokeEx`调用：  
  
|“值”|含义|  
|-----------|-------------|  
|DISPATCH_METHOD|作为一种方法在调用成员。 如果属性具有相同的名称，可能会设置此和 DISPATCH_PROPERTYGET 标志 (由定义`IDispatch`)。|  
|DISPATCH_PROPERTYGET|该成员作为属性或数据成员进行检索 (由定义`IDispatch`)。|  
|DISPATCH_PROPERTYPUT|该成员是否已更改为属性或数据成员 (由定义`IDispatch`)。|  
|DISPATCH_PROPERTYPUTREF|通过引用分配而不是值分配更改成员。 仅当属性接受对对象的引用时，此标志才有效 (由定义`IDispatch`)。|  
|DISPATCH_CONSTRUCT|该成员用作构造函数。 (这是由定义的新值`IDispatchEx`)。 的合法值为`wFlags`是：<br /><br /> DISPATCH_PROPERTYGET DISPATCH_METHOD DISPATCH_PROPERTYPUT DISPATCH_PROPERTYPUTREF DISPATCH_CONSTRUCT|  
  
 `pdp`  
 指向一个结构的指针，该结构包含一个参数数组、一个命名参数的 DISPID 参数数组和数组中元素数的计数。 请参阅`IDispatch`DISPPARAMS 结构的完整说明的文档。  
  
 `pVarRes`  
 结果将为存储或为 Null，如果调用方希望无结果的位置的指针。 如果指定 DISPATCH_PROPERTYPUT 或 DISPATCH_PROPERTYPUTREF，则忽略此参数。  
  
 `pei`  
 指向一个包含异常信息的结构的指针。 如果应填充此结构`DISP_E_EXCEPTION`返回。 可以为 Null。 请参阅`IDispatch`文档的完整说明`EXCEPINFO`结构。  
  
 `pspCaller`  
 指向由调用方，使该对象可以获取调用方中的服务提供的服务提供程序对象的指针。 可以为 Null。  
  
 `IDispatchEx::InvokeEx` 提供所有与相同的功能`IDispatch::Invoke`和添加了一些扩展：  
  
|||  
|-|-|  
|DISPATCH_CONSTRUCT|指示项正用作构造函数。|  
|`pspCaller`|`pspCaller`允许调用方提供的服务对象访问。 特定的服务可能由调用方本身或委派给调用方进一步调用链。 例如，如果脚本引擎在浏览器将发出`InvokeEx`到外部对象，该对象的调用可以按照`pspCaller`链来获取从脚本引擎或浏览器服务。 (请注意，在调用链不创建链相同 — 也称为容器链或站点链。 创建链就能通过其他某种机制如`IObjectWithSite`。)|  
|`this` 指针|DISPATCH_METHOD 如果设置`wFlags`，可能有一个"命名的参数""this"的值。 DISPID 将 DISPID_THIS 并且它必须是第一个命名的参数。|  
  
 未使用`riid`中的参数`IDispatch::Invoke`已删除。  
  
 `puArgArr`中的参数`IDispatch::Invoke`已删除。  
  
 请参阅`IDispatch::Invoke`下面的示例文档：  
  
 "调用不带任何参数的方法"  
  
 "获取和设置属性"  
  
 "将参数传递"  
  
 "索引的属性"  
  
 "在调用期间引发异常"  
  
 "返回错误"  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|||  
|-|-|  
|`S_OK`|成功。|  
|DISP_E_BADPARAMCOUNT|提供给 DISPPARAMS 的元素数与不同的参数接受由方法或属性的数目。|  
|DISP_E_BADVARTYPE|中的自变量之一`rgvarg`不是有效的 variant 类型。|  
|DISP_E_EXCEPTION|应用程序需要引发异常。 在这种情况下，该结构传递`pei`应填充。|  
|DISP_E_MEMBERNOTFOUND|请求的成员不存在，或者对调用`InvokeEx`尝试设置只读属性的值。|  
|DISP_E_NONAMEDARGS|此实现`IDispatch`不支持命名的参数。|  
|DISP_E_OVERFLOW|中的自变量之一`rgvarg`不进行强制转换为指定的类型。|  
|DISP_E_PARAMNOTFOUND|其中一个参数的 Dispid 不对应的方法的参数。|  
|DISP_E_TYPEMISMATCH|一个或多个自变量不能强制。|  
|DISP_E_UNKNOWNLCID|所调用的成员将解释字符串参数，根据 LCID、 LCID 不被识别。 如果不需要 LCID 解释参数，应不会返回此错误。|  
|DISP_E_PARAMNOTOPTIONAL|所需的参数被省略。|  
  
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
 [IDispatchEx::GetDispID](../../winscript/reference/idispatchex-getdispid.md)   
 [IDispatchEx::GetNextDispID](../../winscript/reference/idispatchex-getnextdispid.md)