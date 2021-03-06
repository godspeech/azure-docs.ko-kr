---
title: 리소스 연결을 위한 리소스 관리자 템플릿 | Microsoft Docs
description: 템플릿을 통해 관련 리소스 간 링크를 배포하기 위한 리소스 관리자 스키마를 보여 줍니다.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: ''

ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2016
ms.author: tomfitz

---
# 리소스 링크 템플릿 스키마
두 리소스 간의 링크를 만듭니다. 링크는 원본 리소스라고 하는 리소스에 적용됩니다. 링크의 두 번째 리소스는 대상 리소스라고 합니다.

## 스키마 형식
링크를 만들려면 템플릿의 리소스 섹션에 다음 스키마를 추가합니다.

    {
        "type": enum,
        "apiVersion": "2015-01-01",
        "name": string,
        "dependsOn": [ array values ],
        "properties":
        {
            "targetId": string,
            "notes": string
        }
    }



## 값
다음 표에서는 스키마에 설정해야 하는 값에 대해 설명합니다.

| 이름 | 값 |
| --- | --- |
| type |열거형<br />필수<br />**{namespace}/{type}/providers/links**<br /><br />만들려는 리소스 종류입니다. {namespace} 및 {type} 값은 원본 리소스의 공급자 네임스페이스 및 리소스 종류를 나타냅니다. |
| apiVersion |열거형<br />필수<br />**2015-01-01**<br /><br />리소스를 만들 때 사용하는 API 버전입니다. |
| name |문자열<br />필수<br />**{resouce}/Microsoft.Resources/{linkname}****<br /> 최대 64자이며, <, > %, &, ? 또는 제어 문자를 포함할 수 없습니다.<br /><br />원본 리소스 이름과 링크 이름을 둘 다 지정하는 값입니다. |
| dependsOn |Array<br />선택<br />쉼표로 구분된 리소스 이름 및 리소스 고유 식별자 목록입니다.<br /><br />이 링크에 따라 달라지는 리소스 컬렉션입니다. 연결하려는 리소스가 동일한 템플릿으로 배포되는 경우 해당 리소스 이름을 이 요소에 포함하여 먼저 배포되도록 해야 합니다. |
| properties |개체<br />필수<br />[properties 개체](#properties)<br /><br />연결할 리소스를 식별하고 링크에 대해 설명하는 개체입니다. |

<a id="properties" />

### properties 개체
| 이름 | 값 |
| --- | --- |
| 대상 ID |문자열<br />필수<br />**{resource id}**<br />연결할 대상 리소스의 식별자입니다.<br />. |

## 링크 리소스를 사용하는 방법
리소스가 배포 후에도 계속되는 종속성을 가진 경우 두 리소스 사이에 링크를 적용합니다. 예를 들어 앱이 다른 리소스 그룹의 데이터베이스에 연결할 수 있습니다. 앱에서 데이터베이스로의 링크를 만들어 해당 종속성을 정의할 수 있습니다. 링크를 사용하여 두 리소스 간의 관계를 문서화할 수 있습니다. 나중에 사용자 또는 조직 내 다른 사람이 리소스에 링크를 쿼리하여 해당 리소스가 다른 리소스와 어떻게 함께 작동하는지 검색할 수 있습니다.

연결된 모든 리소스는 동일한 구독에 속해야 합니다. 각 리소스는 다른 50개의 리소스에 연결될 수 있습니다. 연결된 리소스 중 하나가 삭제되거나 이동되면 링크 소유자는 나머지 링크를 청정리해야 합니다.

REST를 통해 링크 작업을 하려면 [연결된 리소스](https://msdn.microsoft.com/library/azure/mt238499.aspx)(영문)를 참조하세요.

다음 Azure PowerShell 명령을 사용하면 구독의 모든 링크를 확인할 수 있습니다. 결과를 제한하려면 다른 매개 변수를 지정할 수 있습니다.

    Get-AzureRmResource -ResourceType Microsoft.Resources/links -isCollection -ResourceGroupName <YourResourceGroupName>

## 예
다음 예제에서는 웹앱에 읽기 전용 잠금을 적용합니다.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "hostingPlanName": {
                "type": "string"
            }
        },
        "variables": {
            "siteName": "[concat('site',uniqueString(resourceGroup().id))]"
        },
        "resources": [
            {
                "apiVersion": "2015-08-01",
                "type": "Microsoft.Web/serverfarms",
                "name": "[parameters('hostingPlanName')]",
                "location": "[resourceGroup().location]",
                "sku": {
                    "tier": "Free",
                    "name": "f1",
                    "capacity": 0
                },
                "properties": {
                    "numberOfWorkers": 1
                }
            },
            {
                "apiVersion": "2015-08-01",
                "name": "[variables('siteName')]",
                "type": "Microsoft.Web/sites",
                "location": "[resourceGroup().location]",
                "dependsOn": [ "[parameters('hostingPlanName')]" ],
                "properties": {
                    "serverFarmId": "[parameters('hostingPlanName')]"
                }
            },
            {
                "type": "Microsoft.Web/sites/providers/links",
                "apiVersion": "2015-01-01",
                "name": "[concat(variables('siteName'),'/Microsoft.Resources/SiteToStorage')]",
                "dependsOn": [ "[variables('siteName')]" ],
                "properties": {
                    "targetId": "[resourceId('Microsoft.Storage/storageAccounts','storagecontoso')]",
                    "notes": "This web site uses the storage account to store user information."
                }
            }
        ],
        "outputs": {}
    }

## 빠른 시작 템플릿
다음 빠른 시작 템플릿은 링크를 사용하여 리소스를 배포합니다.

* [논리 앱으로 큐에 경고](https://azure.microsoft.com/documentation/templates/201-alert-to-queue-with-logic-app)
* [논리 앱으로 Slack에 경고](https://azure.microsoft.com/documentation/templates/201-alert-to-slack-with-logic-app)
* [기존 게이트웨이로 API 앱을 프로비전](https://azure.microsoft.com/documentation/templates/201-api-app-gateway-existing)
* [새 게이트웨이로 API 앱을 프로비전](https://azure.microsoft.com/documentation/templates/201-api-app-gateway-new)
* [템플릿을 사용하여 논리 앱과 API 앱 만들기](https://azure.microsoft.com/documentation/templates/201-logic-app-api-app-create)
* [경고가 발생할 때 문자 메시지를 전송하는 논리 앱](https://azure.microsoft.com/documentation/templates/201-alert-to-text-message-with-logic-app)

## 다음 단계
* 템플릿 구조에 대한 자세한 내용은 [Azure 리소스 관리자 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.

<!---HONumber=AcomDC_0406_2016-->