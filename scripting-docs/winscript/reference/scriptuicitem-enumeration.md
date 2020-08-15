---
title: SCRIPTUICITEM 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: fbf01f1b-5d7f-4d92-8d10-3da65e352d93
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 75827d9ef38fdc18f87c231fbe9a909ebaaa120a
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238759"
---
# <a name="scriptuicitem-enumeration"></a>SCRIPTUICITEM 枚举
表示 UI 项的类型。 在 [IActiveScriptSiteUIControl：： GetUIBehavior 方法](../../winscript/reference/iactivescriptsiteuicontrol-getuibehavior-method.md)中使用。  
  
## <a name="syntax"></a>语法  
  
```vb  
typedef enum tagSCRIPTUICITEM {     SCRIPTUICITEM_INPUTBOX = 1,     SCRIPTUICITEM_MSGBOX = 2,     } SCRIPTUICITEM;   
```  
  
## <a name="enumeration-values"></a>枚举值  
  
|“值”|UI 项类型|  
|-|-|  
|SCRIPTUICITEM_INPUTBOX|输入控件。|  
|SCRIPTUICITEM_MSGBOX|一个消息框。|