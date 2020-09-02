---
title: '&lt;&gt; (ClickOnce 部署) 的 g 元素 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <customErrorReporting> element [ClickOnce deployment manifest]
ms.assetid: 7d31816e-c692-46b5-9cc9-753284b3bcda
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d42bd1f7304d9f50b6334d9ac8ddd4f626605d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62900366"
---
# <a name="ltcustomerrorreportinggt-element-clickonce-deployment"></a>&lt;&gt; (ClickOnce 部署的 g 元素) 
指定发生错误时所显示的 URI。

## <a name="syntax"></a>语法

```xml
<customErrorReporting
   uri
/>
```

## <a name="remarks"></a>备注
 此元素为可选元素。 如果没有该属性，则会 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 显示一个错误对话框，其中显示异常堆栈。 如果该 `customErrorReporting` 元素存在， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 则将改为显示由参数指示的 URI `uri` 。 目标 URI 将包括外部异常类、内部异常类和内部异常消息作为参数。

 使用此元素可将错误报告功能添加到应用程序。 由于生成的 URI 包含有关错误类型的信息，因此您的网站可以分析该信息并显示，例如，相应的故障排除屏幕。

## <a name="example"></a>示例
 以下代码片段显示了 `customErrorReporting` 元素以及它可能生成的 URI。

```xml
<customErrorReporting uri=http://www.contoso.com/applications/error.asp />

Example Generated Error:
http://www.contoso.com/applications/error.asp? outer=System.Deployment.Application.InvalidDeploymentException&&inner=System.Deployment.Application.InvalidDeploymentException&&msg=The%20application%20manifest%20is%20signed,%20but%20the%20deployment%20manifest%20is%20unsigned.%20Both%20manifests%20must%20be%20either%20signed%20or%20unsigned.
```

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)