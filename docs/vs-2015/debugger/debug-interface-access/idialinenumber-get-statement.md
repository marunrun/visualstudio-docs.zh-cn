---
title: IDiaLineNumber：： get_statement |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_statement method
ms.assetid: 22b8ee29-79ef-427f-bd05-00d255ab836b
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b5ad480a3b5d3ed892fc56fec2c882638f986810
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68165685"
---
# <a name="idialinenumberget_statement"></a>IDiaLineNumber::get_statement
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个标志，该标志指示此行信息描述了程序源中语句的开头，而不是表达式。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_statement (   
   BOOL* pRetVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pRetVal`  
 弄 `TRUE` 如果此行信息描述了程序源中语句的开头，则返回。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 语句可以跨多行。 此方法指示关联的行号是否标记此类多行语句的开头。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
