---
title: IDebugFormatter 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugFormatter interface
ms.assetid: 022142d4-c8e1-47ae-b771-3e24953293e5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f35d1b811a017895ca40f3325bd0ac456070184f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979222"
---
# <a name="idebugformatter-interface"></a>IDebugFormatter 接口
允许语言或 IDE 自定义 VARIANT 值或 VARTYPE 类型与字符串之间的转换。  
  
 除了继承的方法之外`IUnknown`，则`IDebugFormatter`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IDebugFormatter::GetStringForVariant](../../winscript/reference/idebugformatter-getstringforvariant.md)|返回一个字符串，表示给定的变体值。|  
|[IDebugFormatter::GetVariantForString](../../winscript/reference/idebugformatter-getvariantforstring.md)|返回包含给定的字符串的变量。|  
|[IDebugFormatter::GetStringForVarType](../../winscript/reference/idebugformatter-getstringforvartype.md)|返回一个字符串，表示给定的 VARTYPE 值。|