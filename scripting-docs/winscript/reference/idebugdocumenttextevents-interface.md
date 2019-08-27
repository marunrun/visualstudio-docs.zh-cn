---
title: IDebugDocumentTextEvents 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentTextEvents interface
ms.assetid: 341b20fd-994c-4030-a06b-6c66ad38c35d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7c83a6e3a41ed7087338989d5cb077fa070e724b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63434263"
---
# <a name="idebugdocumenttextevents-interface"></a>IDebugDocumentTextEvents 接口
提供指示关联文本文档的更改的事件。  
  
> [!NOTE]
> 文档文本更改事件对此接口的 fire 时。 事件处理程序可能检索新的文本使用`IDebugDocumentText`接口。  
  
 除了继承的方法之外`IUnknown`，则`IDebugDocumentTextEvents`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugDocumentTextEvents::onDestroy](../../winscript/reference/idebugdocumenttextevents-ondestroy.md)|指示基础文档已被破坏，将不再有效|  
|[IDebugDocumentTextEvents::onInsertText](../../winscript/reference/idebugdocumenttextevents-oninserttext.md)|指示新的文本已添加到文档|  
|[IDebugDocumentTextEvents::onRemoveText](../../winscript/reference/idebugdocumenttextevents-onremovetext.md)|指示已从文档中删除文本。|  
|[IDebugDocumentTextEvents::onReplaceText](../../winscript/reference/idebugdocumenttextevents-onreplacetext.md)|指示已替换文本。|  
|[IDebugDocumentTextEvents::onUpdateTextAttributes](../../winscript/reference/idebugdocumenttextevents-onupdatetextattributes.md)|指示与底层的字符位置范围关联的文本属性已更改。|  
|[IDebugDocumentTextEvents::onUpdateDocumentAttributes](../../winscript/reference/idebugdocumenttextevents-onupdatedocumentattributes.md)|指示记录属性更改。|