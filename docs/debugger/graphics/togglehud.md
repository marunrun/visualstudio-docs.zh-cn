---
title: ToggleHUD | Microsoft Docs
description: 使用 VsgDbg 的 ToggleHUD() 方法来切换在应用运行时是否显示图形诊断平视显示 (HUD)。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7261e01d-3c72-46ce-9fb3-5f33b2ddb901
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 60bee5a89be0fc1503595a36cfc48a692711d40a
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996066"
---
# <a name="togglehud"></a>ToggleHUD
打开或关闭图形诊断的 HUD（平视显示）覆盖。

## <a name="syntax"></a>语法

```C++
void ToggleHUD();
```

## <a name="remarks"></a>备注
 图像诊断 HUD 显示在正在图形诊断下运行的应用的左上角。 它显示有关此应用和图形信息捕获的运行时信息，以及通过调用 [AddMessage](addmessage.md) 成员函数添加的消息。

 若要切换 HUD，不必主动捕获图形信息 - 也就是说，它可通过 `VsgDbg` 类的实例开关，但首先不必调用 [Init](init.md) 成员函数。