---
title: “选项”对话框 ->“环境”->“区域设置”| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.InternationalSettings
- VS.ToolsOptionsPages.Environment.International_Settings
- VS.Environment.International Settings
- VS.ToolsOptionsPag.Environment.International_Settings
helpviewer_keywords:
- International Settings dialog box
- languages, environment settings
- Options dialog box, international settings
- languages, specifying default
ms.assetid: e3a8815c-6995-4099-8e88-34f91fad55b2
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a42a05c453c328dc156cadb86c9abc55d587c467
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65674305"
---
# <a name="international-settings-environment-options-dialog-box"></a>“选项”对话框 ->“环境”->“区域设置”
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

当你的计算机上安装有多个语言版本的集成开发环境 (IDE) 时，可通过国际设置页面更改默认语言。 要访问此对话框，可从“工具”菜单中选择“选项”，然后从“环境”文件夹中选择“区域设置”。 如果此页未出现在列表中，请在“选项”对话框中选择“显示所有设置”。  
  
> [!NOTE]
> 对话框中的可用选项以及显示的菜单命令的名称和位置可能与“帮助”中的描述不同，具体取决于您的当前设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 **语言**  
 列出已安装产品语言版本的可用语言。 除非你的计算机上安装了多个语言版本，否则此选项不可用。 如果产品的多个语言或产品的混合语言安装可共享环境，则将语言选项更改为“与 Microsoft Windows 相同”。  
  
> [!CAUTION]
> 在安装了多个语言的系统中，Visual C++ 生成工具（cl.exe、link.exe、nmake.exe、bscmake.exe 和相关文件）不受此设置的影响。 这些工具使用上次安装的语言版本，以前安装的语言版本的工具将被覆盖，因为 Visual C++ 生成工具不使用附属 DLL 模型。  
  
## <a name="see-also"></a>请参阅  
 [“选项”对话框 ->“环境”](../../ide/reference/environment-options-dialog-box.md)
