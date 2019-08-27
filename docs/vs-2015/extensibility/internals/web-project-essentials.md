---
title: Web 项目基础知识 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 95c9f7c530d50a7eb89ebe33fad3862f036972d1
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825617"
---
# <a name="web-project-essentials"></a>Web 项目基础知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Web 项目创建 Web 应用程序。 Web 项目可用于创建具有智能的网页的 Web 应用程序。 智能 Web 页面已呈现按需 Web 页面的服务器端代码。  
  
 使用传统编程语言中，如[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]或[!INCLUDE[csprcs](../../includes/csprcs-md.md)]，可以创建智能 Web 页以收集和处理来自用户的信息，将其存储在数据库中，依次类推。  
  
- 代码隐藏模型将依赖于源代码文件与包含文件扩展名.aspx 或.asmx 网页相关联。 例如，hello.aspx 可能依赖源代码文件 hello.aspx.cs。  
  
- 与智能 Web 页关联的服务器端代码编译到位于网站 /bin 文件夹中的可执行文件中。  
  
- 其他的源代码文件，如不与特定的 Web 页上，相关联的帮助程序类位于网站 /App_Code 文件夹中。  
  
  - 网站项目 (WSP) 会生成一个可执行文件为每个智能的网页。 其他可执行文件是从任何 /App_Code 文件夹中的源代码文件生成的。  

  - Web 应用程序项目 (WAP) 生成结合代码，以所有智能 Web 页面，以及 /App_Code 文件夹中的所有源文件的单个可执行文件。  
  
- Web 项目的解决方案文件位于独立于该网站本身。 默认情况下，解决方案文件位于 \Documents 和设置\\*YourAccount*\My Documents\\ *\<Visual Studio # # # >* \Projects\\ *YourWebSite*。  
  
    > [!NOTE]
    > 如果你想要保留与网站的解决方案文件，只需将其移动到并重新打开它。  
  
- 如果您打开在 Visual Studio 中没有解决方案文件的网站，为其自动生成新的解决方案文件。  
  
- Web 项目有没有项目文件。 项目信息存储在解决方案文件、 web.config 文件中，和其他地方。  
  
- 将全局属性会自动添加到 Web 项目的 Web 项目的解决方案文件夹中创建一个存储文件。  
  
- 智能网页可以通过使用页指令与服务器端编程语言相关联或\<脚本 runat ="server"> 标记。  
  
- 此外，Web 页可以具有任意任何的数量脚本语言编写的客户端脚本块。  
  
- 网站项目系统实现通过添加项目和项模板和注册到[!INCLUDE[vwprvw](../../includes/vwprvw-md.md)]项目。  
  
- WAP 系统作为项目子类型，也称为项目风格。 [!INCLUDE[vwprvw](../../includes/vwprvw-md.md)]项目风格的 WAP 子类型，以创建 WAP 系统。 项目子类型的详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。  
  
- 智能的网页将 HTML 与服务器端编程语言相结合。 服务器端的语言称为包含的语言。 若要支持包含的语言，Web 项目系统必须实现<xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage>系列的接口。  
  
  - 若要支持在编辑器中包含的语言，HTML 语言服务必须推迟到包含的语言服务中显示包含的语言代码。  

  - 始终应在代码编辑器的主缓冲区中创建错误标记 （红色标记）。  
  
## <a name="see-also"></a>请参阅  
 [Web 项目](../../extensibility/internals/web-projects.md)
