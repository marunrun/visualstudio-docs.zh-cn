---
title: 'Iprocessdebugmanager:: Createdebugdocumenthelper |Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IProcessDebugManager.CreateDebugDocumentHelper
apilocation:
- pdm.dll
helpviewer_keywords:
- IProcessDebugManager::CreateDebugDocumentHelper
ms.assetid: d644e192-1bcc-4768-a91e-239cd920adcd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 38de1e828ccd1715fb83cc76c06ba837818d2af0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63002358"
---
# <a name="iprocessdebugmanagercreatedebugdocumenthelper"></a>IProcessDebugManager::CreateDebugDocumentHelper
创建此应用程序的新调试文档帮助程序。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateDebugDocumentHelper(  
   IUnknown*               punkOuter,  
   IDebugDocumentHelper**  pddh  
);  
```  
  
#### <a name="parameters"></a>参数  
 `punkOuter`  
 [in]如果返回的对象将进行聚合`punkOuter`是控制的接口指针`IUnknown`。 否则，它是一个 null 指针。  
  
 `pddh`  
 [out]此应用程序的的调试文档帮助程序对象。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法创建此应用程序的新调试文档帮助程序。  
  
## <a name="see-also"></a>请参阅  
 [IProcessDebugManager 接口](../../winscript/reference/iprocessdebugmanager-interface.md)