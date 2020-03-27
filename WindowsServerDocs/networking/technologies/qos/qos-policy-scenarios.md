---
title: QoS 정책 시나리오
description: 이 항목에서는 그룹 정책를 사용 하 여 Windows Server 2016의 특정 응용 프로그램 및 서비스에 대 한 네트워크 트래픽 우선 순위를 지정 하는 방법을 설명 하는 QoS (서비스 품질) 정책 시나리오를 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c4306f06-a117-4f65-b78b-9fd0d1133f95
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 927232a3b191be86ae91b1dd0d6af767d4f024ae
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315424"
---
# <a name="qos-policy-scenarios"></a>QoS 정책 시나리오

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 QoS 정책을 사용 하는 방법, 시기 및 이유를 보여 주는 가상 시나리오를 검토할 수 있습니다.

이 항목의 두 가지 시나리오는 다음과 같습니다.

1. Lob (기간 업무) 응용 프로그램에 대 한 네트워크 트래픽 우선 순위 지정
2. HTTP 서버 응용 프로그램에 대 한 네트워크 트래픽 우선 순위 지정

>[!NOTE]
>이 항목의 일부 섹션에는 설명 된 작업을 수행 하기 위해 수행할 수 있는 일반적인 단계가 포함 되어 있습니다. QoS 정책을 관리 하는 방법에 대 한 자세한 지침은 [Qos 정책 관리](qos-policy-manage.md)를 참조 하세요.

## <a name="scenario-1-prioritize-network-traffic-for-a-line-of-business-application"></a>시나리오 1: lob (기간 업무) 응용 프로그램에 대 한 네트워크 트래픽 우선 순위 지정

이 시나리오에서 IT 부서에는 QoS 정책을 사용 하 여 수행할 수 있는 여러 목표가 있습니다.

- 중요 업무용 응용 프로그램에 더 나은 네트워크 성능을 제공\-합니다.
- 특정 응용 프로그램을 사용 하는 동안 사용자의 키 집합에 대해 더 나은 네트워크 성능을 제공 합니다.
- 회사\-wide data 백업 응용 프로그램에서 한 번에 너무 많은 대역폭을 사용 하 여 네트워크 성능을 방해 하지 않는지 확인 합니다.

IT 부서에서는 DSCP\) 값 \(차별화 서비스 코드 포인트를 사용 하 여 특정 응용 프로그램의 우선 순위를 지정 하는 QoS 정책을 구성 하 여 네트워크 트래픽을 분류 하 고 우선 순위가 높은 트래픽에 대해 기본적으로 적용 되는 라우터를 구성 합니다. 

>[!NOTE]
>DSCP에 대 한 자세한 내용은 [qos (서비스 품질) 정책](qos-policy-top.md)항목의 **차등화 서비스 코드 포인트를 통해 Qos 우선 순위 정의** 섹션을 참조 하세요.

QoS 정책은 DSCP 값 외에 스로틀 률을 지정할 수 있습니다. 제한은 QoS 정책과 일치 하는 모든 아웃 바운드 트래픽을 특정 전송 속도로 제한 하는 효과를 가집니다.

### <a name="qos-policy-configuration"></a>QoS 정책 구성

IT 관리자는 세 가지 별도 목표를 달성 하 여 세 가지 QoS 정책을 만들도록 결정 합니다.

#### <a name="qos-policy-for-lob-app-servers"></a>LOB 앱 서버에 대 한 QoS 정책

IT 부서가 QoS 정책을 만드는 첫 번째 업무\-중요 응용 프로그램은 회사\-wide Enterprise 리소스 계획 \(ERP\) 응용 프로그램입니다. ERP 응용 프로그램은 Windows Server 2016를 실행 하는 여러 컴퓨터에서 호스팅됩니다. Active Directory Domain Services에서 이러한 컴퓨터는 LOB (기간 업무) \(LOB\) 응용 프로그램 서버에 대해 만들어진 조직 구성 단위 \(OU\)의 멤버입니다. ERP 응용 프로그램의 클라이언트\-쪽 구성 요소는 Windows 10 및 Windows 8.1를 실행 하는 컴퓨터에 설치 됩니다.

그룹 정책 IT 관리자는 QoS 정책이 적용 될 GPO\) \(그룹 정책 개체를 선택 합니다. IT 관리자는 QoS 정책 마법사를 사용 하 여 모든 응용 프로그램, 모든 IP 주소, TCP 및 UDP 및 포트 번호에 대해 높은\-우선 순위 DSCP 값 44을 지정 하는 "서버 LOB 정책" 이라는 QoS 정책을 만듭니다.

QoS 정책은 그룹 정책 관리 콘솔 \(GPMC\) 도구를 통해 GPO를 이러한 서버만 포함 하는 OU에 연결 하 여 LOB 서버에만 적용 됩니다. 이 초기 서버 LOB 정책은 컴퓨터에서 네트워크 트래픽을 보낼 때마다 높은\-우선 순위 DSCP 값을 적용 합니다. 나중에이 QoS 정책을\) 그룹 정책 개체 편집기 \(편집 하 여 ERP 응용 프로그램의 포트 번호를 포함할 수 있습니다. 이렇게 하면 지정 된 포트 번호를 사용 하는 경우에만 정책이 적용 되도록 제한할 수 있습니다.

#### <a name="qos-policy-for-the-finance-group"></a>재무 그룹에 대 한 QoS 정책

회사 내의 많은 그룹이 ERP 응용 프로그램에 액세스 하지만 재무 그룹은 고객을 처리할 때이 응용 프로그램에 따라 달라 지 며, 그룹은 앱에서 지속적으로 높은 성능을 필요로 합니다.

재무 그룹이 고객을 지원할 수 있도록 하기 위해 QoS 정책은 이러한 사용자의 트래픽을 높은 우선 순위로 분류 해야 합니다. 그러나 재무 그룹의 구성원이 ERP 응용 프로그램이 아닌 다른 응용 프로그램을 사용 하는 경우에는 정책을 적용 하면 안 됩니다. 

이로 인해 IT 부서는 재무 사용자 그룹이 ERP 응용 프로그램을 실행할 때 DSCP 값 60를 적용 하는 그룹 정책 개체 편집기 도구에서 "클라이언트 LOB 정책" 이라는 두 번째 QoS 정책을 정의 합니다.

#### <a name="qos-policy-for-a-backup-app"></a>백업 앱에 대 한 QoS 정책

모든 컴퓨터에서 별도의 백업 응용 프로그램이 실행 되 고 있습니다. 백업 응용 프로그램의 트래픽이 사용 가능한 모든 네트워크 리소스를 사용 하지 않도록 하기 위해 IT 부서는 백업 데이터 정책을 만듭니다. 이 백업 정책은 백업 앱에 대 한 실행 파일 이름 ( **update.exe**)을 기반으로 하는 DSCP 값을 1로 지정 합니다. 

세 번째 GPO가 만들어지고 도메인의 모든 클라이언트 컴퓨터에 배포 됩니다. 백업 응용 프로그램이 데이터를 보낼 때마다 재무 부서의 컴퓨터에서 발생 한 경우에도 우선 순위가 낮은 DSCP 값이 적용 됩니다.
  
>[!NOTE]
>QoS 정책이 없는 네트워크 트래픽은 DSCP 값을 0으로 보냅니다.

### <a name="scenario-policies"></a>시나리오 정책

다음 표에서는이 시나리오에 대 한 QoS 정책을 요약 합니다.
  
|정책 이름|DSCP 값|스로틀 률|조직 구성 단위에 적용 됨|설명|  
|-----------------|----------------|-------------------|-----------------------------------|-----------------|
|[정책 없음]|0|없음|[배포 없음]|미분류 트래픽에 대 한 최상의 (기본) 처리입니다.|  
|백업 데이터|1|없음|모든 클라이언트|이 대량 데이터에 우선 순위가 낮은 DSCP 값을 적용 합니다.|  
|서버 LOB|44|없음|ERP 서버용 컴퓨터 OU|ERP 서버 트래픽에 대해 우선 순위가 높은 DSCP 적용|  
|클라이언트 LOB|60|없음|재무 사용자 그룹|ERP 클라이언트 트래픽에 우선 순위가 높은 DSCP를 적용 합니다.|  

>[!NOTE]
>DSCP 값은 10 진수 형식으로 표시 됩니다.

QoS 정책을 정의 하 고 그룹 정책를 사용 하 여 적용 하는 경우 아웃 바운드 네트워크 트래픽은 정책 지정 된 DSCP 값을 받습니다. 그러면 라우터는 큐를 사용 하 여 이러한 DSCP 값을 기준으로 차등 처리를 제공 합니다. 이 IT 부서에서 라우터는 우선 순위가 높은, 중간 우선 순위, 최상의 작업 및 낮은 우선 순위의 4 개 큐로 구성 됩니다.

트래픽이 "서버 LOB policy" 및 "클라이언트 LOB 정책"의 DSCP 값을 사용 하 여 라우터에 도착 하면 데이터는 우선 순위가 높은 큐에 배치 됩니다. DSCP 값이 0 인 트래픽은 최상의 서비스 수준을 받습니다. DSCP 값이 1 (백업 응용 프로그램에서) 인 패킷은 낮은 우선 순위의 처리를 수신 합니다.  
  
### <a name="prerequisites-for-prioritizing-a-line-of-business-application"></a>Lob (기간 업무) 응용 프로그램의 우선 순위를 정하는 필수 조건

이 작업을 완료 하려면 다음 요구 사항을 충족 하는지 확인 합니다.

- 관련 된 컴퓨터가 QoS\-호환 되는 운영 체제를 실행 하 고 있습니다.

- 관련 된 컴퓨터는 그룹 정책를 사용 하 여 구성할 수 있도록\) 도메인 AD DS Active Directory Domain Services \(멤버입니다.

- TCP/IP 네트워크는 \(RFC 2474\)에서 DSCP에 대해 구성 된 라우터를 사용 하 여 설정 됩니다. 자세한 내용은 [RFC 2474](https://www.ietf.org/rfc/rfc2474.txt)을 참조 하세요.

- 관리자 자격 증명 요구 사항이 충족 됩니다.

#### <a name="administrative-credentials"></a>관리 자격 증명

이 작업을 완료 하려면 그룹 정책 개체를 만들고 배포할 수 있어야 합니다.
  
#### <a name="setting-up-the-test-environment-for-prioritizing-a-line-of-business-application"></a>Lob (기간 업무) 응용 프로그램의 우선 순위를 정하는 테스트 환경 설정

테스트 환경을 설정 하려면 다음 작업을 완료 합니다.

- 조직 구성 단위에 그룹화 된 클라이언트 및 사용자가 있는 AD DS 도메인을 만듭니다. AD DS 배포에 대 한 지침은 [핵심 네트워크 가이드](https://docs.microsoft.com/windows-server/networking/core-network-guide/core-network-guide)를 참조 하세요.

- DSCP 값을 기준으로 큐를 differentially 하도록 라우터를 구성 합니다. 예를 들어 DSCP 값 44은 "Platinum" 큐에, 다른 모든 큐는가 중-공평 하 게 큐에 들어갑니다.

>[!NOTE]
> 네트워크 모니터와 같은 도구를 사용 하 여 네트워크 캡처를 사용 하 여 DSCP 값을 볼 수 있습니다. 네트워크 캡처를 수행한 후 캡처한 데이터의 TOS 필드를 관찰할 수 있습니다.

#### <a name="steps-for-prioritizing-a-line-of-business-application"></a>Lob (기간 업무) 응용 프로그램의 우선 순위를 정하는 단계

Lob (기간 업무) 응용 프로그램의 우선 순위를 지정 하려면 다음 작업을 완료 합니다.

1. QoS 정책을 사용 하 여 GPO\) \(그룹 정책 개체를 만들고 연결 합니다.

2. 선택한 DSCP 값을 기준으로 기간 업무 응용 프로그램 (큐를 사용 하 여)을 differentially 처리 하도록 라우터를 구성 합니다. 이 작업의 절차는 보유 하 고 있는 라우터 유형에 따라 달라 집니다.

## <a name="scenario-2-prioritize-network-traffic-for-an-http-server-application"></a>시나리오 2: HTTP 서버 응용 프로그램에 대 한 네트워크 트래픽 우선 순위 지정

Windows Server 2016에서 정책 기반 QoS는 기능 URL 기반 정책을 포함 합니다. URL 정책을 사용 하면 HTTP 서버에 대 한 대역폭을 관리할 수 있습니다.

많은 엔터프라이즈 응용 프로그램은 인터넷 정보 서비스 \(IIS\) 웹 서버에 대해 개발 되 고 호스트 되며 웹 앱은 클라이언트 컴퓨터의 브라우저에서 액세스할 수 있습니다.

이 시나리오에서는 모든 조직의 직원에 대해 학습 비디오를 호스트 하는 IIS 서버 집합을 관리 한다고 가정 합니다. 목표는 이러한 비디오 서버의 트래픽이 네트워크에 과부하가 걸리지 않도록 하 고, 비디오 트래픽이 네트워크의 음성 및 데이터 트래픽과 차별화 되는지 확인 하는 것입니다. 

작업은 시나리오 1의 작업과 유사 합니다. 비디오 트래픽의 DSCP 값과 같은 트래픽 관리 설정을 디자인 하 고 구성 하 고, 기간 업무 (lob) 응용 프로그램의 경우와 동일 하 게 조정 요금을 구성 합니다. 그러나 트래픽을 지정할 때는 응용 프로그램 이름을 제공 하는 대신 HTTP 서버 응용 프로그램이 응답할 URL (예: https://hrweb/training)만 입력 하면 됩니다.
  
> [!NOTE]
>URL 기반 QoS 정책을 사용 하 여 Windows 7 및 Windows Server 2008 R2 이전에 릴리스된 Windows 운영 체제를 실행 하는 컴퓨터에 대 한 네트워크 트래픽의 우선 순위를 지정할 수 없습니다.

### <a name="precedence-rules-for-url-based-policies"></a>URL 기반 정책에 대 한 선행 규칙

다음 Url은 모두 유효 하며 QoS 정책에서 지정 하 고 컴퓨터 또는 사용자에 게 동시에 적용할 수 있습니다.

- https://video

- https://training.hr.mycompany.com

- https://10.1.10.249:8080/tech  

- https://*/ebooks

하지만 어떤 것이 우선 순위를 부여 하나요? 규칙은 간단 합니다. URL 기반 정책은 왼쪽에서 오른쪽으로 읽는 순서로 우선 순위가 지정 됩니다. 따라서 가장 높은 우선 순위부터 가장 낮은 우선 순위로 URL 필드는 다음과 같습니다.
  
[1. URL 체계](#bkmk_QoS_UrlScheme)

[2. URL 호스트](#bkmk_QoS_UrlHost)

[3. URL 포트](#bkmk_QoS_UrlPort)

[4. URL 경로](#bkmk_QoS_UrlPath)

세부 정보는 다음과 같습니다.

####  <a name="1-url-scheme"></a><a name="bkmk_QoS_UrlScheme"></a>1. URL 체계

 `https://` `https://`보다 우선 순위가 높습니다.

####  <a name="2-url-host"></a><a name="bkmk_QoS_UrlHost"></a>2. URL 호스트

 가장 높은 우선 순위의 우선 순위는 다음과 같습니다.

1. Hostname

2. IPv6 주소

3. IPv4 주소

4. 와일드카드

호스트 이름의 경우 점으로 구분 된 요소가 더 많은 호스트 이름 (더 깊이)은 더 작은 요소를 포함 하는 호스트 이름 보다 우선 순위가 높습니다. 예를 들어 다음 호스트 이름 중 하나입니다.

- video.internal.training.hr.mycompany.com (깊이 = 6)
  
- selfguide.training.mycompany.com (깊이 = 4)
  
- 학습 (깊이 = 1)
  
- 라이브러리 (깊이 = 1)
  
  **video.internal.training.hr.mycompany.com** 의 우선 순위가 가장 높고 **selfguide.training.mycompany.com** 에는 다음으로 높은 우선 순위가 있습니다. **학습** 및 **라이브러리** 공유는 동일한 낮은 우선 순위를 갖습니다.  
  
####  <a name="3-url-port"></a><a name="bkmk_QoS_UrlPort"></a>3. URL 포트

특정 또는 암시적 포트 번호는 와일드 카드 포트 보다 우선 순위가 높습니다.

####  <a name="4-url-path"></a><a name="bkmk_QoS_UrlPath"></a>4. URL 경로

호스트 이름과 마찬가지로 URL 경로는 여러 요소로 구성 될 수 있습니다. 더 많은 요소를 포함 하는 하나는 항상 더 작은 우선 순위 보다 우선 순위가 높습니다. 예를 들어 다음 경로는 우선 순위별로 나열 됩니다.  

1.  /ebooks/tech/windows/networking/qos

2.  /ebooks/tech/windows/

3.  /ebooks

4.  /

사용자가 URL 경로 뒤에 있는 모든 하위 디렉터리 및 파일을 포함 하도록 선택한 경우이 URL 경로는 선택 하지 않은 경우에 비해 우선 순위가 낮습니다.

사용자가 URL 기반 정책에서 대상 IP 주소를 지정 하도록 선택할 수도 있습니다. 대상 IP 주소는 앞에서 설명한 4 개의 URL 필드 보다 우선 순위가 낮습니다.
  
### <a name="quintuple-policy"></a>5 중 정책

5 중 정책은 프로토콜 ID, 원본 IP 주소, 원본 포트, 대상 IP 주소 및 대상 포트에 의해 지정 됩니다. 5 중 정책은 항상 URL 기반 정책 보다 우선 순위가 높습니다. 

사용자에 대해 5 중 정책이 이미 적용 된 경우에는 새 URL 기반 정책으로 인해 해당 사용자의 클라이언트 컴퓨터에 대 한 충돌이 발생 하지 않습니다.

이 가이드의 다음 항목에 대해서는 [QoS 정책 관리](qos-policy-manage.md)를 참조 하세요.

이 가이드의 첫 번째 항목은 [QoS (서비스 품질) 정책](qos-policy-top.md)을 참조 하세요.
