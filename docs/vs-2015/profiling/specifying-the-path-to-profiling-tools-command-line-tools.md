---
title: 指定分析工具命令行工具的路径 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7047bf18-5779-4f6e-872c-66e2fc47c969
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7fadcff84c4b927a7718d7d4ad1311918ae0f18a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199778"
---
# <a name="specifying-the-path-to-profiling-tools-command-line-tools"></a>指定分析工具命令行工具的路径
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具命令行工具的路径不添加到 PATH 环境变量中。 在 32 位计算机上，这些工具位于单个目录中。 64 位计算机上有这些分析工具的 32 位和 64 位版本。  
  
## <a name="32-bit-computers"></a>32 位计算机  
 在 32 位计算机上，默认的探查器工具目录为 *驱动器*\Program Files\Microsoft Visual Studio 11.0\Team Tools\Performance Tools。  
  
## <a name="64-bit-computers"></a>64 位计算机  
 在 64 位计算机上，根据被分析应用程序的目标平台指定路径。  
  
- 对于 32 位应用程序，默认的探查器工具目录为：  
  
     *驱动器*\Program Files (x86)\Microsoft Visual Studio 11.0\Team Tools\Performance Tools  
  
- 对于 64 位应用程序，默认的探查器工具目录为：  
  
     *驱动器*\Program Files (x86)\Microsoft Visual Studio 11.0\Team Tools\Performance Tools\x64
