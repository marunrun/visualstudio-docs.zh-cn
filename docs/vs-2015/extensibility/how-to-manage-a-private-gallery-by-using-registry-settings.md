---
title: 如何：使用注册表设置管理专用库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a55b7aa486edfd3775b12dca9d143c2e5f280884
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204155"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>如何：通过使用注册表设置管理专用库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你是独立 Shell 扩展的管理员或开发人员，则可以在 Visual Studio 库、示例库或专用库中控制对控件、模板和工具的访问。 若要使库可用或不可用，请创建一个描述修改后的注册表项及其值的 .pkgdef 文件。  
  
## <a name="managing-private-galleries"></a>管理专用库  
 你可以创建一个 .pkgdef 文件来控制对多台计算机上的库的访问。 此文件必须采用以下格式。  
  
```  
[$RootPath$\ExtensionManager\Repositories\{UniqueGUID}]  
@={URI}  (REG_SZ)  
Disabled=0 | 1 (DWORD)  
Priority=0 (highest priority) … MaxInt (lowest priority) (DWORD) (uint)  
Protocol=Atom Feed|Sharepoint (REG_SZ)  
DisplayName={DisplayName} (REG_SZ)  
DisplayNameResourceID={ID} (REG_SZ)  
DisplayNamePackageGuid={GUID} (REG_SZ)  
  
```  
  
 `Repositories`键指的是要启用或禁用的库。 Visual Studio 库和示例库使用以下存储库 Guid：  
  
- Visual Studio 库：0F45E408-7995-4375-9485-86B8DB553DC9  
  
- 示例库： AEB9CB40-D8E6-4615-B52C-27E307F8506C  
  
  `Disabled`该值是可选的。 默认情况下，库处于启用状态。  
  
  `Priority`值决定了库在 "选项" 对话框中的列出顺序。 Visual Studio 库的优先级为10，示例库的优先级为20。 专用库的优先级为100。 如果有多个库具有相同的优先级值，则它们出现的顺序取决于其本地化特性的值 `DisplayName` 。  
  
  此 `Protocol` 值是基于 Atom 或基于 SharePoint 的库所必需的。  
  
  `DisplayName`必须指定，或者 `DisplayNameResourceID` 同时 `DisplayNamePackageGuid` 指定和。 如果指定 all，则 `DisplayNameResourceID` `DisplayNamePackageGuid` 使用和对。  
  
## <a name="disabling-the-visual-studio-gallery-using-a-pkgdef-file"></a>使用 .pkgdef 文件禁用 Visual Studio 库  
 您可以在 .pkgdef 文件中禁用库。 以下条目禁用 Visual Studio 库：  
  
```  
[$RootPath$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]  
"Disabled"=dword:00000001  
  
```  
  
 以下项将禁用示例库：  
  
```  
[$RootPath$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]  
"Disabled"=dword:00000001  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Private Galleries](../extensibility/private-galleries.md)
