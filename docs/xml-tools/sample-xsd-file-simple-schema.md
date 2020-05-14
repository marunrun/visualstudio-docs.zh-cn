---
title: 示例 XSD 文件：简单架构
ms.date: 11/04/2016
ms.topic: sample
ms.assetid: f7e1dde1-b4f6-4371-add4-935b68ec77d7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 788de9f31a58561aa743d6ca6286ef650f4297a4
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "75592537"
---
# <a name="sample-xsd-file-simple-schema"></a>示例 XSD 文件：简单架构

以下 XSD 文件用在 XSD 架构设计器文档中的各个示例中。 此文件是一个简单的订单架构。

```xml
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"
           xmlns:tns="http://tempuri.org/PurchaseOrderSchema.xsd"
           targetNamespace="http://tempuri.org/PurchaseOrderSchema.xsd"
           elementFormDefault="qualified">
 <xsd:element name="PurchaseOrder" type="tns:PurchaseOrderType"/>
 <xsd:complexType name="PurchaseOrderType">
  <xsd:sequence>
   <xsd:element name="ShipTo" type="tns:USAddress" maxOccurs="2"/>
   <xsd:element name="BillTo" type="tns:USAddress"/>
  </xsd:sequence>
  <xsd:attribute name="OrderDate" type="xsd:date"/>
 </xsd:complexType>

 <xsd:complexType name="USAddress">
  <xsd:sequence>
   <xsd:element name="name"   type="xsd:string"/>
   <xsd:element name="street" type="xsd:string"/>
   <xsd:element name="city"   type="xsd:string"/>
   <xsd:element name="state"  type="xsd:string"/>
   <xsd:element name="zip"    type="xsd:integer"/>
  </xsd:sequence>
  <xsd:attribute name="country" type="xsd:NMTOKEN" fixed="US"/>
 </xsd:complexType>
</xsd:schema>
```

> [!NOTE]
> 此处描述的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构。 我们无意将它们与任何真实的公司、单位、产品、域名、电子邮件地址、徽标、人员、地点或事件挂钩，请勿“对号入座”。
