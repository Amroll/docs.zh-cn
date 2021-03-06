---
title: "后期绑定重载解决方法不能应用于 &#39;&lt;过程名称&gt;&#39; 因为访问实例是一个接口类型"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30933
- bc30933
helpviewer_keywords:
- overload resolution [Visual Basic], with late-bound argument
- BC30933
ms.assetid: 8182eea0-dd34-4d6e-9ca0-41d8713e9dc4
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: fb7f8a9f6eadfc9fd856ea57d362b43d25ff81a1
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="latebound-overload-resolution-cannot-be-applied-to-39ltprocedurenamegt39-because-the-accessing-instance-is-an-interface-type"></a>后期绑定重载解决方法不能应用于 &#39;&lt;过程名称&gt;&#39; 因为访问实例是一个接口类型
编译器正在尝试解析的引用的重载的属性或过程，但引用失败，因为自变量的类型`Object`和引用的对象具有接口的数据类型。 `Object`参数强制编译器将引用解析为后期绑定。  
  
 在这些情况下，编译器将解析通过实现类而不是通过基础接口的重载。 如果类重命名其中一个重载版本，则编译器不考虑该版本为重载，因为其名称不同。 这反过来会使编译器忽略重命名的版本时可能已正确的选择来解析引用。  
  
 **错误 ID:** BC30933  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   使用`CType`转换从参数`Object`到你想要调用的重载的签名由指定的类型。  
  
     请注意，它没有任何帮助引用将对象转换为基础的接口。 您必须强制转换的自变量，若要避免此错误。  
  
## <a name="example"></a>示例  
 下面的示例演示对重载的调用`Sub`会在编译时导致此错误的过程。  
  
```  
Module m1  
    Interface i1  
        Sub s1(ByVal p1 As Integer)  
        Sub s1(ByVal p1 As Double)  
    End Interface  
    Class c1  
        Implements i1  
        Public Overloads Sub s1(ByVal p1 As Integer) Implements i1.s1  
        End Sub  
        Public Overloads Sub s2(ByVal p1 As Double) Implements i1.s1  
        End Sub  
    End Class  
    Sub Main()  
        Dim refer As i1 = New c1  
        Dim o1 As Object = 3.1415  
        ' The following reference is INVALID and causes a compiler error.  
        refer.s1(o1)   
    End Sub  
End Module  
```  
  
 在前面的示例中，如果编译器允许调用`s1`顾名思义，解析将通过类`c1`而不是接口`i1`。 这就意味着编译器不会考虑`s2`因为其名称中不同`c1`，即使它是正确的选择，因为由定义`i1`。  
  
 可以通过更改为以下代码行的任何一调用来更正该错误：  
  
```  
refer.s1(CType(o1, Integer))  
refer.s1(CType(o1, Double))  
```  
  
 每个前面几行代码显式强制转换`Object`变量`o1`为重载定义的参数类型之一。  
  
## <a name="see-also"></a>另请参阅  
 [过程重载](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)  
 [重载决策](../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)  
 [CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md)
