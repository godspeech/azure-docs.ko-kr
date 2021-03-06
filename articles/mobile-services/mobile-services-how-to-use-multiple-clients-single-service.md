---
title: 단일 모바일 서비스 백 엔드에서 여러 클라이언트를 사용하는 방법 | Microsoft Docs
description: 다양한 모바일 플랫폼을 대상으로 하는 여러 클라이언트 앱에서 단일 모바일 서비스 백 엔드를 사용하는 방법을 알아봅니다.
services: mobile-services
documentationcenter: ''
author: ggailey777
manager: dwrede
editor: mollybos

ms.service: mobile-services
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/21/2016
ms.author: glenga

---
# 단일 모바일 장치에서 여러 장치 플랫폼 지원
[!INCLUDE [mobile-service-note-mobile-apps](../../includes/mobile-services-note-mobile-apps.md)]

&nbsp;

모바일 앱 개발에서 Azure 모바일 서비스를 사용할 때의 주요 이점 중 하나는 여러 클라이언트 플랫폼에서 앱을 지원하는 단일 백 엔드 서비스를 사용할 수 있다는 것입니다. 모바일 서비스에서는 모든 주요 장치 플랫폼에 대해 네이티브 클라이언트 라이브러리를 제공하기 때문에 단일 백 엔드 서비스를 사용하고 교차 플랫폼 개발자 도구를 사용하여 앱을 좀 더 쉽게 개발할 수 있습니다. 이 항목에서는 단일 모바일 서비스 백 엔드를 사용하면서도 여러 클라이언트 플랫폼에서 앱을 실행할 수 있도록 하기 위한 고려 사항에 대해 설명합니다.

## <a id="push"></a>교차 플랫폼 푸시 알림
모바일 서비스는 Azure 알림 허브를 사용하여 모든 주요 장치 플랫폼의 클라이언트 앱에 푸시 알림을 보냅니다. 알림 허브에서는 장치 등록을 만들고 관리하며 교차 플랫폼 푸시 알림을 보내는 데 사용되는 일관된 통합 인프라를 제공합니다. 알림 허브는 다음과 같은 플랫폼별 알림 서비스를 사용하여 푸시 알림을 보내는 것을 지원합니다.

* iOS 앱용 APNS(Apple Push Notification Service)
* Android 앱용 GCM(Google Cloud Messaging) 서비스
* Windows Store, Windows Phone 8.1 Store 및 범용 Windows 앱용 WNS(Windows Notification Service)
* Windows Phone Silverlight 앱용 MPNS(Microsoft Push Notification Service)

자세한 내용은 [Azure 알림 허브]를 참조하십시오.

클라이언트 등록은 플랫폼별 모바일 서비스 클라이언트 라이브러리에서 등록 기능을 사용하거나 모바일 서비스 REST API를 사용하여 만듭니다. 알림 허브는 두 가지 종류의 장치 등록을 지원합니다.

* **기본 등록**<br/>기본 등록은 플랫폼별 푸시 알림 서비스에 맞춰져 있습니다. 기본 등록을 사용하여 등록된 장치에 알림을 보낼 때는 모바일 서비스에서 플랫폼별 API를 호출해야 합니다. 여러 플랫폼의 장치에 알림을 보내려면 여러 개의 플랫폼별 호출이 필요합니다.
* **템플릿 등록**<br/>알림 허브는 플랫폼별 템플릿 등록도 지원합니다. 템플릿 등록을 사용하면 단일 API 호출을 사용하여 등록된 플랫폼에서 실행 중인 앱에 알림을 보낼 수 있습니다. 자세한 내용은 [알림 허브를 통해 사용자에게 플랫폼 간 알림 보내기]를 참조하십시오.

다음 섹션에 있는 표는 .NET 및 JavaScript 백 엔드 모바일 서비스 모두에서 푸시 알림을 구현하는 방법을 보여 주는 클라이언트별 자습서로 연결됩니다.

### .NET 백 엔드
.NET 백 엔드 모바일 서비스에서는 [ApiServices.Push] 속성에서 가져온 [PushClient](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobile.service.notifications.pushclient.aspx) 개체에 [SendAsync](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobile.service.apiservices.push.aspx) 메서드를 호출함으로써 알림을 보냅니다. 보낸 푸시 알림(기본 또는 템플릿)은 다음 표에서와 같이 [SendAsync](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobile.service.notifications.ipushmessage.aspx) 메서드에 전달된 특정 [IPushMessage] 파생 개체에 따라 다릅니다.

| 플랫폼 | [APNS](mobile-services-dotnet-backend-ios-get-started-push.md) | [GCM](mobile-services-dotnet-backend-android-get-started-push.md) | [WNS](mobile-services-dotnet-backend-windows-store-dotnet-get-started-push.md) | MPNS |
| --- | --- | --- | --- | --- |
| 기본 |[ApplePushMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobile.service.applepushmessage.aspx) |[GooglePushMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobile.service.googlepushmessage.aspx) |[WindowsPushMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobile.service.windowspushmessage.aspx) |[MpnsPushMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobile.service.mpnspushmessage.aspx) |

다음 코드는 .NET 백 엔드 서비스에서 모든 iOS 및 Windows Store 디바이스 등록에 푸시 알림을 보냅니다.

    // Define a push notification for APNS.
    ApplePushMessage apnsMessage = new ApplePushMessage(item.Text, TimeSpan.FromHours(1));

    // Define a push notification for WNS.
    WindowsPushMessage wnsMessage = new WindowsPushMessage();
    wnsMessage.XmlPayload = @"<?xml version=""1.0"" encoding=""utf-8""?>" +
                         @"<toast><visual><binding template=""ToastText01"">" +
                         @"<text id=""1"">" + item.Text + @"</text>" +
                         @"</binding></visual></toast>";

    // Send push notifications to all registered iOS and Windows Store devices.
    await Services.Push.SendAsync(apnsMessage);
    await Services.Push.SendAsync(wnsMessage);

다른 기본 클라이언트 플랫폼에 푸시 알림을 보내는 방법에 대한 예제를 보려면 위 표의 헤더에서 플랫폼 링크를 클릭하세요.

기본 클라이언트 등록 대신 템플릿 클라이언트 등록을 사용할 때는 [SendAsync]에 대한 단일 호출만으로 같은 알림을 보냄으로써 다음과 같이 [TemplatePushMessage] 개체를 제공할 수 있습니다.

    // Create a new template message and add the 'message' parameter.
    var templatePayload = new TemplatePushMessage();
    templatePayload.Add("message", item.Text);

    // Send a push notification to all template registrations.
    await Services.Push.SendAsync(templatePayload);

### JavaScript 백 엔드
JavaScript 백 엔드 모바일 서비스에서는 다음 표에서와 같이 글로벌 **푸시 개체**에서 가져온 플랫폼별 개체에 [send] 메서드를 호출함으로써 알림을 보냅니다.

| 플랫폼 | [APNS](mobile-services-javascript-backend-ios-get-started-push.md) | [GCM](mobile-services-javascript-backend-android-get-started-push.md) | [WNS](mobile-services-javascript-backend-windows-store-dotnet-get-started-push.md) | [MPNS](mobile-services-javascript-backend-windows-phone-get-started-push.md) |
| --- | --- | --- | --- | --- |
| 기본 |[apns 개체](http://msdn.microsoft.com/library/azure/jj839711.aspx) |[gcm 개체](http://msdn.microsoft.com/library/azure/dn126137.aspx) |[wns 개체](http://msdn.microsoft.com/library/azure/jj860484.aspx) |[mpns 개체](http://msdn.microsoft.com/library/azure/jj871025.aspx) |

다음 코드는 모든 Android 및 Windows Phone 등록에 푸시 알림을 보냅니다.

    // Define a push notification for GCM.
    var gcmPayload =
    '{"data":{"message" : item.text }}';

    // Define the payload for a Windows Phone toast notification.
    var mpnsPayload = '<?xml version="1.0" encoding="utf-8"?>' +
    '<wp:Notification xmlns:wp="WPNotification"><wp:Toast>' +
    '<wp:Text1>New Item</wp:Text1><wp:Text2>' + item.text +
    '</wp:Text2></wp:Toast></wp:Notification>';

    // Send push notifications to all registered Android and Windows Phone 8.0 devices.
    push.mpns.send(null, mpnsPayload, 'toast', 22, {
            success: function(pushResponse) {
                // Push succeeds.
                },
                error: function (pushResponse) {
                    // Push fails.
                    }
                });
    push.gcm.send(null, gcmPayload, {
            success: function(pushResponse) {
                // Push succeeds.
                },
                error: function (pushResponse) {
                    // Push fails.
                    }
                });

다른 기본 클라이언트 플랫폼에 푸시 알림을 보내는 방법에 대한 예제를 보려면 위 표의 헤더에서 플랫폼 링크를 클릭하세요.

기본 클라이언트 등록 대신 템플릿 클라이언트 등록을 사용할 때는 글로벌 **푸시 개체**에 대한 [send] 기능의 단일 호출만으로 같은 알림을 보냄으로써 다음과 같이 템플릿 메시지 페이로드를 제공할 수 있습니다.

    // Create a new template message with the 'message' parameter.
    var templatePayload = { "message": item.text };

    // Send a push notification to all template registrations.
    push.send(null, templatePayload, {
            success: function(pushResponse) {
                // Push succeeds.
                },
                error: function (pushResponse) {
                    // Push fails.
                    }
                });

## <a id="xplat-app-dev"></a>교차 플랫폼 앱 개발
모든 주요 모바일 장치 플랫폼에 대한 기본 모바일 장치 앱을 개발하려면 최소한 Objective-C, Java 및 C# 또는 JavaScript 프로그래밍 언어에 대한 전문 지식이 필요합니다. 이처럼 여러 가지 플랫폼에서 개발해야 하는 비용 부담 때문에 일부 개발자들은 완전한 웹 브라우저 기반 환경을 앱에 사용하기로 선택합니다. 하지만 이러한 웹 기반 환경은 사용자들이 모바일 장치에서 기대하는 풍부한 환경을 제공하는 대다수의 기본 리소스에 액세스할 수 없습니다.

교차 플랫폼 도구는 단일 코드 기반(주로 JavaScript)을 공유하면서도 모바일 장치에 보다 풍부한 기본 환경을 제공합니다. 모바일 서비스를 사용하면 다음과 같은 개발 플랫폼에 대해 빠른 시작 자습서를 제공함으로써 교차 플랫폼 앱 개발 플랫폼의 백 엔드 서비스를 쉽게 만들고 관리할 수 있습니다.

* [**PhoneGap**](https://go.microsoft.com/fwLink/p/?LinkID=390707)**/**[**Cordova**](http://cordova.apache.org/)<br/>PhoneGap(Apache Cordova 프로젝트 배포)은 표준화된 웹 API, HTML 및 JavaScript를 사용하여 Android, iOS 및 Windows 장치에서 실행되는 단일 앱을 개발할 수 있게 해 주는 무료 오픈 소스 프레임워크입니다. PhoneGap은 웹 뷰 기반의 UI를 제공하지만 푸시 알림, 가속도계, 카메라, 저장소, 지리적 위치, 앱 내 브라우저 등 장치의 기본 리소스에 액세스함으로써 사용자 환경을 개선합니다. 자세한 내용은 [PhoneGap 빠른 시작 자습서][PhoneGap]를 참조하세요.
  
    이제 Visual Studio에서는 시험판 소프트웨어인 Visual Studio용 Multi-Device Hybrid Apps 확장을 사용하여 교차 플랫폼 Cordova 앱을 구축할 수 있습니다. 자세한 내용은 [HTML 및 JavaScript를 사용하여 Multi-Device Hybrid Apps 시작](http://msdn.microsoft.com/library/dn771545.aspx)(영문)을 참조하십시오.
* [**Sencha Touch**](http://go.microsoft.com/fwlink/p/?LinkId=509988)<br/>Sencha Touch는 단일 HTML 및 JavaScript 코드 기반에서 다양한 모바일 장치에 기본 환경과 비슷한 환경을 제공하는 터치 스크린에 최적화된 다양한 컨트롤을 갖추고 있습니다. Sencha Touch를 PhoneGap 또는 Cordova 라이브러리와 함께 사용하여 기본 장치 리소스에 대한 사용자 액세스를 제공할 수 있습니다. 자세한 내용은 [Sencha Touch 빠른 시작 자습서][Sencha]를 참조하십시오.
* [**Xamarin**](https://go.microsoft.com/fwLink/p/?LinkID=330242)<br/>Xamarin을 사용하면 iOS 및 Android 장치 모두에서 완전한 기본 UI를 갖추고 모든 장치 리소스에 액세스할 수 있는 완전한 기본 앱을 만들 수 있습니다. Xamarin 앱은 Objective-C 및 Java가 아니라 C#으로 코딩되어 있습니다. 따라서 .NET 개발자는 앱을 iOS 및 Android에 게시하고 Windows 프로젝트의 코드를 공유할 수 있습니다. Xamarin은 C# 코드에서 iOS 및 Android 장치 모두에 완전한 기본 사용자 환경을 제공합니다. 덕분에 iOS 및 Android 장치의 Windows 앱에서 일부 모바일 서비스 코드를 재사용할 수 있습니다. 자세한 내용은 아래의 [Xamarin 개발](#xamarin)을 참조하십시오.

<!-- URLs -->
[Azure 알림 허브]: /develop/net/how-to-guides/service-bus-notification-hubs/
[SSO Windows Store]: /develop/mobile/tutorials/single-sign-on-windows-8-dotnet/
[SSO Windows Phone]: /develop/mobile/tutorials/single-sign-on-wp8/
[Tutorials and resources]: /develop/mobile/resources/
[Get started with Notification Hubs]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[알림 허브를 통해 사용자에게 플랫폼 간 알림 보내기]: /manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Get started with push Windows dotnet]: /develop/mobile/tutorials/get-started-with-push-dotnet-vs2012/
[Get started with push Windows js]: /develop/mobile/tutorials/get-started-with-push-js-vs2012/
[Get started with push Windows Phone]: /develop/mobile/tutorials/get-started-with-push-wp8/
[Get started with push iOS]: /develop/mobile/tutorials/get-started-with-push-ios/
[Get started with push Android]: /develop/mobile/tutorials/get-started-with-push-android/
[Dynamic schema]: http://msdn.microsoft.com/library/windowsazure/jj193175.aspx
[How to use a .NET client with Mobile Services]: documentation/articles/mobile-services-windows-dotnet-how-to-use-client-library/
[send]: http://msdn.microsoft.com/library/windowsazure/jj554217.aspx
[TemplatePushMessage]: http://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobile.service.templatepushmessage.aspx
[PhoneGap]: mobile-services-javascript-backend-phonegap-get-started.md
[Sencha]: partner-sencha-mobile-services-get-started.md
[Appcelerator]: partner-appcelerator-mobile-services-javascript-backend-appcelerator-get-started.md
[SendAsync]: http://msdn.microsoft.com/library/microsoft.windowsazure.mobile.service.notifications.pushclient.sendasync.aspx
[ApiServices.Push]: http://msdn.microsoft.com/library/microsoft.windowsazure.mobile.service.notifications.pushclient.sendasync.aspx
[IPushMessage]: http://msdn.microsoft.com/library/microsoft.windowsazure.mobile.service.notifications.pushclient.sendasync.aspx
[What's next for Windows Phone 8 developers]: http://msdn.microsoft.com/library/windows/apps/dn655121(v=vs.105).aspx
[Building universal Windows apps for all Windows devices]: http://go.microsoft.com/fwlink/p/?LinkId=509905
[Universal Windows app project for Azure Mobile Services using MVVM]: http://code.msdn.microsoft.com/Universal-Windows-app-for-db3564de

<!---HONumber=AcomDC_0727_2016-->