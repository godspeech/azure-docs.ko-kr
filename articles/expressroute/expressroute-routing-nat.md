---
title: "ExpressRoute에 대한 라우팅 요구 사항 | Microsoft Docs"
description: "이 페이지는 Express 경로 회로에 라우팅을 구성하고 관리하는 자세한 요구 사항을 제공합니다."
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: osamazia
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: bd7537a81661bc175a770fdbd6388ba07ea912ae


---
# <a name="expressroute-routing-requirements"></a>Express 경로 라우팅 요구 사항
Express 경로를 사용하여 Microsoft 클라우드 서비스에 연결하려면 라우팅을 설치하고 관리해야 합니다. 일부 연결 공급자는 라우팅을 관리 서비스로 설치하고 관리해 줍니다. 연결 공급자를 확인하여 이 서비스를 제공하는지를 확인합니다. 그렇지 않은 경우 다음 요구 사항을 준수해야 합니다. 

쉬운 연결을 위해 설치해야 하는 라우팅 세션에 대한 설명은 [회로 및 라우팅 도메인](expressroute-circuit-peerings.md) 문서를 참조합니다.

> [!NOTE]
> Microsoft는 고가용성 구성을 위해 라우터 중복 프로토콜(예: HSRP, VRRP)을 지원하지 않습니다. 고가용성에 대한 피어링에 대해 BGP 세션의 중복 쌍에 의존합니다.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>피어링에 사용된 IP 주소
몇 블록의 IP 주소를 예약하여 네트워크와 Microsoft의 엔터프라이즈 Edge(MSEE) 라우터 간에 라우팅을 구성해야 합니다. 이 섹션은 이러한 IP 주소를 어떻게 획득하고 사용하는지에 대한 요구 사항 목록을 제공하고 규칙을 설명합니다.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Azure 개인 피어링에 사용된 IP 주소
개인 IP 주소 또는 공용 IP 주소를 사용하여 피어링을 구성할 수 있습니다. 경로를 구성하는 데 사용되는 주소 범위는 Azure에서 가상 네트워크를 만드는 데 사용되는 주소 범위와 겹치지 않아야 합니다. 

* 라우팅 인터페이스에 하나의 /29 서브넷 또는 두 개의 /30 서브넷을 예약해야 합니다.
* 라우팅에 사용되는 서브넷은 개인 IP 주소 또는 공용 IP 주소 모두 가능합니다.
* 서브넷은 Microsoft 클라우드에서 사용하기 위해 고객이 예약한 범위와 충돌하지 않아야 합니다.
* /29 서브넷을 사용한 경우 두 개의 /30 서브넷으로 분할됩니다. 
  * 첫 번째 /30 서브넷 은 기본 링크에 사용하고 두 번째 /30 서브넷은 보조 링크에 사용됩니다.
  * 각 /30 서브넷의 경우 라우터에서 /30의 첫 번째 IP 주소를 사용해야 합니다. Microsoft는 /30의 두 번째 IP 주소를 사용하여 BGP 세션을 설치합니다.
  * [가용성 SLA](https://azure.microsoft.com/support/legal/sla/) 이 유효하기 위해 BGP 세션을 모두 설치해야 합니다.  

#### <a name="example-for-private-peering"></a>개인 피어링에 대한 예제
a.b.c.d/29를 사용하여 피어링을 설치하기로 선택한 경우 두 개의 /30 서브넷으로 분할됩니다. 아래 예제에서는 a.b.c.d/29 서브넷이 어떻게 사용되는지 살펴봅니다. 

a.b.c.d/29는 a.b.c.d/30 및 a.b.c.d+4/30으로 분할되고 프로비전 API를 통해 Microsoft에 전달됩니다. 사용자는 기본 PE에 a.b.c.d+1을 VRF IP로 사용하고 Microsoft는 기본 MSEE에 a.b.c.d+2를 VRF IP로 사용합니다. 사용자는 보조 PE에 a.b.c.d+5를 VRF IP로 사용하고 Microsoft는 보조 MSEE에 a.b.c.d+6를 VRF IP로 사용합니다.

192.168.100.128/29을 선택하여 개인 피어링을 설치한 경우를 고려해 보세요. 192.168.100.128/29는 다음 중 192.168.100.128에서 192.168.100.135까지의 주소를 포함합니다.

* 192.168.100.128/30은 192.168.100.129를 사용하는 공급자 및 192.168.100.130를 사용하는 Microsoft와 함께 링크1에 할당됩니다.
* 192.168.100.132/30은 192.168.100.133를 사용하는 공급자 및 192.168.100.134를 사용하는 Microsoft와 함께 링크2에 할당됩니다.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Azure 공용 네트워크 및 Microsoft 피어링에 사용된 IP 주소
BGP 세션을 설치하기 위해 소유한 공용 IP 주소를 사용해야 합니다. Microsoft은 라우팅 인터넷 레지스트리 및 인터넷 라우팅 레지스트리를 통해 IP 주소의 소유권을 확인할 수 있어야 합니다. 

* 고유한 /29 서브넷 또는 두 개의 /30 서브넷을 사용하여 Express 경로 회로 당(하나 이상이 있는 경우) 각 피어링에 BGP를 설정해야 합니다. 
* /29 서브넷을 사용한 경우 두 개의 /30 서브넷으로 분할됩니다. 
  * 첫 번째 /30 서브넷 은 기본 링크에 사용하고 두 번째 /30 서브넷은 보조 링크에 사용됩니다.
  * 각 /30 서브넷의 경우 라우터에서 /30의 첫 번째 IP 주소를 사용해야 합니다. Microsoft는 /30의 두 번째 IP 주소를 사용하여 BGP 세션을 설치합니다.
  * [가용성 SLA](https://azure.microsoft.com/support/legal/sla/) 이 유효하기 위해 BGP 세션을 모두 설치해야 합니다.

## <a name="public-ip-address-requirement"></a>공용 IP 주소 요구 사항
### <a name="private-peering"></a>개인 피어링
개인 피어링에 대한 공용 또는 개인 IPv4 주소를 사용할 수 있습니다. 개인 피어링의 경우 다른 고객과 주소가 중첩되지 않도록 트래픽의 종단 간 격리를 제공합니다. 이러한 주소는 인터넷에는 보급되지 않습니다. 

### <a name="public-peering"></a>공용 피어링
Azure 공용 피어링 경로를 사용하면 해당 공용 IP 주소에 걸쳐 Azure에서 호스팅되는 모든 서비스에 연결할 수 있습니다. [Expess 경로 FAQ](expressroute-faqs.md) 에 나열된 서비스와 Microsoft Azure에서 ISV가 호스팅하는 서비스를 포함합니다. 공용 피어링의 Microsoft Azure 서비스에 대한 연결은 항상 네트워크에서 Microsoft 네트워크로 시작됩니다. Microsoft 네트워크를 대상으로 하는 트래픽에 대한 공용 IP 주소를 사용해야 합니다.

### <a name="microsoft-peering"></a>Microsoft 피어링
Microsoft 피어링 경로를 사용하면 Azure 공용 피어링 경로를 통해 지원하지 않는 Microsoft 클라우드 서비스에 연결할 수 있습니다. 서비스 목록은 Exchange Online, SharePoint Online, 비즈니스용 Skype 및 CRM Online과 같은 Office 365 서비스를 포함합니다. Microsoft는 Microsoft 피어링에 양방향 연결을 지원합니다. Microsoft 클라우드 서비스에 보내는 트래픽은 Microsoft 네트워크를 입력하기 전에 유효한 공용 IPv4 주소를 사용해야 합니다.

사용자 IP 주소 및 AS 번호가 아래에 나열된 레지스트리 중 하나에 등록되었는지 확인합니다.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> ExpressRoute를 통해 Microsoft에 보급된 공용 IP 주소는 인터넷에 보급하지 않아야 합니다. 다른 Microsoft 서비스에 대한 연결을 중단할 수 있습니다. 그러나 ExpressRoute를 통해 Microsoft 내에서 O365 끝점과 통신하는 네트워크의 서버에서 사용하는 공용 IP 주소를 보급할 수 있습니다. 
> 
> 

## <a name="dynamic-route-exchange"></a>동적 경로 Exchange
라우팅 Exchange는 eBGP 프로토콜을 통합니다. EBGP 세션은 MSEE와 라우터 간에 설정됩니다. BGP 세션의 인증은 요구되지 않습니다. 필요한 경우 MD5 해시를 구성할 수 있습니다. BGP 세션을 구성하는 방법에 대한 정보는 [구성 라우팅](expressroute-howto-routing-classic.md) 및 [회로 프로비전 워크플로 및 회로 상태](expressroute-workflows.md)를 참조하세요.

## <a name="autonomous-system-numbers"></a>자치 시스템 번호
Microsoft는 Azure 공용, Azure 개인 및 Microsoft 피어링에 AS 12076를 사용합니다. 내부 사용을 위해 65515에서 65520으로 ASN을 예약했습니다. 16 및 32비트 AS 번호를 모두 지원합니다.

데이터 전송 대칭에 요구 사항이 없습니다. 전달 및 반환 경로는 다른 라우터 쌍을 트래버스할 수 있습니다. 동일한 경로는 사용자에게 속한 여러 회로 쌍에 걸쳐 한 쪽에서 보급해야 합니다. 경로 메트릭이 동일할 필요는 없습니다.

## <a name="route-aggregation-and-prefix-limits"></a>경로 집계 및 접두사 제한
Azure 개인 피어링을 통해 보급된 최대 4000개의 접두사를 지원합니다. Express 경로 프리미엄 추가 기능을 사용하는 경우 최대 10,000 접두사까지 증가할 수 있습니다. 공용 Azure 및 Microsoft 피어링에 BGP 세션 당 최대 200개의 접두사를 수락합니다. 

접두사의 수가 제한을 초과하는 경우 BGP 세션은 삭제됩니다. 개인 피어링 링크의 기본 경로만을 수락합니다. 공급자는 공용 Azure 및 Microsoft 피어 링 경로에서 기본 경로 및 개인 IP 주소(RFC 1918)를 필터링해야 합니다. 

## <a name="transit-routing-and-crossregion-routing"></a>전송 라우팅 및 영역 간 라우팅
Express 경로는 전송 라우터로 구성할 수 없습니다. 전송 라우팅 서비스의 경우 연결 공급자에 의존해야 합니다.

## <a name="advertising-default-routes"></a>기본 경로 광고
기본 경로는 Azure 개인 피어링 세션에서만 허용됩니다. 이러한 경우에 가상 네트워크에서 사용자의 네트워크에 연결된 모든 트래픽을 라우팅합니다. 기본 경로를 개인 피어링에 보급하면 Azure에서 인터넷 경로가 차단됩니다. Azure에서 호스팅되는 서비스에 대한 인터넷 간에 트래픽을 라우팅하는 회사 Edge에 의존해야 합니다. 

 다른 Azure 서비스 및 인프라 서비스에 연결을 사용하려면 다음 항목 중 하나가 준비되었는지 확인해야 합니다.

* Azure 공용 피어링은 트래픽을 공용 끝점에 라우팅할 수 있도록 설정됩니다.
* 사용자 정의 라우팅을 사용하여 인터넷 연결이 필요한 모든 서브넷에 인터넷 연결을 허용할 수 있습니다.

> [!NOTE]
> 기본 경로를 보급하면 Windows 및 다른 VM 라이선스 정품 인증이 중단됩니다. [여기](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) 서 지침을 수행하여 이 문제를 해결합니다.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>BGP 커뮤니티에 대한 지원(미리 보기)
이 섹션에서는 BGP 커뮤니티를 어떻게 Express 경로와 함께 사용하는지에 대한 개요를 제공합니다. Microsoft는 적절한 커뮤니티 값으로 태그된 경로를 가진 공용 및 Microsoft 피어링 경로에 경로를 광고합니다. 이렇게 하는 이유 및 커뮤니티 값에 대한 세부 정보는 다음과 같습니다. 그러나 Microsoft는 Microsoft에 보급하는 경로에 태그된 커뮤니티 값을 인식하지 못합니다.

지정학적 지역 내의 한 피어링 위치에서 Express 경로를 통해 Microsoft에 연결하는 경우 지정학적 경계 내에서 모든 지역에 걸쳐 모든 Microsoft 클라우드 서비스에 액세스해야 합니다. 

예를 들어 Express 경로를 통해 암스테르담의 Microsoft에 연결하는 경우 북유럽 및 서유럽에서 호스팅되는 모든 Microsoft 클라우드 서비스에 액세스합니다. 

지정학적 지역, 연관된 Azure 지역 및 해당 Express 경로 피어링 위치의 세부 목록은 [Express 경로 파트너와 피어링 위치](expressroute-locations.md) 페이지를 참조합니다.

지정학적 지역 마다 하나 이상의 Express 경로 회로를 구입할 수 있습니다. 여러 연결이 있으면 지리적 중복으로 인해 고가용성에 상당한 이점을 제공합니다. Express 경로 회로가 여러 개 있는 경우 공용 피어링 및 Microsoft 경로 피어링의 Microsoft에서 보급된 동일한 접두사 집합을 받게 됩니다. 즉, 네트워크에서 Microsoft까지 여러 경로가 있습니다. 잠재적으로 네트워크 내에서 최적이 아닌 라우팅이 결정될 수 있습니다. 결과적으로 다른 서비스에 최적이 아닌 연결 환경이 발생할 수도 있습니다. 

Microsoft는 공용 피어링 및 Microsoft 피어링을 통해 접두사가 호스팅된 지역을 나타내는 적절한 BGP 커뮤니티 값으로 보급된 접두사를 태그합니다. 적절한 라우팅을 결정하는 커뮤니티 값에 의존하여 [고객에게 최적의 라우팅](expressroute-optimize-routing.md)을 제공할 수 있습니다.

| **지역** | **Microsoft Azure 지역** | **BGP 커뮤니티 값** |
| --- | --- | --- |
| **북아메리카** | | |
| 미국 동부 |12076:51004 | |
| 미국 동부 2 |12076:51005 | |
| 미국 서부 |12076:51006 | |
| 미국 서부 2 |12076:51026 | |
| 미국 중서부 |12076:51027 | |
| 미국 중북부 |12076:51007 | |
| 미국 중남부 |12076:51008 | |
| 미국 중부 |12076:51009 | |
| 캐나다 중부 |12076:51020 | |
| 캐나다 동부 |12076:51021 | |
| **남미** | | |
| 브라질 남부 |12076:51014 | |
| **유럽** | | |
| 북유럽 |12076:51003 | |
| 서유럽 |12076:51002 | |
| **아시아 태평양** | | |
| 동아시아 |12076:51010 | |
| 동남아시아 |12076:51011 | |
| **일본** | | |
| 일본 동부 |12076:51012 | |
| 일본 서부 |12076:51013 | |
| **오스트레일리아** | | |
| 오스트레일리아 동부 |12076:51015 | |
| 오스트레일리아 남동부 |12076:51016 | |
| **인도** | | |
| 인도 남부 |12076:51019 | |
| 인도 서부 |12076:51018 | |
| 인도 중부 |12076:51017 | |

Microsoft에서 보급하는 모든 경로는 적절한 커뮤니티 값으로 태그되어야 합니다. 

> [!IMPORTANT]
> 전역 접두사는 적절한 커뮤니티 값으로 태그가 지정되며 Express 경로 Premium 추가 기능을 사용하는 경우에만 보급됩니다.
> 
> 

또한 위의 내용 외에도 Microsoft는 자신이 속한 서비스에 기반한 접두사에 태그합니다. Microsoft 피어링에 적용됩니다. 다음 테이블에서는 BGP 커뮤니티 값에 서비스의 매핑을 제공합니다.

| **서비스** | **BGP 커뮤니티 값** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **비즈니스용 Skype** |12076:5030 |
| **CRM Online** |12076:5040 |
| **다른 Office 365 서비스** |12076:5100 |

> [!NOTE]
> Microsoft는 Microsoft에 보급하는 경로에 설정한 BGP 커뮤니티 값을 인식하지 않습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* Express 경로 연결을 구성합니다.
  
  * [클래식 배포 모델용 ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md) 또는 [Azure Resource Manager를 사용하여 ExpressRoute 회로 만들기 및 수정](expressroute-howto-circuit-arm.md)
  * [클래식 배포 모델용 라우팅 구성](expressroute-howto-routing-classic.md) 또는 [Resource Manager 배포 모델용 라우팅 구성](expressroute-howto-routing-arm.md)
  * [ExpressRoute 회로에 클래식 VNet 연결](expressroute-howto-linkvnet-classic.md) 또는 [ExpressRoute 회로에 Resource Manager VNet 연결](expressroute-howto-linkvnet-arm.md)




<!--HONumber=Nov16_HO2-->


