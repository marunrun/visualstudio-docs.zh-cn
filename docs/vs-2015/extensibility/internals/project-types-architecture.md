---
title: 项目类型体系结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], architecture
ms.assetid: 9c1d940f-8a54-41f7-a8aa-c870e324371c
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 775656d2190a36f62c2b047c1ff7f1e02575c1ca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68154147"
---
# <a name="project-types-architecture"></a>项目类型体系结构
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本部分包含有关中的项目类型的体系结构的详细信息 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
## <a name="in-this-section"></a>本节内容  
 [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)  
 列出项目类型可以使用的服务以及它必须实现的接口。  
  
 [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)  
 描述两个必须实现的接口项目类型，并可选择实现以提供附加功能。  
  
 [何时创建项目类型](../../extensibility/internals/when-to-create-project-types.md)  
 帮助您决定何时必须创建项目类型，以及何时可以使用其他 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 扩展性功能，如 vspackage 和编辑器来实现相同的目标。  
  
 [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)  
 介绍如何 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 使用层次结构和选择上下文来提供一致、简化的用户体验。  
  
## <a name="related-sections"></a>相关章节  
 [项目子类型](../../extensibility/internals/project-subtypes.md)  
 说明项目子类型如何允许您自定义和的项目系统的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 行为 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 。  
  
 [项目类型](../../extensibility/internals/project-types.md)  
 提供项目概述，作为集成开发环境的基本构建基块 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] (IDE) 。 向说明项目如何控制生成和编译代码的其他主题提供了链接。
