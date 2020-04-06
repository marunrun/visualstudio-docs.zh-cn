---
title: 将 VS 包文件位置指定给 VS 外壳 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, file location
- VSPackages, managed package file location
ms.assetid: beb8607a-4183-4ed2-9ac8-7527f11513b1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f112da4e79bff06d12472f0af7a3fe47b2f25da4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704981"
---
# <a name="specifying-vspackage-file-location-to-the-vs-shell"></a>指定 VS Shell 的 VSPackage 文件位置
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]必须能够定位程序集 DLL 以加载 VS 包。 您可以以各种方式找到它，如下表所述。

| 方法 | 描述 |
| - | - |
| 使用 CodeBase 注册表项。 | CodeBase 密钥可用于从任何完全限定[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的文件路径直接加载 VSPackage 程序集。 键的值应该是 DLL 的文件路径。 这是加载[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]包程序集的最佳方式。 此技术有时称为"CodeBase/私有安装目录技术"。 在注册期间，代码库的值通过<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.RegistrationContext>类型的实例传递给注册属性类。 |
| 将 DLL 放入**私有程序集**目录中。 | 将程序集放在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]目录的**私有程序集**子目录中。 将自动检测到**位于私有程序集中的程序集**，但在 **"添加引用**"对话框中不可见。 **私有程序集**和**公共程序集**之间的区别是，在 **"添加引用"** 对话框中枚举**公共程序集中的程序集**。 如果您选择不使用"CodeBase/私有安装目录"技术，则应安装到**PrivateAssemblies**目录中。 |
| 使用强命名的程序集和程序集注册表项。 | 程序集键可用于显式定向[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载强命名的 VSPackage 程序集。 键的值应为程序集的强名称。 |
| 将 DLL 放入**公共程序集**目录中。 | 最后，程序集也可以放置在**公共程序集**子目录中。 自动检测位于**公共程序集中的程序集**，并且也会显示在 中的 **"添加引用"** 对话框中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。<br /><br /> 仅当 VSPackage 程序集包含旨在供其他 VSPackage 开发人员重用的托管组件时，才应将其放在**PublicAssemblies**目录中。 大多数程序集不符合此条件。 |

> [!NOTE]
> 对所有从属程序集使用强命名、签名程序集。 这些程序集也应安装在您自己的目录或全局程序集缓存 （GAC） 中。 这样可以防止与具有相同基本文件名（称为弱名绑定）的程序集发生冲突。
