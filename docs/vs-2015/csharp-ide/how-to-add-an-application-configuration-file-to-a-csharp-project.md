---
title: 如何：添加到应用程序配置文件C#项目 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bc5c8dbad4d2bb248a3183e2e73d7c2932e7bce4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681729"
---
# <a name="how-to-add-an-application-configuration-file-to-a-c-project"></a>如何：添加到应用程序配置文件C#项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过将应用程序配置文件（app.config 文件）添加到 C# 项目中，你可以自定义公共语言运行时定位和加载程序集文件的方式。 有关应用程序配置文件的详细信息，请参阅[运行时如何定位程序集](https://msdn.microsoft.com/library/772ac6f4-64d2-4cfb-92fd-58096dcd6c34)。  
  
> [!NOTE]
> 不支持 Windows 应用商店<xref:System.Configuration>。 因此，应用商店应用程序不包含 app.config 模板。  
  
 生成项目时，开发环境会自动将你的 app.config 文件的复制、 更改以匹配你可执行文件的副本的文件名，然后会将副本移动到 bin 目录。  
  
### <a name="to-add-an-application-configuration-file-to-your-c-project"></a>若要将应用程序配置文件添加到你的 C# 项目  
  
1. 在菜单栏上依次选择**项目**，**添加新项**。  
  
     “添加新项”对话框随即出现。  
  
2. 展开**已安装**，展开**Visual C# 项**，然后选择**应用程序配置文件**模板。  
  
3. 在“名称”文本框中输入名称，然后选择“添加”按钮。  
  
     名为 app.config 的文件添加到你的项目。  
  
## <a name="see-also"></a>请参阅  
 [管理应用程序设置 (.NET)](../ide/managing-application-settings-dotnet.md)   
 [配置文件架构](https://msdn.microsoft.com/library/69003d39-dc8a-460c-a6be-e6d93e690b38)   
 [配置应用](https://msdn.microsoft.com/library/86bd26d3-737e-4484-9782-19b17f34cd1f)   
 [如何：配置应用以面向.NET Framework 版本](https://msdn.microsoft.com/5247b307-89ca-417b-8dd0-e8f9bd2f4717)   
 [使用 Visual Studio C# 开发环境](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)