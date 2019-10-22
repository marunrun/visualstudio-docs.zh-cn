---
title: -Log (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /Log switch
- Log switch [devenv.exe]
- /Log Devenv switch
ms.assetid: ae23c4ae-2376-4fe3-b8d2-81d34e61c8ba
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f427edfe294605b7b2adcbb0889e48c4f37b6ba9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666843"
---
# <a name="log-devenvexe"></a>/Log (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

将所有活动记录到日志文件以用于疑难解答。 此文件在你至少调用一次 `devenv /log` 后显示。 默认情况下，日志文件为：

 %APPDATA%\Microsoft\VisualStudio\\Version\ActivityLog.xml  

 其中，“版本”是 Visual Studio 的版本  。 但是，可以指定一个不同的路径和文件名。

## <a name="syntax"></a>语法

```
Devenv /log Path\NameOfLogFile
```

## <a name="remarks"></a>备注
 此开关必须显示在命令行的结尾，位于所有其他开关之后。

 对于你使用 /log 开关调用的所有 Visual Studio 实例，都会记录日志。 对于不使用此开关调用的 Visual Studio 实例，将不记录日志。

## <a name="see-also"></a>另请参阅
 [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
