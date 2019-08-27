---
title: NameSearchOptions |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- NameSearchOptions enumeration
ms.assetid: 67dfbede-2678-47df-b664-5c49841d0b9b
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6d721ebc5849fc459d24173ad0500b4b1c12260f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182968"
---
# <a name="namesearchoptions"></a>NameSearchOptions
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定符号和文件名称的搜索选项。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum NameSearchOptions {   
   nsNone,  
   nsfCaseSensitive     = 0x1,  
   nsfCaseInsensitive   = 0x2,  
   nsfFNameExt          = 0x4,  
   nsfRegularExpression = 0x8,  
   nsfUndecoratedName   = 0x10,  
  
// For backward compatibility:  
   nsCaseSensitive           = nsfCaseSensitive,  
   nsCaseInsensitive         = nsfCaseInsensitive,  
   nsFNameExt                = nsfCaseInsensitive | nsfFNameExt,  
   nsRegularExpression       = nsfRegularExpression | nsfCaseSensitive,  
   nsCaseInRegularExpression = nsfRegularExpression | nsfCaseInsensitive  
};  
```  
  
## <a name="elements"></a>元素  
 `nsNone`  
 未指定任何选项。  
  
 `nsfCaseSensitive`  
 将应用与匹配的区分大小写的名称。  
  
 `nsfCaseInsensitive`  
 将应用与匹配的不区分大小写的名称。  
  
 `nsfFNameExt`  
 将视为路径的名称，并将应用与匹配的文件名.ext 名称。  
  
 `nsfRegularExpression`  
 应用使用星号 （*） 和问号 （？） 作为通配符的区分大小写的名称匹配。  
  
 `nsfUndecoratedName`  
 仅适用于具有未修饰和修饰名的符号。  
  
## <a name="remarks"></a>备注  
 此枚举的值将传递到以下方法：  
  
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)  
  
- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)  
  
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)  
  
## <a name="requirements"></a>要求  
 标头： dia2.h  
  
## <a name="see-also"></a>请参阅  
 [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)   
 [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)   
 [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
