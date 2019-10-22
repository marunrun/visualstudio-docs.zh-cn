---
title: IActiveScriptParse：： InitNew |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptParse.InitNew
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptParse_InitNew
ms.assetid: 3a582bd6-fc0d-43a5-812f-5ea55a8517a1
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b4817e103d7408124f35eb7dbaa16e955dd18f17
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573513"
---
# <a name="iactivescriptparseinitnew"></a>IActiveScriptParse::InitNew
初始化脚本引擎。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT InitNew(void);  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`; 如果在初始化过程中出现错误，则返回 `E_FAIL`。  
  
## <a name="remarks"></a>备注  
 在可以使用脚本引擎之前，必须先调用以下方法之一： `IPersist*::Load`、`IPersist*::InitNew` 或 `IActiveScriptParse::InitNew`。 此方法的语义与 `IPersistStreamInit::InitNew` 相同，这是因为此方法会告诉脚本引擎自行初始化。 请注意，既不能调用 `IPersist*::InitNew` 或 `IActiveScriptParse::InitNew` `IPersist*::Load`，也不能将 `IPersist*::InitNew`、`IActiveScriptParse::InitNew` 或 `IPersist*::Load` 多次调用。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParse](../../winscript/reference/iactivescriptparse.md)