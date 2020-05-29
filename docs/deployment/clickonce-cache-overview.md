---
title: ClickOnce 缓存概述 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployemtn
- ClickOnce applications, cache
- ClickOnce deployment, cache
ms.assetid: e379921e-9ef1-4326-bbf3-53ba67925526
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3d7abeeec4a640119e3089c795ac529a10f8dc09
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84182620"
---
# <a name="clickonce-cache-overview"></a>ClickOnce 缓存概述
所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序（无论是本地安装还是联机承载）都存储在客户端计算机上的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序*缓存*中。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]缓存是当前用户的 "文档和设置" 文件夹的 "本地设置" 目录下的隐藏目录系列。 此缓存保存应用程序的所有文件，包括程序集、配置文件、应用程序和用户设置以及数据目录。 缓存还负责将应用程序的数据目录迁移到最新版本。 有关数据迁移的详细信息，请参阅[在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)。

 通过为应用程序存储提供单个位置，可接管 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 管理应用程序的物理安装的任务。 缓存还可通过保留所有应用程序的程序集和数据文件以及它们彼此之间的不同版本来帮助隔离应用程序。 例如，在升级 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，会在缓存中为该版本及其数据资源提供其自己的目录。

## <a name="cache-storage-quota"></a>缓存存储配额
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]通过限制缓存大小的配额，在联机托管的应用程序可以占用的空间量限制 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 缓存大小适用于所有用户的联机应用程序;一个部分受信任的联机应用程序仅占用一半的配额空间。 已安装的应用程序不受缓存大小限制，并且不会根据缓存限制进行计数。 对于所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，缓存仅保留当前版本和以前安装的版本。

 默认情况下，客户端计算机为联机应用程序提供了 250 MB 的存储空间 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 数据文件不计入此限制。 系统管理员可以通过更改注册表项（ **HKEY_CURRENT_USER \software\classes\software\microsoft\windows\currentversion\deployment\onlineappquotainkb**，这是一个表示缓存大小（以 kb 为单位）的 DWORD 值，在特定客户端计算机上放大或缩小此配额。 例如，为了减小缓存大小为 50 MB，请将此值更改为51200。

## <a name="see-also"></a>请参阅
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)