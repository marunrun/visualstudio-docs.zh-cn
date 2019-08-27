---
title: IActiveScriptProperty::GetProperty | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptProperty.GetProperty
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetProperty method, IActiveScriptProperty interface
ms.assetid: a43383db-b148-4d76-83bd-4f0e899b7cb1
caps.latest.revision: 24
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e10d72e289fc2dc31464ce4505cea5c03e8d7f9d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992793"
---
# <a name="iactivescriptpropertygetproperty"></a>IActiveScriptProperty::GetProperty
获取由参数指定的属性。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetProperty(  
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
 要获取的属性值。  
  
 `pvarIndex`  
 未使用。  
  
 `pvarValue`  
 该属性的值。  
  
 允许使用值`dwProperty`以下表所述。  
  
|返回的常量|“值”|含义|  
|--------------|-----------|-------------|  
|SCRIPTPROP_INTEGERMODE|0x00003000|强制将整数模式而不是浮动点模式中的脚本引擎。|  
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
 主机可以使用 SCRIPTPROP_ABBREVIATE_GLOBALNAME_RESOLUTION 属性以通知其他任何脚本引擎存在于全局对象提供的脚本引擎。 例如，可以通知 Internet Explorer[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]引擎所呈现页只包含[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本。 因此，仅[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]引擎可以将新属性添加到全局对象窗口中，并且没有任何 Visual Basic Scripting Edition (VBScript) 引擎执行此操作。 该引擎可以忽略此标志，或可以使用它来优化的新成员添加到全局对象的管理。  
  
 主机可以使用 SCRIPTPROP_INVOKEVERSIONING 属性选择的语言功能集时支持[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本引擎已启动。 如果此属性设置为 1 (SCRIPTLANGUAGEVERSION_5_7)，可用的语言功能将与那些在版本 5.7 中出现相同[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]脚本引擎。 如果它设置为 2 (SCRIPTLANGUAGEVERSION_5_8)，可用的语言功能是出现在版本 5.7 除了 5.8 版本中已添加的功能。 默认情况下，此属性设置为 0 (SCRIPTLANGUAGEVERSION_DEFAULT)，除非该主机支持不同的默认行为，此操作等效于在版本 5.7 中出现的语言功能集。 例如，Internet Explorer 8 选择[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]5.8 版本支持的语言功能[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]默认情况下，Internet Explorer 8 的文档模式是"Internet Explorer 8 标准"模式时的脚本引擎。  
  
## <a name="see-also"></a>请参阅  
 [定义文档兼容性](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/compatibility/cc288325(v=vs.85))   
 [IActiveScriptProperty](../../winscript/reference/iactivescriptproperty.md)   
 [版本信息](../../javascript/reference/javascript-version-information.md)