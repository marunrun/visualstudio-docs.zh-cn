---
title: Windows Vista 上的 ClickOnce 部署 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- UAC manifest generation
- ClickOnce deployment, Windows
- manifest generation
- Windows, ClickOnce deployment
ms.assetid: b21a0ebc-0ff6-4f49-8993-7d1ad3f8cac2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4beefddd429384fadda71d9742e8c0fac606c38e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900497"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Windows Vista 上的 ClickOnce 部署

在 Visual Studio 中的构建应用程序的 Windows Vista 上的用户帐户控制 (UAC) 通常将生成一个嵌入的清单编码中应用程序的可执行文件作为二进制 XML 数据。  ClickOnce 和免注册 COM 应用程序需要外部清单，因此 Visual Studio 将生成这些项目包含 UAC 数据而不是嵌入的清单的文件。 对于 ClickOnce 和免注册 COM 部署，Visual Studio 使用信息从名为的文件*app.manifest*生成外部 UAC 清单信息。 对于所有其他情况下，Visual Studio 将 UAC 数据嵌入在应用程序的可执行文件。

Visual Studio 以便生成清单中提供以下选项：

- 使用嵌入式的清单。 在应用程序的可执行文件中嵌入 UAC 数据并以普通用户身份运行。

   这是默认设置 （除非使用 ClickOnce）。 此设置在 Windows Vista 上支持通常在 Visual Studio 上进行操作的方式，与内部和外部的生成清单使用`AsInvoker`。

- 使用外部清单。 使用生成外部清单*app.manifest*。

   这将通过使用中的信息生成仅在外部清单*app.manifest*。 通过使用 ClickOnce 或免注册 COM 发布应用程序，在 Visual Studio 添加*app.manifest*到项目，然后添加此选项。

- 使用没有清单。 创建不带清单的应用程序。

   这种方法是也称为*虚拟化*。 使用此选项与现有的应用程序从 Visual Studio 的早期版本的兼容性。

  新的属性可用于**应用程序**（对于 Visual C# 项目只能） 在项目设计器页以 MSBuild 项目文件格式。

  在 Visual Studio IDE 中配置 UAC 清单生成的方法不同，具体取决于项目类型 （Visual C# 或 Visual Basic）。

  * 有关配置的清单生成的 Visual C# 项目的信息，请参阅[应用程序页，项目设计器 (C#)](../ide/reference/application-page-project-designer-csharp.md)。

  * 有关配置的清单生成的 Visual Basic 项目的信息，请参阅[应用程序页，项目设计器 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)。

## <a name="see-also"></a>请参阅
- [ClickOnce 安全和部署](../deployment/clickonce-security-and-deployment.md)
- [用户权限和 Visual Studio](https://msdn.microsoft.com/library/d5c55084-1e7b-4b61-b478-137db01c0fc0)
- [“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md)
- [“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)