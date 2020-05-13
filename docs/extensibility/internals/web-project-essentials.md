---
title: 网络项目要点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 09e33248ca264fefa79a8d5d5fa5d0cfa3d2da1d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703551"
---
# <a name="web-project-essentials"></a>Web 项目基础知识
Web 项目创建 Web 应用程序。 可以使用 Web 项目创建具有智能 Web 页的 Web 应用程序。 智能网页具有服务器端代码，可按需呈现该网页。

 使用传统的编程语言（如[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]或[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]）可以创建智能网页来收集和处理用户的信息，将其存储在数据库中，等等。

- 代码后面模型将相关的源代码文件与具有文件扩展名 .aspx 或 .asmx 的网页关联。 例如，hello.aspx 可能具有从属源代码文件hello.aspx.cs。

- 与智能 Web 页关联的服务器端代码将编译为位于网站/bin 文件夹中的可执行文件。

- 其他源代码文件（如未与特定网页关联的帮助程序类）位于网站 /App_Code文件夹中。

  - 网站项目 （WSP） 为每个智能网页生成一个可执行文件。 其他可执行文件从 /App_Code 文件夹中的任何源代码文件生成。

  - Web 应用程序项目 （WAP） 生成单个可执行文件，该文件结合了所有智能 Web 页以及 /App_Code 文件夹中的所有源文件的代码。

- Web 项目的解决方案文件与网站本身分开。 默认情况下，解决方案文件位于 [文档和设置\\*您的帐户*]我的文档\\*\<可视化工作室 [>*[项目\\*您的网站*。

  > [!NOTE]
  > 如果要将解决方案文件保留到 Web 站点中，只需将其移到该站点并重新打开它。

- 如果打开 Visual Studio 中没有解决方案文件的网站，将自动为其生成新的解决方案文件。

- Web 项目没有项目文件。 项目信息存储在解决方案文件、Web.config 文件和其他地方。

- 将全局属性添加到 Web 项目会自动在 Web 项目解决方案文件夹中创建存储文件。

- 通过使用 Page 指令或脚本 runat_"server">标记，\<智能 Web 页可以与服务器端编程语言相关联。

- 此外，网页可以用任何脚本语言编写任意数量的客户端脚本块。

- 通过将项目和项目模板以及注册添加到项目，[!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)]实现了网站项目系统。

- WAP 系统作为项目子类型实现，也称为项目风格。 项目[!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)]由 WAP 子类型调味以创建 WAP 系统。 有关项目子类型的详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

- 智能网页将 HTML 与服务器端编程语言相结合。 服务器端语言称为包含语言。 为了支持包含的语言，Web 项目系统必须实现接口<xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage>的系列。

  - 要支持编辑器中包含的语言，HTML 语言服务必须将显示包含的语言代码推迟到包含的语言服务。

  - 错误标记（红色波浪）应始终在代码编辑器的主缓冲区中创建。

## <a name="see-also"></a>请参阅
- [Web 项目](../../extensibility/internals/web-projects.md)
