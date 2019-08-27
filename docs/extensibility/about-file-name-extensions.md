---
title: 有关文件扩展名 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 60a721581c3deb4588df59974768c634c2e9515f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66313720"
---
# <a name="about-file-name-extensions"></a>有关文件扩展名
当你注册 VSPackage 的文件扩展名时，您将其与关联的版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 这是重要如果多个是的一个版本[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]的计算机上安装。

 下注册 Vspackage 的文件扩展名**HKEY_CLASSES_ROOT**键，其默认值指向关联的编程标识符 (ProgID)。

 下面的示例演示的注册信息 *.vcproj*文件扩展名：

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)=" VisualStudio.vcproj.8.0"
```

 与关联的文件[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]必须具有版本控制的 ProgID，如`VisualStudio.vcproj.8.0`。 版本控制的 ProgID 允许要维护产品版本间的文件扩展名关联的产品通过并行安装。 特定于版本的 ProgID 还可以使用标准动词，如打开、 编辑和在其他方面，而无需考虑的覆盖或其他应用程序或版本的覆盖[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

 在某些情况下，不应更改与文件扩展名相关联的 ProgID。 例如，对于 ProgID *.htm*文件扩展名 (progid = htmlfile) 中的许多操作系统中的位置进行硬编码，与广泛已知和已用在关联 *.htm*和 *.html*文件。

## <a name="see-also"></a>请参阅
- [注册文件扩展名为通过并行部署](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [指定文件扩展名的文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md)