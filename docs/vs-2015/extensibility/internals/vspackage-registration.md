---
title: VSPackage 注册 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: ecd20da8-b04b-4141-a8f4-a2ef91dd597a
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a11f05edb4e7d476fdbcab82d365f9327dd4869a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685286"
---
# <a name="vspackage-registration"></a>VSPackage 注册
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Vspackage 必须告知[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]他们安装，并应被加载。 通过在注册表中写入信息来完成此过程。 这是安装程序的典型的作业。  
  
> [!NOTE]
> 已接受的做法是在使用自助注册 VSPackage 开发过程。 但是，[!INCLUDE[vsipprvsip](../../includes/vsipprvsip-md.md)]合作伙伴，无法提供其产品作为安装的一部分使用自助注册。  
  
 在 Windows 安装程序包的注册表项通常由注册表表中。 您还可以在注册表表注册文件扩展名。 但是，Windows Installer 提供了内置支持通过编程标识符 (ProgId)、 类、 扩展和谓词表。 有关详细信息，请参阅[数据库表](https://msdn.microsoft.com/library/aa368259\(VS.85\).aspx)。  
  
 请确保你的注册表条目是与适用于你所选的并行策略的组件相关联。 例如，共享文件的注册表项应与该文件的 Windows 安装程序组件相关联。 同样，特定于版本的文件的注册表项应与该文件的组件相关联。 否则为安装或卸载你的 VSPackage 的某个版本的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]可能会在其他版本中中断你的 VSPackage。 有关详细信息，请参阅[支持多个 Visual Studio 版本](../../extensibility/supporting-multiple-versions-of-visual-studio.md)  
  
> [!NOTE]
> 管理注册的最简单方法是在同一文件中进行开发者注册和安装时间注册使用相同的数据。 例如，某些安装程序开发工具可以在生成时使用.reg 格式文件中。 如果开发人员维护.reg 文件进行日常开发和调试，这些相同的文件可以包含在安装程序自动。 如果您不能自动共享注册数据，则必须确保安装程序的副本的注册数据是最新。  
  
## <a name="registering-unmanaged-vspackages"></a>注册非托管的 Vspackage  
 （包括那些由 Visual Studio 包模板生成） 的非托管的 Vspackage 使用 ATL 样式.rgs 文件来存储注册信息。 .Rgs 文件格式是特定于 ATL 并通常不能用作-通过创作工具的安装。 VSPackage 安装程序的注册信息必须单独进行维护。 例如，开发人员可以保留文件以.reg 格式与.rgs 同步文件更改。 可以为开发工作与 RegEdit 合并或由安装程序使用.reg 文件。  
  
## <a name="registering-managed-vspackages"></a>注册托管的 Vspackage  
 RegPkg 工具读取从托管的 VSPackage 注册属性和可以是信息直接写入注册表或可供安装程序的写.reg 格式文件。  
  
> [!NOTE]
> RegPkg 工具不是可再发行组件，并不能用于注册用户的系统上的 VSPackage。  
  
## <a name="why-vspackages-should-not-self-register-at-install-time"></a>为什么 Vspackage 不应自行注册在安装时  
 VSPackage 安装程序不应依赖于自注册。 第一次看到仅在 VSPackage 本身中保留的 VSPackage 的注册表值看起来是个好主意。 提供有关其日常工作的开发人员需要可用的注册表值和测试，最好避免维护单独的安装程序中的注册表数据副本。 安装程序可以依赖于 VSPackage 本身可以写入注册表值。  
  
 虽然从理论上讲适用，自注册有几个缺点，使其不适合 VSPackage 安装：  
  
- 正确支持安装、 卸载、 安装回滚和卸载回滚需要你编写为通过调用 RegPkg 自我注册每个托管 VSPackage 的四个自定义操作。  
  
- 方法的-同时支持可能需要您编写的每个受支持的版本调用 RegSvr32 或 RegPkg 的四个自定义操作[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
- 不能安全地回滚与自助注册的模块的安装，因为没有告诉自行注册的密钥由另一个功能或应用程序的方法。  
  
- 自助注册的 Dll 有时链接到不存在或版本有错误的辅助 Dll。 与此相反，Windows 安装程序可以注册使用此注册表表而不依赖于系统的当前状态的 Dll。  
  
- 自注册代码可以对其拒绝访问网络资源，例如类型库中，如果一个组件是同时指定为运行从源和 SelfReg 表中列出。 这会导致要在管理安装过程中失败的组件安装。  
  
## <a name="see-also"></a>请参阅  
 [Windows 安装程序](https://msdn.microsoft.com/library/cc185688\(VS.85\).aspx)   
 [托管的包注册](https://msdn.microsoft.com/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)
