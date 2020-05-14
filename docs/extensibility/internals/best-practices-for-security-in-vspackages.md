---
title: VS 包中安全最佳实践 |微软文档
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
ms.openlocfilehash: d4309feeed3233d2149586afb1bf4efafacb21ec
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709905"
---
# <a name="best-practices-for-security-in-vspackages"></a>VS 包中的安全最佳实践
要在计算机上[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]安装 ， 必须在具有管理凭据的上下文中运行。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]应用程序的安全和部署的基本单位是[VSPackage。](../../extensibility/internals/vspackages.md) VSPackage 必须使用 注册[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，这也需要管理凭据。

 管理员具有写入注册表和文件系统以及运行任何代码的完整权限。 您必须具有这些权限才能开发、部署或安装 VS 包。

 一旦安装，VSPackage 即完全受信任。 由于与 VSPackage 关联的这种高级别权限，因此可能会无意中安装具有恶意的 VSPackage。

 用户应确保仅从受信任的源安装 VS 包。 开发 VSPackages 的公司应牢固地命名并签署它们，以确保用户防止篡改。 开发 VSPackages 的公司应检查其外部依赖项（如 Web 服务和远程安装），以评估和纠正任何安全问题。

 有关详细信息，请参阅[.NET 框架的安全编码准则](/previous-versions/visualstudio/visual-studio-2008/d55zzx87(v=vs.90))。

## <a name="see-also"></a>请参阅
- [外接程序安全性](https://msdn.microsoft.com/Library/44a5c651-6246-4310-b371-65378917c799)
- [DDEX 安全性](https://msdn.microsoft.com/library/44a52a70-5c98-450e-993d-4a3b32f69ba8)
