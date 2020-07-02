---
title: IActiveScriptParse32：： InitNew |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 7c77aa16-f391-4c93-9f1a-4e529a9930b2
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 887e4ce44662cc591fee64f5e0549edcdcbc14af
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835701"
---
# <a name="iactivescriptparse32initnew"></a>IActiveScriptParse32::InitNew
初始化脚本引擎。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT InitNew(void);  
```  
  
## <a name="return-value"></a>返回值  
 `S_OK`如果成功，则返回; `E_FAIL` 如果在初始化过程中出现错误，则返回。  
  
## <a name="remarks"></a>备注  
 在可以使用脚本引擎之前，必须先调用以下方法之一： `IPersist*::Load` 、 `IPersist*::InitNew` 或 `IActiveScriptParse32::InitNew` 。 此方法的语义与相同，这是因为 `IPersistStreamInit::InitNew` 此方法会告诉脚本引擎自行初始化。 请注意，调用、和都无效，也不能调用 `IPersist*::InitNew` `IActiveScriptParse32::InitNew` `IPersist*::Load` `IPersist*::InitNew` 、或多次 `IActiveScriptParse32::InitNew` `IPersist*::Load` 。  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)