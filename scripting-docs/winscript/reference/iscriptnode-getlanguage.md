---
title: IScriptNode::GetLanguage |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.GetLanguage
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::GetLanguage
ms.assetid: 089715fd-6746-474e-94ed-2e57ee4bc0da
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 36b7076bf7f261e462802174c6f9014403606ac8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786953"
---
# <a name="iscriptnodegetlanguage"></a>IScriptNode::GetLanguage
返回由当前的脚本节点的脚本语言。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetLanguage(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstr`  
 [out]如果脚本节点使用 JScript 中或"VBScript"如果脚本节点使用 Visual Basic Scripting Edition (VBScript)，则返回"JScript"。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)