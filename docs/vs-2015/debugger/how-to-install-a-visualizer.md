---
title: 如何：安装可视化工具 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, visualizers
- visualizers, installing
ms.assetid: 3310ef43-515c-4d97-b0f9-51047247d3da
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5726cea8b2e81c53b5f3fff963357946f26b199f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840470"
---
# <a name="how-to-install-a-visualizer"></a>如何：安装可视化工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建了可视化工具后，您还必须安装该可视化工具，这样您才可在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中使用它。 安装可视化工具是个简单的过程。  
  
> [!NOTE]
> 在应用 **商店** 应用中，仅支持标准文本、HTML、XML 和 JSON 可视化工具。 不支持自定义（用户创建的）可视化工具。  
  
### <a name="to-install-a-visualizer"></a>安装可视化工具  
  
1. 查找包含已创建的可视化工具的 DLL。  
  
2. 将 DLL 复制到下列位置之一：  
  
    - VisualStudioInstallPath `\Common7\Packages\Debugger\Visualizers`  
  
    - `My Documents\` VisualStudioVersion `\Visualizers`  
  
3. 若要使用托管可视化工具进行远程调试，请将 DLL 复制到远程计算机上的同一路径。  
  
4. 重新启动调试会话。  
  
## <a name="see-also"></a>另请参阅  
 [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)   
 [如何：编写可视化工具](../debugger/how-to-write-a-visualizer.md)
