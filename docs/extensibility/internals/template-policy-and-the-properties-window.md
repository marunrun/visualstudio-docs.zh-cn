---
title: 模板策略和属性窗口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Properties window, template policy
ms.assetid: 1d8019d3-5e57-47ba-b358-526b0796a63b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 08ed6f416441d06767661e63b5e32454dbe07f93
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704667"
---
# <a name="template-policy-and-the-properties-window"></a>模板策略和属性窗口
当项目包含在企业模板项目中时，该企业模板项目可以强制执行策略。 模板策略成为约束系统，可用于设置属性的默认值、隐藏属性、添加属性等。

 使用模板策略来控制**属性窗口中信息**的显示与实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>不同。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>在组件级别处理对象属性，而模板策略可用于在解决方案或项目级别约束对象属性。 换句话说

- 实现 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>，以确定特定对象的 **"属性"** 窗口中显示的内容

- 在解决方案和项目级别使用模板策略来确定以前指定对象的 **"属性"** 窗口中显示的内容

  在**解决方案资源管理器**中选择指定类型的项目项时，使用模板策略有选择地约束**属性**窗口中的特定属性，这对处理项目的开发团队的所有成员都是有益的。 例如，使用模板策略，可以为开发人员设置数据库中的所有连接字符串信息，并使连接字符串为只读。 通过这种方式，您可以提供一种简单的方法来确保每个开发人员使用正确的路径进行数据访问。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>
- [扩展属性](../../extensibility/internals/extending-properties.md)
