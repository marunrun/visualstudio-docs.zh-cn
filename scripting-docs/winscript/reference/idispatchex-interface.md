---
title: IDispatchEx 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDispatchEx interface, about IDispatchEx
- IDispatchEx interface
ms.assetid: 37a3303f-f78e-4b5b-aac8-b836c92819de
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: df3fd7d46fdcb1f3e86bddd53700d7bce6e21381
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63000833"
---
# <a name="idispatchex-interface"></a>IDispatchEx 接口
`IDispatchEx`的扩展`IDispatch`接口，适合脚本编写语言之类的动态语言的支持的功能。 本部分介绍`IDispatchEx`接口本身之间的差异`IDispatch`和`IDispatchEx`，和扩展的基本原理。 应读者都熟悉`IDispatch`并且有权`IDispatch`文档。  
  
## <a name="remarks"></a>备注  
 `IDispatch` 被开发实质上是 for Microsoft Visual Basic 的。 主要限制`IDispatch`是它假定对象是静态。 换而言之，因为未在运行时更改对象，类型信息可以充分描述了它们在编译时。 动态脚本编写语言如 Visual Basic Scripting Edition (VBScript) 中找到的运行时模型和[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]和对象模型，如动态 HTML 需要更灵活的接口。  
  
 `IDispatchEx` 开发用于提供的所有服务`IDispatch`以及一些扩展，适用于更多动态后期绑定语言，如脚本语言。 其他功能`IDispatchEx`超出所提供的`IDispatch`是：  
  
- 将新成员添加到对象 ("expando")，使用`GetDispID`与`fdexNameEnsure`标志。  
  
- 删除对象的成员，使用`DeleteMemberByName`或`DeleteMemberByDispID`。  
  
- 区分大小写的调度操作 — 使用`fdexNameCaseSensitive`或`fdexNameCaseInsensitive`。  
  
- 搜索名称为隐式成员 — 使用`fdexNameImplicit`。  
  
- 枚举的对象的 Dispid — 使用`GetNextDispID`。  
  
- 从 DISPID 到元素名称映射 — 使用`GetMemberName`。  
  
- 获取对象成员的属性 — 使用`GetMemberProperties`。  
  
- 方法调用替换`this`指针 — 使用`InvokeEx`DISPATCH_METHOD 使用。  
  
- 允许浏览器支持的命名空间，以获取父对象的名称空间概念 — 使用`GetNameSpaceParent`。  
  
  对象支持`IDispatchEx`可能还支持`IDispatch`为了向后兼容。 支持的对象的动态特性`IDispatchEx`有几个含义为`IDispatch`这些对象的接口。 例如，`IDispatch`进行以下假设：  
  
- 成员和参数 Dispid 必须保持不变的对象的生存期内。 这允许客户端一次获取 Dispid 并缓存以供将来使用。  
  
  由于`IDispatchEx`允许添加和删除成员，有效的 Dispid 的一套不会不保持不变。 但是，`IDispatchEx`需要 DISPID 和成员名称之间的映射保持不变。 这意味着，如果删除成员：  
  
- 不能重复使用 DISPID，直到创建了一个同名的成员。  
  
- DISPID 必须保持有效`GetNextDispID`。  
  
- DISPID 必须适当地接受的任一`IDispatch`或`IDispatchEx`方法，它们必须识别为已删除的成员，并返回相应的错误代码 （通常 DISP_E_MEMBERNOTFOUND 或 S_FALSE）。  
  
## <a name="examples"></a>示例  
 这[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]函数 test （） 中的代码执行以下操作：  
  
- 通过调用创建一个新对象`Object`构造函数并将指针赋给变量的目标的新对象  
  
- 创建新的元素名 Elem 为对象中并将分配给此元素的指针到函数 cat。  
  
- 调用此函数。 由于它作为一种方法，正在调用`this`指针引用的对象目标该函数将添加新元素栏中的，对对象。  
  
  完整的 HTML 代码是：  
  
```html
<html>  
<body>  
<script type="text/javascript">  
function cat()  
{  
   // Create new element and assign the value 10  
   this.Bar = 10;  
}  
  
function test()  
{  
   // Construct new object  
   Obj = new Object();  
  
   // Create new element and assign function pointer  
   Obj.Elem = cat;  
  
   // Call Elem method ("this" == Obj)  
   Obj.Elem();  
  
   // Obj.Bar now exists  
}  
test();  
</script>  
</body>  
</html>  
```  
  
 在此同一网页上放置的控件可能从浏览器到脚本引擎获取调度指针。 然后，该控件可以实现函数 test （）：  
  
```html
<html>  
<body>  
<script type="text/javascript">  
function cat()  
{  
   // Create new element and assign the value 10  
   this.Bar = 10;  
}  
</script>  
<object id="test" <CLASSID="CLSID:9417DB5D-FA2A-11D0-8CB3-00C04FC2B085">>  
</object>  
</body>  
</html>  
```  
  
 从控件的代码、 测试、 执行同样的操作作为[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]函数`test()`。 请注意，这些调度调用到正在运行[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]引擎和引擎的状态更改：  
  
- 获取调度指向 cat 函数使用`GetDispID()`。  
  
- 获取调度指向对象的函数使用`GetDispID()`。  
  
- 构造一个对象，通过调用对象配合`InvokeEx()`并获取指向新构造的对象的调度。  
  
- 创建新的元素，Elem，在对象中使用`GetDispID()`与`fdexNameEnsure`标志。  
  
- 将调度指针放到在元素中使用的 cat `InvokeEx()`。  
  
- 通过调用作为方法调用调度指向 cat`InvokeEx()`并在调度指针将传递给构造的对象作为`this`指针。  
  
- Cat 方法创建新的元素，栏中的，在当前`this`对象。  
  
- 验证新元素，条形图、 创建中构造的对象进行枚举通过使用的元素，从而`GetNextDispID()`。  
  
  测试控件的代码：  
  
```cpp
   BOOL test(IDispatchEx *pdexScript)  
   {  
      HRESULT hr;  
      VARIANT var;  
      DISPID dispid, putid;  
      BOOL retval = FALSE;  
      BSTR bstrName = NULL;  
      IDispatch   *pdispObj = NULL, *pdispCat = NULL;  
      IDispatchEx *pdexObj = NULL;  
      DISPPARAMS dispparams, dispparamsNoArgs = {NULL, NULL, 0, 0};  
  
      // Get dispatch pointer for "cat"  
      bstrName = SysAllocString(OLESTR("cat"));  
         if (bstrName == NULL) goto LDone;  
      hr = pdexScript->GetDispID(bstrName, 0, &dispid);  
         if (FAILED(hr)) goto LDone;  
      SysFreeString(bstrName);  
         bstrName = NULL;  
      hr = pdexScript->InvokeEx(dispid, LOCALE_USER_DEFAULT,   
         DISPATCH_PROPERTYGET, &dispparamsNoArgs,   
         &var, NULL, NULL);  
         if (FAILED(hr)) goto LDone;  
      pdispCat = var.pdispVal;  
  
      // Create object by calling "Object" constructor  
      bstrName = SysAllocString(OLESTR("Object"));  
         if (NULL == bstrName) goto LDone;  
      hr = pdexScript->GetDispID(bstrName, 0, &dispid);  
         if (FAILED(hr)) goto LDone;  
      SysFreeString(bstrName);  
         bstrName = NULL;  
      hr = pdexScript->InvokeEx(dispid, LOCALE_USER_DEFAULT,   
         DISPATCH_CONSTRUCT, &dispparamsNoArgs,   
         &var, NULL, NULL);  
         if (FAILED(hr)) goto LDone;  
      pdispObj = var.pdispVal;  
      hr = pdispObj->QueryInterface(IID_IDispatchEx, (void **)&pdexObj);  
         if (FAILED(hr)) goto LDone;  
  
      // Create new element in object  
      bstrName = SysAllocString(OLESTR("Elem"));  
         if (NULL == bstrName) goto LDone;  
      hr = pdexObj->GetDispID(bstrName, fdexNameEnsure, &dispid);  
         if (FAILED(hr)) goto LDone;  
      SysFreeString(bstrName);  
         bstrName = NULL;  
  
      // Assign "cat" dispatch pointer to element  
      putid = DISPID_PROPERTYPUT;  
      var.vt = VT_DISPATCH;  
      var.pdispVal = pdispCat;  
      dispparams.rgvarg = &var;  
      dispparams.rgdispidNamedArgs = &putid;  
      dispparams.cArgs = 1;  
      dispparams.cNamedArgs = 1;  
      hr = pdexObj->InvokeEx(dispid, LOCALE_USER_DEFAULT,   
         DISPATCH_PROPERTYPUTREF, &dispparams,  
         NULL, NULL, NULL);  
         if (FAILED(hr)) goto LDone;  
  
      // Invoke method with "this" pointer  
      putid = DISPID_THIS;  
      var.vt = VT_DISPATCH;  
      var.pdispVal = pdispObj;  
      dispparams.rgvarg = &var;  
      dispparams.rgdispidNamedArgs = &putid;  
      dispparams.cArgs = 1;  
      dispparams.cNamedArgs = 1;  
      hr = pdexObj->InvokeEx(dispid, LOCALE_USER_DEFAULT,  
         DISPATCH_METHOD, &dispparams,  
            NULL, NULL, NULL);  
         if (FAILED(hr)) goto LDone;  
  
      // Confirm that new element "Bar" is in object  
      hr = pdexObj->GetNextDispID(fdexEnumAll, DISPID_STARTENUM, &dispid);  
      while (hr == NOERROR)  
      {  
            hr = pdexObj->GetMemberName(dispid, &bstrName);  
            if (FAILED(hr)) goto LDone;  
            retval = !wcscmp(bstrName, OLESTR("Bar"));  
            SysFreeString(bstrName);  
            bstrName = NULL;  
            if (retval) goto LDone;  
         hr = pdexObj->GetNextDispID(fdexEnumAll, dispid, &dispid);  
      }  
LDone:  
   SysFreeString(bstrName);  
   if (pdispCat != NULL)  
      pdispCat->Release();  
   if (pdispObj != NULL)  
      pdispObj->Release();  
   if (pdexObj != NULL)  
      pdexObj->Release();  
  
   return retval;  
   }  
```  
  
## <a name="methods"></a>方法  
 [IDispatchEx 方法](../../winscript/reference/idispatchex-methods.md)