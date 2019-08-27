---
title: IActiveScriptErrorDebug110 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptErrorDebug110 Interface
ms.assetid: 5c1a4993-4cad-4ccf-89c2-53abfddfe1f2
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 72f545f5a48fc7b8aa3f9250b13a62ba659e94bc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436055"
---
# <a name="iactivescripterrordebug110-interface"></a>IActiveScriptErrorDebug110 接口
将功能添加到[IActiveScriptDebug 接口](../../winscript/reference/iactivescriptdebug-interface.md)。 此接口由 JavaScript 引擎实现，用于确定为什么会发生 BREAKREASON_ERROR 事件。  
  
> [!IMPORTANT]
> 此接口由 PDM v11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="methods"></a>方法  
 `IActiveScriptErrorDebug110` 接口公开以下方法。  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptErrorDebug110::GetExceptionThrownKind](../../winscript/reference/iactivescripterrordebug110-getexceptionthrownkind.md)|返回某一引发的异常的异常类型。|