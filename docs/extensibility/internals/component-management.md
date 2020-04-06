---
title: 组件管理 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709326"
---
# <a name="component-management"></a>组件管理
Windows 安装程序中的任务单元称为 Windows 安装程序组件（有时称为 WIC 或只是组件）。 GUID 标识每个 WIC，这是使用 Windows 安装程序的安装和引用计数的基本单元。

 尽管可以使用多个产品创建 VSPackage 安装程序，但此讨论假定使用 Windows 安装程序 *（.msi*） 文件。 创建安装程序时，必须正确管理文件部署，以便随时进行正确的引用计数。 因此，在安装和卸载混合方案中，产品的不同版本不会相互干扰或破裂。

 在 Windows 安装程序中，引用计数发生在组件级别。 您必须仔细将资源（文件、注册表项等）组织到组件中。 还有其他级别的组织（如模块、功能和产品）可以在不同方案中提供帮助。 有关详细信息，请参阅[Windows 安装程序基础知识](../../extensibility/internals/windows-installer-basics.md)。

## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>并行安装的创作设置指南

- 创作在版本之间共享的文件和注册表项到其自己的组件中。

     这样做允许您在下一版本中轻松使用它们。 例如，键入全局注册的库、文件扩展名、**在HKEY_CLASSES_ROOT**中注册的其他项目等。

- 将共享组件分组到单独的合并模块中。

     此策略可帮助您正确创作并行安装。

- 跨版本使用相同的 Windows 安装程序组件安装共享文件和注册表项。

     如果使用其他组件，则在卸载一个版本化的 VSPackage 但仍安装另一个 VSPackage 时，将卸载文件和注册表项。

- 不要在同一组件中混合版本控制项目和共享项目。

     这样，就无法将共享项目安装到全局位置，并将项目版本控制到隔离位置。

- 没有指向版本化文件的共享注册表项。

     如果这样做，则在安装另一个版本化的 VSPackage 时，共享密钥将被覆盖。 删除第二个版本后，键指向的文件将消失。

## <a name="see-also"></a>请参阅
- [在共享和版本化 VS 包之间进行选择](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VS包设置方案](../../extensibility/internals/vspackage-setup-scenarios.md)
