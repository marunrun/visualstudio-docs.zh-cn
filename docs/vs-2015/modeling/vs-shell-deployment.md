---
title: VS Shell 部署 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: be8f2ffe-a322-4ac0-9c9e-873bd28e5d5e
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5bfe88d7e7d742eb67273d307c3a8e72e9a85833
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704038"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

独立的 shell，可以确定哪些 Visual Studio 需要与域特定语言以及如何显示该解决方案应进行交互的功能。 有关 Visual Studio 独立 shell 的详细信息，请参阅[自定义独立 Shell](../extensibility/customizing-the-isolated-shell.md)。 你可以找到有关如何自定义中的独立的 shell 的详细信息[自定义独立 Shell](https://msdn.microsoft.com/d75463cd-1155-42e4-8b7a-046ed6becbbf)。  
  
### <a name="to-set-a-visual-studio-shell-as-the-deployment-target"></a>若要将 Visual Studio Shell 设置为部署目标  
  
1. 在中**DslPackage**项目中，打开**source.extension.tt**。  
  
2. 下`<SupportedProducts>`插入：  
  
    ```  
    <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>  
    ```  
  
     替换*MyIsolatedShell*与独立的 shell 包的名称。
