---
title: QoS 정책 시나리오
description: 이 항목에서는 그룹 정책을 사용 하 여 특정 응용 프로그램 및 Windows Server 2016에서 서비스의 네트워크 트래픽 우선 순위를 지정 하는 방법을 설명 하는 서비스 품질 (QoS) 정책 시나리오를 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c4306f06-a117-4f65-b78b-9fd0d1133f95
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2617c897ed2ea173d29fc7c4a87e52557154d463
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446995"
---
# <a name="qos-policy-scenarios"></a>QoS 정책 시나리오

>적용 대상: Windows Server (반기 채널), Windows Server 2016

보여 주는 가상의 시나리오를 검토 하려면이 항목을 사용할 수 있습니다 하는 방법, 시기 및 QoS 정책을 사용 하는 이유입니다.

이 항목의 두 시나리오는 다음과 같습니다.

1. 기간 업무 응용 프로그램 네트워크 트래픽의 우선 순위
2. HTTP 서버 응용 프로그램에 대 한 네트워크 트래픽의 우선 순위

>[!NOTE]
>이 항목의 일부 섹션 일반 단계를 설명된 하는 작업을 수행 하기 위해 취할 수를 포함 합니다. 자세한 내용을 보려면 QoS 정책 관리에 대 한 지침을 참조 하세요 [QoS 정책 관리](qos-policy-manage.md)합니다.

## <a name="scenario-1-prioritize-network-traffic-for-a-line-of-business-application"></a>시나리오 1: 기간 업무 응용 프로그램 네트워크 트래픽의 우선 순위

이 시나리오에서는 IT 부서에 QoS 정책을 사용 하 여 작업을 수행할 수 있는 몇 가지 목표가 있습니다.

- 업무 수행에 대 한 더 나은 네트워크 성능을 제공할\-중요 한 응용 프로그램입니다.
- 특정 응용 프로그램을 사용 하는 동안 사용자의 키 집합에 대 한 더 나은 네트워크 성능을 제공 합니다.
- 회사 되도록\-전체 데이터 백업 응용 프로그램이 한 번에 너무 많은 대역폭을 사용 하 여 네트워크 성능을 방해 하지.

IT 부서에서 차별화 서비스 코드 포인트를 사용 하 여 특정 응용 프로그램 우선 순위를 지정 하는 QoS 정책을 구성 하기로 \(DSCP\) 값 네트워크 트래픽을 분류 하 고 구독을 제공 하는 라우터를 구성 하려면 더 높은 우선 순위 트래픽을 처리 합니다. 

>[!NOTE]
>DSCP에 대 한 자세한 내용은 섹션을 참조 하세요 **정의 QoS 우선 순위를 통해는 Differentiated Services Code Point** 항목에서 [의 QoS (서비스 품질) 정책을](qos-policy-top.md)합니다.

DSCP 값 이외에 QoS 정책을 스로틀 속도 지정할 수 있습니다. 제한 일치 QoS 정책을 특정 전송 속도 모든 아웃 바운드 트래픽을 제한 하는 효과가 있습니다.

### <a name="qos-policy-configuration"></a>QoS 정책 구성

위해 세 개의 별도 목표를 사용 하 여 IT 관리자는 세 가지 다른 QoS 정책을 만들려면 결정 합니다.

#### <a name="qos-policy-for-lob-app-servers"></a>LOB 앱 서버에 대 한 QoS 정책

첫 번째 업무\-IT 부서는 QoS 정책을 만들고 중요 한 응용 프로그램은 회사\-와이드 엔터프라이즈 리소스 계획 \(ERP\) 응용 프로그램입니다. ERP 응용 프로그램은 모든 Windows Server 2016 실행 되는 여러 컴퓨터에서 호스팅됩니다. Active Directory Domain Services에서 이러한 컴퓨터의 멤버인 조직 구성 단위 \(OU\) -업무에 대해 만들어진 \(LOB\) 응용 프로그램 서버. 클라이언트\-ERP 응용 프로그램에 대 한 쪽 구성 요소는 Windows 10 및 Windows 8.1 실행 중인 컴퓨터에 설치 됩니다.

그룹 정책에서 IT 관리자는 그룹 정책 개체 선택 \(GPO\) QoS 정책이 적용 될 때입니다. QoS 정책 마법사를 사용 하면 IT 관리자는 호출 QoS 정책을 만듭니다 "LOB 서버 정책"를 지정 하는 높은\-DSCP 값 44 모든 응용 프로그램, 모든 IP 주소, TCP 및 UDP 및 포트 번호에 대 한 우선 순위입니다.

QoS 정책 그룹 정책 관리 콘솔을 통해이 서버만 포함 된 OU에 GPO을 연결 하 여 LOB 서버에만 적용 됩니다 \(GPMC\) 도구입니다. 이 초기 서버 LOB 정책 적용 높은\-우선 순위 DSCP 값 때마다 컴퓨터에서 네트워크 트래픽을 전송 합니다. 이 QoS 정책이 나중에 편집할 수 있습니다 \(그룹 정책 개체 편집기 도구에서\) 제한 정책이 지정된 된 포트 번호를 사용한 경우에 적용 하는 ERP 응용 프로그램의 포트 번호를 포함 합니다.

#### <a name="qos-policy-for-the-finance-group"></a>재무 그룹에 대 한 QoS 정책

회사 내의 여러 그룹 ERP 응용 프로그램에 액세스 하는 동안 고객을 처리할 때이 응용 프로그램에 따라 달라 집니다 재무 그룹 및 그룹에는 앱에서 일관 되 게 높은 성능이 필요 합니다.

재무 그룹 고객을 지원할 수 있는지를 확인 하려면 QoS 정책을 높은 우선 순위로 이러한 사용자의이 트래픽을 분류 해야 합니다. 그러나 재무 그룹의 멤버는 ERP 응용 프로그램이 아닌 응용 프로그램을 사용 하는 경우에 정책을 적용 하지 않아야 합니다. 

이 때문에 IT 부서는 이라는 두 번째 QoS 정책을 정의 "LOB 클라이언트 정책" finance 사용자 그룹에 ERP 응용 프로그램을 실행 하는 경우 60 DSCP 값을 적용 하는 그룹 정책 개체 편집기 도구에서.

#### <a name="qos-policy-for-a-backup-app"></a>백업 응용 프로그램에 대 한 QoS 정책

별도 백업 응용 프로그램을 모든 컴퓨터에서 실행 됩니다. 백업 응용 프로그램의 트래픽이 모든 사용 가능한 네트워크 리소스를 사용 하지 않습니다을 보장 하려면 IT 부서에는 백업 데이터 정책을 만듭니다. 이 백업 정책을 지정 DSCP 값이 1 인 백업 응용 프로그램에 대 한 실행 파일 이름에 따라 **backup.exe**합니다. 

세 번째 GPO 만들어지고 도메인의 모든 클라이언트 컴퓨터에 배포 합니다. 데이터를 전송 하는 백업 응용 프로그램을 때마다 재무 부서에는 컴퓨터에서 발생 한 경우에 우선 순위가 낮은 DSCP 값 적용 됩니다.
  
>[!NOTE]
>QoS 정책 없이 네트워크 트래픽을 DSCP 값 0 사용 하 여 보냅니다.

### <a name="scenario-policies"></a>시나리오 정책

다음 표에서이 시나리오에 대 한 QoS 정책을 보여 줍니다.
  
|정책 이름|DSCP 값|스로틀 속도|조직 구성 단위에 적용|설명|  
|-----------------|----------------|-------------------|-----------------------------------|-----------------|
|[정책 없음]|0|없음|[배포 없음]|미분류 트래픽에 대 한 최상의 노력 (기본값) 처리 합니다.|  
|백업 데이터|1|없음|모든 클라이언트|이 대량 데이터에 대 한 우선 순위가 낮은 DSCP 값을 적용합니다.|  
|LOB 서버|44|없음|ERP 서버용 컴퓨터 OU|우선 순위가 높은 DSCP ERP server 트래픽에 적용 됩니다.|  
|LOB 클라이언트|60|없음|재무 사용자 그룹|우선 순위가 높은 DSCP ERP 클라이언트 트래픽에 대해 적용 됩니다.|  

>[!NOTE]
>DSCP 값은 10 진수 형식으로 표현 됩니다.

QoS 정책을 정의 하 고 그룹 정책을 사용 하 여 적용을 사용 하 여 아웃 바운드 네트워크 트래픽의 DSCP 정책이 지정 값을 받습니다. 라우터는 다음 큐를 사용 하 여 이러한 DSCP 값에 따라 차등 처리를 제공 합니다. 이 IT 부서에 라우터 4 큐를 사용 하 여 구성 됩니다: 우선 순위가 높은, 중간 우선 순위, 최상의 노력 및 낮은 우선 순위입니다.

트래픽이에서 DSCP 값을 사용 하 여 라우터에 도착 하는 경우 "LOB 서버 정책" 및 "LOB 클라이언트 정책을" 데이터는 우선 순위가 높은 큐에 배치 됩니다. DSCP 값 0 사용 하 여 트래픽 최상의 수준으로 서비스를 받습니다. DSCP 값 (백업 응용 프로그램)에서 1 사용 하 여 패킷 우선 순위가 낮은 처리를 수신 합니다.  
  
### <a name="prerequisites-for-prioritizing-a-line-of-business-application"></a>기간 업무 응용 프로그램을 우선 순위를 지정 하는 것에 대 한 필수 구성 요소

이 작업을 완료 하려면 다음 요구 사항을 맞는지 확인 합니다.

- QoS를 실행 하는 포함 된 컴퓨터는\-호환 되는 운영 체제입니다.

- 포함 된 컴퓨터는 Active Directory Domain Services의 멤버인 \(AD DS\) 도메인 그룹 정책을 사용 하 여 구성할 수 있도록 합니다.

- DSCP에 대해 구성 된 라우터를 사용 하 여 TCP/IP 네트워크 설정 \(RFC 2474\)합니다. 자세한 내용은 [RFC 2474](https://www.ietf.org/rfc/rfc2474.txt)합니다.

- 관리 자격 증명 요구 사항은 충족 됩니다.

#### <a name="administrative-credentials"></a>관리 자격 증명

이 작업을 완료 하려면 만들고 그룹 정책 개체를 배포 해야 합니다.
  
#### <a name="setting-up-the-test-environment-for-prioritizing-a-line-of-business-application"></a>기간 업무 응용 프로그램을 우선 순위를 지정 하는 것에 대 한 테스트 환경 설정

테스트 환경을 설정 하려면 다음 작업을 완료 합니다.

- 클라이언트 및 조직 구성 단위를 그룹화 하는 사용자를 사용 하 여 AD DS 도메인을 만듭니다. AD DS를 배포 하는 방법에 대 한 지침을 참조 하세요. 합니다 [핵심 네트워크 가이드](https://docs.microsoft.com/windows-server/networking/core-network-guide/core-network-guide)합니다.

- DSCP 값을 기반으로 하는 큐 미분 보정 하도록 라우터를 구성 합니다. 예를 들어, DSCP 값 44가 "platinum 인" 큐를 입력 하 고 나머지는 모두 가중치 fair 지연 합니다.

>[!NOTE]
> 네트워크 모니터와 같은 도구를 사용 하 여 네트워크 캡처를 사용 하 여 DSCP 값을 볼 수 있습니다. 네트워크 캡처를 수행한 후에 캡처된 데이터에서 TOS 필드를 확인할 수 있습니다.

#### <a name="steps-for-prioritizing-a-line-of-business-application"></a>기간 업무 응용 프로그램을 우선 순위를 지정 하는 단계

기간 업무 응용 프로그램을 우선 순위를 지정 하려면 다음 작업을 완료:

1. 만들고 그룹 정책 개체 연결 \(GPO\) QoS 정책을 사용 하 여 합니다.

2. 미분 보정 된 줄의 업무를 처리 하는 라우터 구성 (사용 하 여 큐) 응용 프로그램 선택한 DSCP 값을 기반으로 합니다. 이 작업의 절차는 라우터 있는 형식에 따라 달라 집니다.

## <a name="scenario-2-prioritize-network-traffic-for-an-http-server-application"></a>시나리오 2: HTTP 서버 응용 프로그램에 대 한 네트워크 트래픽의 우선 순위

Windows Server 2016에서 정책 기반 QoS에는 URL 기반 정책을 기능이 포함 됩니다. URL 정책을 통해 HTTP 서버에 대 한 대역폭을 관리할 수 있습니다.

대부분의 엔터프라이즈 응용 프로그램에 대 한 개발 및 인터넷 정보 서비스에서 호스팅된 \(IIS\) 웹 서버 및 웹 앱 클라이언트 컴퓨터에서 브라우저에서 액세스 됩니다.

이 시나리오에서 관리 하는 일련의 IIS 서버를 호스트 교육 비디오는 조직의 모든 직원을 가정 합니다. 목표는에서 이러한 비디오 서버 트래픽은 네트워크에 과부하가 없습니다 및 네트워크에서 음성 및 데이터 트래픽을에서 차별화 되는 비디오 트래픽 확인 되도록 합니다. 

작업은 시나리오 1에서 작업 하는 것과 비슷합니다. 디자인 및 트래픽 관리 설정이 비디오 트래픽에 대 한 DSCP 값과 같이 구성 됩니다 및 기간 업무 응용 프로그램에 대해서와 마찬가지로 동일한 속도 제한 합니다. 하지만 HTTP 서버 응용 프로그램은 응답 하는 URL만 입력 응용 프로그램 이름을 제공 하는 대신 트래픽을 지정 하는 경우: 예를 들어 https://hrweb/training합니다.
  
> [!NOTE]
>Windows 7 및 Windows Server 2008 R2 이전의 발표 된 Windows 운영 체제를 실행 하는 컴퓨터에 대 한 네트워크 트래픽의 우선 순위를 URL 기반 QoS 정책을 사용할 수 없습니다.

### <a name="precedence-rules-for-url-based-policies"></a>URL 기반 정책에 대 한 선행 규칙

다음 Url을 유효 하 고 수 모든 QoS 정책에 지정 하 고 사용자나 컴퓨터에 동시에 적용 합니다.

- https://video

- https://training.hr.mycompany.com

- https://10.1.10.249:8080/tech  

- https://*/ebooks

하지만 어느 우선 순위를 받을? 규칙은 간단 합니다. URL 기반 정책은 왼쪽에서 오른쪽 읽기 순서에 따라 우선 순위가 지정 됩니다. 따라서 가장 낮은 우선 순위를 높은 우선 순위에서 URL 필드를 다음과 같습니다.
  
[1. URL 구성표](#bkmk_QoS_UrlScheme)

[2. URL 호스트](#bkmk_QoS_UrlHost)

[3. URL 포트](#bkmk_QoS_UrlPort)

[4. URL 경로](#bkmk_QoS_UrlPath)

세부 정보는 다음과 같습니다.

####  <a name="bkmk_QoS_UrlScheme"></a> 1. URL 구성표

 `https://` 보다 높은 우선 순위가 `https://`합니다.

####  <a name="bkmk_QoS_UrlHost"></a> 2. URL 호스트

 가장 낮은 가장 높은 우선 순위는 다음과 같습니다.

1. Hostname

2. IPv6 주소

3. IPv4 주소

4. 와일드카드

호스트 이름, 경우 더 점선된 요소 (자세히)를 사용 하 여 호스트 이름을 더 적은 수의 점된 요소를 사용 하 여 호스트 이름 보다 높은 우선 순위를 있습니다. 예를 들어, 다음 호스트 이름 간에:

- video.internal.training.hr.mycompany.com (깊이 = 6)
  
- selfguide.training.mycompany.com (depth = 4)
  
- 학습 (깊이 = 1)
  
- 라이브러리 (깊이 = 1)
  
  **video.internal.training.hr.mycompany.com** 우선 순위가 가장 높은, 및 **selfguide.training.mycompany.com** 다음 가장 높은 우선 순위를 갖습니다. **교육** 하 고 **라이브러리** 같은 낮은 우선 순위를 공유 합니다.  
  
####  <a name="bkmk_QoS_UrlPort"></a> 3. URL 포트

특정 특성 또는 특정 암시적 포트 번호를 와일드 카드 포트 보다 높은 우선 순위를 있습니다.

####  <a name="bkmk_QoS_UrlPath"></a> 4. URL 경로

URL 경로 호스트 이름 처럼 여러 요소 구성 될 수 있습니다. 더 많은 요소가 있는 것 보다 더 적은 노력으로 더 높은 우선 순위를 항상에 있습니다. 예를 들어 다음 경로 우선 순위별로 나열 됩니다.  

1.  /ebooks/tech/windows/networking/qos

2.  /ebooks/tech/windows/

3.  /ebooks

4.  /

모든 하위 디렉터리 및 파일 URL 경로 포함 하도록 선택한 경우에이 URL 경로 선택 변경 되지 않은 했을 때 보다 낮은 우선 순위를 해야 합니다.

사용자는 URL 기반 정책에서 대상 IP 주소를 지정할 수도 있습니다. 대상 IP 주소는 앞에서 설명한 네 URL 필드 보다 낮은 우선 순위입니다.
  
### <a name="quintuple-policy"></a>Quintuple 정책

프로토콜 ID, 원본 ip, 원본 포트, 대상 IP 주소 및 대상 포트 Quintuple 정책을 지정 됩니다. Quintuple 정책을 항상 우선을 순위가 높은 모든 URL 기반 정책 보다 합니다. 

사용자에 대 한 Quintuple 정책이 이미 적용 되어 경우 새 URL 기반 정책을 발생 하지 않습니다 충돌 해당 사용자의 클라이언트에서 컴퓨터.

이 가이드의 다음 항목을 참조 하세요 [QoS 정책 관리](qos-policy-manage.md)합니다.

이 가이드의 첫 번째 항목을 참조 하세요 [의 QoS (서비스 품질) 정책을](qos-policy-top.md)합니다.
