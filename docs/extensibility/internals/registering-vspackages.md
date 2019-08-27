---
title: 注册 Vspackage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, registering
- registration, managed VSPackages
ms.assetid: 79b9424e-7e9b-4fc8-9b9f-00212674573c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1ac51f23132d855c3da921cc2743c3064a353524
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331321"
---
# <a name="registering-vspackages"></a>注册 VSPackage
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 依赖于要描述和定位 VSPackage 的.pkgdef 文件。 .Pkgdef 文件包含否则会添加到系统注册表的所有注册信息。 通过将属性添加到源代码，然后运行注册托管的 Vspackage [CreatePkgDef 实用工具](../../extensibility/internals/createpkgdef-utility.md)上生成的程序集生成.pkgdef 文件。

## <a name="in-this-section"></a>本节内容
- [指定 VS Shell 的 VSPackage 文件位置](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)

 介绍 Vspackage 的加载路径。

- [注册和注销 Vspackage](../../extensibility/registering-and-unregistering-vspackages.md)

 介绍如何注册 VSPackage。
