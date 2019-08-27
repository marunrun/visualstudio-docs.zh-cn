---
title: Visual Studio 命令表 (。Vsct) 文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, overview
- Visual Studio command table configuration files (VSCT), overview
ms.assetid: 1313adb4-add4-4e74-90e2-f4be522f5259
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd39cfe801df1393ab099e691fbf34021ead70fb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332946"
---
# <a name="visual-studio-command-table-vsct-files"></a>Visual Studio 命令表格 (.Vsct) 文件
命令表配置文件是描述的 VSPackage 包含的命令集的文本文件。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]命令表 (VSCT) 编译器将基于 XML 的配置文件 （.vsct 文件） 编译为二进制的命令表输出 (.cto) 文件。 生成.cto 文件是不同于使用命令表 (启动 CTC) 编译器来编译.ctc 配置文件创建的。 但是，基于 XML 的.vsct 文件具有一些优势，例如 XML 编辑器和 XML IntelliSense。

 若要了解有关语法和语义的.vsct 文件的详细信息，请参阅[设计 XML 命令表 (。Vsct) 文件](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

## <a name="in-this-section"></a>本节内容
 [设计 XML 命令表格 (.Vsct) 文件](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

 介绍如何设计.vsct 文件。

 [如何：创建 .Vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)

 比较用于创建.vsct 文件的方法。 介绍手动创建一个新的.vsct 文件的过程。

## <a name="related-sections"></a>相关章节
 [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)

 提供有关每个部分的命令表 XML 配置文件的详细信息。

 [命令表配置 (。Ctc) 文件](https://msdn.microsoft.com/library/3413dda1-f372-4669-bcf0-c64d3463842c)概括介绍了不推荐使用的.ctc 文件格式。

 [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 描述命令表格式规范。

 [Vspackage 中的资源](../../extensibility/internals/resources-in-vspackages.md)

 介绍如何使用托管的 Vspackage 中的托管和非托管资源。

 [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

 说明如何创建包含菜单、工具栏和命令组合框的 UI。