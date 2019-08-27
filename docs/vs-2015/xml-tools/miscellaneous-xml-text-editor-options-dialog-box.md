---
title: 杂项，XML，文本编辑器选项对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: fd3fff31-cddc-422d-a2f0-a5a1ef492afd
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: edf638420ac41d6ad6f7ebf5e20ab5d78d1c7b3d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435369"
---
# <a name="miscellaneous-xml-text-editor-options-dialog-box"></a>杂项，XML，文本编辑器，“选项”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用此对话框可以更改“XML 编辑器”的自动完成和架构设置。 您可以访问**选项**对话框从**工具**菜单。  
  
> [!NOTE]
> 当您选择这些设置才可用**文本编辑器**文件夹中， **XML**文件夹，然后**杂项**选项**选项**对话框。  
  
## <a name="auto-insert"></a>自动插入  
 **结束标记**  
 如果选中自动完成设置，则编辑器将键入右尖括号 (>) 以结束开始标记时，如果该标记尚未结束时自动添加结束标记。 这是默认行为。  
  
 空元素的完成不依赖于自动完成设置。 可通过键入反斜杠 (/) 来始终自动完成空元素。  
  
 **特性引号**  
 在编写 XML 属性时，编辑器会插入 `=" "` 字符并将插入符号 (^) 置于双引号之间。  
  
 默认情况下选中此选项。  
  
 **命名空间声明**  
 编辑器根据需要自动插入命名空间声明。  
  
 默认情况下选中此选项。  
  
 **其他标记（注释、CDATA）**  
 自动完成注释、CDATA、DOCTYPE、处理指令和其他标记。  
  
 默认情况下选中此选项。  
  
## <a name="network"></a>网络  
 **自动下载 DTD 和架构**  
 架构和文档类型定义 (DTD) 自动从 HTTP 位置下载。 此功能在启用自动代理服务器检测的情况下使用 System.Net。  
  
 默认情况下选中此选项。  
  
## <a name="outlining"></a>大纲显示  
 **打开文件时进入大纲模式**  
 在打开文件时启用大纲功能。  
  
 默认情况下选中此选项。  
  
## <a name="caching"></a>缓存  
 **架构**  
 指定架构缓存的位置。 浏览按钮 (**...**) 打开**目录浏览**对话框在当前架构缓存位置。 可以选择不同的目录，也可以在对话框中，选择一个文件夹右键单击，然后选择**打开**来查看目录中的内容。  
  
## <a name="see-also"></a>请参阅  
 [XML 文档属性，属性窗口](../xml-tools/xml-document-properties-properties-window.md)   
 [“XML 编辑器”的组件](../xml-tools/xml-editor-components.md)
