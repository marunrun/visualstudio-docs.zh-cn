---
title: 用于创建单元测试的示例项目 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit test sample [Visual Studio]
- unit tests, samples
ms.assetid: db80aaf2-0652-4d3f-a8c5-2a98fd8502a2
caps.latest.revision: 32
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d495d0bf12c900d34a04a84e950b002494b7b5c3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660399"
---
# <a name="sample-project-for-creating-unit-tests"></a>用于创建单元测试的示例项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

提供此示例代码用于下面的演练：

- [演练：创建并运行托管代码的单元测试](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)。 本演练将引导你完成创建和自定义单元测试、运行它们以及检查测试结果的步骤。

- [演练：运行测试并查看代码覆盖率](https://msdn.microsoft.com/d4aab8e2-2140-4975-b4e3-41ef3fa944c8)。 本演练演示了如何查看代码覆盖率数据，这显示了所测试的项目代码的比例。

- [演练：使用命令行测试实用工具](https://msdn.microsoft.com/library/52c11992-9e94-4067-a4b7-59f19d69d867)。 在本演练中，你可以使用 MSTest.exe 命令行实用工具运行测试和查看结果。

## <a name="sample-code"></a>代码示例
 在此示例中唯一的有意错误是，Debit 方法“m_balance += amount”的等号之前应有减号而不是加号。

```
using System;

namespace BankAccountNS
{
    /// <summary>
    /// Bank Account demo class.
    /// </summary>
    public class BankAccount
    {
        private string m_customerName;

        private double m_balance;

        private bool m_frozen = false;

        private BankAccount()
        {
        }

        public BankAccount(string customerName, double balance)
        {
            m_customerName = customerName;
            m_balance = balance;
        }

        public string CustomerName
        {
            get { return m_customerName; }
        }

        public double Balance
        {
            get { return m_balance; }
        }

        public void Debit(double amount)
        {
            if (m_frozen)
            {
                throw new Exception("Account frozen");
            }

            if (amount > m_balance)
            {
                throw new ArgumentOutOfRangeException("amount");
            }

            if (amount < 0)
            {
                throw new ArgumentOutOfRangeException("amount");
            }

            m_balance += amount; // intentionally incorrect code
        }

        public void Credit(double amount)
        {
            if (m_frozen)
            {
                throw new Exception("Account frozen");
            }

            if (amount < 0)
            {
                throw new ArgumentOutOfRangeException("amount");
            }

            m_balance += amount;
        }

        private void FreezeAccount()
        {
            m_frozen = true;
        }

        private void UnfreezeAccount()
        {
            m_frozen = false;
        }

        public static void Main()
        {
            BankAccount ba = new BankAccount("Mr. Bryan Walton", 11.99);

            ba.Credit(5.77);
            ba.Debit(11.22);
            Console.WriteLine("Current balance is ${0}", ba.Balance);
        }

    }
}
```

 /* 此处描述的示例公司、组织、产品、域名、电子邮件地址、徽标、人员、地点和事件均属虚构。  无意与任何真实的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点或事件相关联，也不应进行这方面的推断。 \*/

## <a name="working-with-the-code"></a>使用代码
 若要使用这些代码，您必须首先在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中为其创建一个项目。 按照[演练：创建并运行托管代码的单元测试](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)中“准备演练”部分所述的步骤操作。

## <a name="see-also"></a>请参阅
 [演练：创建并运行托管代码的单元测试](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)[演练：运行测试并查看代码覆盖率](https://msdn.microsoft.com/d4aab8e2-2140-4975-b4e3-41ef3fa944c8)[演练：使用命令行测试实用工具](https://msdn.microsoft.com/library/52c11992-9e94-4067-a4b7-59f19d69d867)
