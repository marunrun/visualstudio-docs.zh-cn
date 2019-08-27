---
title: 注册 Vspackage |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157392"
---
# <a name="registering-vspackages"></a>注册 VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 依赖于要描述和定位 VSPackage 的.pkgdef 文件。 .Pkgdef 文件包含否则会添加到系统注册表的所有注册信息。 通过将属性添加到源代码，然后运行注册托管的 Vspackage [CreatePkgDef 实用工具](../../extensibility/internals/createpkgdef-utility.md)上生成的程序集生成.pkgdef 文件。  
  
## <a name="in-this-section"></a>本节内容  
 [指定 VS Shell 的 VSPackage 文件位置](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)  
 介绍 Vspackage 的加载路径。  
  
 [注册和注销 Vspackage](../../extensibility/registering-and-unregistering-vspackages.md)  
 介绍如何注册 VSPackage。  
  
 [使用自定义注册特性注册扩展](../../misc/using-a-custom-registration-attribute-to-register-an-extension.md)  
 介绍如何创建可用于部署托管的 VSPackage 注册清单。
