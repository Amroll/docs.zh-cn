---
title: "客户端体系结构"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 02624403-0d77-41cb-9a86-ab55e98c7966
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6418c3b5c82ac42fb7e6d3ce85913896a3f76442
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="client-architecture"></a>客户端体系结构
应用程序使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端对象来调用服务操作。 本主题讨论 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端对象、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端通道以及它们与基础通道体系结构的关系。 有关的基本概述[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端对象，请参阅[WCF 客户端概述](../../../../docs/framework/wcf/wcf-client-overview.md)。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]通道层，请参阅[扩展通道层](../../../../docs/framework/wcf/extending/extending-the-channel-layer.md)。  
  
## <a name="overview"></a>概述  
 服务模型运行时创建 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端，这些客户端由以下各项构成：  
  
-   自动生成的服务协定客户端实现，该实现可以将应用程序代码中的调用转换为传出消息，将响应消息转换为输出参数并返回应用程序可以检索的值。  
  
-   控制接口 (<xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType>) 的实现，它可将各个接口组合在一起，并提供对控制功能（特别是用于关闭客户端会话和释放通道的能力）的访问。  
  
-   基于由使用的绑定指定的配置设置而生成的客户端通道。  
  
 应用程序可以按需，不论是通过创建此类客户端<xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType>或通过创建的实例<xref:System.ServiceModel.ClientBase%601>派生类，如由生成[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。 这些预先生成的客户端类可以封装并委托给由 <xref:System.ServiceModel.ChannelFactory> 动态构造的客户端通道实现。 因此，客户端通道和生成这些客户端通道的客户端工厂是此处讨论的焦点。  
  
## <a name="client-objects-and-client-channels"></a>客户端对象和客户端通道  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的基接口是 <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType> 接口，该接口公开核心客户端功能以及 <xref:System.ServiceModel.ICommunicationObject?displayProperty=nameWithType> 的基本通信对象功能、<xref:System.ServiceModel.IContextChannel?displayProperty=nameWithType> 的上下文功能和 <xref:System.ServiceModel.IExtensibleObject%601?displayProperty=nameWithType> 的可扩展行为。  
  
 但 <xref:System.ServiceModel.IClientChannel> 接口并不定义服务协定本身。 这些声明的服务协定接口 (通常根据服务元数据使用之类的工具生成[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md))。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端类型同时扩展 <xref:System.ServiceModel.IClientChannel> 和目标服务协定接口，以使应用程序能够直接调用操作，同时还可以访问客户端运行时功能。 创建一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端可以向 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]<xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> 对象提供必要信息，以便创建可以连接到配置的服务终结点并与此终结点交互的运行时。  
  
 如前所述，这两个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端类型必须进行配置才能使用。 最简单的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端类型是从 <xref:System.ServiceModel.ClientBase%601> 中派生的对象（如果服务协定是双工协定，则为从 <xref:System.ServiceModel.DuplexClientBase%601> 中派生的对象）。 通过使用以编程方式进行配置的构造函数，或者通过使用配置文件，然后直接调用该配置文件以调用服务操作，可以创建这些类型。 有关的基本概述<xref:System.ServiceModel.ClientBase%601>对象，请参阅[WCF 客户端概述](../../../../docs/framework/wcf/wcf-client-overview.md)。  
  
 第二个类型是在运行时从对 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A> 方法的调用中生成的。 通常涉及严格控制通信详细信息的应用程序使用此客户端类型，调用*客户端通道对象*，因为它使更直接的交互，与基础客户端运行时和通道系统。  
  
## <a name="channel-factories"></a>通道工厂  
 负责创建可支持客户端调用的基础运行时的类为 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> 类。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端对象和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端通道对象都使用 <xref:System.ServiceModel.ChannelFactory%601> 对象来创建实例；<xref:System.ServiceModel.ClientBase%601> 派生的客户端对象封装通道工厂的处理，但在有些情况下，完全可以直接使用通道工厂。 对此，常见的情况是从现有工厂重复创建新的客户端通道。 如果要使用客户端对象，可以通过调用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 属性从 <xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A?displayProperty=nameWithType> 客户端对象中获取基础通道工厂。  
  
 应该记住的是，在调用 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType> 之前，通道工厂会为所提供的配置创建客户端通道的新实例。 一旦调用 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A>（或 <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType>、<xref:System.ServiceModel.ClientBase%601.CreateChannel%2A?displayProperty=nameWithType> 或对 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端对象执行的任何操作）后，不能修改通道工厂和期待获取到不同服务实例的通道，即使只是更改目标终结点地址也是如此。 如果您想用不同配置创建客户端对象或客户端通道，则必须首先创建新的通道工厂。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用的各种问题[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端对象和[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端通道，请参阅[使用 WCF 客户端访问服务](../../../../docs/framework/wcf/feature-details/accessing-services-using-a-client.md)。  
  
 以下两节说明 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端通道对象的创建和使用。  
  
#### <a name="creating-a-new-wcf-client-channel-object"></a>创建新的 WCF 客户端通道对象  
 为了说明客户端通道的用法，假设已生成以下服务协定。  
  
 [!code-csharp[C_GeneratedCodeFiles#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#12)]  
  
 若要连接到 `ISampleService` 服务，请直接与通道工厂 (<xref:System.ServiceModel.ChannelFactory%601>) 一起使用生成的协定接口。 一旦为特定协定创建并配置通道工厂后，即可以调用 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A> 方法以返回可用于与 `ISampleService` 服务通信的客户端通道对象。  
  
 当 <xref:System.ServiceModel.ChannelFactory%601> 类与服务协定接口一起使用时，您必须强制转换到 <xref:System.ServiceModel.IClientChannel> 接口以显式打开、关闭或中止通道。 为便于操作，Svcutil.exe 工具还生成一个帮助器接口，该接口可同时实现服务协定接口和 <xref:System.ServiceModel.IClientChannel> ，以使您无需进行强制转换就能够与客户端通道基础结构进行交互。 下面的代码演示实现上述服务协定的帮助器客户端通道的定义。  
  
 [!code-csharp[C_GeneratedCodeFiles#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#13)]  
  
#### <a name="creating-a-new-wcf-client-channel-object"></a>创建新的 WCF 客户端通道对象  
 若要使用客户端通道连接到 `ISampleService` 服务，请直接与通道工厂一起使用生成的协定接口（或帮助器版本），将协定接口的类型作为参数进行传递。 一旦为特定协定创建并配置通道工厂后，即可以调用 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType> 方法以返回可用于与 `ISampleService` 服务通信的客户端通道对象。  
  
 客户端通道对象在创建后可实现 <xref:System.ServiceModel.IClientChannel> 和协定接口。 因此，可以直接使用这些对象来调用操作，与支持该协定的服务进行交互。  
  
 使用客户端对象和客户端通道对象之间的区别仅仅在于其易于使用性和开发人员的喜好。 许多习惯于使用类和对象的开发人员喜欢使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端对象，而不喜欢使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端通道。  
  
 有关示例，请参阅[如何： 使用 ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)。
