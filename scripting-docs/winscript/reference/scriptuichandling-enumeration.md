---
title: SCRIPTUICHANDLING 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 5b89c6e8-064c-406f-bb14-91c77bf42daf
caps.latest.revision: 2
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f0c6505449e6b54bdbc02998e78770c7cde54976
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238252"
---
# <a name="scriptuichandling-enumeration"></a>SCRIPTUICHANDLING 枚举
表示应对 UI 控件进行处理的方式。  
  
## <a name="syntax"></a>语法  
  
```vb  
typedef enum tagSCRIPTUICHANDLING {     SCRIPTUICHANDLING_ALLOW = 0,     SCRIPTUICHANDLING_NOUIERROR = 1,     SCRIPTUICHANDLING_NOUIDEFAULT = 2, } SCRIPTUICHANDLING;   
```  
  
## <a name="enumeration-value"></a>枚举值  
  
|“值”|UIC 处理方法|  
|-|-|  
|SCRIPTUICHANDLING_ALLOW|允许显示控件。|  
|SCRIPTUICHANDLING_NOUIERROR||  
|SCRIPTUICHANDLING_NOUIDEFAULT||