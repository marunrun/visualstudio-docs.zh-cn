---
title: 杂项，XML，文本编辑器，"选项" 对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: fd3fff31-cddc-422d-a2f0-a5a1ef492afd
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d30564c11951d6ffec420c6a2ea95c41695de3dd
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656240"
---
# <a name="miscellaneous-xml-text-editor-options-dialog-box"></a>杂项，XML，文本编辑器，“选项”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用此对话框可以更改“XML 编辑器”的自动完成和架构设置。 可以从 "**工具**" 菜单访问 "**选项**" 对话框。

> [!NOTE]
> 选择 "**文本编辑器**" 文件夹、" **XML** " 文件夹，然后选择 "**选项**" 对话框中的 "**杂项**" 选项时，可以使用这些设置。

## <a name="auto-insert"></a>自动插入
 **关闭标记**如果选中了 "自动完成" 设置，则当你键入右尖括号（>）以关闭开始标记时，如果尚未关闭标记，编辑器将自动添加结束标记。 这是默认行为。

 空元素的完成不依赖于自动完成设置。 可通过键入反斜杠 (/) 来始终自动完成空元素。

 **特性引号**创作 XML 属性时，编辑器会插入 `=" "` 字符并将插入符号（^）置于双引号中。

 默认情况下选中此选项。

 **命名空间声明**编辑器会自动在需要时插入命名空间声明。

 默认情况下选中此选项。

 **其他标记（注释、CDATA）** 注释、CDATA、DOCTYPE、处理指令和其他标记自动完成。

 默认情况下选中此选项。

## <a name="network"></a>网络
 **自动下载 dtd 和架构**架构和文档类型定义（Dtd）是从 HTTP 位置自动下载的。 此功能在启用自动代理服务器检测的情况下使用 System.Net。

 默认情况下选中此选项。

## <a name="outlining"></a>大纲显示
 **打开文件时进入大纲模式**打开文件时启用大纲显示功能。

 默认情况下选中此选项。

## <a name="caching"></a>缓存
 **架构**指定架构缓存的位置。 浏览按钮（ **...** ）在当前架构缓存位置打开 "**目录浏览**" 对话框。 你可以选择不同的目录，也可以在对话框中选择一个文件夹，右键单击，然后选择 "**打开**" 以查看目录中的内容。

## <a name="see-also"></a>请参阅
 [Xml 文档属性，"属性" 窗口](../xml-tools/xml-document-properties-properties-window.md) [XML 编辑器组件](../xml-tools/xml-editor-components.md)
