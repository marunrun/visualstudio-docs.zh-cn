---
title: CA2212:不要使用 WebMethod 标记服务组件
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2212
- DoNotMarkServicedComponentsWithWebMethod
helpviewer_keywords:
- CA2212
- DoNotMarkServicedComponentsWithWebMethod
ms.assetid: 774bc55d-e588-48ee-8f38-c228580feca2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7b2ace5f6e51fc7a8d29faab14cc2332fd808f93
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231658"
---
# <a name="ca2212-do-not-mark-serviced-components-with-webmethod"></a>CA2212:不要使用 WebMethod 标记服务组件

|||
|-|-|
|TypeName|DoNotMarkServicedComponentsWithWebMethod|
|CheckId|CA2212|
|类别|Microsoft.Usage|
|重大更改|重大|

## <a name="cause"></a>原因

从<xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName>继承的类型中的方法使用<xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>进行标记。

## <a name="rule-description"></a>规则说明

<xref:System.Web.Services.WebMethodAttribute>适用于 XML web services 中使用 ASP.NET 创建的方法;它使方法可从远程 web 客户端调用。 方法和类必须是公共的并在 ASP.NET web 应用程序中执行。 <xref:System.EnterpriseServices.ServicedComponent>类型由 COM + 应用程序托管，可以使用 COM + 服务。 <xref:System.Web.Services.WebMethodAttribute>不应用于<xref:System.EnterpriseServices.ServicedComponent>类型，因为它们并非适用于相同的方案。 具体而言，将特性添加到<xref:System.EnterpriseServices.ServicedComponent>方法不会使方法从远程 web 客户端调用。 <xref:System.Web.Services.WebMethodAttribute> 由于<xref:System.EnterpriseServices.ServicedComponent>和方法与上下文和事务流的行为和要求存在冲突，因此该方法的行为在某些情况下会不正确。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请从<xref:System.EnterpriseServices.ServicedComponent>方法中删除该特性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 在这种情况下，组合这些元素是正确的。

## <a name="see-also"></a>请参阅

- <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName>
- <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>