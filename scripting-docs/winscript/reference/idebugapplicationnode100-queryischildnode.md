---
title: IDebugApplicationNode100::QueryIsChildNode | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationNode100::QueryIsChildNode
ms.assetid: 4f36f435-0f34-4f9e-bba3-e75285fd7bbb
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 959de620e1e556d92a51dcab0062fa6ff055ec46
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446668"
---
# <a name="idebugapplicationnode100queryischildnode"></a>IDebugApplicationNode100::QueryIsChildNode
确定此节点的子节点之一是否属于指定的文档。  
  
> [!IMPORTANT]
> [IDebugApplicationNode100 接口](../../winscript/reference/idebugapplicationnode100-interface.md)是实现由 PDM 10.0 版及更高版本。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT QueryIsChildNode(        [in] IDebugDocument* pSearchKey        );  
```  
  
#### <a name="parameters"></a>参数  
 `pSearchKey`  
 搜索键中。  
  
## <a name="see-also"></a>请参阅  
 [IDebugApplicationNode100 接口](../../winscript/reference/idebugapplicationnode100-interface.md)