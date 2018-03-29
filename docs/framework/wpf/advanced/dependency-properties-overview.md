---
title: "依赖项属性概述"
description: "由 WPF 属性系统支持的属性称为依赖项属性。 本概述介绍 WPF 属性系统和依赖项属性的功能。"
ms.date: 03/30/2017
ms.prod: .net-framework
ms.technology: dotnet-wpf
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties [WPF], attached
- properties [WPF], overview
- styles [WPF]
- attached properties [WPF]
- data binding [WPF]
- dependency properties [WPF]
- resources [WPF], references to
ms.assetid: d119d00c-3afb-48d6-87a0-c4da4f83dee5
caps.latest.revision: "30"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: d90e47c400f24eb10f2d262f9cb0e757ff472f0a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="dependency-properties-overview"></a>依赖项属性概述

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供一组服务，这些服务可用于扩展 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性的功能。 这些服务通常统称为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统。 由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统支持的属性称为依赖属性。 本概述介绍 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统以及依赖属性的功能。 这包括如何在 XAML 和在代码中使用现有依赖属性。 本概述还介绍依赖属性所特有的方面（如依赖属性元数据），并说明如何在自定义类中创建自己的依赖属性。

## <a name="prerequisites"></a>系统必备
本主题假设你在 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 和面向对象的编程方面有一些基础知识。 若要理解本主题中的示例，还应当了解 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 并知道如何编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。 有关详细信息，请参阅[演练： 我第一个 WPF 桌面应用程序](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)。  
  
## <a name="dependency-properties-and-clr-properties"></a>依赖项属性和 CLR 属性
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，属性通常公开为[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性。 在基本级别，可以直接与这些属性交互，而不必了解它们是以依赖属性的形式实现的。 但是，应当熟悉 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统的部分或全部功能，才能利用这些功能。

依赖属性的用途在于提供一种方法来基于其他输入的值计算属性值。 这些其他输入可能包括系统属性（如主题和用户首选项）、实时属性确定机制（如数据绑定和动画/情节提要）、重用模板（如资源和样式）或者通过与元素树中其他元素的父子关系来公开的值。 另外，可以通过实现依赖属性来提供独立验证、默认值、监视其他属性的更改的回叫以及可以基于可能的运行时信息来强制指定属性值的系统。 派生类还可以通过重写依赖属性元数据（而不是重写现有属性的实际实现或者创建新属性）来更改现有属性的某些具体特征。

在 SDK 参考中，可以根据某个属性的托管引用页上是否存在“依赖属性信息”部分来确定该属性是否为依赖属性。 依赖项属性信息部分包含的链接<xref:System.Windows.DependencyProperty>标识符字段对于该依赖项属性，并且还设置该属性，每个类重写信息和其他详细信息的元数据选项的列表。

## <a name="dependency-properties-back-clr-properties"></a>依赖项属性返回的 CLR 属性
依赖属性和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统通过提供一个支持属性的类型来扩展属性功能，这是使用私有字段支持该属性的标准模式的替代实现方法。 此类型的名称是<xref:System.Windows.DependencyProperty>。 其他重要类型，它定义[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]属性系统是<xref:System.Windows.DependencyObject>。 <xref:System.Windows.DependencyObject>定义可以注册并拥有依赖项属性的基类。

下面汇集了在本[!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] 文档中，在讨论依赖属性时所使用的术语：

- **依赖项属性：**由支持的属性<xref:System.Windows.DependencyProperty>。

- **依赖项属性标识符：** 一个<xref:System.Windows.DependencyProperty>实例，这是作为返回值中获得的注册依赖属性时，然后存储为类的静态成员。 对于与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统交互的许多 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，此标识符用作一个参数。

- **CLR“包装器”：**属性的实际 get 和 set 实现。 这些实现通过使用在将合并的依赖项属性标识符<xref:System.Windows.DependencyObject.GetValue%2A>和<xref:System.Windows.DependencyObject.SetValue%2A>调用，从而使属性使用后备[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]属性系统。

下面的示例定义`IsSpinning`依赖项属性，并显示的关系<xref:System.Windows.DependencyProperty>它支持的属性的标识符。

[!code-csharp[PropertiesOvwSupport#DPFormBasic](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#dpformbasic)]
[!code-vb[PropertiesOvwSupport#DPFormBasic](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#dpformbasic)]  
  
属性以及支持的命名约定<xref:System.Windows.DependencyProperty>字段很重要。 字段总是与属性同名，但其后面追加了 `Property` 后缀。 有关此约定及其原因的详细信息，请参阅[自定义依赖属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。  

## <a name="setting-property-values"></a>设置属性值
可以在代码或 XAML 中设置属性。

### <a name="setting-property-values-in-xaml"></a>在 XAML 中设置属性值 
下面的 XAML 示例将按钮的背景色指定为红色。 此示例阐释了其中一种 XAML 特性的简单的字符串值是到 WPF XAML 分析器类型转换的情况[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]类型 ( <xref:System.Windows.Media.Color>，通过<xref:System.Windows.Media.SolidColorBrush>) 生成的代码中。

[!code-xaml[PropertiesOvwSupport#MostBasicProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml#mostbasicproperty)]

XAML 支持多种设置属性的语法格式。 要对特定的属性使用哪种语法取决于该属性所使用的值类型以及其他因素（例如，是否存在类型转换器）。 有关属性设置的 XAML 语法的详细信息，请参阅 [XAML 概述 (WPF)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md) 和 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)。

作为非属性语法的示例，下面的 XAML 示例显示了另一种按钮背景。 这一次不是设置简单的纯色，而是将背景设置为图像，用一个元素表示该图像并将该图像的源指定为嵌套元素的属性。 这是属性元素语法的示例。

[!code-xaml[PropertiesOvwSupport#PESyntaxProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml#pesyntaxproperty)]

### <a name="setting-properties-in-code"></a>在代码中设置属性
 在代码中设置依赖属性值通常只是调用由 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]“包装器”公开的 set 实现。

[!code-csharp[PropertiesOvwSupport#ProceduralPropertySet](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml.cs#proceduralpropertyset)]
[!code-vb[PropertiesOvwSupport#ProceduralPropertySet](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page1.xaml.vb#proceduralpropertyset)]

获取属性值实质上也是在调用 get“包装器”实现：

[!code-csharp[PropertiesOvwSupport#ProceduralPropertyGet](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml.cs#proceduralpropertyget)]
 [!code-vb[PropertiesOvwSupport#ProceduralPropertyGet](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page1.xaml.vb#proceduralpropertyget)]

你还可以调用属性系统[!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]<xref:System.Windows.DependencyObject.GetValue%2A>和<xref:System.Windows.DependencyObject.SetValue%2A>直接。 如果使用的是现有属性，则上述操作通常不是必需的（使用包装器会更方便，并能够更好地向开发人员工具公开属性），但是在某些情况下适合直接调用 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]。

还可以在 XAML 中设置属性，然后通过代码隐藏在代码中访问这些属性。 有关详细信息，请参阅 [WPF 中的代码隐藏和 XAML](../../../../docs/framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)。

## <a name="property-functionality-provided-by-a-dependency-property"></a>提供由依赖项属性的属性功能
依赖属性提供用来扩展属性功能的功能，这与字段支持的属性相反。 每个这样的功能通常都表示或支持整套 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能中的特定功能：

- [资源](#resources)

- [数据绑定](#data-binding)

- [样式](#styles)

- [动画](#animations)

- [元数据重写](#metadata-overrides)

- [属性值继承](#property-value-inheritance)

- [WPF 设计器集成](#wpf-designer-integration)

### <a name="resources"></a>资源
依赖属性值可以通过引用资源来设置。 资源通常指定为页面根元素或应用程序的 `Resources` 属性值（通过这些位置可以非常方便地访问资源）。 下面的示例演示如何定义<xref:System.Windows.Media.SolidColorBrush>资源。

[!code-xaml[PropertiesOvwSupport#ResourcesResource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page2.xaml#resourcesresource)]

在定义该资源之后，可以引用该资源并使用它来提供属性值：

[!code-xaml[PropertiesOvwSupport#ResourcesReference](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page2.xaml#resourcesreference)]

这个特定资源称为 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)（在 WPF XAML 中，可以使用静态或动态资源引用）。 若要使用动态资源引用，必须设置为依赖属性，因此它是由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统明确启用的动态资源引用用法。 有关详细信息，请参阅 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。

> [!NOTE]
> 资源被视为本地值，这意味着，如果设置另一个本地值，该资源引用将被消除。 有关详细信息，请参阅[依赖属性值优先级](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)。

### <a name="data-binding"></a>数据绑定
依赖属性可以通过数据绑定来引用值。 在 XAML 中，绑定通过特定的标记扩展语法的工作原理的数据或<xref:System.Windows.Data.Binding>在代码中的对象。 使用数据绑定，最终属性值的确定将延迟到运行时，在运行时，将从数据源获取属性值。

下面的示例设置<xref:System.Windows.Controls.ContentControl.Content%2A>属性<xref:System.Windows.Controls.Button>，在 XAML 中使用绑定声明。 绑定使用继承的数据上下文和<xref:System.Windows.Data.XmlDataProvider>（未显示） 的数据源。 绑定本身指定依据的所需的源属性<xref:System.Windows.Data.Binding.XPath%2A>数据源中。

[!code-xaml[PropertiesOvwSupport#BasicInlineBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#basicinlinebinding)]

> [!NOTE]
> 绑定被视为本地值，这意味着，如果设置另一个本地值，该绑定将被消除。 有关详细信息，请参阅[依赖属性值优先级](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)。

依赖项属性，或<xref:System.Windows.DependencyObject>类，本身不执行支持<xref:System.ComponentModel.INotifyPropertyChanged>为了生成中的更改的通知<xref:System.Windows.DependencyObject>源的数据绑定操作的属性值。 有关如何创建要用在数据绑定中并且可以向数据绑定目标报告变化的属性的详细信息，请参阅[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。

### <a name="styles"></a>样式
样式和模板是使用依赖属性的两个主要激发方案。 在设置定义应用程序[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 的属性时，样式尤其有用。 在 XAML 中，通常将样式定义为资源。 样式与属性系统交互，因为它们通常包含特定属性的“资源库”，以及基于另一个属性的实时值更改属性值的“触发器”。

下面的示例创建一个非常简单的样式 (这将内部定义<xref:System.Windows.FrameworkElement.Resources%2A>字典，未显示)，然后将直接应用该样式<xref:System.Windows.FrameworkElement.Style%2A>属性<xref:System.Windows.Controls.Button>。 中的样式集 setter<xref:System.Windows.Controls.Control.Background%2A>样式的属性<xref:System.Windows.Controls.Button>为绿色。

[!code-xaml[PropertiesOvwSupport#SimpleStyleDef](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#simplestyledef)]

[!code-xaml[PropertiesOvwSupport#SimpleStyle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#simplestyle)]

有关详细信息，请参阅[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。

### <a name="animations"></a>动画
可以对依赖属性进行动画处理。 在应用和运行动画时，经过动画处理的值的操作优先级高于该属性以其他方式具有的任何值（如本地值）。

下面的示例进行动画处理<xref:System.Windows.Controls.Control.Background%2A>上<xref:System.Windows.Controls.Button>属性 (从技术上讲，<xref:System.Windows.Controls.Control.Background%2A>动画处理的通过使用属性元素语法指定空白<xref:System.Windows.Media.SolidColorBrush>作为<xref:System.Windows.Controls.Control.Background%2A>，则<xref:System.Windows.Media.SolidColorBrush.Color%2A>的属性<xref:System.Windows.Media.SolidColorBrush>是直接进行动画处理的属性)。

[!code-xaml[PropertiesOvwSupport#MiniAnimate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#minianimate)]

有关对属性进行动画处理的详细信息，请参阅[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)和[情节提要概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。

### <a name="metadata-overrides"></a>元数据重写
在从最初注册依赖属性的类派生时，可以通过重写依赖属性的元数据来更改该属性的某些行为。 重写元数据依赖于<xref:System.Windows.DependencyProperty>标识符。 重写元数据不需要重新实现属性。 元数据的更改由属性系统在本机处理；对于所有从基类继承的属性，每个类都有可能基于每个类型保留元数据。

下面的示例重写依赖项属性的元数据<xref:System.Windows.FrameworkElement.DefaultStyleKey%2A>。 重写此特定依赖属性的元数据是某个实现模式的一部分，该模式创建可以使用主题中的默认样式的控件。

[!code-csharp[PropertiesOvwSupport#OverrideMetadata](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml.cs#overridemetadata)]
[!code-vb[PropertiesOvwSupport#OverrideMetadata](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page3.xaml.vb#overridemetadata)]

有关替代或获取属性元数据的详细信息，请参阅[依赖属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)。

### <a name="property-value-inheritance"></a>属性值继承
元素可以从其在对象树中的父级继承依赖属性的值。

> [!NOTE]
> 属性值继承行为并未针对所有依赖属性在全局启用，因为继承的计算时间确实会对性能产生一定的影响。 属性值继承通常只有在特定方案指出适合使用属性值继承时才对属性启用。 可以通过在 SDK 参考中查看某个依赖属性的**依赖属性信息**部分，来确定该依赖属性是否继承属性值。

下面的示例演示一个绑定，并设置<xref:System.Windows.FrameworkElement.DataContext%2A>指定的绑定，而未显示在早期绑定的示例中的绑定源的属性。 中子对象的任何后续绑定不需要指定源，则可使用继承的值从<xref:System.Windows.FrameworkElement.DataContext%2A>的父代中<xref:System.Windows.Controls.StackPanel>对象。 (或者，子对象无法改为选择直接指定其自己<xref:System.Windows.FrameworkElement.DataContext%2A>或<xref:System.Windows.Data.Binding.Source%2A>中<xref:System.Windows.Data.Binding>，并用于以防出现故意不继承的值的自己的绑定的数据上下文。)

[!code-xaml[PropertiesOvwSupport#InheritanceContext](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#inheritancecontext)]

有关详细信息，请参阅[属性值继承](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)。

### <a name="wpf-designer-integration"></a>WPF 设计器集成
如果自定义控件具有实现为依赖属性的属性，则它会收到相应的[!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)]支持。 一个示例就是能够在“属性”窗口中编辑直接依赖属性和附加依赖属性。 有关详细信息，请参阅[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。

## <a name="dependency-property-value-precedence"></a>依赖项属性值优先级
获取依赖属性的值时，可能会获得通过其他参与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统且基于属性的任一输入而在该属性上设置的值。 由于存在依赖属性值优先级，使得属性获取值的方式的各种方案得以按可预测的方式交互。

请看下面的示例。 该示例包含适用于所有按钮样式及其<xref:System.Windows.Controls.Control.Background%2A>属性，然后使用本地设置还指定一个按钮，但<xref:System.Windows.Controls.Control.Background%2A>值。

> [!NOTE]
> SDK 文档在讨论依赖属性时有时会使用“本地值”或“本地设置的值”等术语。 本地设置的值是指在代码中直接为对象实例设置的属性值，或者在 XAML 中设置为元素特性的属性值。  
  
原则上，对于第一个按钮，该属性会设置两次，但是仅应用一个值，即具有最高优先级的值。 本地设置的值具有最高优先级（对于正在运行的动画除外，但是在本示例中没有应用动画），因此，对于第一个按钮的背景将使用本地设置的值，而不使用样式资源库值。 第二个按钮没有本地值（而且没有其他比样式资源库优先级更高的值），因此该按钮中的背景来自样式资源库。

[!code-xaml[PropertiesOvwSupport#MiniPrecedence](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#miniprecedence)]  

### <a name="why-does-dependency-property-precedence-exist"></a>为什么存在依赖项属性的优先级？
通常，你不会希望总是应用样式，而且不希望样式遮盖单个元素的哪怕一个本地设置值（否则，通常很难使用样式或元素）。 因此，来自样式的值的操作优先级低于本地设置的值。 有关依赖属性以及它的有效值可能来自何处的更完整列表，请参阅[依赖属性值优先级](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)。

> [!NOTE]
> 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素定义了许多非依赖属性的属性。 一般说来，只有在需要支持至少一个由属性系统启用的方案（数据绑定、样式、动画、默认值支持、继承、附加属性或失效）时，才将属性实现为依赖属性。

## <a name="learning-more-about-dependency-properties"></a>了解有关依赖项属性的更多信息  

- 附加属性是一种支持 XAML 中的专用语法的属性。 附加属性通常与[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性不具有 1:1 对应关系，而且不一定是依赖属性。 附加属性的典型用途是使子元素可以向其父元素报告属性值，即使父元素和子元素的类成员列表中均没有该属性也是如此。 一个主要方案是以启用子元素，以通知父它们中呈现的方式[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]; 例如，请参阅<xref:System.Windows.Controls.DockPanel.Dock%2A>或<xref:System.Windows.Controls.Canvas.Left%2A>。 有关详细信息，请参阅[附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)。

- 组件开发人员或应用程序开发人员可能希望创建自己的依赖属性，以便实现数据绑定或样式支持之类的功能，或者实现对失效和值强制的支持。 有关详细信息，请参阅[自定义依赖属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。

- 通常，依赖属性应当被视为公共属性，这些公共属性可以由任何具有实例访问权限的调用方访问，或至少可被这样的调用方发现。 有关详细信息，请参阅[依赖属性的安全性](../../../../docs/framework/wpf/advanced/dependency-property-security.md)。

## <a name="see-also"></a>请参阅
 [自定义依赖属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)  
 [只读依赖项属性](../../../../docs/framework/wpf/advanced/read-only-dependency-properties.md)  
 [XAML 概述 (WPF)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)  
 [WPF 体系结构](../../../../docs/framework/wpf/advanced/wpf-architecture.md)
