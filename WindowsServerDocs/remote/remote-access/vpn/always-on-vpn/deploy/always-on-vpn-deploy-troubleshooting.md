---
title: Always On VPN 문제 해결
description: 이 항목에서는 Windows Server 2016에 Always On VPN 배포를 확인 하 고 문제를 해결 하기 위한 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 649fbc16e3dfef2ed1061d0ba6a5c22a8712b186
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404376"
---
# <a name="troubleshoot-always-on-vpn"></a>Always On VPN 문제 해결 

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

Always On VPN 설정에서 클라이언트를 내부 네트워크에 연결 하지 못하는 경우 원인은 잘못 된 VPN 인증서, 잘못 된 NPS 정책 또는 클라이언트 배포 스크립트나 라우팅 및 원격 액세스와 관련 된 문제가 원인일 수 있습니다. VPN 연결 문제를 해결 하 고 테스트 하는 첫 번째 단계는 Always On VPN 인프라의 핵심 구성 요소를 이해 하는 것입니다. 

연결 문제는 여러 가지 방법으로 해결할 수 있습니다. 클라이언트 쪽 문제 및 일반적인 문제 해결을 위해 클라이언트 컴퓨터의 응용 프로그램 로그는 매우 유용 합니다. 인증 관련 문제의 경우 NPS 서버의 NPS 로그를 통해 문제의 원인을 확인할 수 있습니다.

## <a name="error-codes"></a>오류 코드

### <a name="error-code-800"></a>오류 코드: 800

- **오류 설명입니다.** 시도한 VPN 터널이 실패 하 여 원격 연결이 설정 되지 않았습니다. VPN 서버에 연결할 수 없습니다. 이 연결에서 L2TP/IPsec 터널을 사용 하려고 하는 경우 IPsec 협상에 필요한 보안 매개 변수가 제대로 구성 되지 않을 수 있습니다.

- **가능한 원인입니다.** 이 오류는 VPN 터널 유형이 **자동** 이 고 모든 vpn 터널에 대해 연결 시도가 실패 하는 경우에 발생 합니다.

- **가능한 해결 방법:**

    - 배포에 사용할 터널을 알고 있는 경우 vpn 클라이언트 쪽에서 VPN의 종류를 특정 터널 유형으로 설정 합니다.

    - 특정 터널 유형을 사용 하 여 VPN 연결을 설정 하면 연결이 여전히 실패 하지만 더 높은 터널 관련 오류 (예: "PPTP에 대해 차단 된 GRE")가 생성 됩니다.

    - 이 오류는 VPN 서버에 연결할 수 없거나 터널 연결에 실패 한 경우에도 발생 합니다.

- **확실히 하세요:**

    - IKE 포트 (UDP 포트 500 및 4500)가 차단 되지 않습니다.

    - IKE에 대 한 올바른 인증서는 클라이언트와 서버 모두에 표시 됩니다.

### <a name="error-code-809"></a>오류 코드: 809

- **오류 설명입니다.**  원격 서버가 응답 하지 않아 컴퓨터와 VPN 서버 간의 네트워크 연결을 설정할 수 없습니다. 컴퓨터와 원격 서버 간의 네트워크 장치 (예: 방화벽, NAT, 라우터) 중 하나가 VPN 연결을 허용 하도록 구성 되어 있지 않기 때문일 수 있습니다. 관리자 또는 서비스 공급자에 게 문의 하 여 문제를 일으킬 수 있는 장치를 확인 하세요.

- **가능한 원인입니다.** 이 오류는 VPN 서버 또는 방화벽에서 차단 된 UDP 500 또는 4500 포트에 의해 발생 합니다.

- **가능한 해결 방법입니다.** UDP 포트 500 및 4500이 클라이언트와 RRAS 서버 간의 모든 방화벽을 통해 허용 되는지 확인 합니다.

### <a name="error-code-812"></a>오류 코드: 812

- **오류 설명입니다.** Always On VPN에 연결할 수 없습니다. RAS/VPN 서버에 구성 된 정책 때문에 연결 하지 못했습니다. 특히 사용자 이름 및 암호를 확인 하는 데 사용 되는 서버 인증 방법이 연결 프로필에 구성 된 인증 방법과 일치 하지 않을 수 있습니다. RAS 서버의 관리자에 게 문의 하 여이 오류를 알려 주세요.

- **가능한 원인:**

    - 이 오류의 일반적인 원인은 NPS가 클라이언트에서 충족 하지 못하는 인증 조건을 지정 했기 때문입니다. 예를 들어 NPS는 PEAP 연결을 보호 하기 위해 인증서를 사용 하도록 지정할 수 있지만, 클라이언트는 Eap-mschapv2를 사용 하려고 합니다.

    - RRAS 기반 VPN 서버 인증 프로토콜 설정이 VPN 클라이언트 컴퓨터의 설정과 일치 하지 않는 경우 이벤트 로그 20276이 이벤트 뷰어에 기록 됩니다.

- **가능한 해결 방법입니다.** 클라이언트 구성이 NPS 서버에 지정 된 조건과 일치 하는지 확인 합니다.

### <a name="error-code-13806"></a>오류 코드: 13806

- **오류 설명입니다.** IKE에서 유효한 컴퓨터 인증서를 찾지 못했습니다. 적절 한 인증서 저장소에 유효한 인증서를 설치 하는 방법에 대 한 자세한 내용은 네트워크 보안 관리자에 게 문의 하세요.

- **가능한 원인입니다.** 이 오류는 일반적으로 VPN 서버에 컴퓨터 인증서 또는 루트 컴퓨터 인증서가 없는 경우에 발생 합니다.

- **가능한 해결 방법입니다.** 이 배포에 설명 된 인증서가 클라이언트 컴퓨터와 VPN 서버 모두에 설치 되어 있는지 확인 합니다.

### <a name="error-code-13801"></a>오류 코드: 13801

- **오류 설명입니다.** IKE 인증 자격 증명은 허용 되지 않습니다.

- **가능한 원인입니다.** 이 오류는 일반적으로 다음과 같은 경우에 발생 합니다.

    - RAS 서버에서 IKEv2 유효성 검사에 사용 되는 컴퓨터 인증서의 **확장 된 키 사용**에서 **서버 인증** 을 사용 하지 않습니다.

    - RAS 서버의 컴퓨터 인증서가 만료 되었습니다.

    - RAS 서버 인증서의 유효성을 검사 하기 위한 루트 인증서가 클라이언트 컴퓨터에 없습니다.

    - 클라이언트 컴퓨터에서 사용 되는 VPN 서버 이름이 서버 인증서의 **subjectName** 일치 하지 않습니다.

- **가능한 해결 방법입니다.** 서버 인증서의 **확장 된 키 사용**에서 **서버 인증** 을 포함 하는지 확인 합니다. 서버 인증서가 여전히 유효한 지 확인 합니다. 사용 된 CA가 RRAS 서버에서 **신뢰할 수 있는 루트 인증 기관** 아래에 나열 되는지 확인 합니다. Vpn 클라이언트가 vpn 서버의 인증서에 표시 된 대로 vpn 서버의 FQDN을 사용 하 여 연결 하는지 확인 합니다.

### <a name="error-code-0x80070040"></a>오류 코드: 0x80070040

- **오류 설명입니다.** 서버 인증서는 인증서 사용 항목 중 하나로 **서버 인증** 을 사용 하지 않습니다.

- **가능한 원인입니다.** 이 오류는 RAS 서버에 서버 인증 인증서가 설치 되어 있지 않은 경우에 발생할 수 있습니다.

- **가능한 해결 방법입니다.** RAS 서버에서 **IKEv2** 에 사용 하는 컴퓨터 인증서가 인증서 사용 항목 중 하나로 **서버 인증** 을 사용 하는지 확인 합니다.

### <a name="error-code-0x800b0109"></a>오류 코드: 0x800B0109

일반적으로 VPN 클라이언트 컴퓨터는 Active Directory 기반 도메인에 연결 됩니다. 도메인 자격 증명을 사용 하 여 VPN 서버에 로그온 하는 경우 인증서는 신뢰할 수 있는 루트 인증 기관 저장소에 자동으로 설치 됩니다. 그러나 컴퓨터가 도메인에 가입 되어 있지 않거나 대체 인증서 체인을 사용 하는 경우이 문제가 발생할 수 있습니다.

- **오류 설명입니다.** 인증서 체인이 처리 되었지만 트러스트 공급자가 신뢰 하지 않는 루트 인증서에서 종료 되었습니다.

- **가능한 원인입니다.** 이 오류는 해당 하는 신뢰할 수 있는 루트 CA 인증서가 클라이언트 컴퓨터의 신뢰할 수 있는 루트 인증 기관 저장소에 설치 되어 있지 않은 경우에 발생할 수 있습니다.

- **가능한 해결 방법입니다.** 루트 인증서가 클라이언트 컴퓨터의 신뢰할 수 있는 루트 인증 기관 저장소에 설치 되어 있는지 확인 합니다.

## <a name="logs"></a>로그

### <a name="application-logs"></a>응용 프로그램 로그

클라이언트 컴퓨터의 응용 프로그램 로그는 VPN 연결 이벤트에 대 한 높은 수준의 세부 정보를 기록 합니다.

원본 RasClient에서 이벤트를 찾습니다. 모든 오류 메시지는 메시지의 끝에 오류 코드를 반환 합니다. 보다 일반적인 오류 코드 중 일부는 아래에 자세히 설명 되어 있지만 [라우팅 및 원격 액세스 오류 코드](https://msdn.microsoft.com/library/windows/desktop/bb530704.aspx)에서 전체 목록을 사용할 수 있습니다.

## <a name="nps-logs"></a>NPS 로그

Nps가 NPS 계정 로그를 만들어 저장 합니다. 기본적으로이 파일은*xxxx*.txt에 명명 된 파일에\\% SYSTEMROOT%\\System32\\Logfiles에 저장 됩니다. 여기서 *xxxx* 는 파일이 만들어진 날짜입니다.

기본적으로 이러한 로그는 쉼표로 구분 된 값 형식 이지만 제목 행은 포함 되지 않습니다. 제목 행은 다음과 같습니다.

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

이 머리글 행을 로그 파일의 첫 번째 줄로 붙여 넣은 후 파일을 Microsoft Excel로 가져오면 열에 레이블이 올바르게 지정 됩니다.

NPS 로그는 정책 관련 문제를 진단 하는 데 유용할 수 있습니다. NPS 로그에 대 한 자세한 내용은 [Nps 데이터베이스 형식 로그 파일 해석](https://technet.microsoft.com/library/cc771748.aspx)을 참조 하세요.

## <a name="vpn_profileps1-script-issues"></a>VPN_Profile. p s 1 스크립트 문제

VPN_ Profile. p s 1을 수동으로 실행 하는 경우 가장 일반적인 문제는 다음과 같습니다.

- 원격 연결 도구를 사용 하나요?  사용자 로그인 검색 시 RDP 또는 다른 원격 연결 방법을 사용 하지 않도록 합니다.

- 사용자가 해당 로컬 컴퓨터의 관리자 인가요?  VPN_Profile. p s 1을 실행 하는 동안 사용자에 게 관리자 권한이 있는지 확인 합니다.

- 추가 PowerShell 보안 기능이 사용 하도록 설정 되어 있나요? PowerShell 실행 정책에서 스크립트를 차단 하지 않는지 확인 합니다. 설정 된 경우 스크립트를 실행 하기 전에 제한 된 언어 모드를 해제 하는 것을 고려할 수 있습니다. 스크립트가 성공적으로 완료 된 후 제한 된 언어 모드를 활성화할 수 있습니다.

## <a name="always-on-vpn-client-connection-issues"></a>Always On VPN 클라이언트 연결 문제

잘못 된 구성으로 인해 클라이언트 연결이 실패 하 고 원인을 찾기가 어려울 수 있습니다.  Always On VPN 클라이언트는 연결을 설정 하기 전에 몇 가지 단계를 거칩니다. 클라이언트 연결 문제를 해결 하는 경우 다음을 제거 하는 과정을 진행 합니다.

1. 템플릿 컴퓨터가 외부적으로 연결 되어 있나요? **Whatismyip** 검색에는 사용자에 게 속하지 않는 공용 IP 주소가 표시 되어야 합니다.

2. IP 주소에 대 한 원격 액세스/v m 서버 이름을 확인할 수 있나요? **제어판** 에서 **네트워크** 및 **인터넷** > **네트워크 연결** > VPN 프로필에 대 한 속성을 엽니다. **일반** 탭의 값은 DNS를 통해 공개적으로 확인할 수 있어야 합니다.

3. 외부 네트워크에서 VPN 서버에 액세스할 수 있나요? 외부 인터페이스에 대 한 ICMP (Internet Control Message Protocol)를 열고 원격 클라이언트에서 이름을 ping 하는 것이 좋습니다. Ping이 성공적으로 완료 되 면 ICMP 허용 규칙을 제거할 수 있습니다.

4. VPN 서버에서 내부 및 외부 Nic가 올바르게 구성 되어 있습니까? 다른 서브넷에 있나요? 외부 NIC가 방화벽의 올바른 인터페이스에 연결 되나요?

5. UDP 500 및 4500 포트가 클라이언트에서 VPN 서버의 외부 인터페이스로 열려 있나요? 클라이언트 방화벽, 서버 방화벽 및 하드웨어 방화벽을 확인 합니다. IPSEC은 UDP 포트 500를 사용 하므로 IPEC를 사용 하지 않도록 설정 하거나 차단 하지 않았는지 확인 합니다.

6. 인증서 유효성 검사에 실패 하나요? NPS 서버에 IKE 요청을 처리 하는 서버 인증 인증서가 있는지 확인 합니다. NPS 클라이언트로 지정 된 올바른 VPN 서버 IP가 있는지 확인 합니다. PEAP를 사용 하 여 인증 하 고 있으며 보호 된 EAP 속성은 인증서 인증만 허용 해야 합니다. NPS 이벤트 로그에서 인증 실패를 확인할 수 있습니다. 자세한 내용은 [NPS 서버 설치 및 구성](vpn-deploy-nps.md) 을 참조 하세요.

7. 연결 하 고 인터넷/로컬 네트워크에 액세스할 수 없습니까? DHCP/VPN 서버 IP 풀에서 구성 문제를 확인 합니다.

8. 연결 하 고 있고 유효한 내부 IP가 있지만 로컬 리소스에 대 한 액세스 권한이 없는 경우  클라이언트에서 이러한 리소스를 가져오는 방법을 알고 있는지 확인 합니다. VPN 서버를 사용 하 여 요청을 라우팅할 수 있습니다.

## <a name="azure-ad-conditional-access-connection-issues"></a>Azure AD 조건부 액세스 연결 문제

### <a name="oops---you-cant-get-to-this-yet"></a>죄송 합니다 .이를 아직 가져올 수 없습니다.

- **오류 설명입니다.** 조건부 액세스 정책이 충족 되지 않으면 VPN 연결을 차단 하지만 사용자가 **X** 를 선택 하 여 메시지를 닫은 후 연결 합니다.  **[확인]** 을 선택 하면 다른 인증 시도를 발생 시킵니다. 다른 인증 시도는 다른 "메시지"로 끝납니다. 이러한 이벤트는 클라이언트의 AAD 작업 이벤트 로그에 기록 됩니다.

- **가능한 원인**

  - 사용자에 게 Azure AD에서 발급 하지 않은 유효한 클라이언트 인증 인증서가 개인 인증서 저장소에 있습니다.

  - VPN 프로필 \<TLSExtensions\> 섹션이 없거나 **\<EKUName\>Aad 조건부 액세스\</EKUName\>\<EKUOID\>1.3.6.1.4.1.311.87 </EKUOID\>\<EKUName > AAD 조건부 액세스 </EKUName\>\<EKUOID\>1.3.6.1.4.1.311.87 </EKUOID\>** 항목을 포함 하지 않습니다. \<EKUName > 및 \<EKUOID > 항목은 vpn 클라이언트에 게 인증서를 VPN 서버에 전달할 때 사용자의 인증서 저장소에서 검색할 인증서를 알려 줍니다. 이를 사용 하지 않으면 VPN 클라이언트는 사용자의 인증서 저장소에 있는 유효한 클라이언트 인증 인증서를 사용 하 고 인증에 성공 합니다. 

  - RADIUS 서버 (NPS)가 **AAD 조건부 액세스** OID를 포함 하는 클라이언트 인증서만 허용 하도록 구성 되지 않았습니다.

- **가능한 해결 방법입니다.** 이 루프를 이스케이프 하려면 다음을 수행 합니다.

  1. Windows PowerShell에서 **get-wmiobject** cmdlet을 실행 하 여 VPN 프로필 구성을 덤프 합니다. 
  2. **\<TLSExtensions >** , **\<EKUName >** 및 **\<EKUOID >** 섹션이 있는지 확인 하 고 올바른 이름과 OID를 표시 합니다.
      
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

  3. 사용자의 인증서 저장소에 유효한 인증서가 있는지 확인 하려면 **Certutil** 명령을 실행 합니다.

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
     >발급자 **CN = MICROSOFT VPN ROOT CA gen 1** 의 인증서가 사용자의 개인 저장소에 있지만 사용자가 액세스 권한을 얻은 경우에는 사용자가 **X** 를 선택 하 여 해당 메시지를 닫고, CAPI2 이벤트 로그를 수집 하 여 인증에 사용 된 인증서가 Microsoft VPN 루트 CA에서 발급 되지 않은 유효한 클라이언트 인증 인증서 인지 확인 합니다.

  4. 사용자의 개인 저장소에 유효한 클라이언트 인증 인증서가 있는 경우 사용자가 **X** 를 선택 하 고 **\<TLSExtensions >** , **\<EKUName >** 및 **\<EKUOID >** 섹션이 존재 하 고 올바른 정보를 포함 하는 경우 연결이 실패 합니다.
   
     "확장 가능한 인증 프로토콜에서 사용할 수 있는 인증서를 찾을 수 없습니다." 라는 오류 메시지가 나타납니다.

### <a name="unable-to-delete-the-certificate-from-the-vpn-connectivity-blade"></a>VPN 연결 블레이드에서 인증서를 삭제할 수 없습니다.

- **오류 설명입니다.** VPN 연결 블레이드에서 인증서를 삭제할 수 없습니다.

- **가능한 원인입니다.** 인증서가 **기본**으로 설정 되어 있습니다.

- **가능한 해결 방법입니다.**

    1. VPN 연결 블레이드에서 인증서를 선택 합니다.
    2. **주**아래에서 **아니요**를 선택 하 고 **저장**을 선택 합니다.
    3. VPN 연결 블레이드에서 인증서를 다시 선택 합니다.
    4. **삭제**를 선택 합니다.
