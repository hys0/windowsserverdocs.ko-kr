---
title: Always On VPN 문제 해결
description: 이 항목에서는 확인 및 Windows Server 2016에서 Always On VPN 배포 문제 해결에 대 한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 47d22d566407f45fe6ac78931ffea7b5b2854a1c
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067377"
---
# Always On VPN 문제 해결 

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

Always On VPN 설정, 클라이언트 내부 네트워크에 연결할 실패 하는 경우 잘못 된 VPN 인증서, 잘못 된 NPS 정책 또는 클라이언트 배포 스크립트를 사용 하 여 또는 라우팅 및 원격 액세스 문제는 원인 가능성이입니다. Always On VPN 인프라의 핵심 구성 요소를 이해 하는 첫 번째 단계 문제 해결 및 VPN 연결을 테스트 합니다. 

여러 가지 방법으로 연결 문제를 해결할 수 있습니다. 클라이언트 쪽 문제 및 일반 문제 해결에 대 한 클라이언트 컴퓨터에서 응용 프로그램 로그는 중요 합니다. 인증 관련 문제에 대 한 NPS 서버에서 NPS 로그 유용 문제의 원인을 파악 합니다.


## 오류 코드


### 오류 코드: 800

-   **오류 설명입니다.** 원격 연결을 시도한 VPN 터널 실패 했기 때문에 되어 있지 않습니다. VPN 서버를 연결할 수 없을 수 있습니다. 이 연결 L2TP/IPsec 터널을 사용 하려고 하는 경우 협상 제대로 구성 되지 않음 ipsec 보안 매개 변수가 필요 합니다.


-   **가능한 원인 합니다.** VPN 터널 유형을 **자동** 이며 모든 VPN 터널에 대 한 연결 시도가 실패 하면이 오류가 발생 합니다.

-   **가능한 해결 방법:**

    -   배포에 사용 하 여 어떤 터널을 알고 있는 경우 VPN 클라이언트 쪽에서 해당 특정 터널 형식으로 VPN 유형을 설정 합니다.

    -   특정 터널 종류를 사용 하 여 VPN 연결을 만들어서 연결이 실패 여전히 있지만 더 터널 관련 오류 (예를 들어 "GRE pptp 차단")에 발생 합니다.

    -   VPN 서버에 연결할 수 없는 또는 터널 연결이 실패 하는 경우에이 오류가 발생 합니다.

-   **확실히 하세요:**

    -   IKE 포트 (UDP ports500 및 4500) 차단 되지 않습니다.

    -   IKE에 대 한 올바른 인증서를 클라이언트와 서버 모두에서 제공 됩니다.

### 오류 코드: 809

-   **오류 설명입니다.**  원격 서버 응답 하지 않으므로 컴퓨터와 VPN 서버 간의 네트워크 연결을 설정할 수 없습니다. 이 수 있기 때문에 네트워크 디바이스 중 하나 \ (예: NAT, 방화벽, routers\) 컴퓨터와 원격 서버 간에 하도록 구성 되지 않은 VPN 연결을 허용 합니다. 관리자에 게 문의 하거나 디바이스를 결정 하려면 서비스 공급자 문제를 일으킬 수 있습니다.

-   **가능한 원인 합니다.** 이 오류는 차단된 UDP 500 또는 4500 포트 VPN 서버 또는 방화벽에 의해 발생 합니다.

-   **가능한 솔루션입니다.** UDP ports500 및 4500 RRAS 서버와 클라이언트 간의 모든 방화벽을 통해 사용할 수 있는지 확인 합니다. 
    
    
### 오류 코드: 812

-   **오류 설명입니다.** Always On VPN에 연결할 수 없습니다. RAS/VPN 서버에 구성 된 정책으로 인해 연결 하지 못했습니다. 특히, 사용자 이름 확인 하는 데 필요한 서버를 인증 방법 및 암호 연결 프로필에 구성 된 인증 방법이 일치 하지 않을 수 있습니다. RAS 서버 관리자에 게 문의 하 고 님이 오류를 알립니다.

-   **가능한 원인:**

    -  NPS가 클라이언트 만족 하는 인증 상태를 지정 하는 것이이 오류는 일반적인 발생 합니다. NPS PEAP 연결을 보호 하는 인증서를 사용을 지정할 수 있지만 클라이언트 EAP MSCHAPv2를 사용 하려고 합니다. 예를 들어.

    -  VPN 클라이언트 컴퓨터의 RRAS 기반 VPN 서버 인증 프로토콜 설정 일치 하지 않을 때 이벤트 뷰어에 이벤트 로그 20276 기록 됩니다.

-   **가능한 솔루션입니다.** 클라이언트 구성 NPS 서버에 지정 된 조건을 일치 하는지 확인 합니다.


### 오류 코드: 13806

-   **오류 설명입니다.** IKE 유효한 컴퓨터 인증서를 찾을 수 없습니다. 적절 한 인증서 저장소에 유효한 인증서를 설치 하는 방법에 대 한 네트워크 보안 관리자에 게 문의 합니다.

-   **가능한 원인 합니다.** 이 오류는 일반적으로 경우 컴퓨터 인증서 발생 또는 VPN 서버에서 루트 컴퓨터 인증서.

-   **가능한 솔루션입니다.** 이 배포에 설명 된 인증서를 VPN 서버와 클라이언트 컴퓨터에 설치 되어 있는지 확인 합니다.

### 오류 코드: 13801

-   **오류 설명입니다.** IKE 인증 자격 증명 허용 되지 않습니다.

-   **가능한 원인 합니다.** 이 오류는 일반적으로 다음과 같은 경우 중 하나에 발생합니다.

    -   RAS 서버의 IKEv2 유효성 검사에 사용 되는 컴퓨터 인증서 **키 사용**에서 **서버 인증이** 필요는 없습니다.

    -   RAS 서버의 컴퓨터 인증서 만료 되었습니다.

    -   RAS 서버 인증서의 유효성을 검사 하 여 루트 인증서는 클라이언트 컴퓨터에 존재 하지 않습니다.

    -   클라이언트 컴퓨터에 사용 되는 VPN 서버 이름 서버 인증서의 **subjectName** 일치 하지 않습니다.

-   **가능한 솔루션입니다.** **확장 된 키 사용**에서 **서버 인증** 서버 인증서에 포함 되어 있는지 확인 합니다. 서버 인증서가 여전히 유효한 지 확인 합니다. RRAS 서버에서 **신뢰할 수 있는 루트 인증 기관** 에서 사용 되는 CA 나열 되어 있는지 확인 합니다. VPN 클라이언트가 VPN 서버 인증서에 표시 되는 VPN 서버의 FQDN을 사용 하 여 연결 되는지 확인 합니다.


### 오류 코드: 0x80070040

-   **오류 설명입니다.** 서버 인증서 없는 **서버 인증** 인증서 사용 항목 중 하나로 합니다.

-   **가능한 원인 합니다.** RAS 서버에 서버 인증 인증서가 설치 하는 경우이 오류가 발생할 수 있습니다.

-   **가능한 솔루션입니다.** RAS 서버는 **IKEv2** 에 사용 하는 컴퓨터 인증서에 인증서 사용 항목 중 하나로 **서버 인증이** 있는지 확인 합니다.

### 오류 코드: 0x800B0109

일반적으로 VPN 클라이언트 컴퓨터가 Active Directory 기반 도메인에 가입 됩니다. 인증서는 신뢰할 수 있는 루트 인증 기관에 자동으로 설치 하 고 도메인 자격 증명을 사용 하 여 VPN 서버에 로그온 할 경우를 저장 합니다. 그러나 컴퓨터를 도메인에 가입 되지 않은 경우 또는 다른 인증서 체인을 사용 하는 경우이 문제가 발생할 수 있습니다.

-   **오류 설명입니다.** 인증서 체인 처리 하지만 종료 루트 인증서를 신뢰 공급자를 신뢰 하지 않습니다.

-   **가능한 원인 합니다.** 신뢰할 수 있는 루트 인증 기관에서 적절 한 신뢰할 수 있는 루트 CA 인증서를 설치 하지 않은 경우이 오류가 발생할 클라이언트 컴퓨터에 저장 합니다.

-   **가능한 솔루션입니다.** 루트 인증서는 신뢰할 수 있는 루트 인증 기관 저장소에서 클라이언트 컴퓨터에 설치 되어 있는지 확인 합니다.

## 로그

### 응용 프로그램 로그

클라이언트 컴퓨터에서 응용 프로그램 로그는 대부분의 VPN 연결 이벤트의 상위 세부 정보를 기록합니다.

다음 인터페이스의 원본에서 이벤트를 찾습니다. 모든 오류 메시지는 메시지의 끝에 오류 코드를 반환 합니다. 아래에 자세히 설명 되어 보다 일반적인 오류 코드의 일부 이지만 전체 목록은 [라우팅 및 원격 액세스 오류 코드에서](https://msdn.microsoft.com/library/windows/desktop/bb530704.aspx)사용할 수 있습니다.

## NPS 로그
NPS 만들고 NPS 계정 로그를 저장 합니다. 기본적으로 %SYSTEMROOT%\\System32\\Logfiles\\에 명명 된 파일에서에 저장 됩니다*XXXX.* *XXXX* 은 날짜 txt 파일을 작성 합니다.

기본적으로 이러한 로그 쉼표로 구분 된 값 형식에는 제목 행을 포함 하지 않습니다. 제목 행은입니다.

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

로그 파일의 첫 번째 줄이 머리글 행을 붙여 후 Microsoft Excel로 파일을 가져옵니다, 그리고 열을 제대로 표시 됩니다.

NPS 로그 정책 관련 문제를 진단 하는 데 유용할 수 있습니다. NPS 로그에 대 한 자세한 내용은 [해석 NPS 데이터베이스 형식 로그 파일](https://technet.microsoft.com/library/cc771748.aspx)을 참조 하세요.

## VPN_Profile.ps1 스크립트 문제
수동으로 VPN_ Profile.ps1 스크립트를 실행할 때 가장 일반적인 문제는 다음과 같습니다.

- 원격 연결 도구를 사용 합니까?  사용자 로그인 감지를 사용 하 여 디자인이 바뀝니다 RDP 또는 기타 원격 연결 방법을 사용 했는지 확인 합니다.

- 사용자는 로컬 컴퓨터의 관리자 인지 확인 합니다.  VPN_Profile.ps1 스크립트를 실행 하는 동안 사용자가 관리자 권한이 있는지 확인 합니다.

- 추가 PowerShell 보안 기능을 사용할 수 있습니까? PowerShell 실행 정책을 스크립트를 차단 하 고 있지 있는지 확인 합니다. 스크립트를 실행 하기 전에 활성화 된 경우 제한 된 언어 모드를 해제 하는 것이 좋습니다. 스크립트가 완료 된 후 제한 된 언어 모드를 활성화할 수 있습니다.

## Always On VPN 클라이언트 연결 문제
작은 잘못 된 구성은 클라이언트 연결에 실패 하면 및 원인을 찾으려면 하기가 어려울 수 있습니다.  Always On VPN 클라이언트 연결을 설정 하기 전에 몇 가지 단계를 거칩니다. 클라이언트 연결 문제를 해결할 때 다음으로 제거 하는 프로세스를 수행 합니다.


1. 템플릿 컴퓨터를 외부 연결 되어 있습니까? **Whatismyip** 검사에 속하지 않는 공용 IP 주소를 표시 해야 합니다.

2. 원격 액세스/VPN 서버 이름을 IP 주소로 해결할 수 있나요? **제어판**에서 \> **네트워크** 및 **인터넷** \> **네트워크 연결**을 VPN 프로필에 대 한 속성을 엽니다. **일반** 탭에 있는 값 DNS를 통해 공개적으로 확인할 수 있어야 합니다.

3. VPN 서버 외부 네트워크에서 액세스할 수 있나요? 외부 인터페이스에 인터넷 제어 메시지 프로토콜 (ICMP)를 열고 원격 클라이언트에서 이름을 ping을 실행 하는 것이 좋습니다. ICMP를 제거할 수 ping 작업이 성공한 후 규칙을 허용 합니다.

4. 올바르게 구성 하는 VPN 서버에서 내부 및 외부 Nic 있습니까? 다른 서브넷에 있는 란? 방화벽에서 올바른 인터페이스에 연결 되어 외부 NIC 있습니까?

5. UDP 500 및 4500 포트 VPN 서버의 외부 인터페이스로 클라이언트에서 열려 있는? 클라이언트 방화벽, 서버 방화벽 및 하드웨어 방화벽을 확인 합니다. IPSEC 사용 UDP 포트 500, 따라서 확인 있는지 IPEC 비활성화 되거나 아무 곳 이나 차단 되지 않은 합니다.

7. 인증서 유효성 검사 실패 NPS 서버에 IKE 요청을 지원할 수 있는 서버 인증 인증서를 확인 합니다. NPS 클라이언트로 지정 하 여 올바른 VPN 서버 IP 했는지 확인 합니다. 인증 하 고 있는 PEAP 및 EAP 보호 속성에는 인증 인증서로만 허용 해야 하는지 확인 합니다. 인증 실패에 대 한 NPS 이벤트 로그를 확인할 수 있습니다. 자세한 내용은 [NPS 서버 설치 및 구성](vpn-deploy-nps.md) 를 참조 하세요.

8. 연결 하는 인터넷/로컬 네트워크 액세스 권한이 없습니다. DHCP/VPN 서버 IP 풀 구성 문제를 확인 합니다.

9.  연결 하 고는 유효한 내부 ip 없이 로컬 리소스에 액세스할 수 없습니다.  클라이언트는 해당 리소스를 다운로드 하는 방법을 알고 있는지 확인 합니다. 경로 요청 하도록 VPN 서버를 사용할 수 있습니다.


## Azure AD 조건부 액세스 연결 문제

### 이런-가져올 수 없습니다이 아직

-   **오류 설명입니다.** 조건부 액세스 정책, 충족 되지 않으면 VPN 연결을 차단 하지만 후 연결 하는 경우 사용자가 메시지를 닫으면 **X** 클릭 합니다.  **확인** 을 클릭 하면 다른 _Oops_ 메시지에는 다른 인증 시도 합니다. 이러한 이벤트는 클라이언트의 AAD 운영 이벤트 로그에 기록 됩니다. 

-   **가능한 원인 합니다.** 

    - 사용자가 Azure AD에서 발급 하지는 유효한 클라이언트 인증에에서 인증서의 개인 인증서 저장소에 있습니다.

    - VPN 프로필 \ < TLSExtensions\ > 섹션은 없거나 **는 포함 되어 있지 \ < EKUName\ > AAD 조건부 Access\ < / EKUName\ > \ < EKUOID\ > 1.3.6.1.4.1.311.87 < / EKUOID\ > \ < EKUName > AAD 조건부 액세스 < / EKUName\ > \ < EKUOID\ > 1.3.6.1.4.1.311.87 < / EKUOID\ >** 항목입니다. \ < EKUName > 및 \ < EKUOID > 항목 알 VPN 클라이언트 인증서를 VPN 서버에 인증서를 전달할 때 사용자의 인증서 저장소에서 검색 합니다. 이렇게 하지 않으면 모든 유효한 클라이언트 인증 인증서가 사용자의 인증서 저장소에 VPN 클라이언트는 및 인증이 성공 합니다. 

    - RADIUS 서버 (NPS)만 포함 OID **AAD 조건부 액세스** 하는 클라이언트 인증서를 수락 하도록 구성 되지 않았습니다.

-   **가능한 솔루션입니다.** 이 루프를 이스케이프할 하려면 다음을 수행 합니다.

    1. Windows PowerShell에서 VPN 프로필 구성 덤프 **Get-wmiobject** cmdlet을 실행 합니다. 
    2. 되어 있는지 확인 합니다 **\ < TLSExtensions >**, **\ < EKUName >**, 및 **\ < EKUOID >** 섹션 존재 하 고 올바른 이름과 OID를 보여 줍니다. 
        ```
        PS C:\> Get-WmiObject -Class MDM_VPNv2_01 -Namespace root\cimv2\mdm\dmmap

        __GENUS                 : 2
        __CLASS                 : MDM_VPNv2_01
        __SUPERCLASS            :
        __DYNASTY               : MDM_VPNv2_01
        __RELPATH               : MDM_VPNv2_01.InstanceID="AlwaysOnVPN",ParentID="./Vendor/MSFT/VPNv2"
        __PROPERTY_COUNT        : 10
        __DERIVATION            : {}
        __SERVER                : DERS2
        __NAMESPACE             : root\cimv2\mdm\dmmap
        __PATH                  : \\DERS2\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="AlwaysOnVPN",ParentID="./Vendor/MSFT/VP
                                    Nv2"
        AlwaysOn                :
        ByPassForLocal          :
        DnsSuffix               :
        EdpModeId               :
        InstanceID              : AlwaysOnVPN
        LockDown                :
        ParentID                : ./Vendor/MSFT/VPNv2
        ProfileXML              : <VPNProfile><RememberCredentials>false</RememberCredentials><DeviceCompliance><Enabled>true</
                                    Enabled><Sso><Enabled>true</Enabled></Sso></DeviceCompliance><NativeProfile><Servers>derras2.
                                    corp.deverett.info;derras2.corp.deverett.info</Servers><RoutingPolicyType>ForceTunnel</Routin
                                    gPolicyType><NativeProtocolType>Ikev2</NativeProtocolType><Authentication><UserMethod>Eap</Us
                                    erMethod><MachineMethod>Eap</MachineMethod><Eap><Configuration><EapHostConfig
                                    xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId
                                    xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config
                                    xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.
                                    com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.mic
                                    rosoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptFor
                                    ServerValidation>true</DisableUserPromptForServerValidation><ServerNames></ServerNames></Serv
                                    erValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Ea
                                    p xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type>
                                    <EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><Credenti
                                    alsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore
                                    ></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUse
                                    rPromptForServerValidation><ServerNames></ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b
                                    1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>fal
                                    se</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/E
                                    apTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://ww
                                    w.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</AcceptServerName><TLSExtens
                                    ions
                                    xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xml
                                    ns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><
                                    EKUName>AAD Conditional
                                    Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList
                                    Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></Client
                                    AuthEKUList></FilteringInfo></TLSExtensions></EapType></Eap><EnableQuarantineChecks>false</En
                                    ableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><Perfo
                                    rmServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2"
                                    >false</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisionin
                                    g/MsPeapConnectionPropertiesV2">false</AcceptServerName></PeapExtensions></EapType></Eap></Co
                                    nfig></EapHostConfig></Configuration></Eap></Authentication></NativeProfile></VPNProfile>
        RememberCredentials     : False
        TrustedNetworkDetection :
        PSComputerName          : DERS2
        ```

    3. 사용자의 인증서 저장소에 유효한 인증서가 있는지를 확인 하려면 **Certutil** 명령을 실행 합니다.

       ```
       C:\>certutil -store -user My

        My "Personal"
        ================ Certificate 0 ================
        Serial Number: 32000000265259d0069fa6f205000000000026
        Issuer: CN=corp-DEDC0-CA, DC=corp, DC=deverett, DC=info
         NotBefore: 12/8/2017 8:07 PM
         NotAfter: 12/8/2018 8:07 PM
        Subject: E=winfed@deverett.info, CN=WinFed, OU=Users, OU=Corp, DC=corp, DC=deverett, DC=info
        Certificate Template Name (Certificate Type): User
        Non-root Certificate
        Template: User
        Cert Hash(sha1): a50337ab015d5612b7dc4c1e759d201e74cc2a93
          Key Container = a890fd7fbbfc072f8fe045e680c501cf_5834bfa9-1c4a-44a8-a128-c2267f712336
          Simple container name: te-User-c7bcc4bd-0498-4411-af44-da2257f54387
          Provider = Microsoft Enhanced Cryptographic Provider v1.0
        Encryption test passed
        
        ================ Certificate 1 ================
        Serial Number: 367fbdd7e6e4103dec9b91f93959ac56
        Issuer: CN=Microsoft VPN root CA gen 1
         NotBefore: 12/8/2017 6:24 PM
         NotAfter: 12/8/2017 7:29 PM
        Subject: CN=WinFed@deverett.info
        Non-root Certificate
        Cert Hash(sha1): 37378a1b06dcef1b4d4753f7d21e4f20b18fbfec
          Key Container = 31685cae-af6f-48fb-ac37-845c69b4c097
          Unique container name: bf4097e20d4480b8d6ebc139c9360f02_5834bfa9-1c4a-44a8-a128-c2267f712336
          Provider = Microsoft Software Key Storage Provider
        Private key is NOT exportable
        Encryption test passed
       ```
       >[!NOTE]
       >발급자에서 인증서 경우 **CN = 1 Microsoft VPN 루트 CA 생성** **X** Oops 메시지를 닫고 CAPI2 이벤트 로그를 수집을 클릭 하 여 액세스 권한을 얻은 사용자 인증에 사용 된 인증서를 확인 하는 사용자의 개인 저장소에 있으면는 유효한 클라이언트 인증 인증서가 Microsoft VPN 루트 CA에서에서 발급 되지 않았습니다.

   4. 유효한 클라이언트 인증 인증서는 사용자의 개인 저장소에 있으면 연결에 실패 하면 (는) 한 후 **X** 를 클릭할 경우 합니다 **\ < TLSExtensions >**, **\ < EKUName >**, 및 **\ < EKUOID >** 섹션과 존재 올바른 정보를 포함 합니다.<p>_확장할 수 있는 인증 프로토콜을 사용 하 여 사용할 수 있는 인증서를 찾을 수 없습니다._ 오류 메시지가 나타납니다.

### VPN 연결 블레이드에서 인증서를 삭제할 수 없습니다.

-   **오류 설명입니다.** VPN 연결 블레이드에서 인증서를 삭제할 수 없습니다.

-   **가능한 원인 합니다.** 인증서는 **기본**으로 설정 됩니다.

-   **가능한 솔루션입니다.** 

    1. VPN 연결 블레이드에서 인증서를 선택 합니다.
    2. **기본**영역에서 **아니요** 를 선택 하 고 **저장**을 클릭 합니다.
    3. VPN 연결 블레이드에서 인증서를 다시 선택 합니다.
    4. **삭제**를 클릭 합니다.


---
