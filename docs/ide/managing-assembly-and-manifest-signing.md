---
title: 管理程序集和清单签名
ms.date: 02/17/2017
ms.technology: vs-ide-deployment
ms.topic: conceptual
helpviewer_keywords:
- manifests [Visual Studio]
- signing manifests [Visual Studio]
- application manifests [Visual Studio]
- assemblies [Visual Studio], signing
ms.assetid: 6c1ef36b-25f7-4ad0-b29a-51801b7a5420
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3add6e3e4f38b5ba73cd5154720d7b283189526e
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461491"
---
# <a name="manage-assembly-and-manifest-signing"></a>管理程序集和清单签名

强名称签名可为软件组件提供全局唯一标识。 使用强名称可保证程序集不被其他用户伪造，还可确保组件依赖关系和配置语句映射到正确的组件和组件版本。

强名称是由程序集的标识加上公钥令牌和数字签名组成的。其中，程序集的标识包括简单文本名称、版本号和区域性信息。

有关 Visual Basic 和 C# 项目中签名程序集的信息，请参阅[创建和使用具有强名称的程序集](/dotnet/framework/app-domains/create-and-use-strong-named-assemblies)。

有关 Visual C++ 项目中签名程序集的信息，请参阅[强名称程序集 (C++/CLI)](/cpp/dotnet/strong-name-assemblies-assembly-signing-cpp-cli)。

> [!NOTE]
> 强名称签名不能保护程序集免受反向工程的威胁。 若要防止反向工程，请参阅 [Dotfuscator Community](dotfuscator/index.md)。

## <a name="asset-types-and-signing"></a>资产类型和签名

可对 .NET 程序集和应用程序清单进行签名：

- 可执行文件 (.exe  )

- 应用程序清单 (.exe.manifest  )

- 部署清单 (.application  )

- 共享组件程序集 (.dll  )

对以下类型的资产进行签名：

1. 程序集，如果想要将它们部署到全局程序集缓存 (GAC)。

2. ClickOnce 应用程序和部署清单。 Visual Studio 默认情况下将启动对这些应用程序的签名。

3. 主互操作程序集，适用于 COM 互操作性。 从 COM 类型库中创建主互操作程序集时，TLBIMP 实用程序将强制实施强命名。

通常不应该对可执行文件进行签名。 强命名组件无法引用与应用程序一同部署的非强命名组件。 Visual Studio 不会对应用程序可执行文件进行签名，但会对指向弱命名可执行文件的应用程序清单进行签名。 避免对应用程序专用的组件进行签名，因为签名可能增加管理依赖项的难度。

## <a name="how-to-sign-an-assembly-in-visual-studio"></a>如何对 Visual Studio 中的程序集进行签名

若要对应用程序或组件进行签名，可使用项目属性窗口中的“签名”  选项卡（在“解决方案资源管理器”  中，右键单击项目节点并选择“属性”  ）。 选择“签名”  选项卡，然后选中“为程序集签名”  复选框。

指定密钥文件。 如果选择新建密钥文件，始终以 .pfx 格式创建新密钥文件  。 需要为新文件设置名称和密码。

> [!WARNING]
> 应始终使用密码保护密钥文件，以防他人使用。 还可以使用提供程序或证书存储来保护密钥。

也可以指向已创建的密钥。 有关创建密钥的详细信息，请参阅[创建公钥/私钥对](/dotnet/framework/app-domains/how-to-create-a-public-private-key-pair)。

如果仅对公钥具有访问权限，可以使用延迟签名来推迟分配密钥。 可通过选择“仅延迟签名”  复选框来启用延迟签名。 延迟签名的项目将不会运行，并且无法调试。 但是，可以通过 [Sn.exe 强名称工具](/dotnet/framework/tools/sn-exe-strong-name-tool)及 `-Vr` 选项，在开发过程中跳过验证。

有关对清单签名的详细信息，请参阅[如何：对应用程序和部署清单签名](../ide/how-to-sign-application-and-deployment-manifests.md)。

## <a name="see-also"></a>请参阅

- [具有强名称的程序集](/dotnet/framework/app-domains/strong-named-assemblies)
- [具有强名称的程序集 (C++/CLI)](/cpp/dotnet/strong-name-assemblies-assembly-signing-cpp-cli)
