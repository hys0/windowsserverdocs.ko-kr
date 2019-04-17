---
title: 정책 QoS 시나리오
description: 이 항목의 특정 응용 프로그램 및 Windows Server 2016 서비스 네트워크 교통 우선 순위를 정하는 그룹 정책을 사용 하는 방법을 보여 주는 (QoS) 서비스 품질 정책 시나리오를 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c4306f06-a117-4f65-b78b-9fd0d1133f95
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b635f73cc25552f4c1a05f8db6303f636eda3c54
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-scenarios"></a>정책 QoS 시나리오

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목을 보여 주는 가상 시나리오를 검토 하는 데 사용할 수 방법을 때를 고 QoS 정책을 사용 하는 이유.

이 항목에서 두 시나리오는 다음과 같습니다.

1. 온라인 비즈니스 응용 프로그램에 대 한 네트워크 교통 우선 순위를 지정합니다
2. HTTP 서버 응용 프로그램에 대 한 네트워크 교통 우선 순위를 지정합니다

>[!NOTE]
>이 항목의 몇 가지 섹션에 설명된 작업을 수행할 수 있는 일반적인 단계 포함 됩니다. 자세한 내용은 QoS 정책을 관리에 표시 [QoS 정책 관리](qos-policy-manage.md)합니다.

## <a name="scenario-1-prioritize-network-traffic-for-a-line-of-business-application"></a>시나리오 1: 온라인 비즈니스 응용 프로그램에 대 한 네트워크 교통 우선 순위를 지정합니다

이 시나리오 IT 부서 QoS 정책을 사용 하 여 수행할 수 있는 몇 가지 목표는 다음과 같습니다.

- 중요 한 mission\ 응용 프로그램에 대 한 네트워크 성능을 제공 합니다.
- 특정 응용 프로그램 사용 하면서 사용자의 키 집합에 대 한 네트워크 성능을 제공 합니다.
- Company\ 수준의 데이터를 백업 응용 프로그램이 너무 많이 대역폭을 한 번에 사용 하 여 네트워크 성능이 저하 될 하지 있는지 확인 합니다.

IT 부서 특정 응용 프로그램에 대해 높은 우선 순위 교통 우선 순위를 제공 하기 위해 해당 라우터 구성 하 고 네트워크 교통량을을 분류 하 구분 서비스 코드 지점 \(DSCP\) 값을 사용 하 여 우선순위를 지정 하도록 QoS 정책을 구성 하기로 결정 합니다. 

>[!NOTE]
>대 한 자세한 내용은 DSCP, 섹션을 참조 **정의 QoS 우선 순위 통해 DSCP(Differentiated Services Code Point)** 항목에서 [(QoS) 서비스 품질 정책](qos-policy-top.md)합니다.

뿐만 아니라 DSCP 값 QoS 정책을 조절 속도 지정할 수 있습니다. 일치 하는 특정 QoS 정책 전송 속도 모든 아웃 바운드 교통 제한 영향을 주지 조절 합니다.

### <a name="qos-policy-configuration"></a>정책 QoS 구성

수행 세 개의 별도 목표도 IT 관리자 세 가지 다른 QoS 정책을 결정 합니다.

#### <a name="qos-policy-for-lob-app-servers"></a>LOB 앱 서버에 대 한 QoS 정책

IT 부서 있는 QoS 정책을 만듭니다 첫 번째 mission\ 중요 응용 프로그램 \(ERP\) 응용 프로그램 계획 company\ 전체 Enterprise 리소스입니다. 모든 Windows Server 2016을 실행 하는 몇 가지 컴퓨터에서 호스트 ERP 응용 프로그램입니다. 이 컴퓨터 Active Directory Domain Services 소속 그룹의 회원 들 비즈니스 선 \(LOB\) 응용 프로그램 서버의 만든 \(OU\) 합니다. Client\ 측 구성 ERP 응용 프로그램에 대 한 Windows 10 및 Windows 8.1 실행 하는 컴퓨터에 설치 됩니다.

그룹 정책 IT 관리자는 그룹 정책 개체 \(GPO\) QoS 정책이 적용 되는 선택 합니다. IT 관리자 만들고 이라는 QoS 정책을 QoS 정책 마법사를 사용 하 여 "서버 LOB 정책" high\ 우선 순위 DSCP 값이 44 모든 응용 프로그램, IP 주소, TCP UDP 및 포트 번호를 지정 하는 합니다.

QoS 정책이 GPO만 이러한 서버, 그룹 정책 관리 콘솔 \(GPMC\) 도구를 통해 포함 된를 연결 하 여 LOB 서버에만 적용 됩니다. 이 초기 서버 LOB 정책 컴퓨터가 네트워크 교통 전송 될 때마다 high\ 우선 순위 DSCP 값을 적용 됩니다. 나중에이 QoS 정책 편집할 수 \ (그룹 정책 개체 편집기 tool\)에서 지정된 포트 번호를 사용한 경우에 적용 정책을 제한 ERP 응용 프로그램의 포트 번호를 포함 합니다.

#### <a name="qos-policy-for-the-finance-group"></a>금융 그룹에 대 한 QoS 정책

회사에서 많은 그룹 ERP 응용 프로그램을 액세스 하는 동안 고객의 경우 다룰 때 금융 그룹이 응용이 프로그램에 따라 다르며 그룹 앱에서 일관 되 게 고성능 필요 합니다.

금융 그룹 고객에 게을 지원할 수 있도록 QoS 정책 높은 우선 순위 부여도 이러한 사용자의이 교통을 분류 해야 합니다. 그러나 금융 그룹의 회원 ERP 응용 프로그램이 아닌 응용 프로그램을 사용할 때 정책이 적용 되지 해야 합니다. 

이 때문 IT 부서 정의 이라는 두 번째 QoS 정책을 "클라이언트 LOB 정책" DSCP 값 60 금융 사용자 그룹 ERP 응용 프로그램을 실행 하는 경우 해당 그룹 정책 개체 편집기 도구에 있습니다.

#### <a name="qos-policy-for-a-backup-app"></a>백업 앱에 대 한 정책을 QoS

일부 컴퓨터에서는 별도 백업 응용 프로그램을 제거할 수 없습니다. 백업 응용 프로그램 교통 모든 사용 가능한 네트워크 리소스를 사용 하지 않는 되도록 IT 부서 백업 데이터 정책을 만듭니다. 이 백업 정책은 지정 DSCP 값은 백업 앱에 대 한 실행 파일 이름에 따라 1 **backup.exe**합니다. 

제 GPO 만들고 도메인에 있는 모든 클라이언트 컴퓨터에 대 한 배포 됩니다. 백업 응용 프로그램은 데이터를 전송 될 때마다 금융 부서에서 컴퓨터에서 발생 한 경우에 낮은 우선 순위 DSCP 값 적용 됩니다.
  
>[!NOTE]
>네트워크 교통 QoS 정책을 없이 0 DSCP 값으로 보냅니다.

### <a name="scenario-policies"></a>시나리오 정책

다음 표에서 이러한 시나리오 QoS 정책을 요약 되어 있습니다.
  
|정책 이름|DSCP 값|속도 제한|조직 장치에 적용|설명|  
|-----------------|----------------|-------------------|-----------------------------------|-----------------|
|[정책이]|0|없음|[없음 배포]|분류 교통에 대 한 최상의 (기본) 노력 처리 합니다.|  
|백업 데이터|1|없음|모든 클라이언트|대량이 데이터에 대 한 낮은 우선 순위 DSCP 값을 적용 됩니다.|  
|서버 LOB|44|없음|컴퓨터 OU ERP 서버에 대 한|우선 순위가 높은 DSCP ERP 서버 교통에 적용 됩니다.|  
|클라이언트 LOB|60|없음|금융 사용자 그룹|우선 순위가 높은 DSCP ERP 클라이언트 교통에 적용 됩니다.|  

>[!NOTE]
>형태로 DSCP 값 표시 됩니다.

정의 하 고 그룹 정책을 사용 하 여 적용 QoS 정책을 사용 하 여 네트워크 교통 아웃 바운드 정책 지정 DSCP 값을 받습니다. 라우터 차등 처리 큐 사용 하 여 이러한 DSCP 값에 따라 제공 합니다. 라우터 네 큐도 구성 된이 IT 부서에 대 한: 우선 순위가 높은, 중간 우선 순위가, 최상의 결과 및 저 우선 순위 부여 합니다.

교통 DSCP 값을 사용 하 여 라우터에 도착 하는 경우 "서버 LOB 정책" 및 "클라이언트 LOB 정책에" 데이터 우선 순위가 높은 큐에 배치 됩니다. 0 DSCP 값와 함께 교통 체증 최대한 수준의 서비스를 받습니다. (출처: 백업 응용 프로그램) 1 DSCP 값 패킷을 저 우선 순위 부여 하 게 처리를 받습니다.  
  
### <a name="prerequisites-for-prioritizing-a-line-of-business-application"></a>온라인 비즈니스 응용 프로그램 우선순위 사항

이 작업을 완료 하려면 다음과 같은 요구 사항을 충족 하는지 확인 합니다.

- 포함 된 컴퓨터 QoS\-호환 되는 운영 체제를 실행 합니다.

- 포함 된 컴퓨터 된 Active Directory Domain Services의 회원은 \ (AD DS \) 도메인을 그룹 정책을 사용 하 여 구성할 수 있습니다.

- TCP/IP 네트워크 라우터에 DSCP \(RFC 2474\)에 대해 구성으로 설정 되어 있습니다. 자세한 내용은 참조 [RFC 2474](http://www.ietf.org/rfc/rfc2474.txt)합니다.

- 관리자 자격 증명 요구 사항은 충족 됩니다.

#### <a name="administrative-credentials"></a>관리자 자격 증명

이 작업을 완료 하려면을 만들어 그룹 정책 개체 배포할 수 있어야 합니다.
  
#### <a name="setting-up-the-test-environment-for-prioritizing-a-line-of-business-application"></a>테스트 환경을 우선순위 온라인 비즈니스 응용 프로그램에 대 한 설정

테스트 환경으로 설정 하려면 다음 작업을 수행 합니다.

- 조직 장치도 그룹화 하는 사용자가 하는 클라이언트와 AD DS 도메인을 만듭니다. AD DS 배포 지침은 참조는 [Core 네트워크 가이드](https://docs.microsoft.com/windows-server/networking/core-network-guide/core-network-guide)합니다.

- 라우터 DSCP 값에 따라 큐 differentially를 구성 합니다. 예를 들어, DSCP 값 44 입력 "백 금" 큐 되며 다른 모든 사용자가 중 박람회 대기 수 있습니다.

>[!NOTE]
> 네트워크 캡처 도구와 같은 네트워크 모니터와 함께 사용 하 여 DSCP 값을 볼 수 있습니다. 네트워크 캡처를 수행한 후 캡처한 데이터의 TOS 필드를 확인할 수 있습니다.

#### <a name="steps-for-prioritizing-a-line-of-business-application"></a>우선 순위 지정 온라인 비즈니스 응용 프로그램에 대 한 단계

우선 순위를 정하는 온라인 비즈니스 응용 프로그램을 다음 작업을 수행 합니다.

1. 만들고 그룹 정책 개체 \(GPO\) QoS 정책 사용 하 여 연결 합니다.

2. 라우터는의 업무 differentially 처리 하도록 구성 DSCP 하면 선택한 값에 따라 응용 프로그램 (사용 하 여 큐). 이 작업의 절차 라우터의 있는 종류에 따라 달라 집니다.

## <a name="scenario-2-prioritize-network-traffic-for-an-http-server-application"></a>시나리오 2: HTTP 서버 응용 프로그램에 대 한 네트워크 교통 우선 순위를 지정합니다

Windows Server 2016 QoS 정책에 따라 정책 URL 기반 기능을 포함합니다. URL 정책을 사용 HTTP 서버에 대 한 대역폭 관리할 수 있습니다.

많은 Enterprise 응용 프로그램 용으로 개발 된 되며 인터넷 정보 서비스 \(IIS\) 웹 서버에 호스트 및 웹 앱은 클라이언트 컴퓨터에는 브라우저에서 액세스할 수 있습니다.

이 경우에는 관리 IIS 서버 해당 호스트 교육 동영상 조직의 모든 직원 가정 합니다. 이러한 비디오 서버에서 교통량 마비 네트워크에 없습니다 및 비디오 교통 네트워크에서 음성 및 데이터 교통에서 구별는 되도록 목표가입니다. 

작업은 시나리오 1에서 작업 하는 것과 비슷합니다. 가 디자인 하 고 교통 관리 설정을 DSCP 값 비디오 교통 체증 등 구성 하 고 온라인 비즈니스 응용 프로그램에 대 한 것 처럼 같은 속도 제한 합니다. 하지만 HTTP 서버 응용 프로그램이 응답 합니다 URL을 입력 응용 프로그램 이름을 제공 하는 대신 교통 지정 하는 경우: 예를 들어, https://hrweb/training합니다.
  
> [!NOTE]
>Windows 7 및 Windows Server 2008 R2 전에 발표 된 Windows 운영 체제를 실행 하는 컴퓨터에 대 한 네트워크 교통 우선 순위를 정하는 QoS URL 기반 정책을 사용할 수 없습니다.

### <a name="precedence-rules-for-url-based-policies"></a>우선 순위 규칙 URL 기반 정책에 대 한

다음 Url 유효 하며 될 수 있는 모든 QoS 정책에 지정 된 및 사용자 또는 컴퓨터 동시에 적용 합니다.

- http://video

- https://training.hr.mycompany.com

- http://10.1.10.249:8080/tech  

- https://*/ebooks

하지만 어떤 우선 순위를 받게 됩니다 무엇 인가요? 규칙은 간단 합니다. URL 기반 정책의 왼쪽에서 오른쪽 읽는 순서에서 우선 순위가 합니다. 따라서에서 가장 우선 순위를 높은 우선 순위 URL 필드는 다음과 같습니다.
  
[1. URL 구조](#bkmk_QoS_UrlScheme)

[2. URL 호스트](#bkmk_QoS_UrlHost)

[3. URL 포트](#bkmk_QoS_UrlPort)

[4. URL 경로](#bkmk_QoS_UrlPath)

세부 정보는 다음과 같습니다.

####  <a name="bkmk_QoS_UrlScheme"></a>1. URL 구조

 `https://` 보다 우선 `http://`합니다.

####  <a name="bkmk_QoS_UrlHost"></a>2. URL 호스트

 최저에 높은 우선 순위를은 다음과 같습니다.

1. 호스트

2. IPv6 주소

3. IPv4 주소

4. 와일드 카드

호스트의 경우 더 점으로 요소 (더 깊이)와 호스트 호스트 적은 점으로 요소가와 보다 높은 우선 순위를에 있습니다. 예를 들어 다음 호스트 중:

- video.internal.training.hr.mycompany.com (깊이 6 =)
  
- selfguide.training.mycompany.com (깊이 = 4)
  
- 교육 (깊이 1 대당)
  
- 라이브러리 (깊이 1 대당)
  
 **video.internal.training.hr.mycompany.com** 의 우선 순위가 높은 및 **selfguide.training.mycompany.com** 의 우선 순위가 높은 다음 합니다. **교육** 및 **라이브러리** 같은 최저 우선 순위를 공유 합니다.  
  
####  <a name="bkmk_QoS_UrlPort"></a>3. URL 포트

특정 또는 암묵적인 포트 번호 와일드 카드 포트 보다 높은 우선 순위를에 있습니다.

####  <a name="bkmk_QoS_UrlPath"></a>4. URL 경로

호스트와 같은 다중 요소 URL 경로 구성 됩니다. 더 많은 요소 있는 항상 우선을 순위가 높은 보다 적은 합니다. 예를 들어, 우선 순위 부여 하 여 다음 경로 나열 됩니다.  

1.  /ebooks/tech/windows/networking/qos

2.  / ebooks/기술/windows /

3.  /ebooks

4.  /

사용자를 모두 닫은 다음 URL 경로 따라 파일을 포함 하기로 URL이 경로 했을 때는 원하는 수행 하지 않은 경우 보다 낮은 우선을 수 있습니다.

사용자는 URL 기반 정책에 대상 IP 주소를 지정 하도록 선택할 수도 있습니다. 대상 IP 주소가 앞에서 설명한 네 URL 필드 보다 낮은 우선을 있습니다.
  
### <a name="quintuple-policy"></a>다섯 배 정책

다섯 배 정책 프로토콜 ID, 소스 IP 주소, 소스 포트, 대상 IP 주소, 및 포트 대상으로 지정 됩니다. 항상 다섯 배 정책 URL 기반 정책 보다 높은 우선 순위를에 있습니다. 

이미 사용자에 대해 다섯 배 정책이 적용 되어, 경우 새 URL 기반 정책 발생 하지 않습니다 충돌 클라이언트 해당 사용자의 컴퓨터.

이 가이드에 다음 항목에 대 한 참고 [QoS 정책 관리](qos-policy-manage.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요. [(QoS) 서비스 품질 정책](qos-policy-top.md)합니다.
