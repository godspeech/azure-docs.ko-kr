# 개요
## [Application Insights란?](app-insights-overview.md)
## [작동 방법](app-insights-detect-triage-diagnose.md)

# 시작
## Azure 모니터링
### [Azure 웹앱](app-insights-azure-web-apps.md)
### [Azure 클라우드 서비스](app-insights-cloudservices.md)

## ASP.NET 앱 모니터링
### [웹앱](app-insights-asp-net.md)
### [이미 라이브 상태인 웹앱](app-insights-monitor-performance-live-website-now.md)
### [Windows 서비스](app-insights-windows-services.md)
### [Windows 데스크톱](app-insights-windows-desktop.md)

## Java 앱 모니터링
### [웹앱](app-insights-java-get-started.md)
### [웹앱-런타임](app-insights-java-live.md)
### [Docker 앱](app-insights-docker.md)

## 웹 페이지 모니터링
### [JavaScript](app-insights-javascript.md)

## 기타 플랫폼 모니터링
### [Node.js 앱](app-insights-nodejs.md)
### [SharePoint 사이트](app-insights-sharepoint.md)
### [기타 플랫폼](app-insights-platforms.md)

## [ASP.NET에 대한 FAQ](app-insights-troubleshoot-faq.md)

# 방법
## 계획 및 디자인

### [웹앱 및 서비스 심층 진단](app-insights-devops.md)
### [Application Insights 및 HockeyApp을 사용한 개발자 분석](app-insights-developer-analytics.md)
### [웹 응용 프로그램의 성능 모니터링](app-insights-web-monitor-performance.md)
### [Application Insights를 사용하여 사용량 분석](app-insights-overview-usage.md)
### [Application Insights 리소스 구분](app-insights-separate-resources.md)
### [Application Insights에서 다음을 수행하는 방법](app-insights-how-do-i.md)

## 구성

### Azure
#### [진단](app-insights-azure-diagnostics.md)

### ASP.NET
#### [더 많은 원격 분석 수집](app-insights-asp-net-more.md)
#### [예외](app-insights-asp-net-exceptions.md)
#### [로그 추적](app-insights-asp-net-trace-logs.md)
#### [성능 카운터](app-insights-performance-counters.md)
#### [종속성](app-insights-asp-net-dependencies.md)
#### [릴리스 주석](app-insights-annotations.md)


### J2EE
#### [로그 추적](app-insights-java-trace-logs.md)
#### [Unix 메트릭](app-insights-java-collectd.md)
#### [종속성](app-insights-java-agent.md)

### 경고

#### [Availability](app-insights-monitor-web-app-availability.md)
#### [메트릭 경고](app-insights-alerts.md)

### [스마트 감지](app-insights-proactive-diagnostics.md)
#### [실패 감지](app-insights-proactive-failure-diagnostics.md)
#### [이상 감지](app-insights-proactive-performance-diagnostics.md)

## 분석

### Application Insights 포털

#### [대시보드](app-insights-dashboards.md)
#### [이를 통해 검색](app-insights-diagnostic-search.md)
#### [metrics](app-insights-metrics-explorer.md)
#### 분석

##### [분석](app-insights-analytics.md)
##### [분석 둘러보기](app-insights-analytics-tour.md)
##### [분석 사용](app-insights-analytics-using.md)

#### [응용 프로그램 맵](app-insights-app-map.md)
#### [HockeyApp 데이터](app-insights-hockeyapp-bridge-app.md)
#### [리소스 그룹 만들기](app-insights-create-new-resource.md)

### Visual Studio

#### [F5 통찰력](app-insights-visual-studio.md)
#### [추세](app-insights-visual-studio-trends.md)
#### [CodeLens](app-insights-visual-studio-codelens.md)

## 자동화

### [PowerShell 구성](app-insights-powershell.md)
### [리소스 만들기](app-insights-powershell-script-create-resource.md)
### [경고 설정](app-insights-powershell-alerts.md)
### [Azure 진단 가져오기](app-insights-powershell-azure-diagnostics.md)


## 통합

### [연속 내보내기](app-insights-export-telemetry.md)
### [Power BI에 내보내기](app-insights-export-power-bi.md)


## 개발

### [사용자 지정 이벤트 및 메트릭용 API ](app-insights-api-custom-events-metrics.md)
### [필터링 및 원격 분석 전처리](app-insights-api-filtering-sampling.md)
### [ASP.NET Core](app-insights-asp-net-core.md)


## 관리

### [가격 책정 및 할당량 관리](app-insights-pricing.md)
### [SCOM에 대해 Application Insights를 사용하여 응용 프로그램 성능 모니터링](app-insights-scom.md)


## 보안

### [데이터 수집, 보존 및 저장](app-insights-data-retention-privacy.md)
### [리소스, 역할 및 액세스 제어](app-insights-resources-roles-access-control.md)


## 문제 해결
### [.NET에 대한 데이터 없음](app-insights-asp-net-troubleshoot-no-data.md)
### [분석](app-insights-analytics-troubleshooting.md)
### [Java](app-insights-java-troubleshoot.md)

# 참조
## [Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
## [.NET API](https://docs.microsoft.com/dotnet/api)
## [JavaScript API](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
## [분석](app-insights-analytics-reference.md)
## [샘플링](app-insights-sampling.md)
## [IP 주소](app-insights-ip-addresses.md)
## [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)
## [데이터 모델 내보내기](app-insights-export-data-model.md)
## [Azure 끝점 모니터링에서 가용성 테스트로 마이그레이션](app-insights-migrate-azure-endpoint-tests.md)
## [개발자 분석: 언어, 플랫폼 및 통합](app-insights-platforms.md)
### [샘플 및 연습](app-insights-code-samples.md)
#### [연습: Microsoft Dynamics CRM Online에 대한 원격 분석 설정](app-insights-sample-mscrm.md)
#### [연습: Stream Analytics를 사용하여 SQL로 내보내기](app-insights-code-sample-export-sql-stream-analytics.md)
#### [코드 샘플: 내보내는 데이터 구문 분석](app-insights-code-sample-export-telemetry-sql-database.md)
## [Windows Phone 및 Store용 Application Insights SDK에 대한 릴리스 정보](app-insights-release-notes-windows.md)
## [개발자 분석 도구에 대한 릴리스 정보](app-insights-release-notes-vsix.md)
## [SDK 릴리스 정보 - Application Insights](app-insights-release-notes.md)
## [REST API](https://dev.applicationinsights.io/)

# 리소스
## [가격 책정](https://azure.microsoft.com/pricing/details/application-insights/)  
## [MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=ApplicationInsights)  
## [스택 오버플로](http://stackoverflow.com/questions/tagged/az-application-insights)
## [비디오](https://azure.microsoft.com/documentation/videos/index/?services=application-insights) 
## [서비스 업데이트](https://azure.microsoft.com/en-us/updates/?product=application-insights) 
## [지원](app-insights-get-dev-support.md)



<!--HONumber=Nov16_HO2-->


