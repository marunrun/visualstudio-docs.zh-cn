---
title: -LCID (devenv.exe)
description: 了解如何使用 LCID devenv 命令行开关设置 IDE 中文本、货币和其他值所使用的默认语言。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- language default
- locale IDs, setting for IDE
- Devenv, /L switch
- Devenv, /LCID switch
- locale IDs
- L Devenv switch
- /L Devenv switch
- LCID devenv switch
- /LCID Devenv switch
ms.assetid: 3a3f4e70-ea66-4351-9d62-acb1dec30e8e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eda3a4d9242655af1b018664273ceb693c7e775c
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96043980"
---
# <a name="lcid-devenvexe"></a>/LCID (devenv.exe)

设置用于 IDE 内文本、货币和其他值的默认语言。

## <a name="syntax"></a>语法

```shell
devenv {/LCID|/L} LocaleID
```

## <a name="arguments"></a>参数

- *LocaleID*

  必需。 指定的语言的区域设置标识符 (LCID)。

## <a name="remarks"></a>备注

加载 IDE 并设置环境的默认自然语言。 此更改跨会话暂留，IDE 在“工具” > “选项” > “环境” > “国际设置” > “语言”框中显示此更改。

如果指定的语言对系统不可用，`/LCID` 开关遭忽略。

下表列出了 Visual Studio 支持的语言的 LCID。

|语言|LCID|
|--------------|----------|
|中文(简体)|2052|
|中文(繁体)|1028|
|捷克语|1029|
|英语|2052|
|法语|1036|
|德语|1031|
|意大利语|1040|
|日语|1041|
|韩语|1042|
|波兰语|1045|
|葡萄牙语（巴西）|1046|
|俄语|1049|
|西班牙语|3082|
|土耳其语|1055

## <a name="example"></a>示例

此示例加载具有英语资源字符串的 IDE。

```shell
devenv /LCID 1033
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [“选项”对话框 -&gt;“环境”-&gt;“区域设置”](../../ide/reference/international-settings-environment-options-dialog-box.md)
- [自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)
