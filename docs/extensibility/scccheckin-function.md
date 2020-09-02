---
title: SccCheckin 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCheckin
helpviewer_keywords:
- SccCheckin function
ms.assetid: e3f26ac2-6163-42e1-a764-22cfea5a3bc6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5ba512642e1a63d9d39856f96194d717583d44f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701187"
---
# <a name="scccheckin-function"></a>SccCheckin 函数
此函数将以前签出的文件签入到源代码管理系统，存储更改并创建新版本。 调用此函数时使用的是要签入的文件的计数和名称数组。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccCheckin (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPSTR*    lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，SCC 插件可将其用作它所提供的所有对话框的父级。

 n

中选定要签入的文件数。

 lpFileNames

中要签入的文件的完全限定的本地路径名称数组。

 lpComment

中要应用于所选每个选定文件的注释。 `NULL`如果源代码管理插件应该提示输入注释，则此参数为。

 用于

中命令标志，0或 `SCC_KEEP_CHECKEDOUT` 。

 pvOptions

中SCC 插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功签入文件。|
|SCC_E_FILENOTCONTROLLED|所选文件不在源代码管理下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障。 文件未签入。|
|SCC_E_NOTCHECKEDOUT|用户未签出文件，因此无法将其签出。|
|SCC_E_CHECKINCONFLICT|无法执行签入，因为：<br /><br /> -另一个用户已事先签入， `bAutoReconcile` 却为 false。<br /><br /> - 或 -<br /><br /> -不能完成自动合并 (例如，当文件是二进制) 。|
|SCC_E_VERIFYMERGE|文件已自动合并，但尚未签入挂起的用户验证。|
|SCC_E_FIXMERGE|由于必须手动解决的合并冲突，文件已自动合并但尚未签入。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_I_OPERATIONCANCELED|操作在完成前被取消。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTEXIST|找不到本地文件。|

## <a name="remarks"></a>备注
 注释适用于所有要签入的文件。 Comment 参数可以是一个 `null` 字符串，在这种情况下，源代码管理插件可以提示用户提供每个文件的注释字符串。

 `fOptions`可以为参数指定标志的值， `SCC_KEEP_CHECKEDOUT` 以指示用户在中检查文件并再次签出文件的意图。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
