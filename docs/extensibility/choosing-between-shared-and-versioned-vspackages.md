---
title: 共享和版本控制的 Vspackage 之间进行选择 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SxS
- side-by-side installation
- installation [Visual Studio SDK], side-by-side
ms.assetid: e3128ac3-2e92-48e9-87ab-3b6c9d80e8c9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: de7bb2ee0335322e0b089fd2af81026b1f6bd1ca
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66747791"
---
# <a name="choose-between-shared-and-versioned-vspackages"></a>共享和版本控制的 Vspackage 之间进行选择
不同版本的 Visual Studio 可以在同一台计算机上共存。 Vspackage 可以支持的任意组合[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]版本。

 您可以通过两种策略、 共享的策略或版本控制策略的 Vspackage 的并行安装。 同时容纳的多个版本存在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]和相关联的.NET Framework 版本。

 在共享的策略中，一个 VSPackage 注册为使用在多个版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 在版本控制的策略中，安装多个 VSPackage Dll，一个用于每个版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]你支持的。

## <a name="shared-vspackages"></a>共享的 Vspackage
 中的多个版本使用相同的 VSPackage 时，才适合使用共享的 VSPackage [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 若要实现共享的 VSPackage，必须执行以下步骤：

- 使你的 VSPackage 的多个版本与兼容[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 所以，这样做的两种方法都可用于：

  - 限制你与使用仅最早版本的功能的 VSPackage[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]你支持的。

  - 程序 VSPackage 以适应的版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]正在其中运行。 然后，如果较新的服务的查询失败，你的 VSPackage 可以提供的较旧版本中支持的其他服务[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

- 适当地注册你的 VSPackage。 有关详细信息，请参阅[VSPackage 注册](../extensibility/internals/vspackage-registration.md)并[托管 VSPackage 注册](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)。

- 适当地注册文件扩展名。 有关详细信息，请参阅[注册的并行部署的文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 创建部署你的 VSPackage 的相应版本的安装程序[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 有关详细信息，请参阅[使用 Windows Installer 安装 Vspackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)并[组件管理](../extensibility/internals/component-management.md)。

- 解决注册冲突的问题。 有关详细信息，请参阅[VSPackage 注册](../extensibility/internals/vspackage-registration.md)。

- 确保文件共享并设置其版本采用引用计数来允许安全的安装和删除多个版本。 有关详细信息，请参阅[组件管理](../extensibility/internals/component-management.md)。

## <a name="versioned-vspackages"></a>版本控制的 Vspackage
 在版本控制的 VSPackage 策略下创建的每个版本的一个 VSPackage[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]你支持的。 如果您希望充分利用提供的更高版本的服务执行此操作很适合[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，因为每个 VSPackage 可以演化而不影响其他。 不过，从单个代码库或从多个独立的代码库，创建多个二进制文件的版本控制策略，可能需要更多的初始开发比共享策略。 此外，额外的工作可能因为您必须创建单独的安装程序为每个版本，或者单个安装程序检测到的版本所需[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]安装以及在你的 VSPackage 支持的。

## <a name="binary-compatibility"></a>二进制文件兼容性
 通常情况下，二进制文件兼容性使开发与早期版本的 Visual Studio 在更高版本的 Visual Studio 中运行的本机代码 Vspackage。 但是，有三个重要的例外情况：

- 如果你的 VSPackage 依赖于特定版本的公共语言运行时，则它必须确定哪一个版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]正在运行。

- VSPackage 可能依赖于另一个 VSPackage 或另一个产品的特定功能。 因此，VSPackage 可以仅在满足依赖项，在运行。

- 安全修补程序中，VSPackage 可能会影响[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]service pack 或更高版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 在这些情况下，与早期版本的开发 VSPackage[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]的版本中可能会不运行[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]应用安全修补程序后。 但是，可以重新生成包与更高版本，并将其在早期版本中还运行。

  必须使用版本的生成托管的 Vspackage[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]并[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]匹配的目标版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

  除了规划你的 VSPackage 的二进制文件的二进制文件兼容性，您还应考虑解决方案和项目文件格式。 如果你的 VSPackage 创建一个新的项目类型，则必须确定它是否可以运行一个版本中或在多个版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 有关详细信息，请参阅[升级自定义项目](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)。

## <a name="see-also"></a>请参阅
- [使用 Windows Installer 安装 Vspackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)
- [组件管理](../extensibility/internals/component-management.md)