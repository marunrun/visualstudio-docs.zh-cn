---
title: '&apos;Visual Studio 2017 SDK 中的新增功能 |Microsoft Docs'
ms.date: 10/31/2017
ms.topic: conceptual
ms.assetid: 9efcf0a3-dbde-4cab-8ed3-425826a48b2e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6fb5b81341f8184d713755b3b934fbae4c8031b1
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88711594"
---
# <a name="what39s-new-in-the-visual-studio-2017-sdk"></a>Visual Studio 2017 SDK 中的新增功能&#39;

Visual Studio SDK 具有以下新的和更新的 Visual Studio 2017 功能。

## <a name="vsix-v3-format"></a>VSIX v3 格式

为了支持 Visual Studio 2017 的全新轻型安装，已将 VSIX 扩展清单格式更新为版本 3 (VSIX v3) 。

新格式支持：

* 显式声明要由 VSIXInstaller 检测并安装的系统必备组件。
* 扩展安装上的 Ngen 程序集。
* 在普通扩展根外部安装资产。

若要了解这些更改，请参阅以下主题：

* [Visual Studio 2017 的扩展性更改](breaking-changes-2017.md)
* [VSIX v3 中的 Ngen 支持](ngen-support.md)
* [在扩展文件夹外进行安装](set-install-root.md)
* [Visual Studio 2017 扩展性常见问题](faq-2017.md)

## <a name="migrate-extensibility-project-to-visual-studio-2017"></a>将扩展性项目迁移到 Visual Studio 2017

若要了解如何将扩展性项目及其 VSIX 清单更新为 Visual Studio 2017，请参阅 [如何：将扩展性项目迁移到 Visual studio 2017](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)。

## <a name="custom-project-and-item-templates"></a>自定义项目和项模板

从 Visual Studio 2017 开始，将无法再执行对自定义项目和项模板的扫描。 相反，扩展必须提供模板清单文件来描述这些模板的安装位置。 可使用 Visual Studio 2017 来更新 VSIX 扩展。 如果使用 MSI 部署扩展，则必须手动生成模板清单文件。 有关详细信息，请参阅 [为 Visual Studio 2017 升级自定义项目和项模板](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)。 有关模板清单架构，可查看 [Visual Studio 模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

## <a name="updated-extension-performance-guidelines"></a>更新的扩展性能准则

"[管理 vspackage](managing-vspackages.md) " 下有一个新的 "[如何：诊断扩展性能](how-to-diagnose-extension-performance.md)" 一文，以说明如何检测和分析对 Visual Studio 启动和解决方案加载时间的扩展影响。
