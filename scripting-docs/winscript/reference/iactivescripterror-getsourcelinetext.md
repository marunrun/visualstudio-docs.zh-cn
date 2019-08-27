---
title: IActiveScriptError::GetSourceLineText | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptError.GetSourceLineText
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptError_GetSourceLineText
ms.assetid: 64f7f37f-7288-4dbe-b626-a35d90897f36
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 702f1655b244116e1bb7dca3d5fc90de3d1f5bdf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955001"
---
# <a name="iactivescripterrorgetsourcelinetext"></a>IActiveScriptError::GetSourceLineText
检索错误发生脚本引擎运行脚本时的源代码文件中的行。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetSourceLineText(  
    BSTR *pbstrSourceLine  // address of buffer for source line  
);  
```  
  
## <a name="parameter"></a>参数  
 `pbstrSourceLine`  
 [out]接收发生了错误的源代码的行的缓冲区的地址。  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，或`E_FAIL`如果检索不到源文件中的行。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptError](../../winscript/reference/iactivescripterror.md)