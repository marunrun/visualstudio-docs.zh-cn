---
title: Vspackage 中安全性的最佳做法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio SDK]
- security best practices, VSPackages
- best practices, security
ms.assetid: 212a0504-cf6c-4e50-96b0-f2c1c575c0ff
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 144bc62176ebc552e7070b29088acf70329a84d4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309160"
---
# <a name="best-practices-for-security-in-vspackages"></a>在 Vspackage 中安全性的最佳做法
若要安装[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]计算机时，你必须在运行具有管理凭据的上下文。 安全和部署的基本单位[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]应用程序是[VSPackage](../../extensibility/internals/vspackages.md)。 必须使用注册 VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，这也要求管理凭据。

 管理员拥有完全权限写入注册表和文件系统中，并运行任何代码。 必须具有这些权限以开发、 部署或安装 VSPackage。

 一旦安装，VSPackage 是完全受信任。 由于此高级别的权限与 VSPackage 相关联，很可能会无意中安装具有恶意企图的 VSPackage。

 用户应确保它们仅从受信任来源安装 Vspackage。 公司开发 VSPackages 应强命名，并加上签名，以确保用户该篡改阻止。 公司开发 VSPackages 应检查其外部依赖项，如 web 服务和远程安装，以评估并更正任何安全问题。

 有关详细信息，请参阅[安全编码准则适用于.NET Framework](/previous-versions/visualstudio/visual-studio-2008/d55zzx87(v=vs.90))。

## <a name="see-also"></a>请参阅
- [外接程序安全性](https://msdn.microsoft.com/Library/44a5c651-6246-4310-b371-65378917c799)
- [DDEX 安全](https://msdn.microsoft.com/library/44a52a70-5c98-450e-993d-4a3b32f69ba8)