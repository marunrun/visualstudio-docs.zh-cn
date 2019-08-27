---
title: IActiveScriptProperty::SetProperty | Microsoft Docs
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
ms.openlocfilehash: d689b7b2a252b208ae578f9bfd95ab93777f7cc5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385950"
---
# <a name="iactivescriptpropertysetproperty"></a>IActiveScriptProperty::SetProperty
由参数指定的属性设置。  
  
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
  
 允许使用值`dwProperty`以下表所述。  
  
|返回的常量|“值”|含义|  
|--------------|-----------|-------------|  
|SCRIPTPROP_INTEGERMODE|0x00003000|强制将整数模式而不是浮动点模式中的脚本引擎。 默认值为 `False`。|  
|SCRIPTPROP_STRINGCOMPAREINSTANCE|0x00003001|允许脚本引擎要替换的字符串比较功能。|  
|SCRIPTPROP_ABBREVIATE_GLOBALNAME_RESOLUTION|0x70000002|通知其他任何脚本引擎存在于全局对象提供的脚本引擎。|  
|SCRIPTPROP_INVOKEVERSIONING|0x00004000|强制[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本引擎，若要选择的语言功能来支持一组。 支持的语言功能的默认集[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本引擎相当于在版本 5.7 中出现的语言功能集[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本引擎。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|自变量无效。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化）。|  
  
## <a name="remarks"></a>备注  
 若要启用或禁用整数除法，调用`SetProperty`，并将转换`Boolean`到`Object`。 默认情况下，属性值是`False`。 如果设置为`True`，除法运算将返回仅的整数。  
  
 若要启用或禁用自定义的字符串比较，请调用`SetProperty`，并传入`Object`值。 在传递的对象必须实现接口[IActiveScriptStringCompare 接口](../../winscript/reference/iactivescriptstringcompare-interface.md)。 [StrComp](../../winscript/reference/iactivescriptstringcompare-strcomp.md)方法[IActiveScriptStringCompare 接口](../../winscript/reference/iactivescriptstringcompare-interface.md)执行字符串比较函数每次调用接口。  
  
 若要选择的语言功能来时支持一组[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]初始化脚本引擎，则将调用`SetProperty`并将对应的值传递给为 SCRIPTPROP_INVOKEVERSIONING 启用的一组语言功能。 如果此属性设置为 1 (SCRIPTLANGUAGEVERSION_5_7)，可用的语言功能将与那些在版本 5.7 中出现相同[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本引擎。 如果它设置为 2 (SCRIPTLANGUAGEVERSION_5_8)，可用的语言功能是出现在版本 5.7 除了 5.8 版本中添加了的新功能。 默认情况下，此属性设置为 0 (SCRIPTLANGUAGEVERSION_DEFAULT)，除非该主机支持不同的默认行为，此操作等效于在版本 5.7 中出现的语言功能集。 例如，Internet Explorer 8 选择[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]5.8 版本都支持的语言功能[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]默认情况下，Internet Explorer 8 的默认文档模式是"Internet Explorer 8 标准"模式时的脚本引擎。 切换到 Internet Explorer 7 标准的 Internet Explorer 8 文档模式或 Quirks 模式重置[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本引擎来在版本 5.7 中支持仅存在于的语言功能集[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本引擎。  
  
> [!NOTE]
> 应仅当设置 SCRIPTPROP_INVOKEVERSIONING[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]正在初始化脚本引擎。  
  
## <a name="example"></a>示例  
 下面的示例演示如何强制执行要使用整数除法的脚本引擎以及如何允许比较函数的重载。  
  
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
  
## <a name="see-also"></a>请参阅  
 [定义文档兼容性](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/compatibility/cc288325(v=vs.85))   
 [IActiveScriptProperty](../../winscript/reference/iactivescriptproperty.md)   
 [版本信息](../../javascript/reference/javascript-version-information.md)