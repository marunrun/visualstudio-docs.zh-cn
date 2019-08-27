---
title: CA2212:不要将标记服务的组件使用 WebMethod |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2212
- DoNotMarkServicedComponentsWithWebMethod
helpviewer_keywords:
- CA2212
- DoNotMarkServicedComponentsWithWebMethod
ms.assetid: 774bc55d-e588-48ee-8f38-c228580feca2
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6f2e89705e36407e39103296e3eee70482e3d03f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142486"
---
# <a name="ca2212-do-not-mark-serviced-components-with-webmethod"></a>CA2212:不要使用 WebMethod 标记服务组件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotMarkServicedComponentsWithWebMethod|
|CheckId|CA2212|
|类别|Microsoft.Usage|
|是否重大更改|重大|

## <a name="cause"></a>原因
 继承的类型中的方法<xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName>将标有<xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>。

## <a name="rule-description"></a>规则说明
 <xref:System.Web.Services.WebMethodAttribute> 适用于使用 ASP.NET; 创建的 XML Web 服务中的方法它使该方法可调用从远程 Web 客户端。 方法和类必须是公共且在 ASP.NET Web 应用程序执行。 <xref:System.EnterpriseServices.ServicedComponent> 类型由 COM + 应用程序承载，可以使用 COM + 服务。 <xref:System.Web.Services.WebMethodAttribute> 不应用于<xref:System.EnterpriseServices.ServicedComponent>类型，因为它们不用相同的方案。 具体而言，将添加到属性<xref:System.EnterpriseServices.ServicedComponent>方法不会使该方法可调用从远程 Web 客户端。 因为<xref:System.Web.Services.WebMethodAttribute>和一个<xref:System.EnterpriseServices.ServicedComponent>方法具有冲突的行为和要求的上下文和事务流，该方法的行为会在某些情况下不正确。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请删除中的特性<xref:System.EnterpriseServices.ServicedComponent>方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 在任何的情况都其中组合这些元素正确。

## <a name="see-also"></a>请参阅
 <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName> <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>
