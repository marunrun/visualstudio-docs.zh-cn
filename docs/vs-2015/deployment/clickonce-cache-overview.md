---
title: ClickOnce 缓存概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
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
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 58ea758ea10e2c58ff123a2bc991f14191db0aa1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68151655"
---
# <a name="clickonce-cache-overview"></a>ClickOnce 缓存概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

所有[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序，无论它们是安装在本地还是托管，存储在客户端计算机上[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序*缓存*。 一个[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]缓存是一系列的当前用户的 Documents and Settings 文件夹的本地设置目录下隐藏的目录。 此缓存保留在应用程序的所有文件，包括程序集、 配置文件、 应用程序和用户设置和数据目录。 缓存程序还负责将应用程序的数据目录迁移到最新版本。 有关数据迁移的详细信息，请参阅[访问本地数据和 ClickOnce 应用程序中的远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)。  
  
 通过提供应用程序存储的单个位置[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]接管用户管理物理安装应用程序的任务。 缓存还可帮助隔离应用程序通过保留的程序集和所有应用程序的数据文件，并从另一个单独的及其不同版本。 例如，当升级[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序中，使用自己的目录缓存中提供版本和其数据资源。  
  
## <a name="cache-storage-quota"></a>缓存存储配额  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 在线托管的应用程序被限制可占用的空间量的大小可限制的配额[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]缓存。 缓存大小适用于所有用户的联机应用程序;单个部分受信任的在线应用程序被限制为占用一半的配额的空间。 已安装应用程序不受缓存大小并不会抵消缓存限制。 所有[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]缓存的应用程序保留仅最新版本和以前安装的版本。  
  
 默认情况下，客户端计算机具有 250 MB 的存储联机[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。 数据文件不计入此限制。 系统管理员可以放大或缩小特定客户端计算机上的此配额通过更改注册表项，HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment\OnlineAppQuotaInKB，这是一个 DWORD 值表示的缓存大小以千字节为单位。 例如，为了减少到 50 MB 的缓存大小，将为 51200 更改此值。  
  
## <a name="see-also"></a>请参阅  
 [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)
