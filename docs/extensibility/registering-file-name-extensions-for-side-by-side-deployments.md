---
title: 注册并行部署的文件名扩展名 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions, registering for side-by-side
ms.assetid: 9ab046a2-147d-4167-aa14-7d661b1eaaa5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6717625a44b48a25d293f68d01cd9fa3c7c24853
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701540"
---
# <a name="register-file-name-extensions-for-side-by-side-deployments"></a>注册并行部署的文件名扩展名
对于并行环境中部署的 VSPackages，必须注册文件名扩展名，才能将文件与 的正确版本相关联[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 除非使用特定于版本的文件名扩展名，否则注册使用户能够在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]相应的版本中打开项目和项目项目文件。

## <a name="in-this-section"></a>在本节中
- [关于文件名扩展名](../extensibility/about-file-name-extensions.md)讨论如何注册文件名扩展名。

- [为文件名扩展名指定文件处理程序](../extensibility/specifying-file-handlers-for-file-name-extensions.md)提供有关如何注册可以打开、编辑等特定文件名扩展名的应用程序的信息。

- [注册文件名扩展名的谓词](../extensibility/registering-verbs-for-file-name-extensions.md)讨论如何注册动词。

- [管理并行文件关联](../extensibility/managing-side-by-side-file-associations.md)讨论如何并行处理应调用 的特定[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]版本的安装来打开文件。

## <a name="related-sections"></a>相关章节
- [支持多个版本的可视化工作室](../extensibility/supporting-multiple-versions-of-visual-studio.md)描述在开发和部署到最终用户期间与[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]多个版本和 VSPackage 相关的问题。
