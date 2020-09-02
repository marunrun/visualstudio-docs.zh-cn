---
title: 独立 Shell 应用程序的维护准则 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Shell integrated mode, serviceability
- Shell integrated mode [Visual Studio], serviceability
ms.assetid: 747d1a47-b8b3-4e8b-93c0-768724be48f2
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 093690c293ff6857eedc50d5eccc793d7d5bb114
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68159269"
---
# <a name="servicing-guidelines-for-isolated-shell-applications"></a>独立 Shell 应用程序的服务指南
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

分发 Visual Studio 独立 shell 应用程序时，必须能够在安装应用程序后为其提供软件更新。 为此，必须使用 Microsoft Installer (MSI) 文件安装应用程序。 此类安装允许由 Microsoft 提供的软件更新通过 Web 下载进行重新发布，并在无需自定义干预的情况下由客户使用。  
  
## <a name="servicing-requirements"></a>服务要求  
 您可以确保您的安装程序可以通过确保您的安装程序满足以下三个条件来允许更新。  
  
### <a name="redistribute-by-using-an-msi"></a>使用 MSI 重新发布  
 必须使用 MSI 来重新发布应用程序，因为 MSI 会保留产品标识，并确保应用程序在客户端计算机上具有物理位置。 合并模块 ( msm 文件) 不提供此类保证，因此不应使用。  
  
### <a name="accounting-for-custom-actions"></a>自定义操作的会计  
 自定义操作是安装程序中的非标准安装指令。 自定义操作更改文件位置、注册表设置、用户设置或其他安装项等参数。 自定义操作可能在安装时处理数据。  
  
 如果在安装程序中使用自定义操作，则必须确保每个安装时自定义操作都必须有相应的自定义操作，以便在用户卸载应用程序时撤消该操作。 如果安装程序无法提供相应的卸载自定义操作，则删除应用程序将使其部分安装。  
  
- 当软件更新更改这些版本或哈希值时，依赖于特定版本的文件或哈希值的自定义操作将失败。 在这种情况下，您的自定义操作必须手动更新这些值。 如果在产品版本之间共享文件版本或哈希值，则会出现其他问题。 请尽可能避免此依赖项。  
  
### <a name="accounting-for-shared-files"></a>共享文件的记帐  
 共享文件具有相同的名称，并且安装在多个产品所在的同一位置。 这些产品可能不同于版本、库存单位 (SKU) 或二者不同，并且产品可在给定计算机上共存。 但是，共享文件出于以下几个原因导致了服务问题：  
  
- 更新共享文件可能会导致应用程序兼容性问题，因为一个应用程序的更新可能会更改另一个尚未更新的应用程序所使用的文件的版本。 共享文件的产品的安装程序计数对共享文件的引用。 因此，卸载产品不会影响共享文件，而不会减少已安装实例的计数。  
  
- 快速修补工程 (QFE) 安装程序将文件版本恢复为 QFE 安装程序所服务的产品版本。 此过程可能会中断已传递更新共享文件的应用程序。
