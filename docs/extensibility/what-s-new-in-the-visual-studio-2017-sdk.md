---
title: 什么&#39;Visual Studio 2017 SDK 中的新增功能的 s |Microsoft Docs
ms.date: 10/31/2017
ms.topic: conceptual
ms.assetid: 9efcf0a3-dbde-4cab-8ed3-425826a48b2e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 434a04aaa8389b4b09f32778d5de63bd2a7d687f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350797"
---
# <a name="what39s-new-in-the-visual-studio-2017-sdk"></a>什么&#39;s Visual Studio 2017 SDK 中的新增功能

Visual Studio SDK 的 Visual Studio 2017 具有以下新的和更新功能。

## <a name="vsix-v3-format"></a>VSIX v3 格式

若要支持新的轻型安装的 Visual Studio 2017，VSIX 扩展清单格式已更新到版本 3 (VSIX v3)。

新格式具有对支持：

* 显式声明要检测和安装 vsixinstaller 找系统必备组件。
* Ngen 上扩展安装的程序集。
* 安装常用扩展根目录之外的资产。

若要了解有关这些更改，请参阅以下主题：

* [对 Visual Studio 2017 的可扩展性的更改](breaking-changes-2017.md)
* [VSIX v3 中的 Ngen 支持](ngen-support.md)
* [在扩展文件夹外安装](set-install-root.md)
* [Visual Studio 2017 可扩展性的常见问题](faq-2017.md)

## <a name="migrate-extensibility-project-to-visual-studio-2017"></a>将扩展性项目迁移到 Visual Studio 2017

若要了解如何更新到 Visual Studio 2017 的可扩展性项目和各自的 VSIX 清单，请参阅[如何：将扩展性项目迁移到 Visual Studio 2017](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)。

## <a name="custom-project-and-item-templates"></a>自定义项目和项模板

从 Visual Studio 2017 中，扫描自定义项目和项模板将无法再执行。 相反，该扩展插件必须提供模板清单文件描述这些模板的安装位置。 Visual Studio 2017 可用于更新您的 VSIX 扩展。 如果部署使用 MSI 扩展，则必须手动生成模板清单文件。 有关详细信息，请参阅[升级 Visual Studio 2017 的自定义项目和项模板](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)。 模板清单架构记录在[Visual Studio 模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

## <a name="updated-extension-performance-guidelines"></a>更新的扩展性能准则

新增了一个[如何：诊断扩展性能](how-to-diagnose-extension-performance.md)一文下[管理 Vspackage](managing-vspackages.md)来说明如何检测和分析对 Visual Studio 的扩展影响启动和解决方案加载时间。
