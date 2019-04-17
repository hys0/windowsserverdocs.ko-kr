---
title: 소프트웨어 네트워킹 정의 된 인증서를 관리
description: 이 항목 소프트웨어 정의 네트워킹 (SDN) Windows Server 2016 데이터 센터에 배포 하는 경우 네트워크 컨트롤러 Northbound 및 Southbound 통신을 위해 인증서를 관리 하는 방법을 알아보려면 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3036de9161cabc2f3a85a1d3b2ce7739f0ff6bd3
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="manage-certificates-for-software-defined-networking"></a>소프트웨어 네트워킹 정의 된 인증서를 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 소프트웨어 네트워킹 정의 \(SDN\) Windows Server 2016 데이터 센터에 배포 System Center 가상 컴퓨터 Manager \(SCVMM\) SDN 관리 클라이언트를 사용 하는 경우 네트워크 컨트롤러 Northbound 및 Southbound 통신을 위해 인증서를 관리 하는 방법을 알아보려면 사용할 수 있습니다.

>[!NOTE]
>네트워크 컨트롤러에 대 한 개요 내용은 [네트워크 컨트롤러](../technologies/network-controller/Network-Controller.md)합니다.

네트워크 컨트롤러 커뮤니케이션 보호 하기 위한 Kerberos을 사용 하지 않는 경우 X.509 인증서 인증, 권한 및 암호화를 사용할 수 있습니다.

Windows Server 2016 데이터 센터에 SDN self\ 서명 둘 다 지원 및 인증 기관 \ (CA\)-X.509 인증서를 로그인 합니다. 이 항목 부하 분산 소프트웨어가 \(SLB\) 등 네트워크 장치를 관리 하는 클라이언트를 사용 하 여 네트워크 컨트롤러 Northbound 통신 채널 보호를 위해 이러한 인증서 만들고에 적용에 대 한 단계별 지침 및 Southbound 통신을 제공 합니다.
.
Certificate\ 기반 인증을 사용 하는 경우 다음과 같은 방법으로 사용 되는 하나의 인증서 네트워크 컨트롤러 노드에서 등록 해야 합니다.

1. 네트워크 컨트롤러 노드와 클라이언트 management System Center 가상 컴퓨터 Manager 같은 간의 \(SSL\) 주소와 Northbound 통신 암호화 됩니다.
2. 네트워크 컨트롤러 및 Southbound 장치 노드와 간의 서비스, Hyper-v 호스트 부하 분산 소프트웨어가 \(SLBs\) 등 인증 합니다.

## <a name="creating-and-enrolling-an-x509-certificate"></a>홈 그룹을 만들고 X.509 인증서를 등록

만들 수 있으며 self\ 서명 인증서를 나는 캘리포니아에서 발행 인증서를 등록할 수 있습니다.

>[!NOTE]
>SCVMM 배포 하는 네트워크 컨트롤러를 사용 하는 경우 X.509 인증서를 사용 하는 네트워크 컨트롤러 서비스 템플릿을 구성 하는 동안 Northbound 통신 암호화를 지정 해야 합니다.

인증서 구성 다음 값 포함 해야 합니다.

- 에 대 한 값은 **RestEndPoint** 텍스트 상자 네트워크 컨트롤러 정식 도메인 이름 \(FQDN\) 또는 IP 주소 여야 합니다. 
- **RestEndPoint** 값 주제 이름과 일치 해야 \ (일반 이름, CN\) X.509 인증서의 합니다.

### <a name="creating-a-self-signed-x509-certificate"></a>X.509 Self\ 서명 인증서를 만들기

자체 서명된 X.509 인증서를 만들 수 있으며 개인 키와 함께 내보낼 \ (에 password\로 보호) single\ 노드와 multiple\ 노드 배포 네트워크 컨트롤러의 다음이 단계에 따라 합니다.

Self\ 서명 인증서를 만들 때 다음 지침을 사용할 수 있습니다.

- 네트워크 컨트롤러 나머지 끝점의 IP 주소를 사용 하 여 DnsName 매개-에 대 한 있지만 단일 관리 서브넷 내에 있는 모든 네트워크 컨트롤러 노드 지 필요 하기 때문에 권장 하지 않습니다 \ (예:에 단일 rack\)
- 여러 노드 NC 배포 DNS 이름을 지정 하는 네트워크 컨트롤러 클러스터 FQDN가 \ (DNS 호스트 A 기록 자동으로 만들어집니다. \) 
- 단일 노드가 네트워크 컨트롤러 배포 DNS 이름을 네트워크 컨트롤러 호스트 이름 전체 도메인 이름 이어서 될 수 있습니다.

#### <a name="multiple-node"></a>여러 노드

사용할 수 있는 [새로 SelfSignedCertificate](https://technet.microsoft.com/en-us/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) self\ 서명 인증서를 만들기 위해 Windows PowerShell 명령을 합니다.

**구문**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCRESTName>")

**예 사용**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "MultiNodeNC" -DnsName @("NCCluster.Contoso.com")

#### <a name="single-node"></a>단일 노드

사용할 수 있는 [새로 SelfSignedCertificate](https://technet.microsoft.com/en-us/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) self\ 서명 인증서를 만들기 위해 Windows PowerShell 명령을 합니다.

**구문**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCFQDN>")

**예 사용**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "SingleNodeNC" -DnsName @("SingleNodeNC.Contoso.com")

### <a name="creating-a-ca-signed-x509-certificate"></a>X.509 CA\ 서명 인증서를 만들기

캘리포니아를 사용 하 여는 인증서를 만들려면 해야 이미 배포한 된 Active Directory 인증서 서비스 \(AD CS\) 공개 키 인프라 \(PKI\) 합니다. 

>[!NOTE]
>그러나이 항목의 지침 광고 CS 관련 된 인증서를 사용 하기 위해 네트워크 컨트롤러와 만들 수 제 외부 인증 기관 또는 openssl, 같은 도구를 사용할 수 있습니다. 제 3 자 캘리포니아 또는 도구를 사용 하는 방법을 알아보려면, 사용 중인 소프트웨어에 대 한 설명서를 참조 하세요.

한 캘리포니아 된 인증서를 만드는 경우 다음 단계에 있습니다.

1. 사용자 또는 조직의 도메인 또는 보안 관리자 구성 인증서 템플릿을
2. 사용자 또는 조직의 네트워크 컨트롤러 관리자 또는 SCVMM 관리자는 캐나다에서 새 인증서를 요청합니다.

#### <a name="certificate-configuration-requirements"></a>인증서 구성 요구 사항

인증서 템플릿을 다음 단계를 구성 하는 동안 구성한 서식 다음 필요한 요소에 포함 되어 있는지 확인 합니다.

1. 인증서 제목 Hyper-v 호스트 FQDN 여야 합니다.
2. 로컬 컴퓨터 개인 스토어에는 인증서를 배치 합니다 (내 – 인증서: \localmachine\my)
3. 인증서 두 서버 인증 있어야 합니다 (EKU: 1.3.6.1.5.5.7.3.1) 및 클라이언트 인증 (EKU: 1.3.6.1.5.5.7.3.2) 정책 응용 프로그램입니다.

>[!NOTE]
>하는 경우 개인 \ (내 – 인증서: \localmachine\my\) 인증서 Hyper\ V 호스트의 스토어에 둘 이상의 X.509 정식 도메인 이름 \(FQDN\) 호스트로 제목 (CN 이름) 인증서를 SDN에서 사용 되는 인증서 OID 1.3.6.1.4.1.311.95.1.1.1와 사용자 지정 추가 키 사용 향상 등록에 있는지 확인 합니다. 그렇지 않은 경우 네트워크 컨트롤러 및 호스트 간 통신 작동 하지 않을 수 있습니다.

#### <a name="to-configure-the-certificate-template"></a>인증서 템플릿을 구성 하려면
  
>[!NOTE]
>이 절차를 수행 하기 전에 인증서 요구 사항 및 인증서 템플릿 콘솔에서 사용할 수 있는 인증서 템플릿 검토 해야 합니다. 기존 템플릿 수정 하거나 기존 템플릿 복제 하 고 서식 파일의 복사본을 수정할 수 있습니다. 기존 템플릿의 복사본을 만드는 것이 좋습니다.

1. 광고 CS 설치 되어 있는, 서버 관리자 서버 **도구**을 차례로 클릭 하 고 **인증 기관**합니다. 인증 기관 Microsoft Management Console \(MMC\) 열립니다. 
2. 캘리포니아 이름을 두 번 클릭 MMC를 마우스 오른쪽 단추로 클릭 **인증서 템플릿**을 차례로 클릭 하 고 **관리**합니다.
3. 인증서 템플릿 console을 엽니다. 인증서 템플릿이 모든 세부 정보 창에 표시 됩니다.
4. 세부 정보 창에서 중복 템플릿의 클릭 합니다.
5.  클릭 하 고 **알림** 메뉴를 클릭 한 다음 **템플릿 복제**합니다. 서식 **속성** 대화 상자를 엽니다.
6.  서식에서 **속성** 대화 상자의 **주체 이름** 탭을 클릭 **요청에서 제공**합니다. \ (이 설정은 네트워크 컨트롤러 SSL 인증서에 대 한 필요 합니다. \)
7.  템플릿을에서 **속성** 대화 상자의 **요청을 처리** 탭에서 되도록 **허용 개인 키를 내보낼 수** 을 선택 합니다. 확인 하 고 **서명 및 암호화** 목적을 선택 합니다.
8.  서식 파일에 **속성** 대화 상자의 **확장** 탭을 선택 하 고 **키 사용**을 차례로 클릭 하 고 **편집**합니다.
9.  **서명**, 되도록 **디지털 서명** 을 선택 합니다.
10.  템플릿을에서 **속성** 대화 상자의 **확장** 탭을 선택 하 고 **정책**, 클릭 한 다음 **편집**합니다.
11.  **정책**, 되도록 **클라이언트 인증** 및 **서버 인증** 나열 됩니다.
12.  와 같은 인증서 서식 파일의 복사본 고유한 이름으로 저장 **네트워크 컨트롤러 템플릿**합니다.

#### <a name="to-request-a-certificate-from-the-ca"></a>캐나다의에서 인증서를 요청 하려면

인증서를 요청할 스냅인 사용할 수 있습니다. 어떤 종류의 인증서 요청을 처리 캐나다의 관리자가 사용할 수 있게 및이 미리 구성 된 인증서를 요청할 수 있습니다.

**사용자가** 로컬 또는 **관리자** 최소 그룹 구성원이 절차를 수행 하는 데 필요한 합니다.

1. 컴퓨터에 대 한 스냅인 엽니다.
2. 콘솔 트리에서 클릭 **인증서 \(Local Computer\)**합니다. 선택는 **개인** 인증서 저장소.
3. 에 **알림** 메뉴에서 * * 모든 작업 * 누른 다음 **새 인증서를 요청** 인증서 등록이 마법사를 시작 합니다. 클릭 **다음**합니다.
4. 선택는 **관리자가 구성** 인증서 등록이 정책 및 클릭 **다음**합니다.
5. 선택는 **Active Directory 등록 정책** \ (이전 section\로 구성 된 캘리포니아 템플릿을에 따름).
6. 확장은 **세부 정보** 섹션 / 다음 항목을 구성 합니다.
    1. 되도록 **키 사용** 둘 다에 포함 되어 * * 디지털 서명 * * 및 **키 암호화**합니다.
    2. 되도록 **정책** 모두 포함 **서버 인증** \(1.3.6.1.5.5.7.3.1\) 및 **클라이언트 인증** \(1.3.6.1.5.5.7.3.2\) 합니다.
7. 클릭 **속성**합니다.
8. 에 **주제** 탭에 **주체 이름**에서 **종류**선택 **일반 이름**합니다. 값에서 지정 **네트워크 컨트롤러 나머지 끝점**합니다.
9. 클릭 **적용**을 차례로 클릭 하 고 **확인**합니다.
10. 클릭 **등록**합니다.

인증서 MMC에서의 캐나다의 등록 되어 인증서를 보려면 개인 스토어를 클릭 합니다.

## <a name="exporting-and-copying-the-certificate-to-the-scvmm-library"></a>내보내고 인증서 SCVMM 라이브러리에 복사

Self\ 로그인 또는 CA\ 서명 인증서를 만든 후 내보내야 인증서 개인 키와 함께 \(in.pfx format\) 개인 키 없이 \ 기본 64.cer format\) (에서 인증서 스냅인에서 합니다. 

두 개의 내보낸된 파일을 복사 해야는 **ServerCertificate.cr** 및 **NCCertificate.cr** NC 서비스 템플릿의 가져올 때 시 지정 된 폴더 합니다.

1. 인증서 스냅인 (certlm.msc) 열고 로컬 컴퓨터에 대 한 개인 인증서 저장소 인증서를 찾습니다.
2. Right\ 클릭 인증서를 클릭 **모든 작업**을 차례로 클릭 하 고 **내보내려면**합니다. 인증서 내보낼 마법사가 열립니다. 클릭 **다음**합니다.
3. 선택 **예**내보내려면 개인 키 옵션을 클릭 **다음**합니다.
4. 선택 **개인 정보 교환-#12 PKCS (합니다. PFX)** 기본값을 수락 하기만 하면 **모든 인증서를 인증 경로 포함** 가능 합니다.
5. 사용자 가/그룹 및 내보내는 인증서에 대 한 암호를 할당을 클릭 **다음**합니다.
6. 페이지 내보낼 파일, 내보낸된 파일을 저장할 위치를 검색 하 고 이름을 지정 합니다.
7. 마찬가지로,의 인증서를 내보냅니다. CER 형식 있습니다. 참고:를 내보낼 수 있습니다. CER 형식 예 선택을 취소, 개인 키 옵션 내보냅니다.
8. 복사는 합니다. ServerCertificate.cr 폴더로 PFX 합니다.
9. 복사는 합니다. 파일을 CER NCCertificate.cr 폴더로 합니다.

완료 되 면 이러한 SCVMM 라이브러리에이 폴더 복구 하 고 복사한 이러한 인증서 있는지 확인 합니다. 네트워크 컨트롤러 서비스 템플릿 구성 및 배포 계속 진행 합니다.

## <a name="authenticating-southbound-devices-and-services"></a>인증 Southbound 디바이스 및 서비스 

네트워크 컨트롤러 통신 호스트 SLB MUX 디바이스와 인증을 위한 인증서를 사용합니다. 컴퓨터에서와 통신 SLB MUX 디바이스와 통신 WCF 프로토콜 위에 동안 OVSDB 프로토콜 끝났습니다.

### <a name="hyper-v-host-communication-with-network-controller"></a>네트워크 컨트롤러와 Hyper-v 호스트 통신

Hyper-v 호스트 OVSDB 통해와 통신 하는 데 네트워크 컨트롤러 인증서 호스트 컴퓨터를 제공 해야 합니다. 기본적으로 SCVMM 네트워크 컨트롤러에서 구성 된 SSL 인증서를 선택 하 고 호스트와 southbound 통신을 위해 사용 합니다.

왜 SSL 인증서 클라이언트 인증 EKU 구성 되어 있어야 하는 이유입니다. "서버" 나머지에이 인증서가 구성 되어 리소스 \ (Hyper-v 호스트에에서 나타납니다 네트워크 컨트롤러 서버 resource\)를 Windows PowerShell 명령을 실행 하 여 볼 수 **Get NetworkControllerServer**합니다.

다음은 서버 나머지 리소스 부분적으로 예입니다.

      "resourceId": "host31.fabrikam.com",
      "properties": {
        "connections": [
          {
            "managementAddresses": [
               "host31.fabrikam.com"
            ],
            "credential": {
              "resourceRef": "/credentials/a738762f-f727-43b5-9c50-cf82a70221fa"
            },
            "credentialType": "X509Certificate"
          }
        ],

상호 인증을 위해 Hyper-v 호스트도 인증서가 있어야 네트워크 컨트롤러와 통신 하도록 합니다. 

인증서를 인증 기관 \(CA\) 등록할 수 있습니다. 호스트 시스템에 따라 된 인증서를 없으면 SCVMM 자체 서명된 인증서를 만들고 호스트 컴퓨터에서 제공 합니다.

네트워크 컨트롤러 및 Hyper-v 호스트 인증서 서로 신뢰할 수 있어야 합니다. Hyper-v 호스트 인증서 루트 인증서에 있어야 네트워크 컨트롤러 신뢰할 수 있는 루트 인증 기관 그 반대의 로컬 컴퓨터에 저장 합니다. 

Self\ 서명 인증서를 사용 하는 경우 SCVMM 필요한 인증서 로컬 컴퓨터에 대 한 신뢰할 수 있는 인증 기관 스토어에 있는지 확인 합니다. 

캘리포니아 기반 인증서 Hyper-v 호스트에 대 한를 사용 하는 로컬 컴퓨터에 대 한 네트워크 컨트롤러 신뢰할 수 있는 인증 기관 스토어에서 캘리포니아 루트 인증서가 있는지 확인 해야 합니다.

### <a name="software-load-balancer-mux-communication-with-network-controller"></a>네트워크 컨트롤러와 소프트웨어 부하 분산 MUX 통신

네트워크 컨트롤러와 소프트웨어 부하 분산 멀티플렉서 \(MUX\) 통신할 WCF 프로토콜 인증을 위한 인증서를 사용 합니다.

기본적으로 SCVMM 네트워크 컨트롤러에서 구성 된 SSL 인증서를 선택 하 고 Mux 디바이스와 southbound 통신을 위해 사용 합니다. 이 인증서 "NetworkControllerLoadBalancerMux"을 구성 리소스 놓고 Powershell cmdlet 실행 하 여 볼 수 **Get NetworkControllerLoadBalancerMux**합니다.

MUX 나머지 리소스 \(partial\)의 예:

      "resourceId": "slbmux1.fabrikam.com",
      "properties": {
        "connections": [
          {
            "managementAddresses": [
               "slbmux1.fabrikam.com"
            ],
            "credential": {
              "resourceRef": "/credentials/a738762f-f727-43b5-9c50-cf82a70221fa"
            },
            "credentialType": "X509Certificate"
          }
        ],

상호 인증을 해야 인증서 SLB MUX 디바이스에서 합니다. 이 인증서 SCVMM를 사용 하 여 소프트웨어 부하 분산 배포할 때 SCVMM 하 여 자동으로 구성 됩니다.

>[!IMPORTANT]
>호스트 켜고 SLB 노드 것이 중요 신뢰할 수 있는 인증 기관 인증서 스토어 인증서 포함 되지 않습니다 "에 대해 발급" 없는 "인증서가" 동일 합니다. 이 문제가 발생 하면 네트워크 컨트롤러 및 southbound 디바이스 간 통신 작동 하지 않습니다.

네트워크 컨트롤러 및 SLB MUX 인증서 신뢰할 수 있어야 서로 \ (SLB MUX 인증서 루트 인증서 신뢰할 수 있는 인증 기관을 저장 않으며 versa\ 네트워크 컨트롤러 컴퓨터에 이어야 함). SCVMM 필요한 인증서에 있는지 확인 self\ 서명 인증서를 사용 하는 경우는 루트 신뢰할 수 있는 인증 기관에서 로컬 컴퓨터에 저장 합니다.



