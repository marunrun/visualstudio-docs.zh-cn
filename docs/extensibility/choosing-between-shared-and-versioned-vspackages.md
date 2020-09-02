---
title: 在共享和版本控制的 Vspackage 之间选择 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739884"
---
# <a name="choose-between-shared-and-versioned-vspackages"></a>在共享和版本控制之间进行选择 Vspackage
不同版本的 Visual Studio 可以在同一台计算机上共存。 Vspackage 可以支持任意版本组合 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

 你可以通过两个策略之一（共享策略或版本控制策略）来启用 Vspackage 的并行安装。 两者都能容纳 .NET Framework 的多个版本 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 和相关联的版本。

 在共享策略中，注册了一个 VSPackage，以供在多个版本中使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 在版本控制策略中，会安装多个 VSPackage Dll，每个 Dll 都是你支持的每个版本的 Dll [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="shared-vspackages"></a>共享 Vspackage
 使用共享 VSPackage 适用于在多个版本的中使用相同的 VSPackage [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 若要实现共享 VSPackage，必须执行以下步骤：

- 使 VSPackage 与多个版本的兼容 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 可通过两种方式执行此操作：

  - 将 VSPackage 限制为仅使用所支持的最早版本的功能 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

  - 对 VSPackage 进行编程，使 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 其适应运行它的版本。 然后，如果对更新的服务进行查询失败，你的 VSPackage 可以提供更早版本的支持的其他服务 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

- 正确注册 VSPackage。 有关详细信息，请参阅 [VSPackage registration](../extensibility/internals/vspackage-registration.md) And [Managed VSPackage registration](https://msdn.microsoft.com/library/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)。

- 适当地注册文件扩展名。 有关详细信息，请参阅将 [文件扩展名注册到并行部署](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 创建一个为适当版本的 VSPackage 部署的安装程序 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 有关详细信息，请参阅 [安装 vspackage 与 Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md) 和 [组件管理](../extensibility/internals/component-management.md)。

- 解决注册冲突的问题。 有关详细信息，请参阅 [VSPackage registration](../extensibility/internals/vspackage-registration.md)。

- 请确保共享文件和版本控制的文件都遵从引用计数，以允许安全安装和删除多个版本。 有关详细信息，请参阅 [组件管理](../extensibility/internals/component-management.md)。

## <a name="versioned-vspackages"></a>版本控制 Vspackage
 在版本控制 VSPackage 策略下，你为你支持的每个版本创建一个 VSPackage [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 如果希望利用的更高版本提供的服务，则执行此操作是适当的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，因为每个 VSPackage 都可以在不影响其他情况的情况下进行发展。 尽管如此，从单个代码库或从多个独立的基本代码创建多个二进制文件的已进行版本控制的策略可能需要比共享策略更多的初始开发。 此外，可能还需要执行其他设置工作，因为你必须为每个版本创建一个单独的安装程序，或者必须为检测 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 已安装的版本且你的 VSPackage 支持的单个安装程序创建一个。

## <a name="binary-compatibility"></a>二进制兼容性
 通常，二进制兼容性使在 visual studio 的早期版本中开发的本机代码 Vspackage 能够在更高版本的 Visual Studio 中运行。 但有三个重要的例外：

- 如果你的 VSPackage 依赖于特定版本的公共语言运行时，则必须确定它在哪个版本中 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 运行。

- VSPackage 可能依赖于另一 VSPackage 或其他产品的特定功能。 因此，VSPackage 只能运行满足依赖项的位置。

- 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] Service Pack 或更高版本的中，安全修补程序可能会影响 VSPackage [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 在这些情况下，在应用安全修补程序后，使用早期版本的开发的 VSPackage [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 可能不会在的版本中运行 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 但是，你可以使用更高版本重新生成包，并使其也在早期版本中运行。

  托管 Vspackage 必须使用与的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 目标版本匹配的和版本生成 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

  除了规划 VSPackage 二进制文件的二进制兼容性外，还应考虑解决方案和项目文件格式。 如果你的 VSPackage 创建了一个新的项目类型，则必须决定该项目类型是只能在一个版本中运行，也可以在多个版本的中运行 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 有关详细信息，请参阅 [升级自定义项目](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects)。

## <a name="see-also"></a>另请参阅
- [安装 Vspackage 与 Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md)
- [组件管理](../extensibility/internals/component-management.md)
