---
title: 管理程序集签名和清单签名 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- manifests [Visual Studio]
- signing manifests [Visual Studio]
- application manifests [Visual Studio]
- assemblies [Visual Studio], signing
ms.assetid: 6c1ef36b-25f7-4ad0-b29a-51801b7a5420
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 98d764bae48fb7deaa3f3cf917b0d4c8baab185b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651370"
---
# <a name="managing-assembly-and-manifest-signing"></a>管理程序集签名和清单签名
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

强名称签名可为软件组件提供全局唯一标识。 使用强名称可保证程序集不被其他用户伪造，还可确保组件依赖关系和配置语句映射到正确的组件和组件版本。

 强名称是由程序集的标识加上公钥令牌和数字签名组成的。其中，程序集的标识包括简单文本名称、版本号和区域性信息。

 有关 Visual Basic 和 C# 项目中签名程序集的信息，请参阅[创建和使用具有强名称的程序集](https://msdn.microsoft.com/library/ffbf6d9e-4a88-4a8a-9645-4ce0ee1ee5f9)。

 有关 Visual C++ 项目中签名程序集的信息，请参阅[强名称程序集（程序集签名）(C++/CLI)](https://msdn.microsoft.com/library/c337cd3f-e5dd-4c6f-a1ad-437e85dba1cc)。

## <a name="asset-types-and-signing"></a>资产类型和签名
 可对 .NET 程序集和应用程序清单进行签名。 其中包括：

- 可执行文件 (.exe)

- 应用程序清单 (.exe.manifest)

- 部署清单 (.application)

- 共享组件程序集 (.dll)

  必须对以下类型的资产进行签名：

1. 程序集，如果希望将它们部署到全局程序集缓存 (GAC)。

2. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序和部署清单。 Visual Studio 默认情况下将启动对这些应用程序的签名。

3. 主互操作程序集，适用于 COM 互操作性。 从 COM 类型库中创建主互操作程序集时，TLBIMP 实用程序将强制实施强命名。

   通常不应该对可执行文件进行签名。 强命名组件无法引用与应用程序一同部署的非强命名组件。 Visual Studio 不会对应用程序可执行文件进行签名，但会对指向弱命名可执行文件的应用程序清单进行签名。 通常应避免对应用程序专用的组件进行签名，因为签名可能增加管理依赖项的难度。

## <a name="how-to-sign-an-assembly-in-visual-studio"></a>如何对 Visual Studio 中的程序集进行签名
 若要对应用程序或组件进行签名，可使用项目属性窗口中的“签名”  选项卡（在“解决方案资源管理器”  中，右键单击项目节点并选择“属性”  ，或在“快速启动”  窗口中键入 **project properties**，或在“解决方案资源管理器”  窗口中按 ALT + ENTER）。 选择“签名”  选项卡，然后选中“为程序集签名”  复选框。

 指定密钥文件。 如果选择新建密钥文件，请注意，新密钥文件始终以 .pfx 格式创建。 需要为新文件设置名称和密码。

> [!WARNING]
> 应始终使用密码保护密钥文件，以防他人使用。 还可以使用提供程序或证书存储来保护密钥。

 也可以指向已创建的密钥。 有关创建密钥的详细信息，请参阅[如何：创建公钥/私钥对](https://msdn.microsoft.com/library/05026813-f3bd-4d7c-9e0b-fc588eb3d114)。

 如果仅对公钥具有访问权限，可以使用延迟签名来推迟分配密钥。 可通过选择“仅延迟签名”  复选框来启用延迟签名。 延迟签名的项目不会运行也不能进行调试。 但是，可以使用 [Sn.exe（强名称工具）](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)及 `-Vr` 选项，在开发过程中跳过验证。

 有关对清单进行签名的详细信息，请参阅[如何：对应用程序和部署清单进行签名](../ide/how-to-sign-application-and-deployment-manifests.md)。

## <a name="see-also"></a>另请参阅
 [强名称程序集](https://msdn.microsoft.com/library/d4a80263-f3e0-4d81-9b61-f0cbeae3797b)[强名称程序集（程序集签名C++）（/cli）](https://msdn.microsoft.com/library/c337cd3f-e5dd-4c6f-a1ad-437e85dba1cc)
