---
title: 如何将 app.config 文件添加到项目
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- app.config files, adding to C# projects
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: fe659979cadf4d9e5752f7bbe85150aae848de08
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770829"
---
# <a name="how-to-add-an-application-configuration-file-to-a-c-project"></a>如何：向 C# 项目添加应用程序配置文件

通过将应用程序配置文件（app.config 文件）添加到 C# 项目中，可自定义公共语言运行时定位和加载程序集文件的方式  。 有关应用程序配置文件的详细信息，请参阅[运行时如何定位程序集 (.NET Framework)](/dotnet/framework/deployment/how-the-runtime-locates-assemblies)。

> [!NOTE]
> UWP 应用不包含 app.config 文件  。

生成项目时，开发环境会自动复制 app.config 文件，更改副本的文件名以匹配可执行文件，然后将副本移动到“bin”目录   。

## <a name="to-add-an-application-configuration-file-to-a-c-project"></a>若要向 C# 项目添加应用程序配置文件

1. 在菜单栏上，依次选择“项目”   > “添加新项”  。

     “添加新项”  对话框随即出现。

1. 展开“已安装”   > “Visual C# 项”  ，然后选择“应用程序配置文件”模板  。

1. 在“名称”文本框中输入名称，然后选择“添加”按钮   。

     项目中将添加名为 app.config 的文件  。

## <a name="see-also"></a>另请参阅

- [管理应用程序设置 (.NET)](../ide/managing-application-settings-dotnet.md)
- [配置文件架构 (.NET Framework)](/dotnet/framework/configure-apps/file-schema/index)
- [配置应用 (.NET Framework)](/dotnet/framework/configure-apps/index)
