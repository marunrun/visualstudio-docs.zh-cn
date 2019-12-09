---
title: IActiveScriptProperty：： GetProperty |Microsoft Docs
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
ms.openlocfilehash: f1eeec6472a067d18a8b8962cfac70c25c0ff971
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571412"
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
  
 下表描述了 `dwProperty` 允许的值。  
  
|常量|值|含义|  
|--------------|-----------|-------------|  
|SCRIPTPROP_INTEGERMODE|0x00003000|强制脚本引擎以整数模式而不是浮点模式进行拆分。|  
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
 宿主可以使用 SCRIPTPROP_ABBREVIATE_GLOBALNAME_RESOLUTION 属性来通知脚本引擎，不存在其他脚本引擎来提供给全局对象。 例如，Internet Explorer 可以通知 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 引擎，呈现的页面只包含 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本。 因此，只有 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 引擎才能向全局对象窗口添加新属性，并且没有 Visual Basic Scripting Edition （VBScript）引擎来执行相同操作。 引擎可以忽略此标志，也可以使用它来优化添加到全局对象的新成员的管理。  
  
 主机可以使用 "SCRIPTPROP_INVOKEVERSIONING" 属性来选择 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎启动时支持的语言功能集。 如果将此属性设置为1（SCRIPTLANGUAGEVERSION_5_7），则可用的语言功能与 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎版本5.7 中显示的功能相同。 如果将其设置为2（SCRIPTLANGUAGEVERSION_5_8），则可用的语言功能是在版本5.7 中显示的功能，以及在版本5.8 中添加的功能。 默认情况下，此属性设置为0（SCRIPTLANGUAGEVERSION_DEFAULT），它等效于版本5.7 中显示的语言功能集，除非宿主支持不同的默认行为。 例如，internet explorer 8 默认为 "internet explorer 8 标准" 模式下的 "internet explorer 8 标准" 模式下的版本 5.8 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 脚本引擎支持的 [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 语言功能。  
  
## <a name="see-also"></a>另请参阅  
 [定义文档兼容性](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/compatibility/cc288325(v=vs.85))   
 [IActiveScriptProperty](../../winscript/reference/iactivescriptproperty.md)   
 [版本信息](../../javascript/reference/javascript-version-information.md)