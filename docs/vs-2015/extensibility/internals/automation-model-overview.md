---
title: 自动化模型概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], about automation
- extensibility
ms.assetid: 12b6d6db-0d22-4aaa-aa7d-1365f759b7b0
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e17164976062ec916074c6210be6ae42e8ea1d03
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699513"
---
# <a name="automation-model-overview"></a>自动化模型概述
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

自动化模型包含一组可以对其编写的 Visual Studio 外接程序或扩展的对象。 外接程序是可以操作在 Visual Studio 环境，并自动执行常见任务的应用程序。 Visual Studio 扩展可以创建自定义 Visual Studio 组件或添加到标准组件，如文本编辑器功能。  
  
## <a name="objects-in-the-automation-model"></a>自动化模型中的对象  
 自动化模型包含相关组来控制的常见环境的主要方面的对象。 下面是图显示了大量的编写自动化模型的对象。  
  
 ![Visual Studio 自动化对象图](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "vsVisualStudioAutomationObjectChart")  
Visual Studio 自动化对象  
  
 有关详细信息，请参阅[扩展 Visual Studio 环境](https://msdn.microsoft.com/library/4173a963-7ac7-4966-9bb7-e28a9d9f6792)。  
  
 在环境用于不同功能区域中提供了模型。 例如，是您可能会发现代码中的各种元素的代码模型。 没有文档模型的各种文档元素。 一个区域中，项目区域中，是对 VSPackage 提供程序特定的感兴趣。 你可能想在新的项目类型以参与自动化模型，方法与大致相同[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]参与自动化模型。 过程所示[提供的 Vspackage 的自动化](../../extensibility/internals/providing-automation-for-vspackages.md)。  
  
 你可以考虑扩展环境的自动化模型的位置：  
  
- 项目  
  
- Document  
  
- 代码  
  
- Build  
  
  自动化的详细信息，请参阅[的 Visual Studio 自动化和扩展性](https://msdn.microsoft.com/library/f71a2253-3e68-4e5e-9a18-edbba816caf6)。 本文档和文档，它提供了链接，帮助你做出决定，你应如何提供你的 VSPackage 的自动化。  
  
## <a name="see-also"></a>请参阅  
 [如何：创建的外接程序](https://msdn.microsoft.com/library/50be56d2-e3a5-4cd2-8569-2a0666b268ce)
