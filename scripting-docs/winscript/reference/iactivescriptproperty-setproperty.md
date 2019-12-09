---
title: IActiveScriptProperty：： SetProperty |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProperty.SetProperty
apilocation:
- scrobj.dll
helpviewer_keywords:
- SetProperty method, IActiveScriptProperty interface
ms.assetid: 0ba429c5-04a3-4505-bc5f-69c505dfca91
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0f8307a82f181be20205c7bfcc47e881b0fa1e90
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571311"
---
# <a name="iactivescriptpropertysetproperty"></a>IActiveScriptProperty::SetProperty
设置由参数指定的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT SetProperty(  
// The property value:  
    uint dwProperty,    
// Not used:   
    IntPtr pvarIndex,    
// The value of the property:   
    out object pvarValue,    
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwProperty`  
 要设置的属性值。  
  
 `pvarIndex`  
 未使用。  
  
 `pvarValue`  
 该属性的值。  
  
 下表描述了 `dwProperty` 允许的值。  
  
|常量|值|含义|  
|--------------|-----------|-------------|  
|SCRIPTPROP_INTEGERMODE|0x00003000|强制脚本引擎以整数模式而不是浮点模式进行拆分。 默认值为 `False`。|  
|SCRIPTPROP_STRINGCOMPAREINSTANCE|0x00003001|允许替换脚本引擎的字符串比较函数。|  
|SCRIPTPROP_ABBREVIATE_GLOBALNAME_RESOLUTION|0x70000002|通知脚本引擎，不存在其他脚本引擎来提供给全局对象。|  
|SCRIPTPROP_INVOKEVERSIONING|0x00004000|强制 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎选择一组要支持的语言功能。 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎支持的语言功能的默认集合等效于 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎版本5.7 中显示的语言功能集。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|自变量无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，尚未加载或初始化脚本引擎）。|  
  
## <a name="remarks"></a>备注  
 若要启用或禁用整数除法，请调用 `SetProperty` 并将 `Boolean` 转换为 `Object`。 默认情况下，属性值为 `False`。 如果将其设置为 `True`，除法运算将仅返回整数。  
  
 若要启用或禁用自定义字符串比较，请调用 `SetProperty` 并传入 `Object` 值。 传入的对象必须实现接口[IActiveScriptStringCompare 接口](../../winscript/reference/iactivescriptstringcompare-interface.md)。 每次执行字符串比较函数时，都会调用[IActiveScriptStringCompare 接口](../../winscript/reference/iactivescriptstringcompare-interface.md)接口的[StrComp](../../winscript/reference/iactivescriptstringcompare-strcomp.md)方法。  
  
 若要在初始化 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎时选择要支持的语言功能集，请调用 `SetProperty` 并传递与为 SCRIPTPROP_INVOKEVERSIONING 启用的语言功能设置对应的值。 如果将此属性设置为1（SCRIPTLANGUAGEVERSION_5_7），则可用的语言功能与 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎版本5.7 中显示的功能相同。 如果将其设置为2（SCRIPTLANGUAGEVERSION_5_8），则可用的语言功能是在版本5.7 中显示的功能，以及在版本5.8 中添加的新功能。 默认情况下，此属性设置为0（SCRIPTLANGUAGEVERSION_DEFAULT），它等效于版本5.7 中显示的语言功能集，除非宿主支持不同的默认行为。 例如，Internet explorer 8 引入了版本 5.8 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎支持的 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 语言功能，默认情况下，Internet Explorer 8 的默认文档模式为 "Internet Explorer 8 标准" 模式。 将 Internet Explorer 8 文档模式切换到 Internet Explorer 7 标准或兼容模式，将 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎重置为仅支持版本 5.7 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎中存在的语言功能集。  
  
> [!NOTE]
> 只应在初始化 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎时设置 SCRIPTPROP_INVOKEVERSIONING。  
  
## <a name="example"></a>示例  
 下面的示例演示如何强制脚本引擎使用整数除法，以及如何允许重载比较函数。  
  
```c#  
BMLScriptEngine bmlScriptEngine = new BMLScriptEngine();  
IActiveScriptProperty scriptProperties = bmlScriptEngine as   
    IActiveScriptProperty;  
  
// Force the scripting engine to use integer division.  
Boolean enableIntegerDivision = true;  
Object vtIntegerDivInstance = (Object)enableIntegerDivision;  
                scriptProperties.SetProperty(SCRIPTPROP_INTEGERDIVISION,   
    System.IntPtr.Zero, ref vtIntegerDivInstance);  
  
// Allow overloading of the compare function.  
BMLScriptStringCompare bmlScriptStringCompareInstance = new   
    BMLScriptStringCompare();  
Object vtStrCmpInstance = (Object)bmlScriptStringCompareInstance;  
scriptProperties.SetProperty(SCRIPTPROP_STRCOMPINST,   
    System.IntPtr.Zero, ref vtStrCmpInstance);  
```  
  
## <a name="see-also"></a>另请参阅  
 [定义文档兼容性](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/compatibility/cc288325(v=vs.85))   
 [IActiveScriptProperty](../../winscript/reference/iactivescriptproperty.md)   
 [版本信息](../../javascript/reference/javascript-version-information.md)