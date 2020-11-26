---
title: Vspackage 中安全性的最佳做法 |Microsoft Docs
description: 了解 VSPackage 中安全性的最佳实践，以及 Visual Studio 应用程序的基本安全和部署单元。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f81f682271a949954d113ffd2f6228db0de814e8
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96190039"
---
# <a name="best-practices-for-security-in-vspackages"></a>Vspackage 中安全性的最佳做法
若要 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 在计算机上安装，则必须在具有管理凭据的上下文中运行。 应用程序的安全和部署的基本单元 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 是 [VSPackage](../../extensibility/internals/vspackages.md)。 必须使用注册 VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，这也需要管理凭据。

 管理员具有写入注册表和文件系统的完全权限，并可运行任何代码。 您必须具有这些权限才能开发、部署或安装 VSPackage。

 一旦安装，就会完全信任 VSPackage。 由于与 VSPackage 关联的权限级别较高，因此可能会无意中安装具有恶意目的的 VSPackage。

 用户应确保他们仅从受信任的源中安装 Vspackage。 开发 Vspackage 的公司应该对其进行强名称和签名，以确保阻止用户篡改。 开发 Vspackage 的公司应检查其外部依赖项（如 web 服务和远程安装），以评估和更正任何安全问题。

 有关详细信息，请参阅 [.NET Framework 的安全编码指导原则](/previous-versions/visualstudio/visual-studio-2008/d55zzx87(v=vs.90))。

## <a name="see-also"></a>请参阅
- [外接程序安全性](/previous-versions/1326zbk3(v=vs.140))
- [DDEX 安全性](/previous-versions/bb163703(v=vs.140))