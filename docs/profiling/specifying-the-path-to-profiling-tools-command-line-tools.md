---
title: 指定分析工具命令行工具的路径 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7047bf18-5779-4f6e-872c-66e2fc47c969
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 087407f511c038a369694beca8a9fe4ecc2ff7b7
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74771566"
---
# <a name="specify-the-path-to-profiling-tools-command-line-tools"></a>指定分析工具命令行工具的路径

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具命令行工具的路径不添加到 PATH 环境变量中。 在 32 位计算机上，这些工具位于单个目录中。 64 位计算机上有这些分析工具的 32 位和 64 位版本。

## <a name="32-bit-computers"></a>32 位计算机

::: moniker range="vs-2017"
 对于本机代码，Visual Studio 探查器 API 位于 VSPerf.dll 中  。 头文件 VSPerf.h 和导入库 VSPerf.lib 位于 Microsoft Visual Studio \2017\Team Tools\Performance Tools\PerfSDK 目录中    。
::: moniker-end

 对于托管代码，探查器 API 位于 Microsoft.VisualStudio.Profiler.dll 中  。 此 DLL 位于 Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools 目录  。

## <a name="64-bit-computers"></a>64 位计算机

在 64 位计算机上，根据被分析应用程序的目标平台指定路径。

::: moniker range="vs-2017"
- 对于 32 位应用程序，默认的探查器工具目录为：

     （本机）Microsoft Visual Studio\2017\Team Tools\Performance Tools\PerfSDK（托管）Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools  

- 对于 64 位应用程序，默认的探查器工具目录为：

     （本机）Microsoft Visual Studio\2017\Team Tools\Performance Tools\x64\PerfSDK（托管）Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools\64  
::: moniker-end
