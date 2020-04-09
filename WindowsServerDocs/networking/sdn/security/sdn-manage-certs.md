---
title: 소프트웨어 정의 네트워킹에 대 한 인증서 관리
description: 이 항목을 사용 하 여 Windows Server 2016 데이터 센터에서 SDN (소프트웨어 정의 네트워킹)을 배포할 때 네트워크 컨트롤러 Northbound 및 Southbound 통신용 인증서를 관리 하는 방법을 배울 수 있습니다.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/22/2018
ms.openlocfilehash: 3225b3f5065e49521411b35fa3781338086b4e59
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854356"
---
# <a name="manage-certificates-for-software-defined-networking"></a>소프트웨어 정의 네트워킹에 대 한 인증서 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 Windows Server 2016 데이터 센터에서 SDN\) 소프트웨어 정의 네트워킹 \(배포할 때 네트워크 컨트롤러 Northbound 및 Southbound 통신용 인증서를 관리 하는 방법을 알아보고, SDN 관리 클라이언트로 SCVMM\) System Center Virtual Machine Manager \(를 사용할 수 있습니다.

>[!NOTE]
>네트워크 컨트롤러에 대 한 개요 정보는 [네트워크 컨트롤러](../technologies/network-controller/Network-Controller.md)를 참조 하세요.

네트워크 컨트롤러 통신을 보호 하는 데 Kerberos를 사용 하지 않는 경우 인증, 권한 부여 및 암호화에 x.509 인증서를 사용할 수 있습니다.

Windows Server 2016 Datacenter의 SDN은 CA\)서명 된 x.509 인증서 \(자체\-서명 된 인증 기관 및 인증 기관 둘 다 지원 합니다. 이 항목에서는 이러한 인증서를 만들어 보안 네트워크 컨트롤러 Northbound 통신 채널에 적용 하는 방법에 대 한 단계별 지침을 제공 합니다. 이러한 인증서는 관리 클라이언트를 사용 하 여 통신 하 고 Southbound는 소프트웨어 Load Balancer \(SLB\)와 같은 네트워크 장치와 통신 합니다.
.
인증서\-기반 인증을 사용 하는 경우 다음과 같은 방법으로 사용 되는 네트워크 컨트롤러 노드에 하나의 인증서를 등록 해야 합니다.

1. 네트워크 컨트롤러 노드와 관리 클라이언트 (예: System Center Virtual Machine Manager) 간에 SSL\)를 \(SSL(Secure Sockets Layer) Northbound 통신을 암호화 합니다.
2. 네트워크 컨트롤러 노드와 Southbound 장치 및 서비스 (예: Hyper-v 호스트 및 소프트웨어 부하 분산 장치 \(SLBs\)간 인증.

## <a name="creating-and-enrolling-an-x509-certificate"></a>X.509 인증서 만들기 및 등록

자체\-서명 된 인증서 또는 CA에서 발급 한 인증서를 만들고 등록할 수 있습니다.

>[!NOTE]
>SCVMM을 사용 하 여 네트워크 컨트롤러를 배포 하는 경우 네트워크 컨트롤러 서비스 템플릿을 구성 하는 동안 Northbound 통신을 암호화 하는 데 사용 되는 x.509 인증서를 지정 해야 합니다.

인증서 구성에는 다음 값이 포함 되어야 합니다.

- **RestEndPoint** 텍스트 상자의 값은 FQDN\) 또는 IP 주소 \(네트워크 컨트롤러의 정규화 된 도메인 이름 이어야 합니다. 
- **RestEndPoint** 값은 x.509 인증서의 일반 이름, CN\) \(주체 이름과 일치 해야 합니다.

### <a name="creating-a-self-signed-x509-certificate"></a>자체\-서명 된 x.509 인증서 만들기

자체 서명 된 x.509 인증서를 만들어 개인 키로 보호할 수 있습니다 .이 단계는 단일\-노드와 네트워크 컨트롤러의 여러\-노드 배포에 대해 다음 단계를 수행 하 여 암호로\) 보호 \(.

자체\-서명 된 인증서를 만드는 경우 다음 지침을 사용할 수 있습니다.

- DnsName 매개 변수에 대 한 네트워크 컨트롤러 REST 끝점의 IP 주소를 사용할 수 있지만 네트워크 컨트롤러 노드는 모두 단일 랙에 단일 관리 \(서브넷 (예: 단일 랙에 배치 되어야 하므로 권장 되지 않음\)
- 여러 노드 NC 배포의 경우 사용자가 지정 하는 DNS 이름이 DNS 호스트 \(네트워크 컨트롤러 클러스터의 FQDN이 됩니다. 레코드가 자동으로 만들어집니다.\) 
- 단일 노드 네트워크 컨트롤러 배포의 경우 DNS 이름은 네트워크 컨트롤러의 호스트 이름 뒤에 전체 도메인 이름이 올 수 있습니다.

#### <a name="multiple-node"></a>다중 노드

[New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) Windows PowerShell 명령을 사용 하 여 자체\-서명 된 인증서를 만들 수 있습니다.

**구문**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCRESTName>")

**사용 예**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "MultiNodeNC" -DnsName @("NCCluster.Contoso.com")

#### <a name="single-node"></a>단일 노드

[New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) Windows PowerShell 명령을 사용 하 여 자체\-서명 된 인증서를 만들 수 있습니다.

**구문**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCFQDN>")

**사용 예**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "SingleNodeNC" -DnsName @("SingleNodeNC.Contoso.com")

### <a name="creating-a-ca-signed-x509-certificate"></a>CA\-서명 된 x.509 인증서 만들기

CA를 사용 하 여 인증서를 만들려면 AD CS\)\(Active Directory 인증서 서비스를 사용 하 여 PKI\) \(공개 키 인프라를 이미 배포 했어야 합니다. 

>[!NOTE]
>타사 Ca 또는 openssl와 같은 도구를 사용 하 여 네트워크 컨트롤러에서 사용할 인증서를 만들 수 있지만이 항목의 지침은 AD CS와 관련이 있습니다. 타사 CA 또는 도구를 사용 하는 방법에 대 한 자세한 내용은 사용 중인 소프트웨어에 대 한 설명서를 참조 하세요.

CA를 사용 하 여 인증서를 만드는 단계는 다음과 같습니다.

1. 사용자 또는 조직의 도메인 또는 보안 관리자가 인증서 템플릿을 구성 합니다.
2. 사용자 또는 조직의 네트워크 컨트롤러 관리자 또는 SCVMM 관리자는 CA에서 새 인증서를 요청 합니다.

#### <a name="certificate-configuration-requirements"></a>인증서 구성 요구 사항

다음 단계에서 인증서 템플릿을 구성 하는 동안 구성 하는 템플릿에 다음 필수 요소가 포함 되어 있는지 확인 합니다.

1. 인증서 주체 이름은 Hyper-v 호스트의 FQDN 이어야 합니다.
2. 인증서는 로컬 컴퓨터 개인 저장소 (My – cert: \ localmachine\my)에 배치 해야 합니다.
3. 인증서에 서버 인증 (EKU: 1.3.6.1.5.5.7.3.1) 및 클라이언트 인증 (EKU: 1.3.6.1.5.5.7.3.2) 응용 프로그램 정책이 둘 다 있어야 합니다.

>[!NOTE]
>\-Hyper-v 호스트의 개인 \(My – cert: \ localmachine\my\) 인증서 저장소에 FQDN\)\(호스트 정규화 된 도메인 이름으로 CN (주체 이름)이 있는 x.509 인증서가 두 개 이상 있는 경우 SDN에서 사용할 인증서에는 OID 1.3.6.1.4.1.311.95.1.1.1를 사용 하는 추가 사용자 지정 향상 된 키 사용 속성이 있는지 확인 합니다. 그렇지 않으면 네트워크 컨트롤러와 호스트 간의 통신이 작동 하지 않을 수 있습니다.

#### <a name="to-configure-the-certificate-template"></a>인증서 템플릿을 구성 하려면
  
>[!NOTE]
>이 절차를 수행 하기 전에 인증서 요구 사항 및 인증서 템플릿 콘솔에서 사용 가능한 인증서 템플릿을 검토 해야 합니다. 기존 템플릿을 수정 하거나 기존 템플릿의 복제본을 만든 다음 템플릿 복사본을 수정할 수 있습니다. 기존 템플릿의 복사본을 만드는 것이 좋습니다.

1. AD CS가 설치 된 서버에서 서버 관리자에 있는 **도구**를 클릭 한 다음 **인증 기관**을 클릭 합니다. 인증 기관 Microsoft Management Console \(MMC\) 열립니다. 
2. MMC에서 CA 이름을 두 번 클릭 마우스 오른쪽 단추로 클릭 **인증서 템플릿**, 를 클릭 하 고 **관리**합니다.
3. 인증서 템플릿 콘솔이 열립니다. 인증서 템플릿의 모든 세부 정보 창에 표시 됩니다.
4. 세부 정보 창에서 복제 하려는 템플릿을 클릭 합니다.
5.  클릭 된 **작업** 메뉴를 차례로 클릭 **중복 된 템플릿**합니다. 서식 파일 **속성** 대화 상자가 열립니다.
6.  템플릿 **속성** 대화 상자의 **주체 이름** 탭에서 **요청에 제공**을 클릭 합니다. \(이 설정은 네트워크 컨트롤러 SSL 인증서에 필요 합니다.\)
7.  템플릿 **속성** 대화 상자의 **요청 처리** 탭에서 **개인 키를 내보낼 수 있음** 이 선택 되어 있는지 확인 합니다. **서명 및 암호화** 목적도 선택 되어 있는지 확인 합니다.
8.  템플릿 **속성** 대화 상자의 **확장** 탭에서 **키 사용**을 선택 하 고 **편집**을 클릭 합니다.
9.  **서명**에서 **디지털 서명** 이 선택 되어 있는지 확인 합니다.
10.  템플릿 **속성** 대화 상자의 **확장** 탭에서 **응용 프로그램 정책**을 선택 하 고 **편집**을 클릭 합니다.
11.  **응용 프로그램 정책**에서 **클라이언트 인증** 및 **서버 인증** 이 나열 되는지 확인 합니다.
12.  인증서 템플릿의 복사본을 **네트워크 컨트롤러 템플릿**등의 고유한 이름으로 저장 합니다.

#### <a name="to-request-a-certificate-from-the-ca"></a>CA에서 인증서를 요청 하려면

인증서 스냅인을 사용 하 여 인증서를 요청할 수 있습니다. 인증서 요청을 처리 하는 CA의 관리자가 미리 구성 하 고 사용할 수 있도록 설정한 모든 유형의 인증서를 요청할 수 있습니다.

**사용자** 또는 로컬 **관리자** 는이 절차를 완료 하는 데 필요한 최소 그룹 멤버 자격입니다.

1. 컴퓨터의 인증서 스냅인을 엽니다.
2. 콘솔 트리에서 **인증서 \(로컬 컴퓨터\)** 를 클릭 합니다. **개인** 인증서 저장소를 선택 합니다.
3. **작업** 메뉴에서 * * 모든 작업을 가리킨<strong>다음 * * 새 인증서 요청을 클릭</strong> 하 여 인증서 등록 마법사를 시작 합니다. **다음**을 클릭합니다.
4. 관리자 인증서 등록 정책 **으로 구성** 된를 선택 하 고 **다음**을 클릭 합니다.
5. 이전 섹션\)에서 구성한 CA 템플릿에 따라 **Active Directory 등록 정책** \(를 선택 합니다.
6. **세부 정보** 섹션을 확장 하 고 다음 항목을 구성 합니다.
   1. **키 사용** 에 <strong>디지털 서명 * * 및 * * 키 암호화</strong>가 모두 포함 되어 있는지 확인 합니다.
   2. **응용 프로그램 정책** 에 **서버 인증** \(1.3.6.1.5.5.7.3.1\) 및 **클라이언트 인증** \(1.3.6.1.5.5.7.3.2\)가 모두 포함 되어 있는지 확인 합니다.
7. **속성**을 클릭합니다.
8. **주체** 탭에서 **주체 이름**의 **유형**으로 **일반 이름**을 선택 합니다. 값에서 **네트워크 컨트롤러 REST 끝점**을 지정 합니다.
9. **적용**, **확인**을 차례로 클릭합니다.
10. **등록**을 클릭합니다.

인증서 MMC에서 개인 저장소를 클릭 하 여 CA에서 등록 한 인증서를 확인 합니다.

## <a name="exporting-and-copying-the-certificate-to-the-scvmm-library"></a>SCVMM 라이브러리로 인증서 내보내기 및 복사

자체\-서명 된 인증서 또는 CA\-서명 된 인증서를 만든 후에는 인증서 스냅인에서 \(개인 키 \(를 .pfx 형식으로\) 하 고 개인 키 64\)를 사용 하지 않고 인증서를 내보내야 합니다. 

그런 다음 두 개의 내보낸 파일을 NC 서비스 템플릿을 가져올 때 지정한 **ServerCertificate.cr** 및 **NCCertificate.cr** 폴더에 복사 해야 합니다.

1. 인증서 스냅인 (인증서 스냅인)을 열고 로컬 컴퓨터의 개인 인증서 저장소에서 인증서를 찾습니다.
2. 인증서를 마우스 오른쪽 단추로 클릭 하\-**모든 작업**, **내보내기**를 차례로 클릭 합니다. 인증서 내보내기 마법사가 열립니다. **다음**을 클릭합니다.
3. **예**, 개인 키를 내보냅니다. 옵션을 선택 하 고 **다음**을 클릭 합니다.
4. **개인 정보 교환-PKCS #12 (를 선택 합니다.** 가능 하면 **인증 경로에 있는 모든 인증서를 포함** 하도록 기본값을 적용 합니다.
5. 내보내려는 인증서의 사용자/그룹 및 암호를 할당 하 고 **다음**을 클릭 합니다.
6. 내보낼 파일 페이지에서 내보낸 파일을 저장할 위치를 찾아보고 이름을 지정 합니다.
7. 마찬가지로에서 인증서를 내보냅니다. CER 형식입니다. 참고:로 내보내려면로 내보냅니다. CER 형식에서 예, 개인 키를 내보냅니다. 옵션을 선택 취소 합니다.
8. 를 복사 합니다. ServerCertificate.cr 폴더에 대 한 PFX입니다.
9. 를 복사 합니다. NCCertificate.cr 폴더에 CER 파일을 추가할 수 있습니다.

완료 되 면 SCVMM 라이브러리에서 이러한 폴더를 새로 고치고 이러한 인증서를 복사 했는지 확인 합니다. 네트워크 컨트롤러 서비스 템플릿 구성 및 배포를 계속 합니다.

## <a name="authenticating-southbound-devices-and-services"></a>Southbound 장치 및 서비스 인증 

호스트 및 SLB MUX 장치와의 네트워크 컨트롤러 통신에서는 인증을 위해 인증서를 사용 합니다. SLB MUX 장치와의 통신은 WCF 프로토콜을 통해 호스트와의 통신은 OVSDB 프로토콜을 통해 전달 됩니다.

### <a name="hyper-v-host-communication-with-network-controller"></a>네트워크 컨트롤러와의 hyper-v 호스트 통신

OVSDB를 통해 Hyper-v 호스트와 통신 하려면 네트워크 컨트롤러가 호스트 컴퓨터에 인증서를 제공 해야 합니다. 기본적으로 SCVMM은 네트워크 컨트롤러에 구성 된 SSL 인증서를 선택 하 고 호스트와의 southbound 통신에이 인증서를 사용 합니다.

이것은 SSL 인증서에 클라이언트 인증 EKU를 구성 해야 하는 이유입니다. 이 인증서는 "서버" REST 리소스 \(Hyper-v 호스트는 네트워크 컨트롤러에\)서버 리소스로 표시 되며 Windows PowerShell 명령 **NetworkControllerServer**를 실행 하 여 볼 수 있습니다.

다음은 서버 REST 리소스의 일부 예입니다.

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

상호 인증의 경우 Hyper-v 호스트에도 네트워크 컨트롤러와 통신 하기 위한 인증서가 있어야 합니다. 

CA\)\(인증 기관에서 인증서를 등록할 수 있습니다. 호스트 컴퓨터에서 CA 기반 인증서를 찾을 수 없는 경우 SCVMM은 자체 서명 된 인증서를 만들어 호스트 컴퓨터에 프로 비전 합니다.

네트워크 컨트롤러 및 Hyper-v 호스트 인증서는 서로 신뢰 해야 합니다. Hyper-v 호스트 인증서의 루트 인증서는 로컬 컴퓨터의 네트워크 컨트롤러 신뢰할 수 있는 루트 인증 기관 저장소에 있어야 하며 그 반대의 경우도 마찬가지입니다. 

자체\-서명 된 인증서를 사용 하는 경우 SCVMM은 필요한 인증서가 로컬 컴퓨터의 신뢰할 수 있는 루트 인증 기관 저장소에 있는지 확인 합니다. 

Hyper-v 호스트에 대 한 CA 기반 인증서를 사용 하는 경우 로컬 컴퓨터에 대 한 네트워크 컨트롤러의 신뢰할 수 있는 루트 인증 기관 저장소에 CA 루트 인증서가 있는지 확인 해야 합니다.

### <a name="software-load-balancer-mux-communication-with-network-controller"></a>네트워크 컨트롤러와의 MUX 통신 소프트웨어 Load Balancer

소프트웨어 Load Balancer 멀티플렉서 \(MUX\) 및 네트워크 컨트롤러는 인증을 위해 인증서를 사용 하 여 WCF 프로토콜을 통해 통신 합니다.

기본적으로 SCVMM은 네트워크 컨트롤러에 구성 된 SSL 인증서를 선택 하 고이 인증서를 사용 하 여 Mux 장치와의 통신을 southbound 합니다. 이 인증서는 "NetworkControllerLoadBalancerMux" REST 리소스에 구성 되며 Powershell cmdlet **NetworkControllerLoadBalancerMux**를 실행 하 여 볼 수 있습니다.

일부\)\(MUX REST 리소스의 예:

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

상호 인증의 경우 SLB MUX 장치에도 인증서가 있어야 합니다. SCVMM을 사용 하 여 소프트웨어 부하 분산 장치를 배포할 때이 인증서는 SCVMM에 의해 자동으로 구성 됩니다.

>[!IMPORTANT]
>호스트 및 SLB 노드에서는 신뢰할 수 있는 루트 인증 기관 인증서 저장소에 "발급 대상"이 "발급자"와 같지 않은 인증서를 포함 하지 않는 것이 중요 합니다. 이 문제가 발생 하면 네트워크 컨트롤러와 southbound 장치 간의 통신이 실패 합니다.

네트워크 컨트롤러와 SLB MUX 인증서는 서로 신뢰 해야 합니다 \(SLB MUX 인증서의 루트 인증서는 네트워크 컨트롤러 컴퓨터의 신뢰할 수 있는 루트 인증 기관 저장소에 있어야 하 고\)반대의 경우도 마찬가지입니다. 자체\-서명 된 인증서를 사용 하는 경우 SCVMM은 필요한 인증서가 로컬 컴퓨터의 신뢰할 수 있는 루트 인증 기관 저장소에 있는지 확인 합니다.



