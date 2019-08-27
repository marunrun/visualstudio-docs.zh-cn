---
title: IActiveScriptStringCompare::StrComp | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptStringCompare.StrComp
apilocation:
- scrobj.dll
helpviewer_keywords:
- StrComp method, IActiveScriptStringCompare interface
ms.assetid: 124d1281-8037-4766-a2a1-61244ac1f114
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 66cccb4281e19aebb25b3b4cde06705b500f53a3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991434"
---
# <a name="iactivescriptstringcomparestrcomp"></a>IActiveScriptStringCompare::StrComp
定义脚本引擎的字符串比较方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT StrComp(  
// The first string:  
    [in] BSTR bszStr1,    
// The second string:   
    [in] BSTR bszStr2,    
// The result of the comparison:  
    [out, retval] LONG* iRet   
);  
```  
  
#### <a name="parameters"></a>参数  
 `bszStr1`  
 第一个字符串。  
  
 `bszStr2`  
 第二个字符串。  
  
 `iRet`  
 比较的结果。 0`bszStr1`并`bszStr2`完全相同; 如果`bszStr1`  <  `bszStr2`; 1，如果`bszStr1`  >  `bszStr2`。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|自变量无效。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化）。|  
  
## <a name="remarks"></a>备注  
 此方法是执行字符串比较每次调用。  
  
## <a name="example"></a>示例  
 下面的示例演示如何重载的字符串比较函数。 当您使用重载允许[IActiveScriptProperty::SetProperty](../../winscript/reference/iactivescriptproperty-setproperty.md)设置 SCRIPTPROP_STRINGCOMPAREINSTANCE。  
  
```cpp#  
cpp_quote("// {58562769-ED52-42f7-8403-4963514E1F11}")  
cpp_quote("DEFINE_GUID(IID_IActiveScriptStringCompare, 0x58562769,   
    0xED52, 0x42f7, 0x84, 0x03, 0x49, 0x63, 0x51, 0x4E, 0x1F, 0x11);")  
cpp_quote("")  
  
cpp_quote("#define SCRIPTPROP_INTEGERMODE              0x00003000")  
cpp_quote("#define SCRIPTPROP_STRINGCOMPAREINSTANCE    0x00003001")  
cpp_quote("")  
interface IActiveScriptStringCompare;  
[  
         object,  
         uuid(58562769-ED52-42f7-8403-4963514E1F11),  
         pointer_default(unique)  
]  
interface IActiveScriptStringCompare : IUnknown  
{  
        // StrComp  
        //     bszStr1: first string  
        //     bszStr2: second string  
        //     iRet: 0 if identical, -1 if bszStr1 < bszStr2, 1 if   
        //         bszStr1 > bszStr2  
        //            
        //     Return values:  
        //         S_OK: Success  
        //         E_NOTIMPL: Not implemented  
        //  
        HRESULT StrComp(  
                [in] BSTR bszStr1,  
                [in] BSTR bszStr2,  
                [out, retval] LONG* iRet  
        );  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptStringCompare 接口](../../winscript/reference/iactivescriptstringcompare-interface.md)