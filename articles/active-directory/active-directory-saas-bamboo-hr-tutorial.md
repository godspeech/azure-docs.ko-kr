---
title: '자습서: Bamboo HR과 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory에서 Bamboo HR을 사용하여 Single Sign-On, 자동화된 프로비전 등을 사용하도록 설정하는 방법을 알아봅니다.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila

ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2016
ms.author: jeedes

---
# 자습서: Bamboo HR과 Azure Active Directory 통합
이 자습서는 Azure 및 BambooHR의 통합을 보여주기 위한 것입니다.  
이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 항목이 있다고 가정합니다.

* 유효한 Azure 구독
* BambooHR Single Sign-on이 설정된 구독

이 자습서를 완료한 후 BambooHR에 할당한 Azure AD 사용자가 BambooHR 회사 사이트(서비스 공급자가 시작한 로그온)에서 또는 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 사용하여 응용 프로그램에 Single Sign-On 할 수 있습니다.

이 자습서에 설명된 시나리오는 다음 구성 요소로 이루어져 있습니다.

1. BambooHR에 응용 프로그램 통합 사용
2. Single Sign-On 구성
3. 사용자 프로비전 구성
4. 사용자 할당

![시나리오](./media/active-directory-saas-bamboo-hr-tutorial/IC796685.png "시나리오")

## BambooHR에 응용 프로그램 통합 사용
이 섹션은 BambooHR에 응용 프로그램 통합을 사용하도록 설정하는 방법을 간략하게 설명하기 위한 것입니다.

### BambooHR에 응용 프로그램 통합을 사용하도록 설정하려면 다음 단계를 수행합니다.
1. Azure 클래식 포털의 왼쪽 탐색 창에서 **Active Directory**를 클릭합니다.
   
   ![Active Directory](./media/active-directory-saas-bamboo-hr-tutorial/IC700993.png "Active Directory")
2. **디렉터리** 목록에서 디렉터리 통합을 사용하도록 설정할 디렉터리를 선택합니다.
3. 응용 프로그램 보기를 열려면 디렉터리 보기의 최상위 메뉴에서 **응용 프로그램**을 클릭합니다.
   
   ![응용 프로그램](./media/active-directory-saas-bamboo-hr-tutorial/IC700994.png "응용 프로그램")
4. 페이지 맨 아래에 있는 **추가**를 클릭합니다.
   
   ![응용 프로그램 추가](./media/active-directory-saas-bamboo-hr-tutorial/IC749321.png "응용 프로그램 추가")
5. **원하는 작업을 선택하세요.** 대화 상자에서 **갤러리에서 응용 프로그램 추가**를 클릭합니다.
   
   ![갤러리에서 응용 프로그램 추가](./media/active-directory-saas-bamboo-hr-tutorial/IC749322.png "갤러리에서 응용 프로그램 추가")
6. **검색 상자**에 **BambooHR**을 입력합니다.
   
   ![응용 프로그램 갤러리](./media/active-directory-saas-bamboo-hr-tutorial/IC796686.png "응용 프로그램 갤러리")
7. 결과 창에서 **BambooHR**을 선택하고 **완료**를 클릭하여 응용 프로그램을 추가합니다.
   
   ![BambooHR](./media/active-directory-saas-bamboo-hr-tutorial/IC796687.png "BambooHR")
   
   ## Single Sign-On 구성

이 섹션은 사용자가 SAML 프로토콜 기반 페더레이션을 사용하여 Azure AD의 계정으로 BambooHR에 인증할 수 있게 하는 방법을 간략하게 설명하기 위한 것입니다.  
이 절차의 일부로 base 64로 인코딩된 인증서 파일을 만들어야 합니다.  
이 절차를 잘 모르는 경우 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)을 참조하십시오.

### Single Sign-On을 구성하려면 다음 단계를 수행합니다.
1. Azure 클래식 포털의 **BambooHR** 응용 프로그램 통합 페이지에서 **Single Sign-On 구성**을 클릭하여 **Single Sign-On 구성** 대화 상자를 엽니다.
   
   ![시나리오](./media/active-directory-saas-bamboo-hr-tutorial/IC796685.png "시나리오")
2. **BambooHR에 대한 사용자 로그온 방법을 선택하십시오.** 페이지에서 **Microsoft Azure AD Single Sign-on**을 선택하고 **다음**을 클릭합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-bamboo-hr-tutorial/IC796688.png "Single Sign-On 구성")
3. **앱 URL 구성** 페이지의 **BambooHR 로그온 URL** 텍스트 상자에서 사용자가 사용한 URL을 입력하여 BambooHR 응용 프로그램에 로그인하고(예: https://company.bamboohr.com) **다음**을 클릭합니다.
   
   ![앱 URL 구성](./media/active-directory-saas-bamboo-hr-tutorial/IC796689.png "앱 URL 구성")
4. **BambooHR에서 Single Sign-On 구성** 페이지에서 **인증서 다운로드**를 클릭한 다음 컴퓨터에 인증서 파일을 저장합니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-bamboo-hr-tutorial/IC796690.png "Single Sign-On 구성")
5. 다른 웹 브라우저 창에서 BambooHR 회사 사이트에 관리자로 로그인합니다.
6. 홈페이지에서 다음 단계를 수행합니다.
   
   ![SSO(Single sign-on)](./media/active-directory-saas-bamboo-hr-tutorial/IC796691.png "SSO\(Single sign-on\)")
   
   1. **앱**을 클릭합니다.
   2. 왼쪽의 앱 메뉴에서 **Single Sign-on**을 클릭합니다.
   3. **SAML Single Sign-On**을 클릭합니다.
7. **SAML Single Sign-On** 섹션에서 다음 단계를 수행합니다.
   
   ![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/IC796692.png "SAML Single Sign-On")
   
   1. Azure 클래식 포털의 **BambooHR에 대한 Single Sign-On 구성** 대화 상자 페이지에서 **Single Sign-On 서비스 URL** 값을 복사한 다음 **SSO 로그인 URL** 텍스트 상자에 붙여넣습니다.
   2. 다운로드한 인증서에서 **Base-64로 인코딩된** 파일을 만듭니다.  
      
      > [!TIP]
      > 자세한 내용은 [이진 인증서를 텍스트 파일로 변환하는 방법](http://youtu.be/PlgrzUZ-Y1o)을 참조하십시오.
      > 
      > 
   3. Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **X.509 인증서** 텍스트 상자에 붙여넣습니다.
   4. **Save**를 클릭합니다.
8. Azure 클래식 포털에서 Single Sign-On 구성 확인을 선택하고 **완료**를 클릭하여 **Single Sign-On 구성** 대화 상자를 닫습니다.
   
   ![Single Sign-On 구성](./media/active-directory-saas-bamboo-hr-tutorial/IC796693.png "Single Sign-On 구성")
   
   ## 사용자 프로비전 구성

Azure AD 사용자가 BambooHR에 로그인할 수 있도록 하려면 BambooHR로 프로비전되어야 합니다.  
BambooHR의 경우 프로비전은 수동 작업입니다.

### 사용자 계정을 프로비전하려면 다음 단계를 수행합니다.
1. **BambooHR** 사이트에 관리자 권한으로 로그인합니다.
2. 위쪽에 도구 모음에서 **설정**을 클릭합니다.
   
   ![설정](./media/active-directory-saas-bamboo-hr-tutorial/IC796694.png "설정")
3. **개요**를 클릭합니다.
4. 왼쪽 탐색 창에서 **보안 > 사용자**로 이동합니다.
5. 관련된 텍스트 상자에 프로비전할 유효한 AAD 계정의 사용자 이름, 암호 및 전자 메일 주소를 입력합니다.
6. **Save**를 클릭합니다.

> [!NOTE]
> 다른 BambooHR 사용자 계정 생성 도구 또는 BambooHR이 제공한 API를 사용하여 AAD 사용자 계정을 프로비전할 수 있습니다.
> 
> 

## 사용자 할당
구성을 테스트하려면 응용 프로그램 사용을 허용하려는 Azure AD 사용자를 할당하여 액세스 권한을 부여해야 합니다.

### BambooHR에 사용자를 할당하려면 다음 단계를 수행합니다.
1. Azure 클래식 포털에서 테스트 계정을 만듭니다.
2. **BambooHR** 응용 프로그램 통합 페이지에서 **사용자 할당**을 클릭합니다.
   
   ![사용자 할당](./media/active-directory-saas-bamboo-hr-tutorial/IC796695.png "사용자 할당")
3. 테스트 사용자를 선택하고 **할당**을 클릭한 다음 **예**를 클릭하여 할당을 확인합니다.
   
   ![예](./media/active-directory-saas-bamboo-hr-tutorial/IC767830.png "예")

Single Sign-On 설정을 테스트하려면 액세스 패널을 엽니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](active-directory-saas-access-panel-introduction.md)를 참조하십시오.

<!---HONumber=AcomDC_0713_2016-->