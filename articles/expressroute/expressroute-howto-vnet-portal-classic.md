---
title: 클래식 포털에서 ExpressRoute에 대한 Virtual Network 및 게이트웨이 구성 | Microsoft Docs
description: 이 문서에서는 클래식 배포 모델 및 클래식 포털을 사용하여 ExpressRoute에 가상 네트워크를 설정하는 방법을 안내합니다.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: ''
tags: azure-service-management

ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc

---
# 클래식 포털에서 Express 경로에 대한 가상 네트워크 만들기
이 문서의 단계에서는 클래식 배포 모델 및 클래식 포털을 사용하여 ExpressRoute와 함께 사용할 가상 네트워크 및 가상 네트워크 게이트웨이를 구성하는 과정을 안내합니다.

리소스 관리자 배포 모델에 대한 지침을 보려는 경우 [PowerShell을 사용하여 가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-ps.md) 및 [ExpressRoute에 대한 Resource Manager VNet에 VPN Gateway 추가](expressroute-howto-add-gateway-resource-manager.md) 문서를 참조할 수 있습니다.

**Azure 배포 모델 정보**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## 클래식 VNet 및 게이트웨이 만들기
다음 단계에서는 클래식 VNet 및 가상 네트워크 게이트웨이를 만듭니다. 클래식 VNet을 이미 가지고 있는 경우 이 문서의 [기존 클래식 VNet 구성](#config) 섹션을 참조하세요.

1. [Azure 클래식 포털](http://manage.windowsazure.com)에 로그인합니다.
2. 화면의 왼쪽 아래에서 **새로 만들기**를 클릭합니다. 탐색 창에서 **네트워크 서비스**를 클릭한 다음 **가상 네트워크**를 클릭합니다. **사용자 지정 만들기**를 클릭하여 구성 마법사를 시작합니다.
3. **가상 네트워크 정보** 페이지에서 다음을 입력합니다.
   
   * **이름**: 가상 네트워크 이름을 지정합니다. VM 및 PaaS 인스턴스를 배포할 때 이 가상 네트워크 이름을 사용하므로 너무 복잡하지 않은 이름을 사용하는 것이 좋습니다.
   * **위치** – 위치는 리소스(VM)를 배치할 실제 위치(지역)과 직접적인 관련이 있습니다. 예를 들어, 이 가상 네트워크에 배포할 VM이 미국 동부에 물리적으로 있도록 하려면 해당 위치를 선택합니다. 만든 후 가상 네트워크와 연결된 지역을 변경할 수 없습니다.
4. **DNS 서버 및 VPN 연결** 페이지에서 다음 정보를 입력한 후 오른쪽 아래에서 다음 화살표를 클릭합니다.
   
   * **DNS 서버** - DNS 서버 이름 및 IP 주소를 입력하거나 바로 가기 메뉴에서 이전에 등록된 DNS 서버를 선택합니다. 이 설정은 DNS 서버를 만들지 않습니다. 이렇게 하면 이 가상 네트워크에 대한 이름 확인에 사용하려는 DNS 서버를 지정할 수 있습니다.
   * **사이트 간 연결** - **사이트 간 VPN 구성** 확인란을 선택합니다.
   * **Express 경로** – **Express 경로 사용** 확인란을 선택합니다. **사이트간 VPN 구성**을 선택한 경우에 이 옵션만이 나타납니다
   * **로컬 네트워크** - Express 경로에 대한 로컬 네트워크 사이트가 있어야 합니다. 그러나 Express 경로 연결의 경우 로컬 네트워크 사이트에 지정된 주소 접두사는 무시됩니다. 대신 라우팅을 위해 ExpressRoute 회로를 통해 Microsoft에 보급된 주소 접두사를 사용합니다.<BR>ExpressRoute 연결에 대해 만든 로컬 네트워크가 이미 있는 경우 드롭다운 목록에서 선택할 수 있습니다. 없는 경우 **새 로컬 네트워크 지정**을 선택합니다.
5. 이전 단계에서 새 로컬 네트워크 지정을 선택한 경우 **사이트 간 연결** 페이지가 표시됩니다. 로컬 네트워크를 구성하려면, 다음 정보를 입력한 후 다음 화살표를 클릭합니다.
   
   * **이름** - 로컬(온-프레미스) 네트워크 사이트를 호출할 이름입니다.
   * **주소 공간** - 시작 IP 및 CIDR(주소 수)를 포함합니다. 가상 네트워크에 대한 주소 범위와 겹치지 않는 한 임의의 주소 범위를 지정할 수 있습니다. 일반적으로 온-프레미스 네트워크에 대한 주소 범위를 지정하지만 Express 경로의 경우에 이러한 설정이 사용되지 않습니다. 그러나 이 설정은 클래식 포털을 사용하는 경우 로컬 네트워크를 만들기 위해 필요합니다.
   * **주소 공간 추가** -이 설정은 Express 경로와 관련이 없습니다.
6. **가상 네트워크 주소 공간** 페이지에서 다음 정보를 입력한 후 오른쪽 아래의 확인란을 클릭하여 네트워크를 구성합니다.
   
   * **주소 공간** - 시작 IP 및 주소 수를 포함합니다. 지정한 주소 공간이 로컬 네트워크에 있는 주소 공간과 겹치지 않는지 확인합니다.
   * **서브넷 추가** - 시작 IP 및 주소 수를 포함합니다. 추가 서브넷은 필요하지 않습니다.
   * **게이트웨이 서브넷 추가** - 게이트웨이 서브넷을 추가하려면 클릭합니다. 게이트웨이 서브넷은 가상 네트워크 게이트웨이에 대해서만 사용되며 이 구성에 필요합니다.<BR>ExpressRoute에 대한 게이트웨이 서브넷 CIDR(주소 수)은 /28 이상(/27, /26 등)이어야 합니다. 이렇게 하면 해당 서브넷에서 충분한 IP 주소를 허용하여 작동하도록 구성할 수 있습니다. 클래식 포털에서 ExpressRoute를 사용하는 확인란을 선택힌 경우 포털은 /28인 게이트웨이 서브넷을 지정합니다. 클래식 포털에서 CIDR 주소 수를 조정할 수 없습니다. 만든 게이트웨이 서브넷의 실제 이름이 **GatewaySubnet**이 아니더라도 게이트웨이 서브넷은 클래식 포털에서 **게이트웨이**로 표시됩니다. Azure 포털 또는 PowerShell을 사용하여 이 이름을 볼 수 있습니다.
7. 페이지 아래에 있는 확인 표시를 클릭하면 가상 네트워크 만들기가 시작됩니다. 완료되면 클래식 포털의 **네트워크** 페이지에 있는 **상태**에 **생성됨**이 표시됩니다.

## <a name="gw"></a>게이트웨이 만들기
1. **네트워크** 페이지에서 방금 만든 가상 네트워크를 클릭한 후 페이지 위쪽의 **대시보드**를 클릭합니다.
2. **대시보드** 페이지 아래에서 **게이트웨이 만들기**를 클릭하고 **동적 라우팅**을 선택합니다. **예**를 클릭하여 게이트웨이를 만들려 한다고 확인합니다.
3. 게이트웨이 만들기가 시작되면 게이트웨이가 시작되었음을 알려주는 메시지가 표시됩니다. 게이트웨이를 만드는 데에는 최대 45분이 걸릴 수 있습니다.
4. 네트워크를 회로에 연결합니다. [VNet을 Express 경로 회로에 연결하는 방법](expressroute-howto-linkvnet-classic.md) 문서의 지침을 따르세요.

## <a name="config"></a>Express 경로에 대한 기존 클래식 VNet 구성
이미 클래식 VNet이 있는 경우 클래식 포털에서 Express 경로에 연결하도록 구성할 수 있습니다. 설정은 위의 섹션과 동일하므로 필요한 설정에 익숙해지기 위해 해당 섹션을 읽습니다. Express 경로/사이트 간 공존 연결을 만드는 경우 과정은 [이 문서](expressroute-howto-coexist-classic.md)를 참조하세요. 이 문서의 단계와 다릅니다.

1. VNet 설정의 나머지 부분을 업데이트하기 전에 로컬 네트워크를 만들어야 합니다. 클래식 포털을 통해 Express 경로를 구성할 때 필요한 경우 새 로컬 네트워크를 만들려면 **새로 만들기** **>** **네트워크 서비스** **>** **가상 네트워크** **>** **로컬 네트워크 추가**를 클릭합니다. 마법사 단계를 따라서 로컬 네트워크를 만듭니다.
2. **구성** 페이지를 사용하여 VNet에 대한 설정의 나머지 부분을 업데이트하고 로컬 네트워크에 VNet을 연결합니다.
3. 설정을 구성한 후에 이 문서의 [게이트웨이 만들기](#gw) 섹션으로 이동하여 게이트웨이를 만듭니다.

## 다음 단계
* 가상 컴퓨터를 가상 네트워크에 추가하려면 [가상 컴퓨터 학습 경로](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)를 참조하세요.
* Express 경로에 대한 자세한 내용은 [Express 경로 개요](expressroute-introduction.md)를 참조하세요.

<!---HONumber=AcomDC_0921_2016-->