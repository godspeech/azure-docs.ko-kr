---
title: Azure 보안 센터 빠른 시작 가이드| Microsoft Docs
description: 이 문서는 Azure 보안 센터를 신속하게 시작할 수 있도록 보안 모니터링 및 정책 관리 구성 요소를 안내하고 다음 단계로 연결해 줍니다.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''

ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: terrylan

---
# Azure 보안 센터 빠른 시작 가이드
이 문서는 Azure 보안 센터를 신속하게 시작할 수 있도록 보안 모니터링 및 정책 관리 구성 요소를 안내하고 다음 단계로 연결해 줍니다.

> [!NOTE]
> 이 문서에서는 배포 예제를 사용하여 서비스를 소개합니다. 단계별 가이드는 아닙니다.
> 
> 

## 데이터 수집
보안 센터는 해당 보안 상태를 평가하고 보안 권장 사항을 제공하며 위협에 경고하기 위해 가상 컴퓨터에서 데이터를 수집합니다. 보안 센터에 처음 액세스할 경우 구독의 모든 가상 컴퓨터에서 데이터 수집을 활성화합니다. 데이터 수집를 사용하는 것이 좋지만 보안 센터 정책에서 데이터 수집을 해제하여 옵트아웃할 수 있습니다. 다음 단계에서는 데이터 수집을 해제하는 방법을 보여 줍니다.

## 필수 조건
보안 센터를 시작하려면 Microsoft Azure에 대한 구독이 있어야 합니다. 보안 센터는 구독을 사용하여 사용하도록 설정됩니다. 구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.

보안 센터는 [Azure 포털](https://azure.microsoft.com/features/azure-portal/)에서 액세스합니다. 자세한 내용은 [포털 설명서](https://azure.microsoft.com/documentation/services/azure-portal/)를 참조하세요.

## 보안 센터 엑세스
포털에서 다음 단계에 따라 보안 센터에 액세스합니다.

1. **찾아보기**를 선택한 다음 **보안 센터** 옵션으로 스크롤합니다. ![포털에서 Azure 보안 센터 액세스][1]
2. **보안 센터**를 선택합니다. 그러면 **보안 센터** 블레이드가 열립니다.
3. 나중에 **보안 센터** 블레이드에 간편하게 액세스하려면, **대시보드에 블레이드 고정** 옵션(오른쪽 위)을 선택합니다. ![대시보드 옵션에 블레이드 고정][2]

## 보안 센터 사용
Azure 구독 및 리소스 그룹에 대한 보안 정책을 구성할 수 있습니다. 다음과 같이 구독에 대한 보안 **정책**을 구성하세요.

1. **보안 센터** 블레이드에서 **정책** 타일을 선택합니다. ![보안 센터][3]
2. **보안 정책–구독 또는 리소스 그룹당 정책 정의** 블레이드에서 구독을 선택합니다. ![Azure 보안 센터의 보안 정책 블레이드][4]
3. **보안 정책** 블레이드에서 자동으로 로그를 수집하도록 **데이터 컬렉션**을 활성화합니다. 구독에 있는 현재 VM과 새로운 VM에 모니터링 확장이 프로비전됩니다. (**데이터 수집**을 **Off**로 설정하여 데이터 수집을 옵트아웃할 수 있지만 보안 센터가 보안 경고 및 권장 사항을 제공하지 않도록 방지합니다.)
4. **지역당 저장소 계정 선택**을 선택합니다. 가상 컴퓨터를 실행 중인 각 영역에 대해 가상 컴퓨터에서 수집한 데이터가 저장되는 저장소 계정을 선택합니다. 각 지역에 대한 저장소 계정을 선택하지 않으면 사용자를 위해 계정이 생성됩니다. 수집된 데이터는 보안상의 이유로 다른 고객의 데이터와 논리적으로 격리됩니다.
   
   > [!NOTE]
   > 먼저 구독 수준에서 데이터 수집을 활성화하고 저장소 계정을 선택하는 것이 좋습니다. Azure 구독 수준 및 리소스 그룹 수준에서 보안 정책을 설정할 수 있지만 데이터 수집 및 저장소 계정 구성은 구독 수준에서만 발생합니다.
   > 
   > 
5. 보안 정책의 일부로 표시하려는 **권장 사항**을 켭니다. 예제:
   
   * **시스템 업데이트**를 켜면 지원되는 모든 가상 컴퓨터에 누락된 OS 업데이트가 있는지를 검사합니다.
   * **OS 취약성**을 켜면 가상 컴퓨터를 공격에 취약하게 만들만한 OS 구성이 있는지를 식별하기 위해 지원되는 모든 가상 컴퓨터를 검사합니다.

**권장 사항** 표시:

1. **보안 센터** 블레이드로 돌아가서 **권장 사항** 타일을 선택합니다. 보안 센터에서는 Azure 리소스의 보안 상태를 주기적으로 분석합니다. 잠재적인 보안 취약성이 확인되면 이 위치에 권장 사항이 표시됩니다.
2. 각각의 권장 사항을 선택하고 자세한 정보를 표시하거나 문제를 해결하기 위해 필요한 조치를 취합니다. ![Azure 보안 센터의 권장 사항][5]

**리소스 보안 상태**를 통해 리소스의 상태 및 보안 상태를 봅니다.

1. **보안 센터** 블레이드로 돌아갑니다.
2. **리소스 보안 상태** 타일에는 **가상 컴퓨터**, **네트워킹**, **SQL**, **응용 프로그램**의 보안 상태에 대한 지표가 포함됩니다.
3. 자세한 내용을 보려면 **가상 컴퓨터**를 선택합니다.
4. **가상 컴퓨터** 블레이드는 가상 컴퓨터의 맬웨어 방지 프로그램, 시스템 업데이트, 다시 시작 및 기준 규칙의 상태를 보여 주는 상태 요약을 표시합니다.
5. **가상 컴퓨터 권장 사항**에서 항목을 선택하여 자세한 정보를 보거나/보고 필요한 컨트롤을 구성하도록 조치를 취합니다.
6. 특정 가상 컴퓨터에 대해 추가적인 정보를 보려면 드릴다운합니다. ![Azure 보안 센터의 리소스 상태 타일][6]

**보안 경고**를 다룹니다.

1. **보안 센터** 블레이드로 돌아가서 **보안 경고** 타일을 선택합니다. **보안 경고** 블레이드에 경고 목록이 표시됩니다. 경고는 사용자의 보안 로그 및 네트워크 작업의 Azure 보안 센터 분석을 사용하여 생성됩니다. 통합된 파트너 솔루션에서 보내는 경고도 포함됩니다. ![Azure 보안 센터의 보안 경고][7]
2. 경고를 선택하여 추가적인 정보를 표시합니다. ![Azure 보안 센터의 보안 경고 세부 정보][8]

**파트너 솔루션**의 상태를 봅니다.

1. **보안 센터** 블레이드로 돌아갑니다. **파트너 솔루션** 타일을 통해 Azure 구독과 통합된 파트너 솔루션의 상태를 한 눈에 모니터링할 수 있습니다.
2. **파트너 솔루션** 타일을 선택합니다. 블레이드가 열리고 보안 센터에 연결된 파트너 솔루션의 목록을 표시합니다. ![파트너 솔루션][9]
3. 파트너 솔루션을 선택합니다. 이 예제에서는 **F5 WAF2** 솔루션을 선택하도록 합니다. 블레이드가 열리고 파트너 솔루션의 상태 및 솔루션의 관련 리소스를 표시합니다. **솔루션 콘솔**을 선택하여 이 솔루션에 대한 파트너 관리 환경을 엽니다. ![파트너 솔루션 세부 정보][10]

## 참고 항목
이 문서에서는 보안 센터의 보안 모니터링 및 정책 관리 구성 요소를 소개했습니다. 자세한 알아보려면 다음을 참조하세요.

* [Azure 보안 센터에서 보안 정책 설정](security-center-policies.md) - Azure 구독 및 리소스 그룹에 대해 보안 정책을 구성하는 방법을 알아봅니다.
* [Azure 보안 센터에서 보안 권장 사항 관리](security-center-recommendations.md) - 권장 사항이 Azure 리소스 보호에 어떤 도움이 되는지를 알아봅니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) - Azure 리소스의 상태를 모니터링하는 방법을 알아봅니다.
* [Azure 보안 센터에서 보안 경고 관리 및 대응](security-center-managing-and-responding-alerts.md) - 보안 경고를 관리하고 대응하는 방법을 알아봅니다.
* [Azure 보안 센터를 사용하여 파트너 솔루션 모니터링](security-center-partner-solutions.md) - 파트너 솔루션의 상태를 모니터링하는 방법을 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) - 서비스 사용에 관한 질문과 대답을 찾습니다.
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) - 최신 Azure 보안 뉴스 및 정보를 가져옵니다.

<!--Image references-->
[1]: ./media/security-center-get-started/security-tile.png
[2]: ./media/security-center-get-started/pin-blade.png
[3]: ./media/security-center-get-started/security-center.png
[4]: ./media/security-center-get-started/security-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/partner-solutions-detail.png

<!---HONumber=AcomDC_0810_2016-->