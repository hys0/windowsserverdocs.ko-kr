---
title: Always On VPN 문제 해결
description: 이 항목에서는 확인 하 고 Windows Server 2016에서 Always On VPN 배포 문제 해결에 대 한 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d9e0efede39f5a8189dbb3d62033210c393c424d
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749643"
---
# <a name="troubleshoot-always-on-vpn"></a>Always On VPN 문제 해결 

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

Always On VPN 설정이 내부 네트워크에 클라이언트 연결에 실패 하는 경우 잘못 된 VPN 인증서, 잘못 된 NPS 정책 또는 또는 라우팅 및 원격 액세스 클라이언트 배포 스크립트를 사용 하 여 문제 원인은 것입니다. 문제 해결 및 VPN 연결을 테스트 하려면 먼저 Always On VPN 인프라의 핵심 구성 요소를 이해입니다. 

여러 가지 방법으로 연결 문제를 해결할 수 있습니다. 클라이언트 쪽 문제 및 일반적인 문제 해결, 클라이언트 컴퓨터에서 응용 프로그램 로그를 중요 하지 않습니다. 인증 관련 문제에 대 한 NPS 서버의 NPS 로그 문제의 원인을 확인할 수 있습니다.

## <a name="error-codes"></a>오류 코드

### <a name="error-code-800"></a>오류 코드: 800

- **오류 설명입니다.** 시도한 VPN 터널이 실패 한 원격 연결이 설정 되지 않았습니다. VPN 서버를 연결할 수 없습니다. 이 연결 L2TP/IPsec 터널을 사용 하려고 하는 경우 IPsec 협상 제대로 구성 되지에 보안 매개 변수가 필요 합니다.

- **가능한 원인입니다.** VPN 터널 종류 되 면이 오류는 발생 **자동** 하 고 모든 VPN 터널에 대 한 연결 시도가 실패 합니다.

- **가능한 솔루션:**

    - 배포에 사용 하는 터널을 알고 있는 경우 VPN 클라이언트 쪽 VPN 유형을 해당 특정 터널 유형으로 설정 합니다.

    - 특정 터널 종류를 사용 하 여 VPN 연결을 만들어 연결 여전히 실패 하지만 예를 들어, "GRE (PPTP 차단") 보다 터널 특정 오류를 발생 합니다.

    - VPN 서버에 연결할 수 없거나 터널 연결에 실패 하는 경우에이 오류가 발생 합니다.

- **확실히 하세요:**

    - IKE 포트 (UDP 포트 500과 4500) 차단 되지 않습니다.

    - IKE에 대 한 올바른 인증서는 클라이언트와 서버 모두에 존재 합니다.

### <a name="error-code-809"></a>오류 코드: 809

- **오류 설명입니다.**  원격 서버가 응답 하지 않기 때문에 컴퓨터 및 VPN 서버 간의 네트워크 연결을 설정할 수 없습니다. VPN 연결을 허용 하도록 구성 되지 컴퓨터와 원격 서버 간의 네트워크 장치 (예: 방화벽, NAT 라우터) 중 하나 때문일 수 있습니다. 장치 문제를 일으킬 수를 확인 하려면 관리자 또는 서비스 공급자에 게 문의 하십시오.

- **가능한 원인입니다.** 이 오류는 차단 된 UDP 500 또는 VPN 서버에서 방화벽 포트를 4500으로 발생 합니다.

- **가능한 솔루션입니다.** UDP 포트 500과 4500 RRAS 서버와 클라이언트 간의 모든 방화벽을 통해 허용 되는지 확인 합니다.

### <a name="error-code-812"></a>오류 코드: 812

- **오류 설명입니다.** Always On VPN에 연결할 수 없습니다. RAS/VPN 서버에서 구성 된 정책으로 인해 연결 하지 못했습니다. 특히 사용자 이름을 확인 하는 데 필요한 서버를 인증 방법 및 암호가 연결 프로필에 구성 된 인증 방법을 일치 하지 않을 수 있습니다. RAS 서버의 관리자에 게 문의 하 고이 오류의 님에 게 알림 하세요.

- **가능한 원인:**

    - 이 오류의 일반적인 원인은 NPS가 클라이언트 충족할 수 없는 인증 상태를 지정 하는 합니다. 예를 들어 NPS PEAP 연결을 보호 하기 위한 인증서의 사용을 지정할 수 있지만 클라이언트 EAP-MSCHAPv2 사용 하려고 시도 합니다.

    - 이벤트 로그 20276 RRAS 기반의 VPN 서버 인증 프로토콜 설정을 VPN 클라이언트 컴퓨터에서 일치 하지 않는 경우 이벤트 뷰어에 기록 됩니다.

- **가능한 솔루션입니다.** 클라이언트 구성을 NPS 서버에서 지정 된 조건과 일치 하는지 확인 합니다.

### <a name="error-code-13806"></a>오류 코드: 13806

- **오류 설명입니다.** IKE는 유효한 컴퓨터 인증서를 찾지 못했습니다. 적절 한 인증서 저장소에 유효한 인증서를 설치 하는 방법에 대 한 네트워크 보안 관리자에 게 문의 합니다.

- **가능한 원인입니다.** 때 컴퓨터 인증서에 일반적으로이 오류가 발생 하거나 루트 컴퓨터의 인증서가 VPN 서버에 존재 합니다.

- **가능한 솔루션입니다.** 이 배포에 설명 된 인증서는 VPN 서버와 클라이언트 컴퓨터에 설치 되어 있는지 확인 합니다.

### <a name="error-code-13801"></a>오류 코드: 13801

- **오류 설명입니다.** IKE 인증 자격 증명 허용 되지 않습니다.

- **가능한 원인입니다.** 이 오류는 일반적으로 다음 경우 중 하나에서 발생합니다.

    - RAS 서버의 IKEv2 유효성 검사에 사용 되는 컴퓨터 인증서 없는 **서버 인증** 아래에서 **향상 된 키 용도**합니다.

    - RAS 서버의 컴퓨터 인증서가 만료 되었습니다.

    - RAS 서버 인증서 유효성을 검사할 루트 인증서가 클라이언트 컴퓨터입니다.

    - 클라이언트 컴퓨터에서 사용 되는 VPN 서버 이름이 일치 하지 않습니다 합니다 **subjectName** 서버 인증서입니다.

- **가능한 솔루션입니다.** 서버 인증서에 포함 되어 있는지 확인 **서버 인증** 아래에서 **향상 된 키 용도**합니다. 서버 인증서가 여전히 유효한 지 확인 합니다. 사용 되는 CA 아래 나열 되어 있는지 확인 **신뢰할 수 있는 루트 인증 기관** RRAS 서버에 있습니다. VPN 클라이언트는 VPN 서버의 인증서에 표시 된 대로 VPN 서버의 FQDN을 사용 하 여 연결 되는지 확인 합니다.

### <a name="error-code-0x80070040"></a>오류 코드: 0x80070040

- **오류 설명입니다.** 서버 인증서에 없는 **서버 인증** 인증서 사용 항목 중 하 나와 있습니다.

- **가능한 원인입니다.** RAS 서버에 없는 서버 인증 인증서가 설치 하는 경우이 오류가 발생할 수 있습니다.

- **가능한 솔루션입니다.** 컴퓨터 인증서 RAS 서버를 사용 하는지 확인에 대 한 **IKEv2** 했습니다 **서버 인증** 인증서 사용 항목 중 하나로.

### <a name="error-code-0x800b0109"></a>오류 코드: 0x800B0109

일반적으로 VPN 클라이언트 컴퓨터는 Active Directory 기반 도메인에 가입 됩니다. 인증서가 신뢰할 수 있는 루트 인증 기관에 자동으로 설치 하 고 도메인 자격 증명을 사용 하 여 VPN 서버에 로그온 하는 경우 저장 합니다. 그러나 컴퓨터가 도메인에 가입 되어 있지 않으면,는 대체 인증서 체인을 사용 하는 경우이 문제가 발생할 수 있습니다.

- **오류 설명입니다.** 인증서 체인이 처리 되었지만 트러스트 공급자를 신뢰할 수 없는 루트 인증서에서 종료 되었습니다.

- **가능한 원인입니다.** 적절 한 신뢰할 수 있는 루트 CA 인증서를 신뢰할 수 있는 루트 인증 기관에 설치 되어 있지 않으면이 오류가 발생할 수 있습니다 클라이언트 컴퓨터에 저장 합니다.

- **가능한 솔루션입니다.** 신뢰할 수 있는 루트 인증 기관 저장소에 클라이언트 컴퓨터의 루트 인증서가 설치 되었는지 확인 합니다.

## <a name="logs"></a>로그

### <a name="application-logs"></a>응용 프로그램 로그

클라이언트 컴퓨터에서 응용 프로그램 로그는 대부분의 VPN 연결 이벤트의 더 높은 수준의 세부 정보를 기록합니다.

다음 인터페이스의 원본에서 이벤트를 찾아보십시오. 모든 오류 메시지는 메시지의 끝에 있는 오류 코드를 반환합니다. 일반적인 오류 코드 중 일부는 아래에서 자세히, 이지만 전체 목록을 사용할 수 있습니다 [라우팅 및 원격 액세스 오류 코드](https://msdn.microsoft.com/library/windows/desktop/bb530704.aspx)합니다.

## <a name="nps-logs"></a>NPS 로그

NPS가 만들고 NPS 계정 로그를 저장 합니다. 기본적으로 % SYSTEMROOT %에 저장 된 이러한\\System32\\Logfiles\\ 에 라는 파일에*XXXX*.txt, 여기서 *XXXX* 파일을 만든 날짜입니다.

기본적으로 이러한 로그는 쉼표로 구분 된 값 형식으로 되지만 머리글 행을 포함 하지 않습니다. 머리글 행을 다음과 같습니다.

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

로그 파일의 첫 번째 줄이 머리글 행을 붙여넣으면 다음 Microsoft Excel 파일 연결을 가져올 경우 열에 올바르게 표시 되는 합니다.

NPS 로그 정책 관련 문제를 진단 하는 데 유용할 수 있습니다. NPS 로그에 대 한 자세한 내용은 참조 하세요. [NPS 데이터베이스 형식 로그 파일 해석](https://technet.microsoft.com/library/cc771748.aspx)합니다.

## <a name="vpnprofileps1-script-issues"></a>VPN_Profile.ps1 스크립트 문제

수동으로 VPN_ Profile.ps1 스크립트를 실행할 때 가장 일반적인 문제는 다음과 같습니다.

- 원격 연결 도구를 사용 하나요?  사용자 로그인 검색을 사용 하 여 디자인이 바뀝니다 것 처럼 RDP 또는 다른 원격 연결 방법을 사용 하지 않도록 확인 합니다.

- 사용자는 로컬 컴퓨터의 관리자 인지 확인 합니다.  VPN_Profile.ps1 스크립트를 실행 하는 동안 사용자에 대 한 관리자 권한이 있는지 확인 합니다.

- 추가 PowerShell 보안 기능이 활성화 되어 있습니까? PowerShell 실행 정책은 스크립트를 차단 하지 않는지 있는지 확인 합니다. 스크립트를 실행 하기 전에 사용 하도록 설정 하는 경우 제한 된 언어 모드를 해제 하는 것이 좋습니다. 스크립트가 성공적으로 완료 된 후 제한 된 언어 모드를 활성화할 수 있습니다.

## <a name="always-on-vpn-client-connection-issues"></a>Always On VPN 클라이언트 연결 문제

작은 잘못 구성 되어 클라이언트 연결이 실패 하면 및 원인을 찾기 어려울 수 있습니다.  Always On VPN 클라이언트를 연결 하기 전에 몇 가지 단계를 거칩니다. 클라이언트 연결 문제를 해결할 때는 다음을 사용 하 여 제거 프로세스를 통해 이동 합니다.

1. 템플릿 컴퓨터 외부에서 연결 되어 있습니까? A **whatismyip** 검색에 속해 있지 않은 공용 IP 주소를 표시 해야 합니다.

2. 원격 액세스 및 VPN 서버 이름을 IP 주소로 확인할 수 있습니다? **Control Panel** > **네트워크** 하 고 **인터넷** > **네트워크 연결**, 속성을 열고 VPN 프로필. 값을 **일반** 탭 DNS를 통해 공개적으로 확인할 수 있어야 합니다.

3. 외부 네트워크에서 VPN 서버에 액세스할 수 있습니까? 외부 인터페이스에 제어 메시지 ICMP (Internet Protocol)를 열고 원격 클라이언트에서 이름을 ping을 실행 하는 것이 좋습니다. ICMP ping 성공 되 면 제거할 수 있습니다 규칙을 허용 합니다.

4. 올바르게 구성 하는 VPN 서버에서 내부 및 외부 Nic 있습니까? 서로 다른 서브넷에 인가요? 방화벽에서 올바른 인터페이스에 연결 되어 외부 NIC 있습니까?

5. UDP 500과 4500 포트 VPN 서버의 외부 인터페이스에 클라이언트에서 열려 있는? 클라이언트 방화벽, 서버 방화벽 및 하드웨어 방화벽을 확인 합니다. IPSEC 사용 UDP 포트 500 따라서 확인 확실 한 IPEC 비활성화 되거나 아무 곳 이나 차단 없는 합니다.

6. 인증서 유효성 검사 실패 NPS 서버에 IKE 요청을 처리할 수 있는 서버 인증 인증서를 확인 합니다. 올바른 VPN 서버 IP를 NPS 클라이언트로 지정 했는지 확인 합니다. 인증 시 PEAP와 함께 하 고 보호 된 EAP 속성 인증서를 사용 하 여 인증을 허용 해야 하는지 확인 합니다. 인증 오류에 대 한 NPS 이벤트 로그를 확인할 수 있습니다. 자세한 내용은 참조 하세요. [NPS 서버 설치 및 구성](vpn-deploy-nps.md)

7. 연결할 수 있고 인터넷/로컬 네트워크 액세스 권한이 없습니다. 구성 문제에 대 한 DHCP/VPN 서버 IP 풀을 확인 합니다.

8. 연결 하 고 올바른 내부 IP를 수행 하지만 로컬 리소스에 액세스할 수 있는?  클라이언트는 해당 리소스를 이동 하는 방법을 알아두십시오. 요청을 라우팅하는 VPN 서버를 사용할 수 있습니다.

## <a name="azure-ad-conditional-access-connection-issues"></a>Azure AD 조건부 액세스 연결 문제

### <a name="oops---you-cant-get-to-this-yet"></a>이런 기능을 확인할 수 없는이 아직

- **오류 설명입니다.** 때 조건부 액세스 정책이 충족 되지 않음, VPN 연결을 차단 되었지만 연결을 선택한 후 **X** 메시지를 닫습니다.  선택 **확인** 다른 "Oops" 메시지에 끝나는 다른 인증 시도 발생 합니다. 이러한 이벤트는 클라이언트의 AAD Operational 이벤트 로그에 기록 됩니다.

- **가능한 원인**

  - 사용자는 Azure AD에서 발급 되지 않았습니다 하는 유효한 클라이언트 인증 인증서를 해당 개인 인증서에서 저장소에 있습니다.

  - VPN 프로필 \<TLSExtensions\> 없거나 섹션은 포함 하지는 **\<EKUName\>AAD 조건부 액세스\</EKUName\> \< EKUOID\>1.3.6.1.4.1.311.87 < / EKUOID\>\<EKUName > AAD 조건부 액세스 < / EKUName\>\<EKUOID\>1.3.6.1.4.1.311.87 < / EKUOID\>** 항목입니다. 합니다 \<EKUName > 및 \<EKUOID > 항목 클라이언트에 게 알리는 VPN 인증서를 VPN 서버에 인증서를 전달 하는 경우 사용자의 인증서 저장소에서 검색 합니다. 이렇게 하지 않으면 VPN 클라이언트는 모든 유효한 클라이언트 인증 인증서가 사용자의 인증서 저장소에 사용 하 고 인증에 성공 합니다. 

  - RADIUS 서버 (NPS)만 포함 하는 클라이언트 인증서를 수락 하도록 구성 되지에 **AAD 조건부 액세스** OID입니다.

- **가능한 솔루션입니다.** 이 루프를 이스케이프 하려면 다음을 수행 합니다.

  1. Windows PowerShell에서 실행 합니다 **Get-wmiobject** cmdlet을 VPN 프로필 구성 덤프 합니다. 
  2. 있는지 확인 합니다  **\<TLSExtensions >** 를  **\<EKUName >** , 및  **\<EKUOID >** 섹션 존재 하며 올바른 표시 이름 및 OID입니다.
      
      ```powershell
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

  3. 사용자의 인증서 저장소에 유효한 인증서 있는지를 확인 하려면 다음을 실행 합니다 **Certutil** 명령:

     ```powershell
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
     >발급자 로부터 인증서 **CN = Microsoft VPN 루트 CA gen 1** 사용자의 개인 저장소를 선택 하 여 액세스 권한을 사용자에 있는지 **X** Oops 메시지를 닫으려면 확인 하기 위해 CAPI2 이벤트 로그를 수집 인증에 사용 된 인증서가 유효한 클라이언트 인증 인증서는 Microsoft VPN 루트 CA에서에서 발급 되지 않았습니다.

  4. 사용자의 개인 저장소에 유효한 클라이언트 인증 인증서가 있으면 연결이 실패 하면 (예상) 하는 대로 사용자가 선택 합니다 **X** 경우에  **\<TLSExtensions >** ,  **\<EKUName >** , 및  **\<EKUOID >** 섹션 존재 하 고 올바른 정보를 포함 합니다.
   
     "인증서를 찾지 못했습니다 확장할 수 있는 인증 프로토콜을 사용 하 여 사용할 수 있는" 라는 오류 메시지가 표시 됩니다.

### <a name="unable-to-delete-the-certificate-from-the-vpn-connectivity-blade"></a>VPN 연결 블레이드에서 인증서를 삭제할 수 없습니다.

- **오류 설명입니다.** VPN 연결 블레이드에서 인증서를 삭제할 수 없습니다.

- **가능한 원인입니다.** 인증서로 설정 되어 **기본**입니다.

- **가능한 솔루션입니다.**

    1. VPN 연결 블레이드에서 인증서를 선택 합니다.
    2. 아래 **기본**를 선택 **No**을 선택한 후 **저장**합니다.
    3. VPN 연결 블레이드에서 인증서를 다시 선택 합니다.
    4. 선택 **삭제**합니다.
