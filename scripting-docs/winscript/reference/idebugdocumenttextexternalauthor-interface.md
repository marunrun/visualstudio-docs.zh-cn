---
title: IDebugDocumentTextExternalAuthor 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentTextExternalAuthor interface
ms.assetid: 0b04de1b-f922-4526-af4e-c0af2b7c1ce4
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 60fb0d68d8052990fcc1783f86d0213b714dbfc9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62978479"
---
# <a name="idebugdocumenttextexternalauthor-interface"></a>IDebugDocumentTextExternalAuthor 接口
允许外部编辑器源文件发生更改时通知文档安全地编辑基于文件的调试器文档。  
  
 除了继承的方法之外`IUnknown`，则`IDebugDocumentTextExternalAuthor`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugDocumentTextExternalAuthor::GetPathName](../../winscript/reference/idebugdocumenttextexternalauthor-getpathname.md)|返回文档的完整路径和文件名称。|  
|[IDebugDocumentTextExternalAuthor::GetFileName](../../winscript/reference/idebugdocumenttextexternalauthor-getfilename.md)|返回不包含路径信息的文档的名称。|  
|[IDebugDocumentTextExternalAuthor::NotifyChanged](../../winscript/reference/idebugdocumenttextexternalauthor-notifychanged.md)|通知主机已更改的文档源。|