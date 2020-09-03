---
title: 部署项目类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0fda84d5f7467a65b254d3b12b0466b6ab415d61
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196884"
---
# <a name="deploying-project-types"></a>部署项目类型
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 安装新的项目类型聚合器 ( # A0) 和 Windows Installer 包以便再分发 ( # A1) 。 必须为托管代码项目类型使用新的聚合器。 项目聚合器中的 ProjectAggregator2 方法限制 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 可防止托管代码项目类型正常运行。 以下步骤介绍如何将 VSPackage 更改为使用新的聚合器。  
  
1. 从解决方案中删除 NativeHierarchyWrapper 项目。  
  
2. 从安装程序中删除任何 NativeHierarchyWrapper 二进制文件。  
  
3. 将 ProjectAggregator2.msi 添加到设置。
