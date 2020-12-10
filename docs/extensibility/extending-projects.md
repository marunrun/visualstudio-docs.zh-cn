---
title: 扩展项目 |Microsoft Docs
description: 了解如何在 Visual Studio SDK 中创建自己的自定义项目类型，以及如何管理不同类型的 Visual Studio 解决方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
ms.assetid: 096d273d-4fe9-4f24-9b00-470bfbdf4bdf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 181acea9a5188ba28a4ef109b5bec0e7c040b5da
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994610"
---
# <a name="extend-projects"></a>扩展项目
项目和解决方案是 Visual Studio 将代码和资源文件组织成编译和部署单元的方法。 可在 [Visual STUDIO SDK)  (](../extensibility/extending-projects.md)中找到有关项目的详细信息。

 你可以通过 Visual Studio SDK 和项目的托管包框架创建自己的项目类型，你可以在 [项目的托管包框架](https://github.com/tunnelvisionlabs/MPFProj10)下载这些项目类型。 若要了解如何实现自定义项目，请参阅[新项目生成：在](../extensibility/internals/new-project-generation-under-the-hood-part-one.md)幕后，第二部分是[生成新项目：](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)

 本节中的主题介绍如何创建自定义项目，以及如何管理不同类型的 Visual Studio 解决方案。

## <a name="in-this-section"></a>在本节中
- [创建基本项目系统，第1部分](../extensibility/creating-a-basic-project-system-part-1.md) 描述如何创建自定义项目系统。

- [创建基本项目系统，第2部分](../extensibility/creating-a-basic-project-system-part-2.md) 描述如何创建自定义项目系统。

- [在项目文件中保存数据](../extensibility/saving-data-in-project-files.md) 说明如何将添加到项目 (<em>。</em>proj * ) 文件。

- [在运行时验证项目的子类型](../extensibility/verifying-subtypes-of-a-project-at-run-time.md) 说明如何在运行时验证项目的子类型。

- [添加和删除属性页](../extensibility/adding-and-removing-property-pages.md) 说明如何为自定义项目自定义属性页。

- [向项目项添加特性](../extensibility/adding-an-attribute-to-a-project-item.md) 说明如何将属性添加到自定义项目项。

- [保留项目项的属性](../extensibility/persisting-the-property-of-a-project-item.md) 说明如何保存自定义项目项的属性。

- [管理通用 Windows 项目](../extensibility/managing-universal-windows-projects.md) 介绍如何管理通用项目。
