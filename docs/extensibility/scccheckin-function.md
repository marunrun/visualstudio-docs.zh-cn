---
title: SccCheckin 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCheckin
helpviewer_keywords:
- SccCheckin function
ms.assetid: e3f26ac2-6163-42e1-a764-22cfea5a3bc6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 22264f9882192e05a9812cad4d6ea7f74bfdabfc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333944"
---
# <a name="scccheckin-function"></a>SccCheckin 函数
此函数之前签出文件签入源代码管理系统，存储所做的更改和创建的新版本。 此函数调用计数、 签入的文件的名称的数组。

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

[in]源控制插件上下文结构。

 hWnd

[in]为它提供了任何对话框，父级可以使用插件 SCC，则 IDE 窗口的句柄。

 nFiles

[in]选择要签入的文件的数量。

 lpFileNames

[in]要签入的文件的完全限定的本地路径名称的数组。

 lpComment

[in]要应用于每个所选文件签入注释。 此参数是`NULL`如果源代码管理插件应提示输入注释。

 fOptions

[in]命令标志，为 0 或`SCC_KEEP_CHECKEDOUT`。

 pvOptions

[in]源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功签入文件。|
|SCC_E_FILENOTCONTROLLED|所选的文件不是源代码管理下。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障。 未签入文件。|
|SCC_E_NOTCHECKEDOUT|用户不具有签出该文件，因此不能将其签入。|
|SCC_E_CHECKINCONFLICT|无法执行签入，因为：<br /><br /> -其他用户签入提前和`bAutoReconcile`是 false。<br /><br /> 或<br /><br /> -自动合并不能执行的操作 （例如，文件是二进制文件）。|
|SCC_E_VERIFYMERGE|文件已自动合并，但未签等待用户验证。|
|SCC_E_FIXMERGE|文件已自动合并，但未签由于必须手动解决合并冲突。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_I_OPERATIONCANCELED|操作完成前被取消。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTEXIST|找不到本地文件。|

## <a name="remarks"></a>备注
 注释应用于所有未签入文件。 注释参数可以是`null`源代码管理插件可以在这种情况下提示用户输入的每个文件的注释字符串的字符串。

 `fOptions`参数可以指定一个值的`SCC_KEEP_CHECKEDOUT`标志，用于指示用户的意图，以便签入该文件并再次签出。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)