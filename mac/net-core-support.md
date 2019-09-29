---
title: .NET Core 支持
description: 本文档介绍了 Visual Studio for Mac 中的 .NET Core 版本支持
author: sayedihashimi
ms.author: sayedha
ms.date: 08/20/2019
ms.assetid: 8B8CEBE8-00DA-4AD1-8193-77F58B57F244
ms.openlocfilehash: 98451c728b15344b116f275ca6a40fd902f33f0f
ms.sourcegitcommit: 88f576ac32af31613c1a10c1548275e1ce029f4f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71186796"
---
# <a name="net-core-support"></a>.NET Core 支持

下表说明了 Visual Studio for Mac 稳定版和预览版支持的 .NET Core 版本：

| .NET Core SDK 版本 |Visual Studio for Mac 8.1（稳定版） | Visual Studio for Mac 8.2（稳定版） | Visual Studio for Mac 8.3（稳定版） |
|---------|---------|---------|---------|
|v2.1.0 - v2.1.5xx | | | |
|v2.1.600 + |✔︎|✔︎|✔︎|
|v2.2.1 - v2.2.1xx | | | |
|v2.2.200 + |✔︎|✔︎|✔︎|
|v3.0 | | |✔︎|

> [!IMPORTANT]
> 不支持 .NET Core SDK 的预览版，请更新到已发布版本。 安装 Visual Studio for Mac 8.3 时，将安装 .NET Core v3.0 的已发布版本。

> [!IMPORTANT]
> 如果之前将 .NET Core v2.2.1xx 与 Visual Studio for Mac 8.0 配合使用，则需要手动更新到上表所列的受支持的 .NET Core 版本。 建议使用 [2.1.700](https://dotnet.microsoft.com/download/dotnet-core/2.1) 或 [2.2.300](https://dotnet.microsoft.com/download/dotnet-core/2.2) 版本

* 默认情况下，将为 8.3 安装 .NET Core v3.0。
* 默认为使用安装程序安装 .NET Core v2.1.701（对于 8.1，则默认安装 v2.1.700）。
* 若要访问任何其他 .NET Core 版本，请访问 [dotnet 页面](https://dotnet.microsoft.com/download/dotnet-core)。
* 使用 .NET Core 3.0 时，默认情况下将使用 C# 版本 8。 使用 .NET Core 2.x 时，默认情况下使用 C# 7.3。 请参阅 [C# 语言版本控制](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version)了解更多信息。
* 有关如何安装 Visual Studio for Mac 预览版的信息，请参阅[安装预览版](https://docs.microsoft.com/visualstudio/mac/install-preview)指南。
