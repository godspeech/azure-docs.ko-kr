---
title: "가상 네트워크 VPN 게이트웨이 FAQ | Microsoft Docs"
description: "VPN 게이트웨이 FAQ. Microsoft Azure 가상 네트워크 프레미스 간 연결, 하이브리드 구성 연결 및 VPN 게이트웨이에 대한 FAQ"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2016
ms.author: yushwang
translationtype: Human Translation
ms.sourcegitcommit: 219dcbfdca145bedb570eb9ef747ee00cc0342eb
ms.openlocfilehash: 5528e1c53e58d4b9c70f022290160ac9d6a1a986


---
# <a name="vpn-gateway-faq"></a>VPN 게이트웨이 FAQ
## <a name="connecting-to-virtual-networks"></a>가상 네트워크에 연결
### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>다양한 Azure 지역에서 가상 네트워크를 연결할 수 있습니까?
예. 실제로 지역 제약 조건이 없습니다. 가상 네트워크를 동일한 지역 또는 다른 Azure 지역의 다른 가상 네트워크에 연결할 수 있습니다.

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>다른 구독의 가상 네트워크를 연결할 수 있습니까?
예.

### <a name="can-i-connect-to-multiple-sites-from-a-single-virtual-network"></a>단일 가상 네트워크에서 여러 사이트에 연결할 수 있습니까?
Windows PowerShell 및 Azure REST API를 사용하여 여러 사이트에 연결할 수 있습니다. [다중 사이트 및 VNet 간 연결](#multi-site-and-vnet-to-vnet-connectivity) FAQ 섹션을 참조하세요.

## <a name="what-are-my-crosspremises-connection-options"></a>내 프레미스 간 연결 옵션은 무엇입니까?
다음 프레미스 간 연결을 지원합니다.

* [사이트 간](vpn-gateway-site-to-site-create.md) – IPsec 통한 VPN 연결(IKE v1 및 IKE v2). 이 연결 유형은 VPN 장치 또는 RRAS가 필요합니다.
* [지점 및 사이트 간](vpn-gateway-point-to-site-create.md) -SSTP를 통한 VPN 연결(보안 소켓 터널링 프로토콜). 이 연결에는 VPN 장치가 필요하지 않습니다.
* [VNet 간](virtual-networks-configure-vnet-to-vnet-connection.md) - 이 유형의 연결은 사이트 간 구성과 동일합니다. VNet 간 연결은 IPsec를 통한 VPN 연결(IKE v1 및 IKE v2)입니다. VPN 장치가 필요하지 않습니다.
* [다중 사이트](vpn-gateway-multi-site.md) - 가상 네트워크에 여러 온-프레미스 사이트를 연결할 수 있는 사이트 간 구성의 변형입니다.
* [Express 경로](../expressroute/expressroute-introduction.md) - Express 경로는 공용 인터넷을 사용하지 않고 WAN에서 Azure에 직접 연결합니다. 자세한 내용은 [ExpressRoute 기술 개요](../expressroute/expressroute-introduction.md) 및 [ExpressRoute FAQ](../expressroute/expressroute-faqs.md)를 참조하세요.

연결에 대한 자세한 내용은 [VPN 게이트웨이 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.

### <a name="what-is-the-difference-between-a-sitetosite-connection-and-pointtosite"></a>사이트 간 연결과 지점 및 사이트 간 연결의 차이점은 무엇입니까?
**사이트 간** 연결을 사용하면 라우팅을 구성하기 위해 선택한 방법에 따라 프레미스에 있는 컴퓨터를 가상 네트워크 내의 가상 컴퓨터 또는 역할 인스턴스에 연결할 수 있습니다. 이 연결은 항상 사용할 수 있는 프레미스 간 연결에 유용한 옵션이며 하이브리드 구성에 적합합니다. 이 연결 유형에서는 네트워크의 가장자리에 배포되어야 하는 IPsec VPN 어플라이언스(하드웨어 또는 소프트 어플라이언스)를 사용합니다. 이 유형의 연결을 만들려면 필수 VPN 하드웨어와 외부 연결 IPv4 주소가 있어야 합니다.

**지점 및 사이트 간** 연결을 사용하면 모든 위치의 단일 컴퓨터에서 가상 네트워크에 있는 모든 컴퓨터에 연결할 수 있습니다. Windows 인박스 VPN 클라이언트를 사용합니다. 지점 및 사이트 간 구성 중에 가상 네트워크 내의 가상 컴퓨터 또는 역할 인스턴스에 컴퓨터를 연결할 수 있도록 해주는 설정이 포함된 인증서 및 VPN 클라이언트 구성 패키지를 설치합니다. 가상 네트워크에 연결하려고 하지만 온-프레미스에 없는 경우에 유용합니다. 사이트 간 연결에 필요한 VPN 하드웨어 또는 외부 연결 IPv4 주소에 액세스할 수 없을 때 유용한 옵션입니다. 

게이트웨이에 경로 기반 VPN 유형을 사용하여 사이트 간 연결을 만들 경우 사이트 간 연결과 지점 및 사이트 간 연결을 동시에 사용하도록 가상 네트워크를 구성할 수 있습니다. 경로 기반 VPN 유형은 클래식 배포 모델에서 동적 게이트웨이라고 합니다.

### <a name="what-is-expressroute"></a>Express 경로란?
Express 경로를 사용하면 온-프레미스 또는 공동 배치 환경의 인프라와 Microsoft 데이터 센터 간에 개인 연결을 만들 수 있습니다. Express 경로를 사용하면 Express 경로 파트너 공동 배치 기능으로 Microsoft Azure 및 Office 365와 같은 Microsoft 클라우드 서비스에 대한 연결을 설정하거나, 기존 WAN 네트워크(네트워크 서비스 공급자에서 제공된 MPLS VPN과 같은)에서 직접 연결할 수 있습니다.

Express 경로 연결은 인터넷을 통한 일반 연결보다 안정적이고 대역폭이 높으며 대기 시간이 짧고 보안성이 높습니다. 경우에 따라 온-프레미스 네트워크와 Azure 간 데이터 전송에 Express 경로 연결을 사용하면 상당한 비용 혜택을 얻을 수도 있습니다. 이미 온-프레미스 네트워크에서 Azure로 크로스 프레미스 연결을 설정한 경우, 가상 네트워크를 그대로 유지 하면서 Express 경로 연결로 마이그레이션할 수 있습니다.

자세한 내용은 [Express 경로 FAQ](../expressroute/expressroute-faqs.md) 를 참조하세요.

## <a name="sitetosite-connections-and-vpn-devices"></a>사이트 간 연결 및 VPN 장치
### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>VPN 장치를 선택할 때 고려할 사항은 무엇입니까?
장치 공급업체와 협력하여 표준 사이트 간 VPN 장치의 유효성을 검사했습니다. 알려진 호환 VPN 장치, 해당 구성 지침 또는 샘플 및 장치 사양 목록은 [여기](vpn-gateway-about-vpn-devices.md)서 확인할 수 있습니다. 호환하는 것으로 알려진 목록의 장치 제품군에 포함된 모든 장치는 가상 네트워크에서 작동합니다. VPN 장치를 구성하려면 적절한 장치 제품군에 해당하는 장치 구성 샘플 또는 링크를 참조하세요.

### <a name="what-do-i-do-if-i-have-a-vpn-device-that-isnt-in-the-known-compatible-device-list"></a>사용 중인 VPN 장치가 알려진 호환 장치 목록에 없는 경우 어떻게 해야 합니까?
사용 중인 장치가 알려진 호환 VPN 장치 목록에 표시되지 않지만 해당 장치를 VPN 연결에 사용하려면 해당 장치가 [여기에](vpn-gateway-about-vpn-devices.md#devices-not-on-the-compatible-list)나열된 지원되는 IPsec/IKE 구성 옵션 및 매개 변수를 충족하는지 확인해야 합니다. 최소 요구 사항을 충족하는 장치는 VPN 게이트웨이에서 잘 작동합니다. 추가 지원 및 구성 지침은 장치 제조업체에 문의하세요.

### <a name="why-does-my-policybased-vpn-tunnel-go-down-when-traffic-is-idle"></a>트래픽이 유휴 상태일 때 정책 기반 VPN 터널이 다운되는 이유는 무엇인가요?
정책 기반(정적 라우팅이라고도 함) VPN 게이트웨이에서 예상되는 동작입니다. 터널의 트래픽이 5분 이상 유휴 상태인 경우 터널은 삭제됩니다. 하지만 트래픽이 어느 방향으로든 흐름이 시작되면 즉시 터널이 다시 설정됩니다.

### <a name="can-i-use-software-vpns-to-connect-to-azure"></a>소프트웨어 VPN을 사용하여 Azure에 연결할 수 있습니까?
사이트 사이 프레미스 간 구성에 대해 Windows Server 2012 RRAS(라우팅 및 원격 액세스) 서버를 지원합니다.

다른 소프트웨어 VPN 솔루션은 업계 표준 IPsec 구현을 따르는 경우에만 Microsoft 게이트웨이에 사용할 수 있습니다. 구성 및 지원 지침은 소프트웨어 공급 업체에 문의하세요.

## <a name="pointtosite-connections"></a>지점 및 사이트 간 연결
### <a name="what-operating-systems-can-i-use-with-pointtosite"></a>지점 및 사이트 간 연결에 사용할 수 있는 운영 체제는 무엇입니까?
다음 운영 체제가 지원됩니다.

* Windows 7(32비트 및 64비트)
* Windows Server 2008 R2(64비트 전용)
* Windows 8(32비트 및 64비트)
* Windows 8.1(32비트 및 64비트)
* Windows Server 2012(64비트 전용)
* Windows Server 2012 R2(64비트 전용)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-pointtosite-that-supports-sstp"></a>SSTP를 지원하는 지점 및 사이트 간 연결에 소프트웨어 VPN 클라이언트를 사용할 수 있습니까?
아니요. 위에 나열된 Windows 운영 체제 버전만 지원됩니다.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-pointtosite-configuration"></a>지점 및 사이트 간 구성에서 VPN 클라이언트 끝점을 몇 개까지 지정할 수 있습니까?
최대 128개의 VPN 클라이언트에서 가상 네트워크에 동시에 연결할 수 있도록 지원합니다.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-pointtosite-connectivity"></a>지점 및 사이트 간 연결에 내부 PKI 루트 CA를 사용할 수 있습니까?
예. 이전에는 자체 서명한 루트 인증서만 사용할 수 있었습니다. 여전히 20개의 루트 인증서를 업로드할 수 있습니다.

### <a name="can-i-traverse-proxies-and-firewalls-using-pointtosite-capability"></a>지점 및 사이트 간 기능을 사용하여 프록시와 방화벽을 트래버스할 수 있습니까?
예. SSTP(보안 소켓 터널링 프로토콜)을 사용하여 방화벽을 통해 터널링합니다. 이 터널은 HTTP 연결로 표시됩니다.

### <a name="if-i-restart-a-client-computer-configured-for-pointtosite-will-the-vpn-automatically-reconnect"></a>지점 및 사이트 간 연결에 대해 구성된 클라이언트 컴퓨터를 다시 시작하면 VPN이 자동으로 다시 연결됩니까?
기본적으로 클라이언트 컴퓨터에서는 VPN 연결을 자동으로 다시 설정하지 않습니다.

### <a name="does-pointtosite-support-autoreconnect-and-ddns-on-the-vpn-clients"></a>지점 및 사이트 간 연결은 VPN 클라이언트에서 자동 다시 연결 및 DDNS를 지원합니까?
자동 다시 연결과 DDNS는 현재 지점 및 사이트 간 VPN에서 지원되지 않습니다.

### <a name="can-i-have-sitetosite-and-pointtosite-configurations-coexist-for-the-same-virtual-network"></a>동일한 가상 네트워크에 대해 사이트 간 구성과 지점 및 사이트 간 구성을 함께 사용할 수 있습니까?
예. 게이트웨이에 경로 기반 VPN 유형이 있는 경우 이 솔루션이 모두 작동합니다. 클래식 배포 모델의 경우 동적 게이트웨이가 필요합니다. 고정 라우팅 VPN 게이트웨이 또는 VpnType PolicyBased를 사용하는 게이트웨이에 지점 및 사이트 간을 지원하지 않습니다.

### <a name="can-i-configure-a-pointtosite-client-to-connect-to-multiple-virtual-networks-at-the-same-time"></a>지점 및 사이트 간 클라이언트를 여러 가상 네트워크에 동시에 연결하도록 구성할 수 있습니까?
예, 구성할 수 있습니다. 하지만 가상 네트워크에서는 겹치는 IP 접두사를 사용할 수 없으며, 지점 및 사이트 간 주소 공간은 가상 네트워크 간에 겹쳐질 수 없습니다.

### <a name="how-much-throughput-can-i-expect-through-sitetosite-or-pointtosite-connections"></a>사이트 간 연결 또는 지점 및 사이트 간 연결을 통해 어느 정도의 처리량을 제공할 수 있습니까?
VPN 터널의 정확한 처리량을 유지하는 것은 어렵습니다. IPsec과 SSTP는 암호화 중심 VPN 프로토콜입니다. 또한 처리량은 프레미스와 인터넷 간의 대기 시간과 대역폭에 의해 제한됩니다.

## <a name="gateways"></a>게이트웨이
### <a name="what-is-a-policybased-staticrouting-gateway"></a>정책 기반(고적 라우팅) 게이트웨이란?
정책 기반 게이트웨이는 정책 기반 VPN을 구현합니다. 정책 기반 VPN은 온-프레미스 네트워크와 Azure VNet 간의 주소 접두사의 조합에 따라 IPsec 터널을 통해 패킷을 암호화하고 전달합니다. 정책 또는 트래픽 선택기는 일반적으로 VPN 구성에서 액세스 목록으로 정의됩니다.

### <a name="what-is-a-routebased-dynamicrouting-gateway"></a>경로 기반(동적 라우팅) 게이트웨이란?
경로 기반 게이트웨이는 경로 기반 VPN을 구현합니다. 경로 기반 VPN은 IP 전달 또는 라우팅 테이블에서 “경로"를 사용하여 패킷을 해당 터널 인터페이스에 전달합니다. 그런 다음 터널 인터페이스는 터널로 들어오는 터널에서 나가는 패킷을 암호화하거나 암호 해독합니다. 경로 기반 VPN에 대한 정책 또는 트래픽 선택기는 임의 또는 와일드카드로 구성됩니다.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>VPN 게이트웨이 IP 주소를 만들기 전에 내 VPN 게이트웨이 IP 주소를 가져올 수 있나요?
아니요. IP 주소를 가져오려면 게이트웨이를 먼저 만들어야 합니다. VPN 게이트웨이를 삭제하고 다시 만들면 IP 주소가 변경됩니다.

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>내 VPN 터널을 어떻게 인증합니까?
Azure VPN은 PSK(미리 공유한 키) 인증을 사용합니다. VPN 터널을 만들 때 PSK(미리 공유한 키)를 생성합니다. Set Pre-Shared Key PowerShell cmdlet 또는 REST API를 사용하여 자동 생성된 PSK를 자체 PSK로 변경할 수 있습니다.

### <a name="can-i-use-the-set-preshared-key-api-to-configure-my-policybased-static-routing-gateway-vpn"></a>사전 공유 키 설정 API를 사용하여 정책 기반(고정 라우팅) 게이트웨이 VPN을 구성할 수 있습니까?
예, 사전 공유 키 설정 API 및 PowerShell cmdlet을 Azure 정책 기반(고정) VPN 및 경로 기반(동적) 라우팅 VPN을 구성하는 데 사용할 수 있습니다.

### <a name="can-i-use-other-authentication-options"></a>다른 인증 옵션을 사용할 수 있습니까?
인증에는 PSK(미리 공유한 키)를 사용하도록 제한됩니다.

### <a name="what-is-the-gateway-subnet-and-why-is-it-needed"></a>"게이트웨이 서브넷"은 무엇이고 왜 필요합니까?
프레미스 간 연결을 사용하도록 설정하기 위해 게이트웨이 서비스를 설정했습니다. 

VNet에 대한 게이트웨이 서브넷을 만들어서 VPN 게이트웨이를 구성해야 합니다. 모든 게이트웨이 서브넷이 제대로 작동하려면 이름을 GatewaySubnet으로 지정해야 합니다. 게이트웨이 서브넷에 다른 이름을 지정하지 않습니다. 게이트웨이 서브넷에 VM 또는 다른 항목을 배포하지 않습니다.

게이트웨이 서브넷 최소 크기는 전적으로 만들려는 구성에 따라 달라집니다. 게이트웨이 서브넷을 일부 구성에 대해 /29만큼 작게 만들 수 있지만 게이트웨이 서브넷을 /28 이상으로 만드는 것이 좋습니다(/28, /27, /26등). 

### <a name="can-i-deploy-virtual-machines-or-role-instances-to-my-gateway-subnet"></a>가상 컴퓨터 또는 역할 인스턴스를 내 게이트웨이 서브넷에 배포할 수 있습니까?
아니요.

### <a name="how-do-i-specify-which-traffic-goes-through-the-vpn-gateway"></a>VPN 게이트웨이를 통해 전송되는 트래픽을 지정하려면 어떻게 해야 합니까?
Azure 클래식 포털을 사용하는 경우 로컬 네트워크 아래의 네트워크 페이지에서 가상 네트워크에 대해 게이트웨이를 통해 전송할 각 범위를 추가합니다.

### <a name="can-i-configure-forced-tunneling"></a>강제 터널링을 구성할 수 있습니까?
예. [강제 터널링 구성](vpn-gateway-about-forced-tunneling.md)을 참조하세요.

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-to-connect-to-my-onpremises-network"></a>Azure에서 내 VPN 서버를 설정하여 온-프레미스 네트워크에 연결하는 데 사용할 수 있습니까?
예, Azure 마켓플레이스에서 또는 사용자 VPN 라우터를 만들어서 Azure에 사용자 VPN 게이트웨이 또는 서버를 배포할 수 있습니다. 온-프레미스 네트워크와 가상 네트워크 서브넷 간에 트래픽이 적절하게 라우팅되도록 하려면 가상 네트워크에서 사용자 정의 경로를 구성해야 합니다.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>내 VPN 게이트웨이에서 특정 포트가 열리는 이유는 무엇인가요?
Azure 인프라 통신을 위해 필요합니다. Azure 인증서에 의해 보호(잠김)됩니다. 적절한 인증서가 없는 경우 해당 게이트웨이 고객을 포함하여 외부 엔터티는 해당 끝점에 어떤 영향도 미칠 수 없습니다.

VPN 게이트웨이는 기본적으로 고객 개인 네트워크에 연결하는 하나의 NIC와 공용 네트워크를 연결하는 하나의 NIC를 갖춘 멀티홈 장치입니다. Azure 인프라 엔터티는 준수 이유로 고객 개인 네트워크에 연결할 수 없으므로 인프라 통신용 공용 끝점을 이용해야 합니다. 공용 끝점은 Azure 보안 감사에서 정기적으로 검색됩니다.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>게이트웨이 유형, 요구 사항 및 처리량에 대한 자세한 내용
자세한 내용은 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.

## <a name="multisite-and-vnettovnet-connectivity"></a>다중 사이트 및 VNet 간 연결
### <a name="which-type-of-gateways-can-support-multisite-and-vnettovnet-connectivity"></a>다중 사이트 및 VNet 간 연결을 지원할 수 있는 게이트웨이 유형은 무엇입니까?
경로 기반(동적 라우팅) VPN만 해당합니다.

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a>PolicyBased VPN 형식을 가진 VNet을 다른 RouteBased VPN 형식을 가진 VNet과 연결할 수 있습니까?
아니요, 두 가상 네트워크는 모두 경로 기반(동적 라우팅) VPN을 사용해야 합니다.

### <a name="is-the-vnettovnet-traffic-secure"></a>VNet 간 트래픽은 안전합니까?
예, IPsec/IKE 암호화로 보호됩니다.

### <a name="does-vnettovnet-traffic-travel-over-the-azure-backbone"></a>VNet-VNet 트래픽이 Azure 백본에서 이동됩니까?
예.

### <a name="how-many-onpremises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>하나의 가상 네트워크에 연결할 수 있는 온-프레미스 사이트 및 가상 네트워크 수는 어떻게 됩니까?
최대 기본 및 표준 동적 라우팅 게이트웨이의 경우 총 10개, 고성능 VPN 게이트웨이의 경우 총 30개까지 연결할 수 있습니다.

### <a name="can-i-use-pointtosite-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>여러 VPN 터널을 포함하는 내 가상 네트워크에서 지점 및 사이트 간 VPN을 사용할 수 있습니까?
예, 여러 온-프레미스 사이트 및 기타 가상 네트워크에 연결하는 VPN 게이트웨이에서 지정 및 사이트 간(P2S) VPN을 사용할 수 있습니다.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-onpremises-site-using-multisite-vpn"></a>다중 사이트 VPN을 사용하여 내 가상 네트워크와 온-프레미스 사이트 간에 여러 터널을 구성할 수 있습니까?
아니요, Azure 가상 네트워크와 온-프레미스 사이트 간에 중복 터널은 지원되지 않습니다.

### <a name="can-there-be-overlapping-address-spaces-among-the-connected-virtual-networks-and-onpremises-local-sites"></a>연결된 가상 네트워크와 온-프레미스 로컬 사이트 사이에 주소 공간이 겹칠 수 있습니까?
아니요. 주소 공간이 겹치면 네트워크 구성 파일 업로드 또는 "가상 네트워크 만들기"가 실패합니다.

### <a name="do-i-get-more-bandwidth-with-more-sitetosite-vpns-than-for-a-single-virtual-network"></a>단일 가상 네트워크보다 더 많은 사이트 간 VPN을 사용하면 대역폭이 증가합니까?
아니요, 지점 및 사이트 간 VPN을 포함하여 모든 VPN 터널은 동일한 Azure VPN 게이트웨이 및 사용 가능한 대역폭을 공유합니다.

### <a name="can-i-use-azure-vpn-gateway-to-transit-traffic-between-my-onpremises-sites-or-to-another-virtual-network"></a>Azure VPN 게이트웨이를 사용하여 온-프레미스 사이트 간에 또는 다른 가상 네트워크에 트래픽을 전송할 수 있습니까?
**클래식 배포 모델**<br>
 Azure VPN 게이트웨이 통한 전송 트래픽은 클래식 배포 모델을 사용할 수 있지만 네트워크 구성 파일에서 정적으로 정의된 주소 공간의 영향을 받습니다. BGP는 클래식 배포 모델을 사용하는 Azure 가상 네트워크 및 VPN 게이트웨이에서 아직 지원되지 않습니다. BGP를 사용하지 않고 전송 주소 공간을 수동으로 정의하면 오류가 발생하기 쉬우므로 사용하지 않는 것이 좋습니다.<br>
**리소스 관리자 배포 모델**<br>
Resource Manager 배포 모델을 사용하는 경우 자세한 내용은 [BGP](#bgp) 섹션을 참조하세요.

### <a name="does-azure-generate-the-same-ipsecike-preshared-key-for-all-my-vpn-connections-for-the-same-virtual-network"></a>Azure는 동일한 가상 네트워크의 모든 VPN 연결에 대해 동일한 IPsec/IKE 미리 공유한 키를 생성합니까?
아니요, 기본적으로 Azure는 VPN 연결마다 다른 미리 공유한 키를 생성합니다. 하지만 VPN 게이트웨이 키 생성 REST API 또는 PowerShell cmdlet을 사용하여 원하는 키 값을 설정할 수 있습니다. 키는 1 ~ 128자 사이의 영숫자 문자열이어야 합니다.

### <a name="does-azure-charge-for-traffic-between-virtual-networks"></a>Azure는 가상 네트워크 간 트래픽에 대해 요금을 청구합니까?
다른 Azure 가상 네트워크 간의 트래픽에서 Azure는 다른 Azure 지역 간에 트래버스되는 트래픽에 대해서만 요금을 청구합니다. 청구 요금은 Azure [VPN 게이트웨이 가격](https://azure.microsoft.com/pricing/details/vpn-gateway/) 페이지에 나열되어 있습니다.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-to-my-expressroute-circuit"></a>IPsec VPN을 사용하는 가상 네트워크를 Express 경로 회로에 연결할 수 있습니까?
예, 지원됩니다. 자세한 내용은 [공존하는 Express 경로 및 사이트 간 VPN 연결 구성](../expressroute/expressroute-howto-coexist-classic.md)을 참조하세요.

## <a name="a-namebgpabgp"></a><a name="bgp"></a>BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="crosspremises-connectivity-and-vms"></a>크로스-프레미스 연결 및 VM
### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-crosspremises-connection-how-should-i-connect-to-the-vm"></a>가상 컴퓨터가 가상 네트워크에 있고 프레미스 간 연결을 사용하는 경우 VM에 연결하려면 어떻게 해야 합니까?
몇 가지 옵션이 있습니다. RDP를 사용하도록 설정하고 끝점을 만든 경우 VIP를 사용하여 가상 컴퓨터에 연결할 수 있습니다. 이 경우 VIP 및 연결할 포트를 지정합니다. 가상 컴퓨터에서 트래픽에 대한 포트를 구성해야 합니다. 일반적으로 Azure 클래식 포털로 이동하여 컴퓨터에 대한 RDP 연결 설정을 저장합니다. 설정에는 필요한 연결 정보가 포함됩니다.

가상 네트워크에서 프레미스 간 연결을 구성한 경우 내부 DIP 또는 개인 IP 주소를 사용하여 가상 컴퓨터에 연결할 수 있습니다. 동일한 가상 네트워크에 있는 다른 가상 컴퓨터의 내부 DIP를 통해 가상 컴퓨터에 연결할 수도 있습니다. 가상 네트워크의 외부 위치에서 연결할 경우 DIP를 사용하여 가상 컴퓨터에 RDP할 수 없습니다. 예를 들어 지점 및 사이트 간 가상 네트워크를 구성하고 컴퓨터에서 연결을 설정하지 않은 경우 DIP를 통해 가상 컴퓨터에 연결할 수 없습니다.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-crosspremises-connectivity-does-all-the-traffic-from-my-vm-go-through-that-connection"></a>내 가상 컴퓨터가 프레미스 간 연결을 사용하는 가상 네트워크에 포함된 경우 내 VM의 모든 트래픽이 해당 연결을 통해 이동됩니까?
아니요. 대상 IP가 지정된 가상 네트워크 로컬 네트워크 IP 주소 범위에 포함되는 트래픽만 가상 네트워크 게이트웨이를 통해 이동됩니다. 대상 IP가 가상 네트워크 내에 있는 트래픽은 가상 네트워크 내에 유지됩니다. 다른 트래픽은 부하 분산 장치를 통해 공용 네트워크에 전송되고, 강제 터널링을 사용하는 경우 Azure VPN 게이트웨이를 통해 전송됩니다. 문제를 해결할 경우 게이트웨이를 통해 전송하려는 모든 범위가 로컬 네트워크에 나열되는지 확인해야 합니다. 로컬 네트워크 주소 범위가 가상 네트워크의 주소 범위와 겹치지 않는지 확인합니다. 또한 사용 중인 DNS 서버가 적절한 IP 주소로 이름을 확인하는지 확인합니다.

## <a name="virtual-network-faq"></a>가상 네트워크 FAQ
[가상 네트워크 FAQ](../virtual-network/virtual-networks-faq.md)에서 추가적인 가상 네트워크 정보를 제공합니다.




<!--HONumber=Nov16_HO2-->


