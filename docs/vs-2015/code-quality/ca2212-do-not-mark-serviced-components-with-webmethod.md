---
title: CA2212：不通过 WebMethod 标记服务组件 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a3c707fef5562b932b6232300131f6e6e6efef6a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534558"
---
# <a name="ca2212-do-not-mark-serviced-components-with-webmethod"></a>CA2212:不要使用 WebMethod 标记服务组件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DoNotMarkServicedComponentsWithWebMethod|
|CheckId|CA2212|
|Category|Microsoft. 使用情况|
|是否重大更改|重大|

## <a name="cause"></a>原因
 从继承的类型中的方法 <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName> 使用进行标记 <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 <xref:System.Web.Services.WebMethodAttribute>适用于使用 ASP.NET 创建的 XML Web service 中的方法;它使方法可从远程 Web 客户端调用。 方法和类必须是公共的并在 ASP.NET Web 应用程序中执行。 <xref:System.EnterpriseServices.ServicedComponent>类型由 COM + 应用程序托管，可以使用 COM + 服务。 <xref:System.Web.Services.WebMethodAttribute>不应用于 <xref:System.EnterpriseServices.ServicedComponent> 类型，因为它们并非适用于相同的方案。 具体而言，将特性添加到 <xref:System.EnterpriseServices.ServicedComponent> 方法不会使方法从远程 Web 客户端调用。 由于 <xref:System.Web.Services.WebMethodAttribute> 和 <xref:System.EnterpriseServices.ServicedComponent> 方法与上下文和事务流的行为和要求存在冲突，因此该方法的行为在某些情况下会不正确。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请从方法中删除该特性 <xref:System.EnterpriseServices.ServicedComponent> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 在这种情况下，组合这些元素是正确的。

## <a name="see-also"></a>另请参阅
 <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName> <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>
