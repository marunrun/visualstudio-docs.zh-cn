---
title: SccCheckin 功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701187"
---
# <a name="scccheckin-function"></a>SccCheckin 功能
此函数将以前签出的文件签入到源代码管理系统，存储更改并创建新版本。 此函数使用要签入的文件的计数和名称数组进行调用。

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

[在]源代码管理插件上下文结构。

 hwnd

[在]SCC 插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 n文件

[在]选择要签入的文件数。

 lpFile名称

[在]要签入的文件完全限定的本地路径名称的数组。

 lpComment

[在]要应用于要签入的每个选定文件的注释。 此参数是`NULL`源控件插件应提示发表评论。

 fOptions

[在]命令标志，0 或`SCC_KEEP_CHECKEDOUT`。

 pvOptions

[在]SCC 插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功签入文件。|
|SCC_E_FILENOTCONTROLLED|所选文件不受源代码控制。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特异性故障。 文件未签入。|
|SCC_E_NOTCHECKEDOUT|用户尚未签出该文件，因此无法签入该文件。|
|SCC_E_CHECKINCONFLICT|无法执行签入，因为：<br /><br /> - 其他用户已提前签入，并且`bAutoReconcile`为 false。<br /><br /> \- 或 -<br /><br /> - 无法执行自动合并（例如，当文件为二进制文件时）。|
|SCC_E_VERIFYMERGE|文件已自动合并，但尚未签入等待用户验证。|
|SCC_E_FIXMERGE|文件已自动合并，但由于合并冲突必须手动解决，因此尚未签入。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTEXIST|未找到本地文件。|

## <a name="remarks"></a>备注
 注释应用于正在签入的所有文件。 注释参数可以是字符串`null`，在这种情况下，源代码管理插件可以提示用户为每个文件输入注释字符串。

 可以为`fOptions`参数提供`SCC_KEEP_CHECKEDOUT`标志的值，以指示用户打算签入并再次签出该文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
