---
title: IDebugDocumentHost：： NotifyChanged |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHost.NotifyChanged
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugDocumentHost::NotifyChanged
ms.assetid: 33a4a54f-3bcb-4422-b3c0-bdbf46590f34
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a4fc0c744887eb3592c4d94c520f33da86812bfc
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72569181"
---
# <a name="idebugdocumenthostnotifychanged"></a>IDebugDocumentHost::NotifyChanged
通知宿主已保存文档的源文件，并且应刷新其内容。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT NotifyChanged();  
```  
  
#### <a name="parameters"></a>参数  
 此方法不采用任何参数。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法通知宿主已保存文档的源文件，并且应刷新其内容。  
  
## <a name="see-also"></a>请参阅  
 [IDebugDocumentHost 接口](../../winscript/reference/idebugdocumenthost-interface.md)