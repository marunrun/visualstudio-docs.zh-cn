---
title: IRemoteDebugApplicationEx:RevokeBreak | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplicationEx:RevokeBreak
apilocation:
- scrobj.dll
helpviewer_keywords:
- IRemoteDebugApplicationEx:RevokeBreak
ms.assetid: 1f077860-0a39-4ec9-b676-ae0712819c7b
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0992eb5637434ccdf0dbf4fa6e436c87ae3fdd6c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788399"
---
# <a name="iremotedebugapplicationexrevokebreak"></a>IRemoteDebugApplicationEx:RevokeBreak

撤消换行命令。

## <a name="syntax"></a>语法

```cpp
HRESULT RevokeBreak( );
```

### <a name="parameters"></a>参数

无。

## <a name="return-value"></a>返回值

该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。

|“值”|描述|
|-----------|-----------------|
|`S_OK`|方法成功。|

## <a name="see-also"></a>请参阅

- [IRemoteDebugApplicationEx 接口](iremotedebugapplicationex-interface.md)