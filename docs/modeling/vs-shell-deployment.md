---
title: VS Shell 部署
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99ef0124c06cd6f1a4d24e29b2c02cd0b50a37b0
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76115267"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署

使用独立 shell 可以确定需要与域特定语言交互的 Visual Studio 功能，以及该解决方案应如何显示。 有关 Visual Studio 独立 shell 的详细信息，请参阅[自定义独立 shell](https://vspartner.com/pages/vsshells)。

若要将 Visual Studio Shell 设置为部署目标：

1. 在**DslPackage**项目中，打开**source.extension.tt**。

2. 在 `<SupportedProducts>` 插入：

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   将*MyIsolatedShell*替换为你的独立 shell 包的名称。
