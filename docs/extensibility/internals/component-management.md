---
title: 组件管理 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b5dcac9fb14a83021b852be2c52436fcdca84bf5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709326"
---
# <a name="component-management"></a>组件管理
Windows Installer 中的任务单位称为 Windows Installer 组件 (有时称为 WICs 或只是组件) 。 GUID 标识每个 WIC，这是使用 Windows Installer 的安装程序的基本安装和引用计数。

 尽管可以使用多个产品创建 VSPackage 安装程序，但本讨论假定使用 Windows Installer (*.msi*) 文件。 创建安装程序时，必须正确管理文件部署，使正确的引用计数始终发生。 因此，不同版本的产品在安装和卸载方案混合环境中不会相互干扰或相互中断。

 在 Windows Installer 中，引用计数发生在组件级别。 您必须仔细地将资源（文件、注册表项等）整理到组件中。 还有其他一些级别的组织，如模块、功能和产品，它们可在不同方案中提供帮助。 有关详细信息，请参阅 [Windows Installer 基础知识](../../extensibility/internals/windows-installer-basics.md)。

## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>创作安装程序以进行并行安装的准则

- 创作在各个版本之间共享的文件和注册表项。

     这样做使您可以在下一版本中轻松地使用它们。 例如，键入在全局注册的库、文件扩展名、在 **HKEY_CLASSES_ROOT**中注册的其他项，等等。

- 将共享组件组合到不同的合并模块中。

     此策略可帮助您正确地进行创作，以便进行并行安装。

- 通过在不同版本中使用相同的 Windows Installer 组件来安装共享文件和注册表项。

     如果使用其他组件，则在卸载一个版本控制的 VSPackage 时将卸载文件和注册表项，但仍会安装另一个 VSPackage。

- 不要在同一组件中混合使用版本控制和共享项。

     这样做使无法将共享项安装到全局位置，并将已进行版本管理的项安装到独立的位置。

- 不要包含指向版本控制文件的共享注册表项。

     如果这样做，则在安装其他版本的 VSPackage 时将覆盖共享密钥。 删除第二个版本后，该键指向的文件将不再存在。

## <a name="see-also"></a>另请参阅
- [在共享和版本控制之间进行选择 Vspackage](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VSPackage 安装方案](../../extensibility/internals/vspackage-setup-scenarios.md)
