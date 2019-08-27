---
title: 指定 VS Shell 的 VSPackage 文件位置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, file location
- VSPackages, managed package file location
ms.assetid: beb8607a-4183-4ed2-9ac8-7527f11513b1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 601104e484682b7db833f74a3527139ed312e731
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322452"
---
# <a name="specifying-vspackage-file-location-to-the-vs-shell"></a>指定 VS Shell 的 VSPackage 文件位置
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必须能够找到程序集 DLL 加载 VSPackage。 下表中所述，你可以多种方式找到它。

| 方法 | 描述 |
| - | - |
| 使用代码库注册表项。 | 代码库密钥可用于直接[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]从任何完全限定的文件路径加载 VSPackage 程序集。 键的值应为对 DLL 的文件路径。 这是最佳的方式有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载包程序集。 此方法有时称为"代码库/私钥安装目录技术"。 在注册过程的基本代码的值通过传递到注册特性类的实例<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.RegistrationContext>类型。 |
| 将放置到 DLL **PrivateAssemblies**目录。 | 在程序集放**PrivateAssemblies**子目录[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]目录。 程序集位于**PrivateAssemblies**将自动检测，但不是会显示在**添加引用**对话框。 之间的差异**PrivateAssemblies**并**PublicAssemblies**是程序集在**PublicAssemblies**中枚举**添加引用**对话框。 如果选择不使用"基本代码/私钥安装目录"的技术，则应安装到**PrivateAssemblies**目录。 |
| 使用强名称的程序集和程序集的注册表项。 | 程序集密钥可用于显式指示[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载强名称 VSPackage 程序集。 密钥的值应为程序集的强名称。 |
| 将放置到 DLL **PublicAssemblies**目录。 | 最后，该程序集还可放入**PublicAssemblies**子目录。 程序集位于**PublicAssemblies**自动检测到，并且也会出现在**添加引用**中的对话框[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。<br /><br /> VSPackage 程序集只应置于**PublicAssemblies**目录包含托管组件，旨在由其他 VSPackage 开发人员重复使用。 大多数程序集不符合此条件。 |

> [!NOTE]
> 使用具有强名称的所有依赖程序集签名程序集。 此外应在你自己的目录或全局程序集缓存 (GAC) 中安装这些程序集。 这样可以防止与具有相同的基本文件名称，称为弱名称绑定的程序集冲突。