---
title: IDiaSession::findInlineeLinesByLinenum | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
ms.assetid: cf32ae7c-a0c8-4800-bc8f-d64fdd15fb06
caps.latest.revision: 6
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d16bc6f3e2e8f190e3a26023407237509984cece
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840526"
---
# <a name="idiasessionfindinlineelinesbylinenum"></a>IDiaSession::findInlineeLinesByLinenum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索一个枚举，该枚举允许客户端循环访问指定源文件和行号内直接或间接内联的所有函数的行号信息。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT findInlineeLinesByVA (   
   IDiaSymbol*           compiland,  
   IDiaSourceFile*       file,  
   DWORD                 linenum,  
   DWORD                 column,  
   IDiaEnumLineNumbers** ppResult  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `compiland`  
 中表示要在其中搜索行号的编译单位的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。 此参数不能为 `NULL`。  
  
 `file`  
 中一个 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) 对象，该对象表示要在其中进行搜索的源文件。 此参数不能为 `NULL`。  
  
 `linenum`  
 中指定一个从1开始的行号。  
  
> [!NOTE]
> 不能使用零来指定所有行 (使用 [IDiaSession：： findLines](../../debugger/debug-interface-access/idiasession-findlines.md) 方法查找所有行) 。  
  
 `column`  
 中指定列号。 使用零来指定所有列。 列是行中的字节偏移量。  
  
 `ppResult`  
 弄返回一个 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) 对象，该对象包含检索到的行号的列表。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)   
 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
