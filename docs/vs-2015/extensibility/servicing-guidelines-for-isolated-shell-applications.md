---
title: 服务的准则独立 Shell 应用程序 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159269"
---
# <a name="servicing-guidelines-for-isolated-shell-applications"></a>独立 Shell 应用程序的服务指南
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当您发布了 Visual Studio 独立 shell 应用程序时，您必须能够为应用程序提供的软件更新安装之后。 若要执行此操作，必须通过使用 Microsoft Installer (MSI) 文件安装应用程序。 此类安装允许由 Microsoft 进行重新分配通过 Web 提供的软件更新下载并使用你的客户无需自定义交互的。  
  
## <a name="servicing-requirements"></a>服务要求  
 您可以确保你的独立的 shell 安装可以通过确保您的安装程序满足以下三个条件允许更新。  
  
### <a name="redistribute-by-using-an-msi"></a>使用 MSI 重新分发  
 您必须使用 MSI 重新分发应用程序，因为 MSI 产品标识将保留并可确保应用程序具有客户端计算机上的物理位置。 合并模块 （.msm 文件） 不提供此类保证，不应使用。  
  
### <a name="accounting-for-custom-actions"></a>考虑自定义操作  
 自定义操作是在安装程序中的使用了非标准安装指令。 自定义操作更改参数，如文件位置、 注册表设置、 用户设置或安装的其他项。 自定义操作可能会在安装时处理数据。  
  
 在安装程序中使用自定义操作时，必须确保每个安装时自定义操作必须具有相应的自定义操作，以便当用户卸载应用程序时，撤消操作。 如果安装程序无法正常工作以提供相应卸载自定义操作，删除你的应用程序将其部分安装。  
  
- 软件更新更改这些版本或哈希值时，依赖于特定版本的文件或哈希值的自定义操作将失败。 在这种情况下你的自定义操作必须手动更新这些值。 如果文件或哈希值的版本的产品版本间共享，会发生另一个问题。 避免此依赖关系，只要有可能。  
  
### <a name="accounting-for-shared-files"></a>考虑共享文件  
 共享的文件具有相同的名称，并且可以由多个产品安装到同一位置。 这些产品版本、 库存单位 (SKU)，或两者中, 可能不同，产品可同时存在给定计算机上。 但是，共享的文件创建维护服务问题的原因：  
  
- 更新共享的文件可能导致应用程序兼容性问题，因为对一个应用程序的更新可能会更改使用的第二个应用程序尚未更新的文件的版本。 安装程序的共享文件的产品计数对共享文件的引用。 因此，卸载产品不会影响共享的文件超出递减的已安装的实例计数。  
  
- 快速修复工程 (QFE) 安装程序将恢复到的 QFE 安装程序提供服务的产品版本的文件的版本。 此过程可能会中断的应用程序必须提供更新的共享的文件。
