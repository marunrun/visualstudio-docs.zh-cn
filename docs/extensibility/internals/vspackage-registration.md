---
title: VSPackage 注册 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: ecd20da8-b04b-4141-a8f4-a2ef91dd597a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44114ccdc4a0873887d48c3d191506f10cc3eaf3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721999"
---
# <a name="vspackage-registration"></a>VSPackage 注册
Vspackage 必须建议 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 它们已安装并应加载。 此过程是通过在注册表中写入信息来完成的。 这是安装程序的典型作业。

> [!NOTE]
> 在 VSPackage 开发过程中，它是一种接受使用自注册的已接受的做法。 但是，在安装过程中，[!INCLUDE[vsipprvsip](../../extensibility/includes/vsipprvsip_md.md)] 合作伙伴不能使用自行注册交付其产品。

 Windows Installer 包中的注册表项通常在注册表表中进行。 你还可以在注册表表中注册文件扩展名。 不过，Windows Installer 通过编程标识符（ProgId）、类、扩展和谓词表来提供内置支持。 有关详细信息，请参阅[数据库表](/windows/desktop/Msi/database-tables)。

 请确保注册表项与适用于所选并行策略的组件相关联。 例如，共享文件的注册表项应与该文件的 Windows Installer 组件相关联。 同样，特定于版本的文件的注册表项应与该文件的组件相关联。 否则，安装或卸载一个 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 版本的 VSPackage 可能会破坏其他版本中的 VSPackage。 有关详细信息，请参阅[支持多个版本的 Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)。

> [!NOTE]
> 若要管理注册，最简单的方法是将相同的数据用于开发人员注册和安装时注册。 例如，某些安装程序开发工具可以在生成时使用 .reg 格式的文件。 如果开发人员为自己的日常开发和调试维护 .reg 文件，则可以在安装程序中自动包含这些相同的文件。 如果无法自动共享注册数据，则必须确保安装程序的注册数据副本是最新的。

## <a name="registering-unmanaged-vspackages"></a>注册非托管 Vspackage
 非托管 Vspackage （包括 Visual Studio 包模板生成的）使用 ATL 样式的 .rgs 文件存储注册信息。 .Rgs 文件格式专用于 ATL，并且通常不能通过安装创作工具按原样使用。 必须单独维护 VSPackage 安装程序的注册信息。 例如，开发人员可以将 .reg 格式的文件与 .rgs 文件更改保持同步。 .Reg 文件可以与 RegEdit 合并，以供开发工作或安装程序使用。

## <a name="registering-managed-vspackages"></a>注册托管的 Vspackage
 RegPkg 工具从托管的 VSPackage 读取注册属性，并可以将该信息直接写入注册表或编写可由安装程序使用的 .reg 格式文件。

> [!NOTE]
> RegPkg 工具不可再发行，无法用于在用户系统上注册 VSPackage。

## <a name="why-vspackages-should-not-self-register-at-install-time"></a>为什么 Vspackage 不应在安装时自行注册
 VSPackage 安装程序不应依赖于自行注册。 乍一看，仅将 VSPackage 的注册表值保留在 VSPackage 中，这似乎是一个不错的想法。 假设开发人员需要可用于其日常工作和测试的注册表值，则可避免在安装程序中维护注册表数据的单独副本。 安装程序可以依赖于 VSPackage 本身来写入注册表值。

 尽管理论上如此良好，但自注册有几个瑕疵使其不适用于 VSPackage 安装：

- 正确支持安装、卸载、安装回滚和卸载回滚要求你为通过调用 RegPkg 的每个托管 VSPackage 创作四个自定义操作。

- 并行支持方法可能要求你创作四个自定义操作，这些操作可为 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的每个受支持版本调用 RegSvr32 或 RegPkg。

- 由于无法通知自注册的密钥是否由另一个功能或应用程序使用，因此无法安全地回滚使用自注册模块的安装。

- 自注册 Dll 有时链接到不存在或版本不正确的辅助 Dll。 与此相反，Windows Installer 可以使用注册表表注册 Dll，而不依赖于系统的当前状态。

- 如果某个组件同时指定为 "从源运行" 并在 SelfReg 表中列出，则可以拒绝自注册代码访问网络资源（例如类型库）。 这可能会导致在管理安装过程中组件安装失败。

## <a name="see-also"></a>请参阅
- [Windows 安装程序](/windows/desktop/Msi/windows-installer-portal)
- [托管包注册](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)