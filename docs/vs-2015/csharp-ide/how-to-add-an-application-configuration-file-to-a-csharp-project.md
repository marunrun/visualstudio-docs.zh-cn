---
title: '如何：向 c # 项目添加应用程序配置文件 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
dev_langs:
- CSharp
helpviewer_keywords:
- app.config files, adding to C# projects
ms.assetid: 9caf6bb0-c2fc-4ab6-ba69-bed3b880fbf8
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f8417b5520dc9587fa3231a3bc459335d2a9896d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667533"
---
# <a name="how-to-add-an-application-configuration-file-to-a-c-project"></a>如何：向 C# 项目添加应用程序配置文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过将应用程序配置文件（app.config 文件）添加到 C# 项目中，你可以自定义公共语言运行时定位和加载程序集文件的方式。 有关应用程序配置文件的详细信息，请参阅 [运行时如何定位程序集](https://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34)。

> [!NOTE]
> Windows 应用商店不支持 <xref:System.Configuration> 。 因此，应用商店应用不包含 app.config 模板。

 生成项目时，开发环境会自动复制你的 app.config 文件，更改副本的文件名以匹配你的可执行文件，然后会将副本移动到“bin”目录。

### <a name="to-add-an-application-configuration-file-to-your-c-project"></a>向 c # 项目添加应用程序配置文件

1. 在菜单栏上，依次选择 " **项目**"、" **添加新项**"。

     此时会显示“添加新项”对话框。

2. 展开 " **已安装**"，展开 " **Visual c # 项**"，然后选择 " **应用程序配置文件** " 模板。

3. 在“名称”文本框中输入名称，然后选择“添加”按钮********。

     名为 app.config 的文件将添加到你的项目中。

## <a name="see-also"></a>另请参阅
 [ ( .net) ](../ide/managing-application-settings-dotnet.md) [配置文件架构](https://msdn.microsoft.com/library/69003d39-dc8a-460c-a6be-e6d93e690b38) [Configuring Apps](https://msdn.microsoft.com/library/86bd26d3-737e-4484-9782-19b17f34cd1f)中管理应用程序设置如何：[使用 c # 的 Visual Studio 开发环境](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)[配置应用程序以面向 .NET Framework 版本](https://msdn.microsoft.com/5247b307-89ca-417b-8dd0-e8f9bd2f4717)