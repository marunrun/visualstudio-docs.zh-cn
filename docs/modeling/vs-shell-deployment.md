---
title: VS Shell 部署
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f3729c09198b331728e2cc67299ffc3ad6c3d26
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809643"
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