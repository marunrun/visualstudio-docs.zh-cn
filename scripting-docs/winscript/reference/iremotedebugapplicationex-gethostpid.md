---
title: IRemoteDebugApplicationEx:GetHostPid | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplicationEx:GetHostPid
apilocation:
- scrobj.dll
helpviewer_keywords:
- IRemoteDebugApplicationEx:GetHostPid
ms.assetid: 4cf9f46c-29cf-4201-87f0-5b1ddbed2f2b
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d660cce006e7f84f1b1c01f1ec0a406b5c4b9df3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62934590"
---
# <a name="iremotedebugapplicationexgethostpid"></a>IRemoteDebugApplicationEx:GetHostPid

返回主机应用程序的进程 ID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetHostPid(
   DWORD*  dwHostPid
);
```

### <a name="parameters"></a>参数

`dwHostPid`

[out]主机进程标识符。

## <a name="return-value"></a>返回值

该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。

|“值”|描述|
|-----------|-----------------|
|`S_OK`|方法成功。|

## <a name="remarks"></a>备注

由 IDE。

## <a name="see-also"></a>请参阅

- [IRemoteDebugApplicationEx 接口](iremotedebugapplicationex-interface.md)