---
title: 视觉工作室 2017 SDK 中的&#39;新增功能 |微软文档
ms.date: 10/31/2017
ms.topic: conceptual
ms.assetid: 9efcf0a3-dbde-4cab-8ed3-425826a48b2e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 88330aa68f2a3752431fd2fbe6c5c1c649acbb8b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697199"
---
# <a name="what39s-new-in-the-visual-studio-2017-sdk"></a>视觉工作室 2017 SDK 中的&#39;新增功能

Visual Studio SDK 具有以下 Visual Studio 2017 的新功能和更新功能。

## <a name="vsix-v3-format"></a>VSIX v3 格式

为了支持 Visual Studio 2017 的新轻型安装，VSIX 扩展清单格式已更新为版本 3 （VSIX v3）。

新格式支持：

* 显式声明由 VSIX 安装程序检测到和安装的先决条件。
* 扩展安装上的 Ngen 程序集。
* 在通常的扩展根目录之外安装资源。

要了解这些更改，请参阅以下主题：

* [2017 年可视化工作室扩展性的更改](breaking-changes-2017.md)
* [VSIX v3 中的 Ngen 支持](ngen-support.md)
* [在扩展文件夹外进行安装](set-install-root.md)
* [Visual Studio 2017 扩展性常见问题](faq-2017.md)

## <a name="migrate-extensibility-project-to-visual-studio-2017"></a>将扩展性项目迁移到 Visual Studio 2017

要了解如何将扩展性项目及其 VSIX 清单更新到 Visual Studio 2017，请参阅[如何：将扩展性项目迁移到 Visual Studio 2017](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)。

## <a name="custom-project-and-item-templates"></a>自定义项目和项目模板

从 Visual Studio 2017 开始，将不再执行自定义项目和项目模板的扫描。 相反，扩展必须提供描述这些模板的安装位置的模板清单文件。 您可以使用 Visual Studio 2017 更新 VSIX 扩展。 如果使用 MSI 部署扩展名，则必须手动生成模板清单文件。 有关详细信息，请参阅为[Visual Studio 2017 升级自定义项目和项目模板](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)。 模板清单架构记录在[可视化工作室模板清单架构引用](../extensibility/visual-studio-template-manifest-schema-reference.md)中。

## <a name="updated-extension-performance-guidelines"></a>更新扩展性能指南

在["管理 VSPackages"](managing-vspackages.md)下，有一个新的["如何：诊断扩展性能](how-to-diagnose-extension-performance.md)文章"，以演示如何检测和分析扩展对 Visual Studio 启动和解决方案加载时间的影响。
