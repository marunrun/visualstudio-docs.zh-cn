---
title: IDebugApplicationNode Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationNode interface
ms.assetid: 30be3a97-8191-45ac-8706-3f7056c163d6
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9be864fdb9468668633322066bbbcf11569e4eb3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822420"
---
# <a name="idebugapplicationnode-interface"></a>IDebugApplicationNode 接口
`IDebugApplicationNode`接口扩展的功能`IDebugDocumentProvider`通过提供项目树中的上下文的接口。  
  
 除了继承的方法之外`IDebugDocumentProvider`，则`IDebugApplicationNode`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugApplicationNode::EnumChildren](../../winscript/reference/idebugapplicationnode-enumchildren.md)|枚举此应用程序节点的子节点。|  
|[IDebugApplicationNode::GetParent](../../winscript/reference/idebugapplicationnode-getparent.md)|返回此应用程序节点的父节点。|  
|[IDebugApplicationNode::SetDocumentProvider](../../winscript/reference/idebugapplicationnode-setdocumentprovider.md)|设置此应用程序节点的文档提供程序。|  
|[IDebugApplicationNode::Close](../../winscript/reference/idebugapplicationnode-close.md)|使此应用程序释放所有引用并进入非活动状态。|  
|[IDebugApplicationNode::Attach](../../winscript/reference/idebugapplicationnode-attach.md)|将此应用程序节点添加到指定的项目树。|  
|[IDebugApplicationNode::Detach](../../winscript/reference/idebugapplicationnode-detach.md)|从项目树中删除此应用程序节点。|