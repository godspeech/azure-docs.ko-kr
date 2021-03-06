---
title: Azure Active Directory 로그인 활동 보고서 API 샘플 | Microsoft Docs
description: Azure Active Directory Reporting API를 시작하는 방법
services: active-directory
documentationcenter: ''
author: dhanyahk
manager: femila
editor: ''

ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/25/2016
ms.author: dhanyahk;markvi

---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Azure Active Directory 로그인 활동 보고서 API 샘플
이 항목은 Azure Active Directory Reporting API에 대한 항목 컬렉션의 일부입니다.  
Azure AD Reporting은 코드 또는 관련된 도구를 사용하여 로그인 활동 데이터에 액세스할 수 있는 API를 제공합니다.  
이 항목은 **로그인 활동 API**에 대한 샘플 코드를 제공하는 방법을 다룹니다.

다음을 참조하세요.

* 자세한 개념 정보는 [감사 로그](active-directory-reporting-azure-portal.md#audit-logs)를 참조하세요.
* [Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md) 을 참조하세요.

질문, 문제 또는 피드백은 [AAD Reporting 도움말](mailto:aadreportinghelp@microsoft.com)에 문의하세요.

## <a name="prerequisites"></a>필수 조건
이 항목에서 샘플을 사용하기 전에 [Azure AD Reporting API에 액세스하기 위한 필수 구성 요소](active-directory-reporting-api-prerequisites.md)를 완료해야 합니다.  

## <a name="powershell-script"></a>PowerShell 스크립트
    # This script will require the Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.windows.net/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save the output to a file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-the-script"></a>스크립트 실행
스크립트를 편집한 후에는 실행하여 감사 로그 보고서에서 예상한 데이터가 반환되는지 확인합니다.

스크립트는 JSON 형식으로 로그인 보고서의 출력을 반환합니다. 또한 동일한 출력으로 `SigninActivities.json` 파일을 만듭니다. 다른 보고서의 데이터를 반환하도록 스크립트를 수정하고 필요 없는 출력 형식을 주석으로 처리할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* 이 항목의 샘플을 사용자 지정하시겠습니까? [Azure Active Directory 로그인 활동 API 참조](active-directory-reporting-api-sign-in-activity-reference.md)를 확인하세요. 
* Azure Active Directory Reporting API를 사용하는 전체적인 개요를 확인하려는 경우 [Azure Active Directory Reporting API 시작](active-directory-reporting-api-getting-started.md)을 참조하세요.
* Azure Active Directory Reporting에 대한 자세한 내용을 알아보려면 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)를 참조하세요.  

<!--HONumber=Oct16_HO2-->


