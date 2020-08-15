---
title: SCRIPTLANGUAGEVERSION 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 58aa904a-e3ed-41c6-82d6-e91c8279a792
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 511bc3525480306e0fe3075231c1e55794f01e9e
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238681"
---
# <a name="scriptlanguageversion-enumeration"></a>SCRIPTLANGUAGEVERSION 枚举
指定可能的脚本版本。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef enum tagSCRIPTLANGUAGEVERSION{    SCRIPTLANGUAGEVERSION_DEFAULT = 0,    SCRIPTLANGUAGEVERSION_5_7  = 1,    SCRIPTLANGUAGEVERSION_5_8  = 2,    SCRIPTLANGUAGEVERSION_MAX  = 255} SCRIPTLANGUAGEVERSION ;  
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|“值”|脚本版本|  
|-|-|  
|SCRIPTLANGUAGEVERSION_DEFAULT|默认版本。 整数值为0。|  
|SCRIPTLANGUAGEVERSION_5_7|Windows 脚本版本5.7。 整数值为1。|  
|SCRIPTLANGUAGEVERSION_5_8|Windows 脚本版本5.8。 整数值为2。|  
|SCRIPTLANGUAGEVERSION_MAX|最高版本。 整数值为255。|  
  
## <a name="see-also"></a>另请参阅  
 [活动脚本常量、枚举和错误代码](../../winscript/reference/active-script-constants-enumerations-and-error-codes.md)