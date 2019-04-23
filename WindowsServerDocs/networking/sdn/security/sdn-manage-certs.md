---
title: 소프트웨어 정의 네트워킹에 대 한 인증서 관리
description: 네트워킹 SDN (소프트웨어)에서 Windows Server 2016 Datacenter을 배포할 때 네트워크 컨트롤러 Northbound 및 Southbound 통신에 대 한 인증서를 관리 하는 방법을 알아보려면이 항목에서는 사용할 수 있습니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: c4e2f6c7-0364-4bf8-bb66-9af59c0bbd74
ms.author: pashort
author: shortpatti
ms.date: 08/22/2018
ms.openlocfilehash: 618c2c4da60decc94f84c2a40cd4d2aa80d5f26b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827574"
---
# <a name="manage-certificates-for-software-defined-networking"></a>소프트웨어 정의 네트워킹에 대 한 인증서 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 사용 하 여 소프트웨어 정의 네트워킹 배포 하는 경우 네트워크 컨트롤러 Northbound 및 Southbound 통신에 대 한 인증서를 관리 하는 방법을 알아보려면 \(SDN\) Windows Server 2016 Datacenter에는 시스템 사용 하는 Virtual Machine Manager 가운데 \(SCVMM\) SDN 관리 클라이언트를 합니다.

>[!NOTE]
>네트워크 컨트롤러에 대 한 개요 정보를 참조 하세요 [네트워크 컨트롤러](../technologies/network-controller/Network-Controller.md)합니다.

네트워크 컨트롤러 통신 보안에 대 한 Kerberos를 사용 하지 않는 경우에 인증, 권한 부여 및 암호화에 대 한 X.509 인증서를 사용할 수 있습니다.

Windows Server 2016 Datacenter의 SDN 지원 모두 셀프\-서명 및 인증 기관 \(CA\)-X.509 인증서를 서명 합니다. 이 항목에서는 소프트웨어와 같은 네트워크 장치를 사용 하 여 관리 클라이언트를 사용 하 여 네트워크 컨트롤러 Northbound 통신 채널을 보호 하려면 이러한 인증서를 만들고 적용 하기 위한 단계별 지침 및 Southbound 통신 제공 부하 분산 장치 \(SLB\)합니다.
.
인증서를 사용 하는 경우\-기반 인증의 경우 다음과 같은 방법으로 사용 되는 네트워크 컨트롤러 노드에 대 한 인증서를 등록 해야 합니다.

1. Secure Sockets Layer를 사용 하 여 Northbound 통신을 암호화 \(SSL\) 관리 클라이언트를 System Center Virtual Machine Manager 같은 네트워크 컨트롤러 노드 사이입니다.
2. 네트워크 컨트롤러 노드 및 Southbound 장치와 같은 Hyper-v 호스트 및 소프트웨어 부하 분산 장치 서비스 간 인증 \(SLBs\)합니다.

## <a name="creating-and-enrolling-an-x509-certificate"></a>만들고 X.509 인증서를 등록 합니다.

만들고를 자체 등록할 수 있습니다\-인증서 또는 CA에서 발급 한 인증서를 서명 합니다.

>[!NOTE]
>SCVMM에 네트워크 컨트롤러 배포를 사용 하는 경우 네트워크 컨트롤러 서비스 템플릿을 구성 하는 동안 Northbound 통신을 암호화 하는 데 사용 되는 X.509 인증서를 지정 해야 합니다.

인증서 구성에는 다음 값을 포함 해야 합니다.

- 에 대 한 값을 **RestEndPoint** 텍스트 상자에는 네트워크 컨트롤러 정규화 된 도메인 이름 이어야 합니다. \(FQDN\) 또는 IP 주소입니다. 
- 합니다 **RestEndPoint** 값에는 주체 이름과 일치 해야 \(일반 이름, CN\) X.509 인증서의 합니다.

### <a name="creating-a-self-signed-x509-certificate"></a>자체를 만드는\-서명 된 X.509 인증서

자체 서명 된 X.509 인증서를 만들고 개인 키를 사용 하 여 내보낼 수 있습니다 \(암호로 보호\) 단일이 단계에 따라\-노드와 여러\-네트워크 컨트롤러 노드 배포 .

자체 만들 때\-서명 된 인증서를 다음 지침을 사용할 수 있습니다.

- DnsName 매개 변수-에 대 한 네트워크 컨트롤러 REST 끝점의 IP 주소를 사용할 수 있지만 네트워크 컨트롤러 노드는 모두 단일 관리 서브넷 내에 필요 하기 때문에 권장 되지는 않습니다 \(단일 랙에서 예:\)
- 여러 NC 노드 배포에 대 한 DNS 이름을 지정 하는 네트워크 컨트롤러 클러스터의 FQDN 될 \(DNS 호스트 레코드를 자동으로 생성 됩니다.\) 
- 단일 노드 네트워크 컨트롤러 배포에 대 한 DNS 이름에는 전체 도메인 이름이 옵니다 네트워크 컨트롤러의 호스트 이름일 수 있습니다.

#### <a name="multiple-node"></a>여러 노드

사용할 수는 [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) 자체를 만들려면 Windows PowerShell 명령을\-서명 된 인증서입니다.

**구문**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCRESTName>")

**사용 예**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "MultiNodeNC" -DnsName @("NCCluster.Contoso.com")

#### <a name="single-node"></a>단일 노드

사용할 수는 [New-selfsignedcertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) 자체를 만들려면 Windows PowerShell 명령을\-서명 된 인증서입니다.

**구문**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "<YourNCComputerName>" -DnsName @("<NCFQDN>")

**사용 예**

    New-SelfSignedCertificate -KeyUsageProperty All -Provider "Microsoft Strong Cryptographic Provider" -FriendlyName "SingleNodeNC" -DnsName @("SingleNodeNC.Contoso.com")

### <a name="creating-a-ca-signed-x509-certificate"></a>CA를 만드는\-서명 된 X.509 인증서

CA를 사용 하 여 인증서를 만들려면 해야 이미 배포한 경우 공개 키 인프라 \(PKI\) Active Directory 인증서 서비스를 사용 하 여 \(AD CS\)합니다. 

>[!NOTE]
>이 항목의 지침에는 AD CS 관련이 있지만 네트워크 컨트롤러를 사용 하 여 사용할 인증서를 만들려는 타사 Ca 또는 openssl 같은 도구를 사용할 수 있습니다. 타사 CA 또는 도구를 사용 하는 방법에 알아보려면 사용 중인 소프트웨어에 대 한 설명서를 참조 하세요.

CA를 사용 하 여 인증서를 만드는 다음 단계를 포함 합니다.

1. 사용자 또는 조직의 도메인 또는 보안 관리자 인증서 템플릿 구성
2. 사용자 또는 조직의 네트워크 컨트롤러 관리자 또는 SCVMM 관리자 CA에서 새 인증서를 요청합니다.

#### <a name="certificate-configuration-requirements"></a>인증서 구성 요구 사항

다음 단계에서 인증서 템플릿을 구성 하는 동안 구성한 템플릿을 다음 필요한 요소를 포함 하는지 확인 합니다.

1. 인증서 주체 이름은 Hyper-v 호스트의 FQDN 이어야 합니다.
2. 인증서는 로컬 컴퓨터 개인 저장소에 배치 되어야 합니다 (My-cert: \localmachine\my)
3. 인증서에는 모두 서버 인증 되어야 합니다. (EKU: 1.3.6.1.5.5.7.3.1) 및 클라이언트 인증 (EKU: 1.3.6.1.5.5.7.3.2) 응용 프로그램 정책입니다.

>[!NOTE]
>경우 개인적인 \(내 – cert: \localmachine\my\) 인증서 저장소에를 Hyper\-V 호스트는 호스트의 정규화 된 도메인 이름으로 둘 이상의 X.509 인증서 주체 이름 (CN) 사용 하 여에 \(FQDN\), SDN에서 사용할 인증서 1.3.6.1.4.1.311.95.1.1.1 OID 사용 하 여 추가 사용자 지정 확장 된 키 사용 속성이 있는지 확인 합니다. 그렇지 않은 경우 네트워크 컨트롤러와 호스트 간의 통신 작동 하지 않을 수 있습니다.

#### <a name="to-configure-the-certificate-template"></a>인증서 템플릿을 구성 하려면
  
>[!NOTE]
>이 절차를 수행 하기 전에 인증서 템플릿 콘솔에서 사용할 수 있는 인증서 템플릿 및 인증서 요구 사항을 검토 해야 합니다. 기존 템플릿을 수정 하거나 기존 템플릿을 복제 하 고 템플릿의 복사본을 수정할 수 있습니다. 기존 서식 파일의 복사본을 만드는 것이 좋습니다.

1. 서버의 AD CS가 설치 된 서버 관리자에서 클릭 **도구**를 클릭 하 고 **기관**합니다. 인증 기관 Microsoft Management Console \(MMC\) 열립니다. 
2. MMC에서 CA 이름을 두 번 클릭 마우스 오른쪽 단추로 클릭 **인증서 템플릿**, 를 클릭 하 고 **관리**합니다.
3. 인증서 템플릿 콘솔이 열립니다. 인증서 템플릿의 모든 세부 정보 창에 표시 됩니다.
4. 세부 정보 창에서 복제 하려는 템플릿을 클릭 합니다.
5.  클릭 된 **작업** 메뉴를 차례로 클릭 **중복 된 템플릿**합니다. 서식 파일 **속성** 대화 상자가 열립니다.
6.  템플릿에서 **속성** 대화 상자의 합니다 **주체 이름** 탭을 클릭 **요청에서 제공**합니다. \(이 설정은 네트워크 컨트롤러 SSL 인증서에 대 한 필수입니다.\)
7.  템플릿에서 **속성** 대화 상자의 합니다 **요청 처리** 탭에서 **개인 키를 내보낼 수 있음** 을 선택 합니다. 확인 해야 합니다 **서명 및 암호화** 목적이 선택 되었는지 합니다.
8.  템플릿에서 **속성** 대화 상자의 합니다 **확장** 탭을 선택 **키 사용**를 클릭 하 고 **편집**합니다.
9.  **서명**, 했는지 **디지털 서명을** 을 선택 합니다.
10.  템플릿에서 **속성** 대화 상자의 합니다 **확장** 탭을 선택 **응용 프로그램 정책을**를 클릭 하 고 **편집**합니다.
11.  **응용 프로그램 정책**, 되도록 **클라이언트 인증** 하 고 **서버 인증** 나열 됩니다.
12.  와 같은 고유한 이름을 사용 하 여 인증서 템플릿의 복사본 저장 **네트워크 컨트롤러 템플릿**합니다.

#### <a name="to-request-a-certificate-from-the-ca"></a>CA에서 인증서를 요청 하려면

인증서 스냅인 인증서 요청을 사용할 수 있습니다. 모든 유형의 미리 구성 되었으며 인증서 요청을 처리 하는 CA의 관리자가 사용할 수 있는 인증서를 요청할 수 있습니다.

**사용자가** 또는 로컬 **관리자** 이 절차를 완료 하는 데 필요한 최소 그룹 멤버 자격이 필요 합니다.

1. 컴퓨터에 대 한 인증서 스냅인을 엽니다.
2. 콘솔 트리에서 **인증서 \(로컬 컴퓨터\)** 합니다. 선택 된 **개인** 인증서 저장소입니다.
3. 에 **동작** 메뉴에서 * * 모든 작업 * 및 클릭 한 다음 **새 인증서 요청** 인증서 등록 마법사를 시작 합니다. **다음**을 클릭합니다.
4. 선택 된 **관리자가 구성한** 인증서 등록 정책 및 클릭 **다음**합니다.
5. 선택 된 **Active Directory 등록 정책** \(이전 섹션에서 구성 된 CA 템플릿을 기반으로\)입니다.
6. 확장 된 **세부 정보** 섹션 및 다음 항목을 구성 합니다.
    1. 했는지 **키 사용** 모두 포함 * * 디지털 서명을 * * 및 **키 암호화**합니다.
    2. 했는지 **응용 프로그램 정책** 모두 포함 **Server 인증** \(1.3.6.1.5.5.7.3.1\) 고 **클라이언트 인증** \(1.3.6.1.5.5.7.3.2\)합니다.
7. **속성**을 클릭합니다.
8. 에 **주체** 탭의 **주체 이름**의 **형식**선택 **일반 이름**합니다. 값 지정 **네트워크 컨트롤러 REST 끝점**합니다.
9. **적용**, **확인**을 차례로 클릭합니다.
10. **등록**을 클릭합니다.

인증서 MMC에서 개인 저장소에서 CA를 등록 한 인증서를 보려면 클릭 합니다.

## <a name="exporting-and-copying-the-certificate-to-the-scvmm-library"></a>내보내기 및 SCVMM 라이브러리에 인증서 복사

자체를 만든 후\-서명 또는 CA\-서명 된 인증서를 개인 키를 사용 하 여 인증서를 내보내야 \(.pfx 형식으로\) 및 개인 키 없이 \(Base-64.cer형식으로\) 인증서 스냅인에서. 

두 내보낸된 파일을 복사 해야 합니다 **ServerCertificate.cr** 하 고 **NCCertificate.cr** NC 서비스 템플릿을 가져올 때 시간에 지정한 폴더.

1. 인증서 스냅인 (certlm.msc) 열고 로컬 컴퓨터 개인 인증서 저장소에 인증서를 찾습니다.
2. 오른쪽\-인증서를 클릭 하 고 **모든 작업**를 클릭 하 고 **내보내기**합니다. 인증서 내보내기 마법사가 열립니다. **다음**을 클릭합니다.
3. 선택 **Yes**private key 옵션을 내보내기, 클릭 **다음**합니다.
4. 선택 **개인 정보 교환-PKCS #12 (합니다. PFX ()** 기본값을 수락 **인증 경로 있는 모든 인증서 포함** 가능한 경우.
5. 사용자/그룹 및 내보내는 인증서의 암호를 할당, 클릭 **다음**합니다.
6. 페이지를 내보내려면 파일 내보낸된 파일을 배치 하려는 위치를 찾아 이름을 지정 합니다.
7. 마찬가지로, 인증서를 내보냅니다. CER 형식입니다. 참고: 내보내려면 합니다. CER 형식으로는 Yes를 선택 취소 하, private key 옵션을 내보냅니다.
8. 복사 합니다. ServerCertificate.cr 폴더에 PFX를 제공 합니다.
9. 복사 합니다. CER 파일을 NCCertificate.cr 폴더입니다.

완료 되 면 SCVMM 라이브러리에 이러한 폴더를 새로 고치고이 인증서를 복사 했는지 확인 합니다. 네트워크 컨트롤러 서비스 템플릿 구성 및 배포를 사용 하 여 계속 합니다.

## <a name="authenticating-southbound-devices-and-services"></a>Southbound 장치 및 서비스 인증 

인증에 대 한 인증서를 사용 하는 네트워크 컨트롤러 호스트 및 SLB MUX 장치와 통신 합니다. 호스트와의 통신 OVSDB 프로토콜을 통해는 WCF 프로토콜을 통해는 SLB MUX 장치와 통신 합니다.

### <a name="hyper-v-host-communication-with-network-controller"></a>네트워크 컨트롤러와 Hyper-v 호스트 통신

OVSDB 통해 Hyper-v 호스트와 통신에 대 한 네트워크 컨트롤러 호스트 컴퓨터에 인증서를 제공 해야 합니다. 기본적으로 SCVMM 네트워크 컨트롤러에 구성 된 SSL 인증서를 선택 하 고 호스트와의 southbound 통신에 사용 합니다.

SSL 인증서를 구성 하는 클라이언트 인증 EKU 있어야 하는 이유는 무엇 때문입니다. 이 인증서는 "서버" REST에서 구성 된 리소스 \(Hyper-v 호스트 서버 리소스와 네트워크 컨트롤러에 표시 됩니다\), Windows PowerShell 명령을 실행 하 여 볼 수 있습니다  **Get-NetworkControllerServer**합니다.

다음은 부분적으로 서버 REST 리소스의 예입니다.

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

상호 인증을 위해 Hyper-v 호스트 네트워크 컨트롤러와 통신할 수 인증서를 있어야 합니다. 

인증 기관에서 인증서를 등록할 수 있습니다 \(CA\)합니다. CA 기반 인증서를 호스트 컴퓨터에 없는 경우 SCVMM는 자체 서명 된 인증서를 만들고 호스트 컴퓨터를 프로 비전 합니다.

네트워크 컨트롤러 및 Hyper-v 호스트에서 서로 다른 인증서를 신뢰할 수 있어야 합니다. Hyper-v 호스트 인증서의 루트 인증서에 있어야 네트워크 컨트롤러 신뢰할 수 있는 루트 인증 기관 저장소는 로컬 컴퓨터에 대 한 및 그 반대의 경우도 마찬가지입니다. 

자체 사용 중인 경우\-서명 된 인증서를 SCVMM 필요한 인증서를 로컬 컴퓨터의 신뢰할 수 있는 루트 인증 기관 저장소에 있는지 확인 합니다. 

CA 기반 인증서를 Hyper-v 호스트에 대해 사용 하는 경우 로컬 컴퓨터에 대 한 네트워크 컨트롤러의 신뢰할 수 있는 루트 인증 기관 저장소에 CA 루트 인증서가 있는지 확인 해야 합니다.

### <a name="software-load-balancer-mux-communication-with-network-controller"></a>네트워크 컨트롤러를 사용 하 여 소프트웨어 부하 분산 장치 MUX 통신

소프트웨어 부하 분산 장치 멀티플렉서 \(MUX\) 인증용 인증서를 사용 하 여 네트워크 컨트롤러에서 WCF 프로토콜을 통해 통신 합니다.

기본적으로 SCVMM 네트워크 컨트롤러에 구성 된 SSL 인증서를 선택 하 고 Mux 장치와 southbound 통신에 사용 합니다. 이 인증서는 "NetworkControllerLoadBalancerMux"에 구성 된 리소스 REST 및 Powershell cmdlet을 실행 하 여 볼 수 있습니다 **Get NetworkControllerLoadBalancerMux**합니다.

MUX REST 리소스 예가 \(부분\):

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

상호 인증에도 SLB MUX 장치에서 인증서를 있어야 합니다. SCVMM을 사용 하 여 소프트웨어 부하 분산 장치를 배포 하는 경우이 인증서는 SCVMM에 자동으로 구성 됩니다.

>[!IMPORTANT]
>호스트 및 SLB 노드에서 반드시 신뢰할 수 있는 루트 인증 기관 인증서 저장소에 모든 인증서 포함 되지 않습니다 "발급 대상" 없는 "발급자"와 동일 합니다. 이 경우 네트워크 컨트롤러 southbound 장치 사이의 통신 실패 합니다.

네트워크 컨트롤러와 SLB MUX 인증서 서로 신뢰 해야 합니다 \(SLB MUX 인증서의 루트 인증서는 신뢰할 수 있는 루트 인증 기관 저장소 네트워크 컨트롤러 컴퓨터에 있어야 합니다. 그 반대의\)합니다. 자체를 사용 중인 경우\-서명 된 인증서를 SCVMM 되도록 필요한 인증서에는 신뢰할 수 있는 루트 인증 기관에 로컬 컴퓨터에 저장 합니다.



