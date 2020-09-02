---
title: Vspackage 中安全性的最佳做法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 940644cd3950c38c6383371c1844b54b328acd0c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697271"
---
# <a name="best-practices-for-security-in-vspackages"></a>VSPackage 中安全性的最佳做法
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 在计算机上安装，则必须在具有管理凭据的上下文中运行。 应用程序的安全和部署的基本单元 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 是 [vspackage](../../extensibility/internals/vspackages.md)。 必须使用注册 VSPackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，这也需要管理凭据。  
  
 管理员具有写入注册表和文件系统的完全权限，并可运行任何代码。 您必须具有这些权限才能开发、部署或安装 VSPackage。  
  
 一旦安装，就会完全信任 VSPackage。 由于与 VSPackage 关联的权限级别较高，因此可能会无意中安装具有恶意目的的 VSPackage。  
  
 用户应确保他们仅从受信任的源中安装 Vspackage。 开发 Vspackage 的公司应该对其进行强名称和签名，以确保阻止用户篡改。 开发 Vspackage 的公司应检查其外部依赖项（如 web 服务和远程安装），以评估和更正任何安全问题。  
  
 有关详细信息，请参阅) .NET Framework (安全编码指导原则 [https://msdn.microsoft.com/library/d55zzx87.aspx](https://msdn.microsoft.com/library/d55zzx87.aspx) 。  
  
## <a name="see-also"></a>另请参阅  
 [外接程序安全性](https://msdn.microsoft.com/library/44a5c651-6246-4310-b371-65378917c799)   
 [DDEX 安全性](https://msdn.microsoft.com/44a52a70-5c98-450e-993d-4a3b32f69ba8)
