---
title: 管理 VS 包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 60745d07679ae53b85d169473ed37ab314b67624
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702654"
---
# <a name="manage-vspackages"></a>管理 VSPackage
在大多数情况下，您不必担心管理 VSPackage，因为项目和项目模板会自动注册和加载包。 但是，在某些情况下，您可能需要学习更多，以便管理您的包。

## <a name="use-the-experimental-instance"></a>使用实验实例
 要了解有关实验实例的更多，请参阅[实验实例](../extensibility/the-experimental-instance.md)。

## <a name="register-and-unregister-vspackages"></a>注册和取消注册 VS 包
 要了解如何注册和取消注册 VS 包和其他类型的扩展，请参阅[注册和取消注册 VS 包](../extensibility/registering-and-unregistering-vspackages.md)。

## <a name="load-a-vspackage"></a>加载 VS 包
 VSPackages 可以设置为打开特定 CMDUICONTEXT GUID 时自动加载。 有关详细信息，请参阅加载[VS 包](../extensibility/loading-vspackages.md)。

## <a name="use-asyncpackage-to-load-vspackages-in-the-background"></a>使用异步包在后台加载 VS 包
 该`AsyncPackage`类允许在后台线程上加载包，从而在 Visual Studio 中实现更好的 UI 响应。 有关详细信息，请参阅[：使用异步包在后台加载 VS 包](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)。

## <a name="rule-based-ui-context-for-extensions"></a>扩展的基于规则的 UI 上下文
 基于规则的 UI 上下文允许扩展作者定义激活 UI 上下文并加载关联的 VS 包的确切条件。 有关详细信息，请参阅[操作操作：对可视化工作室扩展使用基于规则的 UI 上下文](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)。

## <a name="diagnose-extension-performance"></a>诊断扩展性能
扩展可能会影响启动和解决方案加载性能。 了解如何计算 Visual Studio 扩展影响，以及如何在本地对其进行分析，以测试扩展是否可以显示为影响扩展的性能。 有关详细信息，请参阅[如何：诊断扩展性能](how-to-diagnose-extension-performance.md)。

## <a name="troubleshoot-vspackages"></a>排除 VS 包故障
 了解对未加载或遇到错误的 VS 包进行故障排除的技术：[对 VSPackages 进行故障排除](../extensibility/troubleshooting-vspackages.md)

## <a name="see-also"></a>请参阅
- [VSPackage](../extensibility/internals/vspackages.md)
