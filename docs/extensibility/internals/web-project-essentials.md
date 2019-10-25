---
title: Web 项目基础知识 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web projects, essentials
ms.assetid: ca2f4e43-322c-4431-8680-52da846940bc
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f3d3069d8cc539deeda7c9d44f8d1cbf27e8821
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721664"
---
# <a name="web-project-essentials"></a>Web 项目基础知识
Web 项目创建 Web 应用程序。 您可以使用 Web 项目来创建包含智能网页的 Web 应用程序。 智能网页包含按需呈现网页的服务器端代码。

 使用传统的编程语言（例如 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 或 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]），您可以创建智能网页来收集和处理来自用户的信息，将其存储在数据库中，等等。

- 代码隐藏模型将相关的源代码文件与具有文件扩展名 .aspx 或 .asmx 的网页相关联。 例如，hello.aspx.cs 可能具有相关的源代码文件。

- 与智能网页关联的服务器端代码编译到位于网站/bin 文件夹中的可执行文件。

- 其他源代码文件（如与特定网页不关联的帮助器类）位于 "网站/App_Code" 文件夹中。

  - 网站项目（WSP）为每个智能网页生成一个可执行文件。 其他可执行文件是从/App_Code 文件夹中的任何源代码文件生成的。

  - Web 应用程序项目（WAP）生成一个可执行文件，该文件合并所有智能网页的代码以及/App_Code 文件夹中的所有源文件。

- Web 项目的解决方案文件与网站本身位于同一位置。 默认情况下，解决方案文件位于 \Documents 和 Settings \\*YourAccount*\My 文档 \\ *\<Visual Studio # # # # >* \Projects \\*YourWebSite*。

  > [!NOTE]
  > 如果要将解决方案文件与网站一起保存，只需将其移动并重新打开即可。

- 如果在 Visual Studio 中打开一个没有解决方案文件的网站，系统会自动为其生成一个新的解决方案文件。

- Web 项目没有项目文件。 项目信息存储在解决方案文件、web.config 文件和其他位置。

- 将全局属性添加到 Web 项目时，会在 Web 项目解决方案文件夹中自动创建存储文件。

- 通过使用 Page 指令或 \<script runat = "server" > 标记，可以将智能网页与服务器端编程语言相关联。

- 此外，网页还可以有任意数量的客户端脚本块，以任何脚本语言编写。

- 网站项目系统是通过将项目和项模板添加到 [!INCLUDE[vwprvw](../../extensibility/internals/includes/vwprvw_md.md)] 项目来实现的。

- WAP 系统作为项目子类型实现，也称为项目风格。 @No__t_0 项目由 WAP 子类型风格以创建 WAP 系统。 有关项目子类型的详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

- 智能网页将 HTML 与服务器端编程语言结合起来。 服务器端语言称为 "包含语言"。 若要支持包含语言，Web 项目系统必须实现 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsContainedLanguage> 的接口系列。

  - 若要在编辑器中支持包含的语言，HTML 语言服务必须延迟向包含的语言服务显示包含的语言代码。

  - 应始终在代码编辑器的主缓冲区中创建错误标记（红色标记）。

## <a name="see-also"></a>请参阅
- [Web 项目](../../extensibility/internals/web-projects.md)