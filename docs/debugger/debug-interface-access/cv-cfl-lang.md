---
title: CV_CFL_LANG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CV_CFL_LANG enumeration
ms.assetid: 4e8e0613-ad02-4de9-9f46-e4753c5b0251
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0fb684d0ff68e5ede6b0847ef9aeba1821ecafcc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745339"
---
# <a name="cv_cfl_lang"></a>CV_CFL_LANG
指定应用程序或链接模块的源代码语言。

## <a name="syntax"></a>语法

```C++
typedef enum CV_CFL_LANG {
    CV_CFL_C       = 0x00,
    CV_CFL_CXX     = 0x01,
    CV_CFL_FORTRAN = 0x02,
    CV_CFL_MASM    = 0x03,
    CV_CFL_PASCAL  = 0x04,
    CV_CFL_BASIC   = 0x05,
    CV_CFL_COBOL   = 0x06,
    CV_CFL_LINK    = 0x07,
    CV_CFL_CVTRES  = 0x08,
    CV_CFL_CVTPGD  = 0x09,
    CV_CFL_CSHARP  = 0x0A,
    CV_CFL_VB      = 0x0B,
    CV_CFL_ILASM   = 0x0C,
    CV_CFL_JAVA    = 0x0D,
    CV_CFL_JSCRIPT = 0x0E,
    CV_CFL_MSIL    = 0x0F,
    CV_CFL_HLSL    = 0x10
} CV_CFL_LANG;
```

## <a name="elements"></a>元素
CV_CFL_C 应用程序语言为 C。

CV_CFL_CXX 应用程序语言C++是。

CV_CFL_FORTRAN 应用程序语言是 FORTRAN。

CV_CFL_MASM 应用程序语言是 Microsoft 宏汇编程序。

CV_CFL_PASCAL 应用程序语言为 Pascal。

CV_CFL_BASIC 应用程序语言 BASIC。

CV_CFL_COBOL 应用程序语言为 COBOL。

CV_CFL_LINK 应用程序是链接器生成的模块。

CV_CFL_CVTRES 应用程序是使用 CVTRES 工具转换的资源模块。

CV_CFL_CVTPGD 应用程序是使用 CVTPGD 工具生成的 POGO 优化模块。

CV_CFL_CSHARP 应用程序语言C#是。

Visual Basic CV_CFL_VB 应用程序语言。

CV_CFL_ILASM 应用程序语言是中间语言程序集（即公共语言运行时（CLR）程序集）。

CV_CFL_JAVA 应用程序语言是 Java。

CV_CFL_JSCRIPT 应用程序语言为 Jscript。

CV_CFL_MSIL 应用程序语言是未知的 Microsoft 中间语言（MSIL），可能是因为使用了[/ltcg （链接时间代码生成）](/cpp/build/reference/ltcg-link-time-code-generation)开关。

CV_CFL_HLSL 应用程序语言是高级着色器语言。

## <a name="remarks"></a>备注
此枚举中的值由对[IDiaSymbol：： get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)方法的调用返回。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)
