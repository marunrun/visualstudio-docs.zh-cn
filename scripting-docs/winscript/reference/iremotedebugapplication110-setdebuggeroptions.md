---
title: IRemoteDebugApplication110：： SetDebuggerOptions |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRemoteDebugApplication110::SetDebuggerOptions
ms.assetid: 58e9fd18-3e0d-47fa-8893-f316146bde84
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e7168a4ef8ec70368c0ff691ba1f721275f9d65d
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577427"
---
# <a name="iremotedebugapplication110setdebuggeroptions"></a>IRemoteDebugApplication110::SetDebuggerOptions
调用以更新调试器选项。 应在[IRemoteDebugApplication：： ConnectDebugger](../../winscript/reference/iremotedebugapplication-connectdebugger.md)后调用此方法。 [IRemoteDebugApplication：:D isconnectdebugger](../../winscript/reference/iremotedebugapplication-disconnectdebugger.md)方法自动重置为默认选项。 选项默认为0（SDO_NONE）。  
  
> [!IMPORTANT]
> [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)由 PDM 11.0 和更高版本实现。 在 activdbg100.h 中发现。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT SetDebuggerOptions(        [in] enum SCRIPT_DEBUGGER_OPTIONS mask,        [in] enum SCRIPT_DEBUGGER_OPTIONS value    );  
```  
  
#### <a name="parameters"></a>参数  
 `mask`  
 [SCRIPT_DEBUGGER_OPTIONS 枚举](../../winscript/reference/script-debugger-options-enumeration.md)掩码。  
  
 `value`  
 [SCRIPT_DEBUGGER_OPTIONS 枚举](../../winscript/reference/script-debugger-options-enumeration.md)值。  
  
## <a name="see-also"></a>请参阅  
 [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)   
 [IRemoteDebugApplication110 接口](../../winscript/reference/iremotedebugapplication110-interface.md)