---
title: -SafeMode (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /SafeMode Devenv switch
- Devenv, /SafeMode switch
- SafeMode switch
ms.assetid: b191f6a5-8f12-47ec-bcc7-b68149a22aa8
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: abaeded184db78085a9629da0e763b2f76dbd328
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655513"
---
# <a name="safemode-devenvexe"></a>/SafeMode (devenv.exe)

在安全模式下启动 Visual Studio，同时仅加载默认环境和服务。

## <a name="syntax"></a>语法

```shell
devenv /SafeMode
```

## <a name="remarks"></a>备注

Visual Studio 启动时，此开关阻止所有第三方 VSPackages 加载，以确保执行稳定。

## <a name="example"></a>示例

下面的示例在安全模式下启动 Visual Studio。

```shell
devenv /safemode
```

## <a name="see-also"></a>请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)