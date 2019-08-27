---
title: IRemoteDebugApplication110::SetDebuggerOptions | Microsoft Docs
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
ms.openlocfilehash: a61eabb307bda39fd871e8f5f4f7198256f0929e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383360"
---
# <a name="iremotedebugapplication110setdebuggeroptions"></a>IRemoteDebugApplication110::SetDebuggerOptions
调用以更新调试器选项。 应调用此方法后[IRemoteDebugApplication::ConnectDebugger](../../winscript/reference/iremotedebugapplication-connectdebugger.md)。 [IRemoteDebugApplication::DisconnectDebugger](../../winscript/reference/iremotedebugapplication-disconnectdebugger.md)方法自动重置为默认选项。 为 0 (SDO_NONE) 选项默认值。  
  
> [!IMPORTANT]
> [IRemoteDebugApplication 接口](../../winscript/reference/iremotedebugapplication-interface.md)是实现由 PDM v11.0 和更高版本。 在 activdbg100.h 中发现。  
  
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