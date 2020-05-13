---
title: 扩展项目 |微软文档
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
ms.openlocfilehash: 14108a304cc5f85c9a870bc66804df7daa98f3ca
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711754"
---
# <a name="extend-projects"></a>扩展项目
项目和解决方案是 Visual Studio 将代码和资源文件组织到编译和部署单元中的方式。 您可以在[项目（可视化工作室 SDK）](../extensibility/extending-projects.md)中找到有关项目的详细信息。

 您可以使用 Visual Studio SDK 和项目的托管包框架创建自己的项目类型，您可以在[项目的托管包框架](https://github.com/tunnelvisionlabs/MPFProj10)中下载。 要了解如何实施自定义项目，请参阅[新项目生成：引擎盖下、第一部分](../extensibility/internals/new-project-generation-under-the-hood-part-one.md)和新[项目生成：在引擎盖下，第二部分](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 本节中的主题介绍如何创建自定义项目以及如何管理不同类型的 Visual Studio 解决方案。

## <a name="in-this-section"></a>在本节中
- [创建基本项目系统，第 1 部分](../extensibility/creating-a-basic-project-system-part-1.md)描述如何创建自定义项目系统。

- [创建基本项目系统，第 2 部分](../extensibility/creating-a-basic-project-system-part-2.md)描述如何创建自定义项目系统。

- [在项目文件中保存数据](../extensibility/saving-data-in-project-files.md)说明如何添加到项目<em>（。</em>proj_） 文件。

- [在运行时验证项目的子类型](../extensibility/verifying-subtypes-of-a-project-at-run-time.md)说明如何在运行时验证项目的子类型。

- [添加和删除属性页](../extensibility/adding-and-removing-property-pages.md)说明如何自定义自定义项目的属性页。

- [将属性添加到项目项](../extensibility/adding-an-attribute-to-a-project-item.md)说明如何向自定义项目项添加属性。

- [保留项目项的属性](../extensibility/persisting-the-property-of-a-project-item.md)说明如何保留自定义项目项的属性。

- [管理通用 Windows 项目](../extensibility/managing-universal-windows-projects.md)说明如何管理通用项目。
