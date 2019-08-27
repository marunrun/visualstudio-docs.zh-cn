---
title: IRemoteDebugApplicationEx:ForceStepMode | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IRemoteDebugApplicationEx:ForceStepMode
apilocation:
- scrobj.dll
helpviewer_keywords:
- IRemoteDebugApplicationEx:ForceStepMode
ms.assetid: 83e69a3e-e4c9-4ddd-b01b-1820e4177a03
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 04a2c700d2cac4bcdc845ebf442de29863e87deb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62934640"
---
# <a name="iremotedebugapplicationexforcestepmode"></a>IRemoteDebugApplicationEx:ForceStepMode

强制调试器单步执行模式。

## <a name="syntax"></a>语法

```cpp
HRESULT ForceStepMode(
   IRemoteDebugApplicationThread*  pStepThread
);
```

### <a name="parameters"></a>参数

`pStepThread`

[in]进程调试监视器单步的线程。 如果为 null，PDM 清除其单步执行线程。

## <a name="return-value"></a>返回值

该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。

|“值”|描述|
|-----------|-----------------|
|`S_OK`|方法成功。|

## <a name="see-also"></a>请参阅

- [IRemoteDebugApplicationEx 接口](iremotedebugapplicationex-interface.md)