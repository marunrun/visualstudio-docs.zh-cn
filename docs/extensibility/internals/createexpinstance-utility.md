---
title: 创建实例实用程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- experimental hive
- experimental instance
- createexpinstance
- createexpinst
ms.assetid: 03779774-9401-49ae-997c-0c3ab25ed0d5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6a6b302976495e6067fad14317856cda4ac4625f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709246"
---
# <a name="createexpinstance-utility"></a>创建 ExpInstance 实用程序
使用**CreateExpInstance**实用程序创建、重置或删除 Visual Studio 的实验实例。 您可以使用实验实例调试和测试 Visual Studio 扩展，而无需更改基础产品。

## <a name="syntax"></a>语法

```
CreateExpInstance.exe [/Create | /Reset | /Clean] /VSInstance=VsInstance /RootSuffix=Suffix
```

## <a name="parameters"></a>参数
 **/创建**创建实验实例。

 **/重置**删除实验实例，然后创建新实例。

 **/清洁**删除实验实例。

 **/VS实例**包含要复制的基本 Visual Studio 实例的目录的名称。

 **/根素缀**追加到实验实例目录名称的后缀。

## <a name="remarks"></a>备注
 处理 Visual Studio 扩展时，可以按 F5 打开默认实验实例并安装当前扩展。 如果没有可用的实验实例，Visual Studio 将创建具有默认设置的实例。

 实验实例的默认位置取决于 Visual Studio 版本号。 例如，对于 Visual Studio 2015，位置为 *%localappdata%*微软_VisualStudio_14.0Exp\\*。 目录位置中的所有文件都被视为该实例的一部分。 除非目录名称更改为默认位置，否则 Visual Studio 不会加载任何其他实验实例。

 Visual Studio 打开实验实例时无法访问系统注册表。 这与早期版本的 Visual Studio 不同，后者使用注册表配置单元的实验版本。

 **CreateExpEx**实用程序取代了**VsRegEx**实用程序。

 以下示例重置 Visual Studio 的默认实验实例：

 **创建Expinstance.exe /重置/VSInstance=14.0 /RootSuffix_Exp**

## <a name="see-also"></a>请参阅
- [VSPackage](../../extensibility/internals/vspackages.md)
