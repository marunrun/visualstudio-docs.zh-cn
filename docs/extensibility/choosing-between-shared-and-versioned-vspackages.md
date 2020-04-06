---
title: 在共享和版本化的 VS 包之间进行选择 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SxS
- side-by-side installation
- installation [Visual Studio SDK], side-by-side
ms.assetid: e3128ac3-2e92-48e9-87ab-3b6c9d80e8c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 21fefb776fceeeef4db6997a5bd12a8b987af7d2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739884"
---
# <a name="choose-between-shared-and-versioned-vspackages"></a>在共享和版本化 VS 包之间进行选择
不同版本的 Visual Studio 可以共存于同一台计算机上。 VS包可以支持任何[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]混合版本。

 您可以通过共享策略或版本化策略这两种策略之一，支持 VSPackages 的并行安装。 两者都适应 .NET Framework[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]的多个版本和相关版本的存在。

 在共享策略中，一个 VSPackage 注册用于 多个[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]版本的 。 在版本化策略中，将安装多个 VSPackage DLL，每个版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]都安装一个。

## <a name="shared-vspackages"></a>共享 VS 包
 在 多个版本中使用相同的 VSPackage 时，使用共享 VS 包是[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]合适的。 要实现共享 VS 包，必须执行以下步骤：

- 使 VSPackage 与 的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]多个版本兼容。 有两种这样做的方法可用：

  - 将 VSPackage 限制为仅使用您支持的最早版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]功能。

  - 对 VSPackage 进行编程，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]以适应其运行的版本。 然后，如果对较新的服务的查询失败，您的 VSPackage 可以提供旧版本中[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]支持的其他服务。

- 正确注册您的 VS 包。 有关详细信息，请参阅[VSPackage 注册](../extensibility/internals/vspackage-registration.md)和[托管 VSPackage 注册](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)。

- 正确注册文件扩展名。 有关详细信息，请参阅注册并行[部署的文件名扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 创建一个安装程序，为[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]的相应版本部署 VSPackage。 有关详细信息，请参阅使用[Windows 安装程序](../extensibility/internals/installing-vspackages-with-windows-installer.md)和[组件管理](../extensibility/internals/component-management.md)安装 VS 包。

- 解决注册冲突问题。 有关详细信息，请参阅[VSPackage 注册](../extensibility/internals/vspackage-registration.md)。

- 确保共享文件和版本文件都尊重引用计数，以便安全安装和删除多个版本。 有关详细信息，请参阅[组件管理](../extensibility/internals/component-management.md)。

## <a name="versioned-vspackages"></a>版本化 VS 包
 在版本化的 VSPackage 策略下，您可以为每个支持版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSPackage 创建一个 VSPackage。 当您希望利用更高版本的 服务时，这样做是合适的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，因为每个 VSPackage 可以在不影响其他版本的情况下发展。 但是，从单个代码库或从多个独立代码库创建多个二进制文件的版本化策略可能需要比共享策略更多的初始开发。 此外，可能还需要其他设置工作，因为您必须为每个版本创建单独的设置，或者创建单个设置，以检测已安装的版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]以及您的 VSPackage 支持的版本。

## <a name="binary-compatibility"></a>二进制兼容性
 通常，二进制兼容性使使用早期版本的 Visual Studio 开发的本机代码 VS 包能够在 Visual Studio 的更高版本中运行。 但是，有三个重要例外：

- 如果您的 VSPackage 依赖于公共语言运行时的特定版本，则必须确定[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]它在哪个版本中正在运行。

- VSPackage 可能依赖于另一个 VSPackage 或其他产品的特定功能。 因此，VSPackage 只能在满足依赖项时运行。

- VSPackage 可能受[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]服务包或[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]更高版本 的安全修补程序的影响。 在这些情况下，使用早期版本的 VSPackage 在应用安全修补程序[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)][!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]后可能无法在 版本中运行。 但是，您可以使用更高版本重新生成包，并且使其在早期版本中也运行。

  托管 VS 包必须使用 和[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)][!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]的版本与 的目标版本匹配。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]

  除了规划 VSPackage 二进制文件的二进制兼容性外，还应考虑解决方案和项目文件格式。 如果 VSPackage 创建新的项目类型，则必须决定它是只能在一个版本中运行，还是在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]多个版本中运行。 有关详细信息，请参阅[升级自定义项目](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)。

## <a name="see-also"></a>请参阅
- [使用 Windows 安装程序安装 VS 包](../extensibility/internals/installing-vspackages-with-windows-installer.md)
- [组件管理](../extensibility/internals/component-management.md)
