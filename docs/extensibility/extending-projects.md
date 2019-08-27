---
title: 扩展项目 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
ms.assetid: 096d273d-4fe9-4f24-9b00-470bfbdf4bdf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d0333e09aee207e10657999dda4b5b1d59e181cf
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341111"
---
# <a name="extend-projects"></a>扩展项目
项目和解决方案是 Visual Studio 将代码和资源文件组织到编译和部署单元的方法。 您可以找到有关中的项目的详细信息[项目 (Visual Studio SDK)](../extensibility/extending-projects.md)。

 可以使用 Visual Studio SDK 和托管包框架中的项目，您可以下载在创建你自己的项目类型[项目的托管包框架](https://github.com/tunnelvisionlabs/MPFProj10)。 若要了解如何实现自定义项目，请参阅[生成新项目：实质上，第一部分](../extensibility/internals/new-project-generation-under-the-hood-part-one.md)和[生成新项目：实质上，第二部分](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 在本部分中的主题介绍如何创建自定义项目以及如何管理不同类型的 Visual Studio 解决方案。

## <a name="in-this-section"></a>本节内容
- [创建基本项目系统，第 1 部分](../extensibility/creating-a-basic-project-system-part-1.md)介绍如何创建自定义项目系统。

- [创建基本项目系统，第 2 部分](../extensibility/creating-a-basic-project-system-part-2.md)介绍如何创建自定义项目系统。

- [将数据保存在项目文件中](../extensibility/saving-data-in-project-files.md)解释了如何将添加到项目 (<em>。</em>proj *） 文件。

- [在运行时验证项目的子类型](../extensibility/verifying-subtypes-of-a-project-at-run-time.md)介绍了如何在运行时验证项目的子类型。

- [添加和删除属性页](../extensibility/adding-and-removing-property-pages.md)说明如何自定义自定义项目的属性页。

- [将属性添加到项目项](../extensibility/adding-an-attribute-to-a-project-item.md)介绍了如何将属性添加到自定义项目项。

- [保存项目项的属性的](../extensibility/persisting-the-property-of-a-project-item.md)介绍了如何持久保存自定义项目项的属性。

- [管理通用 Windows 项目](../extensibility/managing-universal-windows-projects.md)说明如何管理通用项目。