---
title: ToggleHUD | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7261e01d-3c72-46ce-9fb3-5f33b2ddb901
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cb05bb6a424b5639e0ee98e96c80315c51081ace
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62848478"
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