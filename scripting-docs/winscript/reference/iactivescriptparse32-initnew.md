---
title: IActiveScriptParse32::InitNew | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c77aa16-f391-4c93-9f1a-4e529a9930b2
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 685c596caa61a5cbd5042fad3a1bfb39c349c1b1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009419"
---
# <a name="iactivescriptparse32initnew"></a>IActiveScriptParse32::InitNew
初始化脚本引擎。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT InitNew(void);  
```  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，或`E_FAIL`如果初始化期间出错。  
  
## <a name="remarks"></a>备注  
 可以使用脚本引擎之前，必须调用以下方法之一： `IPersist*::Load`， `IPersist*::InitNew`，或`IActiveScriptParse32::InitNew`。 此方法的语义是相同`IPersistStreamInit::InitNew`，因为此方法指示脚本引擎初始化其自身。 请注意，不能用来同时调用`IPersist*::InitNew`或`IActiveScriptParse32::InitNew`并`IPersist*::Load`，也不是有效调用`IPersist*::InitNew`， `IActiveScriptParse32::InitNew`，或`IPersist*::Load`不止一次。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptParse32](../../winscript/reference/iactivescriptparse32.md)