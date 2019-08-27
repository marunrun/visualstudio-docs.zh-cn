---
title: “选项”页 ->“字体和颜色”节点属性 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Tools Options settings, Fonts and Colors node properties
- automation [Visual Studio], controlling Tools Options
ms.assetid: 8e1ab784-5f85-4e2b-8ef9-e5d59ca4dbcb
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 788d6077af99e6fe9fa99328aa9281d6327297b1
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697181"
---
# <a name="options-page-fonts-and-colors-node-properties"></a>“选项”页 ->“字体和颜色”节点属性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本文档介绍某个工具窗口的字体和颜色属性，该窗口注册显示在“选项”对话框“环境”类别中的”字体和颜色”下。 这支持可着色项组的动态特性，安装或卸载 VSPackages 时，这些特性可能会发生更改。  
  
 以下部分显示了已注册窗口类型的示例，以及可用于每个窗口的属性。  
  
## <a name="text-editor-or-printer-or-dialogs-and-tool-windows"></a>文本编辑器、打印机或对话框和工具窗口  
 `DTE.Properties("FontsAndColors", "TextEditor")`  
  
 -或-  
  
 `DTE.Properties("FontsAndColors", "Printer")`  
  
 或  
  
 `DTE.Properties("FontsAndColors", "Dialogs and Tool Windows")`  
  
|属性项名称|值|说明|  
|------------------------|-----------|-----------------|  
|FontFamily|Get/Set (String)|要使用的字体名称，如“Courier New”。|  
|FontCharacterSet|Get/Set (<xref:EnvDTE.vsFontCharSet>)|<xref:EnvDTE.vsFontCharSet> 值，指定要使用的字符集的类型，例如希伯来语或俄语。|  
|FontSize|Get/Set (Short)|要使用的字体大小（以磅为单位）。 例如，10 或 12。|  
  
## <a name="see-also"></a>请参阅  
 [控制选项设置](https://msdn.microsoft.com/library/a09ed242-7494-4cde-bbd1-7a8ec617965d)   
 [确定“选项”页中属性项的名称](https://msdn.microsoft.com/library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)   
 [“选项”页 ->“环境”节点属性](../../ide/reference/options-page-environment-node-properties.md)   
 [“选项”页 ->“文本编辑器”节点属性](../../ide/reference/options-page-text-editor-node-properties.md)
