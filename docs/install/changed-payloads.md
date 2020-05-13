---
title: 当在发布版本后发生包有效负载更改时
description: 当创建布局时，了解如何确定是否在发布版本后发生了包有效负载更改。
ms.date: 05/22/2019
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: dec1478314e752ddace8fae822747e7c8e328b70
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "76114589"
---
# <a name="package-payload-changes"></a>包有效负载更改

允许某些包有效负载在发布版本后更改。 当你或其他人创建布局时，此行为可能会导致不同的布局内容，具体取决于创建布局的时间。

## <a name="verify-that-a-layout-includes-package-payload-changes"></a>验证布局是否包括包有效负载更改

下面介绍了如何确定先前创建的布局是否已获取在发布版本后修改的包有效负载：

1. 打开安装日志。 日志通常位于 `%TEMP%\dd_setup_[date].log` 中，其中 `[date]` 是采用 `yyyyMMddHHmmss` 格式启动布局操作的时间。

2. 在日志中查找其结构类似于以下文本的行：

    `Falling back to signature and signer check because hash verification returned HashMismatch for path: [path]`

3. 然后，在日志的后面部分中查找指示 [path] 的下载已成功的行。 它们可能类似于以下文本：

    `Download of [url] succeeded using engine 'WebClient'`

    `END: Downloading [url] to [path]`

## <a name="see-also"></a>另请参阅

* [创建 Visual Studio 的网络安装](create-a-network-installation-of-visual-studio.md)
* [更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)
