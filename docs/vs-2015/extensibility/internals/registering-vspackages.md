---
title: 正在注册 Vspackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, registering
- registration, managed VSPackages
ms.assetid: 79b9424e-7e9b-4fc8-9b9f-00212674573c
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 053157b0ce1cb4250d8c666725431515c75b5fa2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157392"
---
# <a name="registering-vspackages"></a>注册 VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 依赖 .pkgdef 文件来描述和查找 VSPackage。 .Pkgdef 文件包含其他将被添加到系统注册表中的注册信息。 托管 Vspackage 通过向源代码添加特性，然后在生成的程序集上运行 [CreatePkgDef 实用工具](../../extensibility/internals/createpkgdef-utility.md) 来注册 .pkgdef 文件。  
  
## <a name="in-this-section"></a>本节内容  
 [指定 VS Shell 的 VSPackage 文件位置](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)  
 描述 Vspackage 的加载路径。  
  
 [注册和注销 VSPackage](../../extensibility/registering-and-unregistering-vspackages.md)  
 说明如何注册 VSPackage。  
  
 [使用自定义注册特性注册扩展](../../misc/using-a-custom-registration-attribute-to-register-an-extension.md)  
 介绍如何创建可用于部署托管 VSPackage 的注册清单。
