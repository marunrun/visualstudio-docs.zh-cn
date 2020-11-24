---
title: 关于文件扩展名 |Microsoft Docs
description: 了解如何为 Vspackage 注册文件扩展名，并将其与 Visual Studio 的特定版本相关联。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 9ef0c942e88c10b4f814dc103702edc08229fb9b
ms.sourcegitcommit: d6207a3a590c9ea84e3b25981d39933ad5f19ea3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/24/2020
ms.locfileid: "95597660"
---
# <a name="about-file-name-extensions"></a>关于文件扩展名
注册 VSPackage 的文件扩展名时，可以将其与的版本相关联 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 如果在计算机上安装了多个版本的，则这一点非常重要 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

 Vspackage 的文件扩展名在 **HKEY_CLASSES_ROOT** 键下注册，其默认值指向关联的编程标识符 (ProgID) 。

 下面的示例显示了 *vcproj* 文件扩展名的注册信息：

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)=" VisualStudio.vcproj.8.0"
```

 与关联的文件 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 必须具有一个版本控制的 ProgID，如 `VisualStudio.vcproj.8.0` 。 版本控制的 ProgID 允许并行安装产品以维护产品版本之间的文件扩展名关联。 使用版本特定的 ProgID，还可以使用标准谓词（如 "打开"、"编辑" 等），而无需考虑覆盖或被其他应用程序或版本覆盖的问题 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

 在某些情况下，不应更改与文件扩展名关联的 ProgID。 例如，在操作系统中的多个位置对 *.htm* 文件扩展名 (progid = htmlfile) 进行硬编码，这是众所周知的，并与 *.htm* 和 *.html* 文件关联。

## <a name="see-also"></a>另请参阅
- [为并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [指定文件扩展名的文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
