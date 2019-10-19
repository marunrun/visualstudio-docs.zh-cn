---
title: VS Shell 部署 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: be8f2ffe-a322-4ac0-9c9e-873bd28e5d5e
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a42ec6a762655589bfd589ae9dc0354e3a7d1cb5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659307"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用独立 shell 可以确定需要与域特定语言交互的 Visual Studio 功能，以及该解决方案应如何显示。 有关 Visual Studio 独立 shell 的详细信息，请参阅[自定义独立 shell](../extensibility/customizing-the-isolated-shell.md)。 可在[自定义独立 shell](https://msdn.microsoft.com/d75463cd-1155-42e4-8b7a-046ed6becbbf)中找到有关如何自定义独立 shell 的详细信息。

### <a name="to-set-a-visual-studio-shell-as-the-deployment-target"></a>将 Visual Studio Shell 设置为部署目标

1. 在**DslPackage**项目中，打开**source.extension.tt**。

2. 在 `<SupportedProducts>` 插入：

    ```
    <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
    ```

     将*MyIsolatedShell*替换为你的独立 shell 包的名称。
