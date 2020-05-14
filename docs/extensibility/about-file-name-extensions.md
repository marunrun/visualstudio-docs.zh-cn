---
title: 关于文件名扩展名 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03e07ec233ef975441a1f10507f0db872051558f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740355"
---
# <a name="about-file-name-extensions"></a>关于文件名扩展名
注册 VSPackage 的文件扩展名时，将其与 的版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]相关联。 如果计算机上安装了多个版本的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]

 VS包的文件扩展名在**HKEY_CLASSES_ROOT**键下注册，默认值指向关联的编程标识符 （ProgID）。

 下面的示例显示 *.vcproj*文件扩展名的注册信息：

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)=" VisualStudio.vcproj.8.0"
```

 与 关联的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]文件必须具有版本化的 ProgID，`VisualStudio.vcproj.8.0`如 。 版本化 ProgID 允许产品并行安装，以维护产品版本之间的文件扩展关联。 特定于版本的 ProgID 还允许您使用标准谓词（如打开、编辑等），而无需担心覆盖或被 其他应用程序或版本覆盖[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

 在某些情况下，不应更改与文件扩展名关联的 ProgID。 例如 *，.htm*文件扩展名（progid = htmlfile）的 ProgID 在操作系统中的多个位置进行硬编码，并且与 *.htm*和 *.html*文件关联广为人知和使用。

## <a name="see-also"></a>请参阅
- [注册并行部署的文件名扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [为文件名扩展名指定文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
