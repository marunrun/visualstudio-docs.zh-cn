---
title: -Log (devenv.exe)
ms.date: 12/12/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /Log switch
- Log switch [devenv.exe]
- /Log Devenv switch
ms.assetid: ae23c4ae-2376-4fe3-b8d2-81d34e61c8ba
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 008e7ca15595db249c05485f0d9e8f8b1277993e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75595457"
---
# <a name="log-devenvexe"></a>/Log (devenv.exe)

将所有活动记录到日志文件以用于疑难解答。 此文件在你至少调用一次 `devenv /log` 后显示。 默认情况下，日志文件位于以下路径：

%APPDATA%\\Microsoft\\VisualStudio\\\<Version\>\\ActivityLog.xml

其中，“版本”是 Visual Studio 的版本\<\>。 但是，可以指定一个不同的路径和文件名。

## <a name="syntax"></a>语法

```shell
devenv /Log NameOfLogFile
```

## <a name="arguments"></a>参数

- NameOfLogFile 

  必需。 要保存到的日志文件的完整路径和文件名。

## <a name="remarks"></a>备注

此开关必须显示在命令行的结尾，位于所有其他开关之后。

日志仅针对已使用 `/Log` 开关打开的所有 Visual Studio 实例进行记录。

## <a name="example"></a>示例

下面的示例将日志记录到用户主目录中的 `MyVSLog.xml` 文件。

```shell
devenv /log "%USERPROFILE%\MyVSLog.xml"
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
