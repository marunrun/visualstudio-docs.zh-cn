---
title: VS Shell 部署
description: 了解如何使用独立 shell 来确定需要与 DSL 交互的 Visual Studio 功能以及应如何显示该解决方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 94cffbf5ea1f7ac3c437a4c22f27f881d5493e79
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/12/2020
ms.locfileid: "97361256"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署

使用独立 shell 可以确定需要与域特定语言交互的 Visual Studio 功能，以及该解决方案应如何显示。 有关 Visual Studio 独立 shell 的详细信息，请参阅 [自定义独立 shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)。

若要将 Visual Studio Shell 设置为部署目标：

1. 在 **DslPackage** 项目中，打开 **source.extension.tt**。

2. 在 `<SupportedProducts>` insert：

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   将 *MyIsolatedShell* 替换为你的独立 shell 包的名称。