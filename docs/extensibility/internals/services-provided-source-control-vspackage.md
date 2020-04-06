---
title: 提供的服务（源控制 VS 包） |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f08ebe49756b442ef474ac2a032a72894f6bec15
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705410"
---
# <a name="services-provided-source-control-vspackage"></a>提供的服务（源代码管理 VSPackage）
服务是 VS 包之间以及 Visual Studio 集成开发环境 （IDE） 及其已安装的 VS 包之间共享功能的主要机制。 有关服务及其在可视化工作室 IDE 中的重要性的详细说明，请参阅[使用和提供服务](../../extensibility/using-and-providing-services.md)。

## <a name="the-source-control-service"></a>源代码管理服务
 Visual Studio 提供两层服务，IDE 级服务和包级服务。 视觉工作室 IDE 本机提供 IDE 级服务。 源代码管理包会消耗其中一些服务。 作为 VSPackage 的源代码管理包通过提供自己的私有源代码管理服务来共享其源代码管理功能。 源代码管理包封装了它以可用于 Visual Studio IDE 的协定形式实现的源代码管理相关接口集。

## <a name="see-also"></a>请参阅
- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
