---
title: Windows 10 클라이언트 Always On VPN 연결 구성
description: 이 단계에서는 프로 파일링 옵션 및 스키마에 대해 알아보고 VPN 연결을 사용 하 여 해당 인프라와 통신 하도록 Windows 10 클라이언트 컴퓨터를 구성 합니다.
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 05/29/2018
ms.assetid: d165822d-b65c-40a2-b440-af495ad22f42
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.reviewer: deverette
ms.openlocfilehash: c853926157a4efa414c56d97affa0a1d2faad629
ms.sourcegitcommit: 1bc3c229e9688ac741838005ec4b88e8f9533e8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68314354"
---
# <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>6단계. Windows 10 클라이언트 Always On VPN 연결 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**선행** 5단계. DNS 및 방화벽 설정 구성](vpn-deploy-dns-firewall.md)<br>
- [**그런** 7단계. 필드 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스](../../ad-ca-vpn-connectivity-windows10.md)

이 단계에서는 프로 파일링 옵션 및 스키마에 대해 알아보고 VPN 연결을 사용 하 여 해당 인프라와 통신 하도록 Windows 10 클라이언트 컴퓨터를 구성 합니다.

PowerShell, SCCM 또는 Intune을 통해 Always On VPN 클라이언트를 구성할 수 있습니다. 세 가지 모두 적절 한 VPN 설정을 구성 하려면 XML VPN 프로필이 필요 합니다. SCCM 또는 Intune을 사용 하지 않는 조직에 대 한 PowerShell 등록을 자동화할 수 있습니다.

>[!NOTE]
>그룹 정책에는 Windows 10 원격 액세스 Always On VPN 클라이언트를 구성 하는 관리 템플릿이 포함 되어 있지 않습니다.  그러나 로그온 스크립트를 사용할 수 있습니다.

## <a name="profilexml-overview"></a>프로 파일링 개요

ProfileXML은 VPNv2 CSP 내의 URI 노드입니다. 각 VPNv2 CSP 노드를 개별적으로 구성 하는 대신 (예: 트리거, 경로 목록 및 인증 프로토콜)이 노드를 사용 하 여 단일 CSP 노드에 단일 XML 블록으로 모든 설정을 제공 하 여 Windows 10 VPN 클라이언트를 구성 합니다. 프로 파일링 스키마는 VPNv2 CSP 노드의 스키마와 거의 동일 하지만 일부 용어는 약간 다릅니다.

이 배포에서 설명 하는 Windows PowerShell, System Center Configuration Manager 및 Intune을 비롯 한 모든 배달 방법에서 프로 파일링을 사용 합니다. 다음 두 가지 방법으로이 배포에서 ProfileXML VPNv2 CSP 노드를 구성할 수 있습니다.

- **OMA-URI**. 한 가지 방법은 [VPNV2 CSP 노드](../always-on-vpn-technology-overview.md#vpnv2-csp-nodes)섹션의 앞부분에서 설명한 대로 oma-uri를 사용 하 여 MDM 공급자를 사용 하는 것입니다. 이 방법을 사용 하 여 Intune을 사용 하는 경우 프로 파일링 구성 XML 태그를 프로 파일링 된 CSP 노드에 쉽게 삽입할 수 있습니다.

- **WMI(Windows Management Instrumentation) (WMI)-CSP 브리지**입니다. 프로 파일링 MDM_VPNv2_01 CSP 노드를 구성 하는 두 번째 방법은 VPNv2 CSP 및 프로 파일링 노드에 액세스할 수 있는 WMI-CSP 브리지 ( 이라는 wmi 클래스)를 사용 하는 것입니다. 해당 WMI 클래스의 새 인스턴스를 만들 때 WMI는 CSP를 사용 하 여 Windows PowerShell 및 System Center Configuration Manager을 사용할 때 VPN 프로필을 만듭니다.

이러한 구성 방법이 서로 다른 경우에도 둘 다 올바른 형식의 XML VPN 프로필을 요구 합니다. 프로 파일링 VPNv2 CSP 설정을 사용 하려면 기본 배포 시나리오에 필요한 태그를 구성 하는 ProfileXML 스키마를 사용 하 여 XML을 생성 합니다. 자세한 내용은 [Profilexml XSD](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-profile-xsd)를 참조 하세요.

아래에서 필요한 각 설정 및 해당 ProfileXML 태그를 찾습니다. 프로 파일링 스키마 내에서 특정 태그의 각 설정을 구성 하 고, 일부는 네이티브 프로필 아래에서 찾을 수 없습니다. 추가 태그 배치는 ProfileXML 스키마를 참조 하세요.

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

**연결 형식:** 기본 IKEv2

프로 파일링 요소:

```xml
<NativeProtocolType>IKEv2</NativeProtocolType>
```

**라우팅이** 분할 터널링

프로 파일링 요소:

```xml
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
```

**이름 확인:** 도메인 이름 정보 목록 및 DNS 접미사

프로 파일링 요소:

```xml
<DomainNameInformation>
<DomainName>.corp.contoso.com</DomainName>
<DnsServers>10.10.1.10,10.10.1.50</DnsServers>
</DomainNameInformation>

<DnsSuffix>corp.contoso.com</DnsSuffix>
```

**트리거** Always On 및 신뢰할 수 있는 네트워크 검색

프로 파일링 요소:

```xml
<AlwaysOn>true</AlwaysOn>
<TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

**인증은** PEAP-TPM으로 보호 된 사용자 인증서를 사용 하는 TLS

프로 파일링 요소:

```xml
<Authentication>
<UserMethod>Eap</UserMethod>
<Eap>
<Configuration>...</Configuration>
</Eap>
</Authentication>
```

간단한 태그를 사용 하 여 일부 VPN 인증 메커니즘을 구성할 수 있습니다. 그러나 EAP와 PEAP는 더 관련 됩니다. XML 태그를 만드는 가장 쉬운 방법은 EAP 설정을 사용 하 여 VPN 클라이언트를 구성한 다음 해당 구성을 XML로 내보내는 것입니다.

EAP 설정에 대 한 자세한 내용은 [eap 구성](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/eap-configuration)을 참조 하세요.

## <a name="manually-create-a-template-connection-profile"></a>수동으로 템플릿 연결 프로필 만들기

이 단계에서는 PEAP (Protected Extensible Authentication Protocol)를 사용 하 여 클라이언트와 서버 간의 통신을 보호 합니다. 간단한 사용자 이름 및 암호와 달리이 연결을 사용 하려면 VPN 프로필에 고유한 EAPConfiguration 섹션이 있어야 합니다.

XML 태그를 처음부터 만드는 방법을 설명 하는 대신 Windows의 설정을 사용 하 여 템플릿 VPN 프로필을 만듭니다. 템플릿 VPN 프로필을 만든 후에는 Windows PowerShell을 사용 하 여 해당 템플릿의 EAPConfiguration 부분을 사용 하 여 배포에서 나중에 배포 하는 최종 ProfileXML을 만듭니다.

### <a name="record-nps-certificate-settings"></a>NPS 인증서 설정 기록

템플릿을 만들기 전에 서버 인증서에서 NPS 서버의 호스트 이름 또는 FQDN (정규화 된 도메인 이름) 및 인증서를 발급 한 CA의 이름을 적어둡니다.

**여기서**

1. NPS 서버에서 네트워크 정책 서버를 엽니다.

2. NPS 콘솔의 정책 아래에서 **네트워크 정책**을 클릭 합니다.

3. **VPN (가상 사설망) 연결**을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.

4. **제약 조건** 탭을 클릭 하 고 **인증 방법**을 클릭 합니다.

5. EAP 종류에서 Microsoft를 **클릭 합니다. PEAP (보호 된 EAP**)를 클릭 하 고 **편집**을 클릭 합니다.

6. 및 **발급자** **에 발급 된 인증서** 의 값을 기록 합니다.

    예정 된 VPN 템플릿 구성에서 다음 값을 사용 합니다. 예를 들어 서버의 FQDN이 nps01.corp.contoso.com이 고 호스트 이름이 NPS01.XML 인 경우 인증서 이름은 서버의 FQDN 또는 DNS 이름 (예: nps01.corp.contoso.com)을 기반으로 합니다.

7. 보호 된 EAP 속성 편집 대화 상자를 취소 합니다.

8. VPN (가상 사설망) 연결 속성 대화 상자를 취소 합니다.

9. 네트워크 정책 서버를 닫습니다.

>[!NOTE]
>여러 NPS 서버가 있는 경우 각 서버에서 이러한 단계를 완료 하 여 VPN 프로필이 각 서버를 사용 해야 하는지 확인할 수 있도록 합니다.

### <a name="configure-the-template-vpn-profile-on-a-domain-joined-client-computer"></a>도메인에 가입 된 클라이언트 컴퓨터에서 템플릿 VPN 프로필 구성

이제 도메인에 가입 된 클라이언트 컴퓨터에서 템플릿 VPN 프로필을 구성 하는 데 필요한 정보가 있습니다. 프로세스의이 부분에 사용 하는 사용자 계정 유형 (즉, 표준 사용자 또는 관리자)은 중요 하지 않습니다.

그러나 인증서 자동 등록을 구성한 후 컴퓨터를 다시 시작 하지 않은 경우에는 사용 가능한 인증서가 등록 되도록 템플릿 VPN 연결을 구성 하기 전에이 작업을 수행 합니다.

>[!NOTE]
>VPN의 고급 속성 (예: NRPT 규칙, Always On, 신뢰할 수 있는 네트워크 검색 등)을 수동으로 추가할 수 있는 방법은 없습니다. 다음 단계에서는 vpn 서버의 구성을 확인 하 고 서버에 대 한 VPN 연결을 설정할 수 있는 테스트 VPN 연결을 만듭니다.

**단일 테스트 VPN 연결 수동 만들기**

1.  도메인에 가입 된 클라이언트 컴퓨터에 **VPN 사용자** 그룹의 구성원으로 로그인 합니다.

2.  시작 메뉴에서 **VPN**을 입력 하 고 enter 키를 누릅니다.

3.  세부 정보 창에서 **VPN 연결 추가**를 클릭 합니다.

4.  VPN 공급자 목록에서 **Windows (기본 제공)** 를 클릭 합니다.

5.  연결 이름에 **Template**을 입력 합니다.

6.  서버 이름 또는 주소에 VPN 서버의 **외부** FQDN (예: **vpn.contoso.com**)을 입력 합니다.

7.  **저장**을 클릭합니다.

8.  관련 설정에서 **어댑터 옵션 변경**을 클릭 합니다.

9.  **템플릿**을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.

10. **보안** 탭의 **VPN 유형**에서 **IKEv2**를 클릭 합니다.

11. 데이터 암호화에서 **최대 강도 암호화**를 클릭 합니다.

12. **EAP (확장할 수 있는 인증 프로토콜) 사용을**클릭 합니다. 그런 다음 **EAP (확장할 수 있는 인증 프로토콜) 사용**에서 **Microsoft를 클릭 합니다. PEAP (보호 된 EAP) (암호화 사용**).

13. **속성** 을 클릭 하 여 보호 된 EAP 속성 대화 상자를 열고 다음 단계를 완료 합니다.

    a. **다음 서버에 연결** 상자에이 섹션의 앞부분에 있는 nps 서버 인증 설정에서 검색 한 nps 서버의 이름 (예: nps01.xml)을 입력 합니다.

    >[!NOTE]
    >입력 하는 서버 이름은 인증서의 이름과 일치 해야 합니다. 이 이름은이 섹션의 앞부분에서 복구 했습니다. 이름이 일치 하지 않으면 연결이 실패 하 고 "RAS/VPN 서버에 구성 된 정책으로 인해 연결이 차단 되었습니다." 라는 메시지가 표시 됩니다.

    b.  신뢰할 수 있는 루트 인증 기관에서 NPS 서버의 인증서 (예: contoso-CA)를 발급 한 루트 CA를 선택 합니다.

    c.  연결 하기 전에 알림에서 **사용자에 게 새 서버 또는 신뢰할 수 있는 ca에 대 한 권한을 부여 하지 않음**을 클릭 합니다.

    d.  인증 방법 선택에서 **스마트 카드 또는 기타 인증서**를 클릭 하 고 **구성**을 클릭 합니다. 스마트 카드 또는 기타 인증서 속성 대화 상자가 열립니다.

    e.  **이 컴퓨터에서 인증서 사용**을 클릭 합니다.

    f.  다음 서버에 연결 상자에 이전 단계에서 NPS 서버 인증 설정에서 검색 한 NPS 서버의 이름을 입력 합니다.

    g.  신뢰할 수 있는 루트 인증 기관에서 NPS 서버 인증서를 발급 한 루트 CA를 선택 합니다.

    h.  **새 서버 또는 신뢰할 수 있는 인증 기관에 권한을 부여 하 라는 메시지를 표시 하지 않습니다** . 확인란을 선택 합니다.

    i.  **확인** 을 클릭 하 여 스마트 카드 또는 기타 인증서 속성 대화 상자를 닫습니다.

    j.  **확인** 을 클릭 하 여 보호 된 EAP 속성 대화 상자를 닫습니다.

14. **확인** 을 클릭 하 여 템플릿 속성 대화 상자를 닫습니다.

15. 네트워크 연결 창을 닫습니다.

16. 설정에서 **템플릿**을 클릭 하 고 **연결**을 클릭 하 여 VPN을 테스트 합니다.

>[!IMPORTANT]
>VPN 서버에 대 한 템플릿 VPN 연결이 성공적인 지 확인 합니다. 이렇게 하면 다음 예제에서 사용 하기 전에 EAP 설정이 올바른지 확인 합니다. 계속 하려면 한 번 이상 연결 해야 합니다. 그렇지 않으면 프로필은 VPN에 연결 하는 데 필요한 모든 정보를 포함 하지 않습니다.

## <a name="create-the-profilexml-configuration-files"></a>ProfileXML 구성 파일 만들기

이 섹션을 완료 하기 전에 섹션에서 [수동으로 템플릿 연결 프로필 만들기](#manually-create-a-template-connection-profile) 에 설명 된 템플릿 VPN 연결을 만들고 테스트 했는지 확인 합니다. Vpn 연결 테스트는 프로필에 VPN에 연결 하는 데 필요한 모든 정보가 포함 되어 있는지 확인 하는 데 필요 합니다.

1을 나열 하는 Windows PowerShell 스크립트는 바탕 화면에 두 파일을 만듭니다. 둘 다 이전에 만든 템플릿 연결 프로필을 기반으로 하는 **Eapconfiguration** 태그를 포함 합니다.

- **VPN_Profile.** 이 파일에는 VPNv2 CSP에서 ProfileXML 노드를 구성 하는 데 필요한 XML 태그가 포함 되어 있습니다. Intune과 같은 OMA-URI 호환 MDM 서비스에서이 파일을 사용 합니다.

- **VPN_Profile.** 이 파일은 클라이언트 컴퓨터에서 실행할 수 있는 Windows PowerShell 스크립트로, VPNv2 CSP에서 ProfileXML 노드를 구성 합니다. System Center Configuration Manager를 통해이 스크립트를 배포 하 여 CSP를 구성할 수도 있습니다. Hyper-v 고급 세션을 포함 하 여 원격 데스크톱 세션에서이 스크립트를 실행할 수 없습니다.

>[!IMPORTANT]
>아래 예제 명령에는 Windows 10 빌드 1607 이상이 필요 합니다.

**VPN_Profile 및 VPN_Proflie를 만듭니다.**

1. 설명 된 [템플릿 연결 프로필을 수동으로 만드는](#manually-create-a-template-connection-profile) 것과 동일한 사용자 계정으로 템플릿 VPN 프로필을 포함 하는 도메인에 가입 된 클라이언트 컴퓨터에 로그인 합니다.

2. 목록 1을 Windows PowerShell ISE (통합 스크립팅 환경)에 붙여 넣고 주석에 설명 된 매개 변수를 사용자 지정 합니다. $Template, $ProfileName, $Servers, $DnsSuffix, $DomainName, $TrustedNetwork, $DNSServers입니다. 설명에는 각 설정에 대 한 자세한 설명이 나와 있습니다.

3. 스크립트를 실행 하 여 바탕 화면에 **VPN_Profile** 및 **VPN_Profile** 을 생성 합니다.

#### <a name="listing-1-understanding-makeprofileps1"></a>나열 1. MakeProfile 이해. ps1

이 섹션에서는 VPNv2 CSP에서 프로 파일링을 구성 하기 위해 특히 VPN 프로필을 만드는 방법을 이해 하는 데 사용할 수 있는 예제 코드에 대해 설명 합니다.

이 예제 코드에서 스크립트를 조합 하 고 스크립트를 실행 한 후 스크립트는 다음 두 파일을 생성 합니다. VPN_Profile 및 VPN_Profile. VPN_Profile를 사용 하 여 Microsoft Intune와 같은 OMA DM 규격 MDM 서비스에서 ProfileXML을 구성 합니다.

Windows PowerShell 또는 System Center Configuration Manager에서 **VPN_Profile** 스크립트를 사용 하 여 windows 10 Desktop에서 프로 파일링을 구성 합니다.

>[!NOTE]
>전체 예제 스크립트를 보려면 [Makeprofile. Ps1 전체 스크립트](#makeprofileps1-full-script)섹션을 참조 하세요.

#### <a name="parameters"></a>매개 변수

다음 매개 변수를 구성 합니다.

**$Template**. EAP 구성을 검색할 템플릿의 이름입니다.

**$ProfileName**. 프로필에 대 한 고유한 영숫자 식별자입니다. 프로필 이름에는 슬래시 (/)를 포함 하지 않아야 합니다. 프로필 이름에 공백이 나 영숫자가 아닌 문자가 있으면 URL 인코딩 표준에 따라 올바르게 이스케이프 되어야 합니다.

**$Servers**. VPN gateway에 대 한 공용 또는 라우팅 가능한 IP 주소 또는 DNS 이름입니다. 게이트웨이 또는 서버 팜에 대 한 가상 IP의 외부 IP를 가리킬 수 있습니다. 예, 208.147.66.130 또는 vpn.contoso.com.

**$DnsSuffix**. 쉼표로 구분 된 DNS 접미사를 하나 이상 지정 합니다. 목록의 첫 번째는 VPN 인터페이스에 대 한 기본 연결별 DNS 접미사로도 사용 됩니다. 전체 목록은 SuffixSearchList에도 추가 됩니다.

**$DomainName**. 정책이 적용 되는 네임 스페이스를 나타내는 데 사용 됩니다. 이름 쿼리가 실행 되 면 DNS 클라이언트는 쿼리의 이름을 DomainNameInformationList 아래의 모든 네임 스페이스와 비교 하 여 일치 하는 항목을 찾습니다. 이 매개 변수는 다음 형식 중 하나일 수 있습니다.

- FQDN-정규화 된 도메인 이름
- Suffix-DNS 확인을 위해 짧은 이름 쿼리에 추가 되는 도메인 접미사입니다. 접미사를 지정 하려면 DNS 접미사 앞에 마침표 (.)를 추가 합니다.

**$DNSServers**. 네임 스페이스에 사용할 쉼표로 구분 된 DNS 서버 IP 주소 목록입니다.

**$TrustedNetwork**. 신뢰할 수 있는 네트워크를 식별 하는 쉼표로 구분 된 문자열입니다. 사용자가 보호 된 리소스를 장치에 직접 액세스할 수 있는 회사 무선 네트워크에 있는 경우 VPN이 자동으로 연결 되지 않습니다.

아래 명령에 사용 되는 매개 변수에 대 한 예제 값은 다음과 같습니다. 사용자 환경에 맞게 이러한 값을 변경 해야 합니다.

```xml
$TemplateName = 'Template'
$ProfileName = 'Contoso AlwaysOn VPN'
$Servers = 'vpn.contoso.com'
$DnsSuffix = 'corp.contoso.com'
$DomainName = '.corp.contoso.com'
$DNSServers = '10.10.0.2,10.10.0.3'
$TrustedNetwork = 'corp.contoso.com'
```

### <a name="prepare-and-create-the-profile-xml"></a>프로필 XML 준비 및 만들기

다음 예제 명령은 템플릿 프로필에서 EAP 설정을 가져옵니다.

```xml
$Connection = Get-VpnConnection -Name $TemplateName
if(!$Connection)
{
$Message = "Unable to get $TemplateName connection profile: $_"
Write-Host "$Message"
exit
}
$EAPSettings= $Connection.EapConfigXmlStream.InnerXml
```

### <a name="create-the-profile-xml"></a>프로필 XML 만들기

[!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]

```xml
$ProfileXML =
'<VPNProfile>
  <DnsSuffix>' + $DnsSuffix + '</DnsSuffix>
  <NativeProfile>
<Servers>' + $Servers + '</Servers>
<NativeProtocolType>IKEv2</NativeProtocolType>
<Authentication>
  <UserMethod>Eap</UserMethod>
  <Eap>
    <Configuration>
  '+ $EAPSettings + '
    </Configuration>
  </Eap>
</Authentication>
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>
  </NativeProfile>
  <AlwaysOn>true</AlwaysOn>
  <RememberCredentials>true</RememberCredentials>
  <TrustedNetworkDetection>' + $TrustedNetwork + '</TrustedNetworkDetection>
  <DomainNameInformation>
<DomainName>' + $DomainName + '</DomainName>
<DnsServers>' + $DNSServers + '</DnsServers>
</DomainNameInformation>
</VPNProfile>'
```

### <a name="output-vpnprofilexml-for-intune"></a>Intune에 대 한 출력 VPN_Profile

다음 예제 명령을 사용 하 여 프로필 XML 파일을 저장할 수 있습니다.

```xml
$ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
```

### <a name="output-vpnprofileps1-for-the-desktop-and-system-center-configuration-manager"></a>바탕 화면 및 System Center Configuration Manager에 대 한 출력 VPN_Profile

다음 예제 코드에서는 VPNv2 CSP의 ProfileXML 노드를 사용 하 여 AlwaysOn IKEv2 VPN 연결을 구성 합니다.

Windows 10 desktop 또는 System Center Configuration Manager에서이 스크립트를 사용할 수 있습니다.

### <a name="define-key-vpn-profile-parameters"></a>키 VPN 프로필 매개 변수 정의

```xml
$Script = '$ProfileName = ''' + $ProfileName + ''''
$ProfileNameEscaped = $ProfileName -replace ' ', '%20'
```

## <a name="define-vpn-profilexml"></a>VPN 프로 파일링 정의

```xml
$ProfileXML = ''' + $ProfileXML + '''
```

### <a name="escape-special-characters-in-the-profile"></a>프로필에서 특수 문자를 이스케이프 합니다.

```xml
$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'
```

### <a name="define-wmi-to-csp-bridge-properties"></a>WMI-CSP 브리지 속성 정의

```xml
$nodeCSPURI = "./Vendor/MSFT/VPNv2"
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"
```

### <a name="determine-user-sid-for-vpn-profile"></a>VPN 프로필에 대 한 사용자 SID를 확인 합니다.

```xml
try
{
$username = Gwmi -Class Win32_ComputerSystem | select username
$objuser = New-Object System.Security.Principal.NTAccount($username.username)
$sid = $objuser.Translate([System.Security.Principal.SecurityIdentifier])
$SidValue = $sid.Value
$Message = "User SID is $SidValue."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to get user SID. User may be logged on over Remote Desktop: $_"
Write-Host "$Message"
exit
}
```

### <a name="define-wmi-session"></a>WMI 세션 정의:

```xml
$session = New-CimSession
$options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
$options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
```

### <a name="detect-and-delete-previous-vpn-profile"></a>이전 VPN 프로필 검색 및 삭제:

```xml
try
{
  $deleteInstances = $session.EnumerateInstances($namespaceName, $className, $options)
  foreach ($deleteInstance in $deleteInstances)
  {
    $InstanceId = $deleteInstance.InstanceID
    if ("$InstanceId" -eq "$ProfileNameEscaped")
    {
        $session.DeleteInstance($namespaceName, $deleteInstance, $options)
        $Message = "Removed $ProfileName profile $InstanceId"
        Write-Host "$Message"
    } else {
        $Message = "Ignoring existing VPN profile $InstanceId"
        Write-Host "$Message"
    }
  }
}
catch [Exception]
{
  $Message = "Unable to remove existing outdated instance(s) of $ProfileName profile: $_"
  Write-Host "$Message"
  exit
}
```

### <a name="create-the-vpn-profile"></a>VPN 프로필을 만듭니다.

```xml
try
{
  $newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", "String", "Key")
  $newInstance.CimInstanceProperties.Add($property)
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", "String", "Key")
  $newInstance.CimInstanceProperties.Add($property)
  $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", "String", "Property")
  $newInstance.CimInstanceProperties.Add($property)
  $session.CreateInstance($namespaceName, $newInstance, $options)
  $Message = "Created $ProfileName profile."


  Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}

$Message = "Script Complete"
Write-Host "$Message"
```

### <a name="save-the-profile-xml-file"></a>프로필 XML 파일 저장

```xml
$Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')

$Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
Write-Host "$Message"
```

## <a name="makeprofileps1-full-script"></a>MakeProfile. ps1 전체 스크립트

대부분의 예제에서는 Set-wmiinstance Windows PowerShell cmdlet을 사용 하 여 프로필을 MDM_VPNv2_01 WMI 클래스의 새 인스턴스에 삽입 합니다. 

그러나이 작업은 최종 사용자의 컨텍스트에서 패키지를 실행할 수 없기 때문에 System Center Configuration Manager에는 적용 되지 않습니다. 따라서이 스크립트는 CIM(Common Information Model)을 사용 하 여 사용자의 컨텍스트에서 WMI 세션을 만든 다음 해당 세션에 MDM_VPNv2_01 WMI 클래스의 새 인스턴스를 만듭니다. 이 WMI 클래스는 WMI-CSP 브리지를 사용 하 여 VPNv2 CSP를 구성 합니다. 따라서 클래스 인스턴스를 추가 하 여 CSP를 구성 합니다. 

>[!IMPORTANT]
>WMI-CSP 브리지를 사용 하려면 로컬 관리자 권한이 필요 합니다. 사용자별 VPN 프로필을 배포 하려면 SCCM 또는 MDM을 사용 해야 합니다.

>[!NOTE]
>VPN_Profile 스크립트는 현재 사용자의 SID를 사용 하 여 사용자의 컨텍스트를 식별 합니다. 원격 데스크톱 세션에는 사용할 수 있는 SID가 없으므로 스크립트가 원격 데스크톱 세션에서 작동 하지 않습니다. 마찬가지로 Hyper-v 고급 세션에서는 작동 하지 않습니다. 가상 컴퓨터에서 원격 액세스 Always On VPN을 테스트 하는 경우이 스크립트를 실행 하기 전에 클라이언트 Vm에서 고급 세션을 사용 하지 않도록 설정 합니다.

다음 예제 스크립트에는 이전 섹션의 모든 코드 예제가 포함 되어 있습니다. 예제 값을 사용자 환경에 적합 한 값으로 변경 해야 합니다.
    
   ```XML
    $TemplateName = 'Template'
    $ProfileName = 'Contoso AlwaysOn VPN'
    $Servers = 'vpn.contoso.com'
    $DnsSuffix = 'corp.contoso.com'
    $DomainName = '.corp.contoso.com'
    $DNSServers = '10.10.0.2,10.10.0.3'
    $TrustedNetwork = 'corp.contoso.com'

    
    $Connection = Get-VpnConnection -Name $TemplateName
    if(!$Connection)
    {
    $Message = "Unable to get $TemplateName connection profile: $_"
    Write-Host "$Message"
    exit
    }
    $EAPSettings= $Connection.EapConfigXmlStream.InnerXml
    
    $ProfileXML =
    '<VPNProfile>
      <DnsSuffix>' + $DnsSuffix + '</DnsSuffix>
      <NativeProfile>
    <Servers>' + $Servers + '</Servers>
    <NativeProtocolType>IKEv2</NativeProtocolType>
    <Authentication>
      <UserMethod>Eap</UserMethod>
      <Eap>
       <Configuration>
     '+ $EAPSettings + '
       </Configuration>
      </Eap>
    </Authentication>
    <RoutingPolicyType>SplitTunnel</RoutingPolicyType>
      </NativeProfile>
    <AlwaysOn>true</AlwaysOn>
    <RememberCredentials>true</RememberCredentials>
    <TrustedNetworkDetection>' + $TrustedNetwork + '</TrustedNetworkDetection>
      <DomainNameInformation>
    <DomainName>' + $DomainName + '</DomainName>
    <DnsServers>' + $DNSServers + '</DnsServers>
    </DomainNameInformation>
    </VPNProfile>'
    
    $ProfileXML | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.xml')
    
    $Script = '$ProfileName = ''' + $ProfileName + '''
    $ProfileNameEscaped = $ProfileName -replace ' ', '%20'
    
    $ProfileXML = ''' + $ProfileXML + ''''
    
    $ProfileXML = $ProfileXML -replace '<', '&lt;'
    $ProfileXML = $ProfileXML -replace '>', '&gt;'
    $ProfileXML = $ProfileXML -replace '"', '&quot;'
    
    $nodeCSPURI = "./Vendor/MSFT/VPNv2"
    $namespaceName = "root\cimv2\mdm\dmmap"
    $className = "MDM_VPNv2_01"
    
    try
    {
    $username = Gwmi -Class Win32_ComputerSystem | select username
    $objuser = New-Object System.Security.Principal.NTAccount($username.username)
    $sid = $objuser.Translate([System.Security.Principal.SecurityIdentifier])
    $SidValue = $sid.Value
    $Message = "User SID is $SidValue."
    Write-Host "$Message"
    }
    catch [Exception]
    {
    $Message = "Unable to get user SID. User may be logged on over Remote Desktop: $_"
    Write-Host "$Message"
    exit
    }
    
    $session = New-CimSession
    $options = New-Object Microsoft.Management.Infrastructure.Options.CimOperationOptions
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Type", "PolicyPlatform_UserContext", $false)
    $options.SetCustomOption("PolicyPlatformContext_PrincipalContext_Id", "$SidValue", $false)
    
        try
    {
        $deleteInstances = $session.EnumerateInstances($namespaceName, $className, $options)
        foreach ($deleteInstance in $deleteInstances)
        {
            $InstanceId = $deleteInstance.InstanceID
            if ("$InstanceId" -eq "$ProfileNameEscaped")
            {
                $session.DeleteInstance($namespaceName, $deleteInstance, $options)
                $Message = "Removed $ProfileName profile $InstanceId"
                Write-Host "$Message"
            } else {
                $Message = "Ignoring existing VPN profile $InstanceId"
                Write-Host "$Message"
            }
        }
    }
    catch [Exception]
    {
        $Message = "Unable to remove existing outdated instance(s) of $ProfileName profile: $_"
        Write-Host "$Message"
        exit
    }
    
    try
    {
        $newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", "String", "Key")
        $newInstance.CimInstanceProperties.Add($property)
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", "String", "Key")
        $newInstance.CimInstanceProperties.Add($property)
        $property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", "String", "Property")
        $newInstance.CimInstanceProperties.Add($property)
        $session.CreateInstance($namespaceName, $newInstance, $options)
        $Message = "Created $ProfileName profile."

        Write-Host "$Message"
    }
    catch [Exception]
    {
        $Message = "Unable to create $ProfileName profile: $_"
        Write-Host "$Message"
        exit
    }
    
    $Message = "Script Complete"
    Write-Host "$Message"
    
    $Script | Out-File -FilePath ($env:USERPROFILE + '\desktop\VPN_Profile.ps1')
    
    $Message = "Successfully created VPN_Profile.xml and VPN_Profile.ps1 on the desktop."
    Write-Host "$Message"
   ```

## <a name="configure-the-vpn-client-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 VPN 클라이언트 구성

Windows 10 클라이언트 컴퓨터에서 VPNv2 CSP를 구성 하려면 [프로필 XML 만들기](#create-the-profile-xml) 섹션에서 만든 VPN_Profile Windows PowerShell 스크립트를 실행 합니다. 관리자 권한으로 Windows PowerShell을 엽니다. 그렇지 않으면 _액세스가 거부_되었다는 오류가 표시 됩니다.

VPN_Profile를 실행 하 여 VPN 프로필을 구성한 후에는 Windows PowerShell ISE에서 다음 명령을 실행 하 여 언제 든 지 확인할 수 있습니다.

```powershell
Get-WmiObject -Namespace root\cimv2\mdm\dmmap -Class MDM_VPNv2_01
```

**Get-wmiobject cmdlet의 성공적인 결과**

```powershell
__GENUS : 2
__CLASS : MDM_VPNv2_01
__SUPERCLASS:
__DYNASTY   : MDM_VPNv2_01
__RELPATH   : MDM_VPNv2_01.InstanceID="Contoso%20AlwaysOn%20VPN",ParentID
  ="./Vendor/MSFT/VPNv2"
__PROPERTY_COUNT: 10
__DERIVATION: {}
__SERVER: WIN01
__NAMESPACE : root\cimv2\mdm\dmmap
__PATH  : \\WIN01\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="Conto
  so%20AlwaysOn%20VPN",ParentID="./Vendor/MSFT/VPNv2"
AlwaysOn: True
ByPassForLocal  :
DnsSuffix   : corp.contoso.com
EdpModeId   :
InstanceID  : Contoso%20AlwaysOn%20VPN
LockDown:
ParentID: ./Vendor/MSFT/VPNv2
ProfileXML  : <VPNProfile><RememberCredentials>true</RememberCredentials>
  <AlwaysOn>true</AlwaysOn><DnsSuffix>corp.contoso.com</DnsSu
  ffix><TrustedNetworkDetection>corp.contoso.com</TrustedNetw
  orkDetection><NativeProfile><Servers>vpn.contoso.com;vpn.co
  ntoso.com</Servers><RoutingPolicyType>SplitTunnel</RoutingP
  olicyType><NativeProtocolType>Ikev2</NativeProtocolType><Au
  thentication><UserMethod>Eap</UserMethod><MachineMethod>Eap
  </MachineMethod><Eap><Configuration><EapHostConfig xmlns="h
  ttp://www.microsoft.com/provisioning/EapHostConfig"><EapMet
  hod><Type xmlns="https://www.microsoft.com/provisioning/EapC
  ommon">25</Type><VendorId xmlns="https://www.microsoft.com/p
  rovisioning/EapCommon">0</VendorId><VendorType xmlns="http:
  //www.microsoft.com/provisioning/EapCommon">0</VendorType><
  AuthorId xmlns="https://www.microsoft.com/provisioning/EapCo
  mmon">0</AuthorId></EapMethod><Config xmlns="https://www.mic
  rosoft.com/provisioning/EapHostConfig"><Eap xmlns="https://w
  ww.microsoft.com/provisioning/BaseEapConnectionPropertiesV1
  "><Type>25</Type><EapType xmlns="https://www.microsoft.com/p
  rovisioning/MsPeapConnectionPropertiesV1"><ServerValidation
  ><DisableUserPromptForServerValidation>true</DisableUserPro
  mptForServerValidation><ServerNames>NPS</ServerNames><Trust
  edRootCA>3f 07 88 e8 ac 00 32 e4 06 3f 30 f8 db 74 25 e1
  2e 5b 84 d1 </TrustedRootCA></ServerValidation><FastReconne
  ct>true</FastReconnect><InnerEapOptional>false</InnerEapOpt
  ional><Eap xmlns="https://www.microsoft.com/provisioning/Bas
  eEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="
  https://www.microsoft.com/provisioning/EapTlsConnectionPrope
  rtiesV1"><CredentialsSource><CertificateStore><SimpleCertSe
  lection>true</SimpleCertSelection></CertificateStore></Cred
  entialsSource><ServerValidation><DisableUserPromptForServer
  Validation>true</DisableUserPromptForServerValidation><Serv
  erNames>NPS</ServerNames><TrustedRootCA>3f 07 88 e8 ac 00
  32 e4 06 3f 30 f8 db 74 25 e1 2e 5b 84 d1 </TrustedRootCA><
  /ServerValidation><DifferentUsername>false</DifferentUserna
  me><PerformServerValidation xmlns="https://www.microsoft.com
  /provisioning/EapTlsConnectionPropertiesV2">true</PerformSe
  rverValidation><AcceptServerName xmlns="https://www.microsof
  t.com/provisioning/EapTlsConnectionPropertiesV2">true</Acce
  ptServerName></EapType></Eap><EnableQuarantineChecks>false<
  /EnableQuarantineChecks><RequireCryptoBinding>false</Requir
  eCryptoBinding><PeapExtensions><PerformServerValidation xml
  ns="https://www.microsoft.com/provisioning/MsPeapConnectionP
  ropertiesV2">true</PerformServerValidation><AcceptServerNam
  e xmlns="https://www.microsoft.com/provisioning/MsPeapConnec
  tionPropertiesV2">true</AcceptServerName></PeapExtensions><
  /EapType></Eap></Config></EapHostConfig></Configuration></E
  ap></Authentication></NativeProfile><DomainNameInformation>
  <DomainName>corp.contoso.com</DomainName><DnsServers>10.10.
      0.2,10.10.0.3</DnsServers><AutoTrigger>true</AutoTrigger></
  DomainNameInformation></VPNProfile>
RememberCredentials : True
TrustedNetworkDetection : corp.contoso.com
PSComputerName  : WIN01
```

프로 파일링은 구조, 맞춤법, 구성 및 경우에 따라 올바른 경우 여야 합니다. 구조에서 1을 나열 하는 것과 다른 항목이 표시 되는 경우 프로 파일링 된 태그에 오류가 있을 수 있습니다.

태그 문제를 해결 해야 하는 경우에는 Windows PowerShell ISE에서 문제를 해결 하는 것 보다 XML 편집기에 배치 하는 것이 더 쉽습니다. 두 경우 모두 가장 간단한 버전의 프로필에서 시작 하 여 문제가 다시 발생 될 때까지 한 번에 하나씩 구성 요소를 다시 추가 합니다.

## <a name="configure-the-vpn-client-by-using-system-center-configuration-manager"></a>System Center Configuration Manager를 사용 하 여 VPN 클라이언트 구성

System Center Configuration Manager에서는 Windows PowerShell에서와 마찬가지로 프로 파일링을 사용 하 여 VPN 프로필을 배포할 수 있습니다. 여기서는 [ProfileXML 구성 파일 만들기](#create-the-profilexml-configuration-files)섹션에서 만든 VPN_Profile Windows PowerShell 스크립트를 사용 합니다.

System Center Configuration Manager를 사용 하 여 Windows 10 클라이언트 컴퓨터에 원격 액세스 Always On VPN 프로필을 배포 하려면 먼저 프로필을 배포할 컴퓨터 또는 사용자 그룹을 만들어야 합니다. 이 시나리오에서는 구성 스크립트를 배포할 사용자 그룹을 만듭니다.

### <a name="create-a-user-group"></a>사용자 그룹 만들기

1.  Configuration Manager 콘솔에서 자산 및 준수\\사용자 컬렉션을 엽니다.

2.  **홈** 리본의 **만들기** 그룹에서 **사용자 컬렉션 만들기**를 클릭 합니다.

3.  일반 페이지에서 다음 단계를 완료 합니다.

    a. **이름**에 **VPN 사용자**를 입력 합니다.

    b. **찾아보기**를 클릭 하 고 **모든 사용자** 를 클릭 한 다음 **확인**을 클릭 합니다.

    c. **다음**을 클릭합니다.

4.  멤버 관리 규칙 페이지에서 다음 단계를 완료 합니다.

    a.  **멤버 관리 규칙**에서 **규칙 추가**를 클릭 하 고 **직접 규칙**을 클릭 합니다. 이 예제에서는 사용자 컬렉션에 개별 사용자를 추가 합니다. 그러나 대규모 배포의 경우 쿼리 규칙을 사용 하 여이 컬렉션에 동적으로 사용자를 추가할 수 있습니다.

    b.  **시작** 페이지에서 **다음**을 클릭합니다.

    c.  리소스 검색 페이지의 **값**에 추가 하려는 사용자의 이름을 입력 합니다. 리소스 이름에는 사용자의 도메인이 포함 됩니다. 부분 일치를 기반으로 결과를 포함 하려면 검색 조건의 **%** 한쪽 끝에 문자를 삽입 합니다. 예를 들어 "lori" 문자열을 포함 하는 모든 사용자를 찾으려면 **% lori%** 를 입력 합니다. **다음**을 클릭합니다.

    d.  리소스 선택 페이지에서 그룹에 추가 하려는 사용자를 선택 하 고 **다음**을 클릭 합니다.

    e.  요약 페이지에서 **다음**을 클릭 합니다.

    f.  완료 페이지에서 **닫기**를 클릭 합니다.

6.  사용자 컬렉션 만들기 마법사의 멤버 관리 규칙 페이지로 돌아가 **다음**을 클릭 합니다.

7.  요약 페이지에서 **다음**을 클릭 합니다.

8.  완료 페이지에서 **닫기**를 클릭 합니다.

VPN 프로필을 받을 사용자 그룹을 만든 후에는 [프로 파일링 구성 파일 만들기](#create-the-profilexml-configuration-files)섹션에서 만든 Windows PowerShell 구성 스크립트를 배포 하기 위한 패키지 및 프로그램을 만들 수 있습니다.

### <a name="create-a-package-containing-the-profilexml-configuration-script"></a>ProfileXML 구성 스크립트를 포함 하는 패키지 만들기

1.  사이트 서버 컴퓨터 계정에서 액세스할 수 있는 네트워크 공유에서 VPN_Profile 스크립트를 호스팅합니다.

2.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리\\응용\\프로그램 관리 패키지**를 엽니다.

3.  **홈** 리본의 **만들기** 그룹에서 **패키지 만들기** 를 클릭 하 여 패키지 및 프로그램 만들기 마법사를 시작 합니다.

4.  패키지 페이지에서 다음 단계를 완료 합니다.

    a. **이름**에 **WINDOWS 10 Always On VPN 프로필**을 입력 합니다.

    b. **이 패키지에 소스 파일 포함** 확인란을 선택 하 고 **찾아보기**를 클릭 합니다.

    c. 원본 폴더 설정 대화 상자에서 **찾아보기**를 클릭 하 고 VPN_Profile를 포함 하는 파일 공유를 선택한 다음 **확인**을 클릭 합니다.
        로컬 경로가 아닌 네트워크 경로를 선택 해야 합니다. 즉, 경로는 *c:\\vpnscript*가 아닌  *\\fileserver\\vpnscript*와 같아야 합니다.

1.  **다음**을 클릭합니다.

2.  프로그램 유형 페이지에서 **다음**을 클릭 합니다.

3.  표준 프로그램 페이지에서 다음 단계를 완료 합니다.

    a.  **이름**에 **VPN 프로필 스크립트**를 입력 합니다.

    b.  **명령줄**에 **PowerShell .exe-set-executionpolicy "VPN_Profile"** 를 입력 합니다.

    c.  **실행 모드**에서 **관리자 권한으로 실행**을 클릭 합니다.

    d.  **다음**을 클릭합니다.

4.  요구 사항 페이지에서 다음 단계를 완료 합니다.

    a.  **지정 된 플랫폼 에서만이 프로그램을 실행할 수 있음**을 선택 합니다.

    b.  **모든 windows 10 (32 비트)** 및 **모든 windows 10 (64 비트)** 확인란을 선택 합니다.

    c.  **예상 디스크 공간**에 **1**을 입력 합니다.

    d.  **최대 허용 실행 시간 (분)** 에 **15**를 입력 합니다.

    e.  **다음**을 클릭합니다.

5.  요약 페이지에서 **다음**을 클릭 합니다.

6.  완료 페이지에서 **닫기**를 클릭 합니다.

패키지와 프로그램을 만들었으면 **VPN 사용자** 그룹에 배포 해야 합니다.

### <a name="deploy-the-profilexml-configuration-script"></a>ProfileXML 구성 스크립트 배포

1.  Configuration Manager 콘솔에서 소프트웨어 라이브러리\\응용 프로그램 관리\\패키지를 엽니다.

2.  **패키지**에서 **WINDOWS 10 Always On VPN 프로필**을 클릭 합니다.

3.  **프로그램** 탭의 세부 정보 창 아래쪽에서 **VPN 프로필 스크립트**를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 후 다음 단계를 완료 합니다.

    a.  **고급** 탭에서 **이 프로그램이 컴퓨터에 할당 된 경우**에서 **로그온 한 모든 사용자에 대해 한 번**을 클릭 합니다.

    b.  **확인**을 클릭합니다.

4.  **VPN 프로필 스크립트** 를 마우스 오른쪽 단추로 클릭 하 고 **배포** 를 클릭 하 여 소프트웨어 배포 마법사를 시작 합니다.

5.  일반 페이지에서 다음 단계를 완료 합니다.

    a.  **컬렉션**옆에서 **찾아보기**를 클릭 합니다.

    b.  **컬렉션 형식** 목록 (왼쪽 위)에서 **사용자 컬렉션**을 클릭 합니다.

    c.  **VPN 사용자**를 클릭 하 고 **확인**을 클릭 합니다.

    d.  **다음**을 클릭합니다.

6.  콘텐츠 페이지에서 다음 단계를 완료 합니다.

    a.  **추가**를 클릭 하 고 **배포 지점**을 클릭 합니다.

    b.  **사용 가능한 배포 위치**에서 프로 파일링 구성 스크립트를 배포할 배포 위치를 선택 하 고 **확인**을 클릭 합니다.

    c.  **다음**을 클릭합니다.

7.  배포 설정 페이지에서 **다음**을 클릭 합니다.

8.  일정 페이지에서 다음 단계를 완료 합니다.

    a.  **새로 만들기** 를 클릭 하 여 할당 일정 대화 상자를 엽니다.

    b.  **이 이벤트 바로 다음에 할당**을 클릭 하 고 **확인**을 클릭 합니다.

    c.  **다음**을 클릭합니다.

9.  사용자 환경 페이지에서 다음 단계를 완료 합니다.

    1.  **소프트웨어 설치** 확인란을 선택 합니다.

    2.  **요약**을 클릭 합니다.

10. 요약 페이지에서 **다음**을 클릭 합니다.

11. 완료 페이지에서 **닫기**를 클릭 합니다.

ProfileXML 구성 스크립트를 배포한 후 사용자 컬렉션을 빌드할 때 선택한 사용자 계정을 사용 하 여 Windows 10 클라이언트 컴퓨터에 로그인 합니다. VPN 클라이언트의 구성을 확인 합니다.

>[!NOTE]
>VPN_Profile 스크립트는 원격 데스크톱 세션에서 작동 하지 않습니다. 마찬가지로 Hyper-v 고급 세션에서는 작동 하지 않습니다. 가상 컴퓨터에서 원격 액세스 Always On VPN을 테스트 하는 경우 계속 하기 전에 클라이언트 Vm에서 고급 세션을 사용 하지 않도록 설정 합니다.

### <a name="verify-the-configuration-of-the-vpn-client"></a>VPN 클라이언트의 구성 확인

1.  제어판의 **\\시스템 보안**에서 **Configuration Manager**을 클릭 합니다. 

2.  Configuration Manager 속성 대화 상자의 **동작** 탭에서 다음 단계를 완료 합니다.

    a.  **컴퓨터 정책 검색 & 평가 주기**를 클릭 하 고 **지금 실행**을 클릭 한 다음 **확인**을 클릭 합니다.

    b.  **사용자 정책 검색 & 평가 주기**를 클릭 하 고 **지금 실행**을 클릭 한 다음 **확인**을 클릭 합니다.

    c.  **확인**을 클릭합니다.

3.  제어판을 닫습니다.

잠시 후에 새 VPN 프로필이 표시 되어야 합니다.

## <a name="configure-the-vpn-client-by-using-intune"></a>Intune을 사용 하 여 VPN 클라이언트 구성

Intune을 사용 하 여 Windows 10 원격 액세스 Always On VPN 프로필을 배포 하려면 [profilexml 구성 파일 만들기](#create-the-profilexml-configuration-files)섹션에서 만든 VPN 프로필을 사용 하 여 PROFILEXML CSP 노드를 구성 하거나 제공 된 기본 EAP XML 샘플을 사용할 수 있습니다. 표에서.

>[!NOTE]
>이제 Intune에서 Azure AD 그룹을 사용 합니다. Azure AD Connect VPN 사용자 그룹을 온-프레미스에서 Azure AD로 동기화 하 고 사용자가 VPN 사용자 그룹에 할당 되 면 진행할 준비가 된 것입니다.

VPN 장치 구성 정책을 만들어 그룹에 추가 된 모든 사용자에 대 한 Windows 10 클라이언트 컴퓨터를 구성 합니다. Intune 템플릿에서 VPN 매개 변수를 제공 하기 때문에 VPN_ProfileXML \<파일의 eaphostconfig > \</srhostconfig > 부분만 복사 합니다.

### <a name="create-the-always-on-vpn-configuration-policy"></a>Always On VPN 구성 정책 만들기

1.  [Azure 포털](https://portal.azure.com/)할 수 있습니다.

2.  **Intune** > **장치**구성프로필 > 로 이동 합니다.

3.  **프로필 만들기** 를 클릭 하 여 프로필 만들기 마법사를 시작 합니다.

4.  VPN 프로필의 **이름과** 설명 (선택 사항)을 입력 합니다.

1.   **플랫폼**에서 **Windows 10 이상**을 선택 하 고 프로필 유형 드롭다운에서 **VPN** 을 선택 합니다.

     >[!TIP]
     >사용자 지정 VPN 프로 파일링 Exml을 만드는 경우 지침은 [Intune을 사용 하 여 프로 파일링 적용](https://docs.microsoft.com/windows/security/identity-protection/vpn/vpn-profile-options#apply-profilexml-using-intune) 에서 지침을 참조 하세요.

2. **기본 VPN** 탭에서 다음 설정을 확인 하거나 설정 합니다.

    - **연결 이름:** 클라이언트 컴퓨터의 **설정**아래에 있는 **vpn** 탭에 표시 되는 vpn 연결의 이름을 입력 합니다 (예: _Contoso autovpn_).  
    
    - **서버용** 추가를 클릭 하 여 하나 이상의 VPN 서버를 추가 **합니다.**
    
    - **설명** 및 **IP 주소 또는 FQDN:** VPN 서버의 설명, IP 주소 또는 FQDN을 입력 합니다. 이러한 값은 VPN 서버 인증 인증서의 주체 이름과 일치 해야 합니다. 
    
    - **기본 서버:** 기본 VPN 서버인 경우를 **True**로 설정 합니다. 이렇게 하면이 서버를 장치에서 연결을 설정 하는 데 사용 하는 기본 서버로 사용 하도록 설정 됩니다. 
    
    - **연결 형식:** 을 **IKEv2**로 설정 합니다.  
    
    - **Always On:** 를 **사용** 하도록 설정 하 여 로그인 시 자동으로 VPN에 연결 하 고 사용자가 수동으로 연결을 끊을 때까지 연결 상태를 유지 합니다.
    
    - **로그온 시 자격 증명을 잊지 마십시오**.  자격 증명을 캐시 하는 부울 값 (true 또는 false)입니다. True로 설정 하면 가능한 경우 항상 자격 증명이 캐시 됩니다.

3.  다음 XML 문자열을 텍스트 편집기에 복사 합니다.
 
    [!INCLUDE [important-lower-case-true-include](../../../includes/important-lower-case-true-include.md)]
    
    
    ```XML
    <EapHostConfig xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Eap xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type><EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><CredentialsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUserPromptForServerValidation><ServerNames>NPS.contoso.com</ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>false</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">true</AcceptServerName></EapType></Eap><EnableQuarantineChecks>false</EnableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2">true</AcceptServerName></PeapExtensions></EapType></Eap></Config></EapHostConfig>
    ```

4.  **TrustedRootCA > 5a 89 fe cb 5b 49 a7 0b 1a 52 63 b7 35 ee d7 1c c2 68\/을 두 위치 모두에서 온-프레미스 루트 인증 기관의 인증서 지문을 사용 하 여 샘플의 4b < TrustedRootCA > 바꿉니다. \<**
  
    >[!Important]
    >아래 \<TrustedRootCA >\</TrustedRootCA > 섹션에서 샘플 지문을 사용 하지 마십시오.  TrustedRootCA는 RRAS 및 NPS 서버에 대 한 서버 인증 인증서를 발급 한 온-프레미스 루트 인증 기관의 인증서 지문 이어야 합니다. **이 인증서는 클라우드 루트 인증서와 중간 발급 CA 인증서 지문이**아니어야 합니다.

5.  샘플 XML에서  **\<ServerNames >\</ServerNames >** 를 인증이 수행 되는 도메인에 가입 된 NPS의 FQDN으로 바꿉니다. 

6.  수정 된 XML 문자열을 복사 하 여 기본 VPN 탭 아래의 **EAP xml** 상자에 붙여 넣고 **확인**을 클릭 합니다.
    Intune에서 EAP를 사용 하는 Always On VPN 장치 구성 정책이 만들어집니다.


### <a name="sync-the-always-on-vpn-configuration-policy-with-intune"></a>Always On VPN 구성 정책을 Intune과 동기화

구성 정책을 테스트 하려면 **ALWAYS ON VPN Users** 그룹에 추가한 사용자로 Windows 10 클라이언트 컴퓨터에 로그인 한 후 Intune과 동기화 합니다.

1.  시작 메뉴에서 **설정**을 클릭 합니다.

2.  설정에서 **계정**을 클릭 하 고 **회사 또는 학교 액세스**를 클릭 합니다.

3.  MDM 프로필을 클릭 하 고 **정보**를 클릭 합니다.

4.  **동기화** 를 클릭 하 여 Intune 정책 평가 및 검색을 적용 합니다.

5.  설정을 닫습니다. 동기화 후 컴퓨터에서 사용할 수 있는 VPN 프로필이 표시 됩니다.

## <a name="next-steps"></a>다음 단계

Always On VPN 배포를 완료 했습니다.  구성할 수 있는 다른 기능에 대해서는 아래 표를 참조 하세요.

|원하는 경우  |다음을 참조 하세요.  |
|---------|---------|
|VPN에 대 한 조건부 액세스 구성    |[7단계. 필드 Azure AD](../../ad-ca-vpn-connectivity-windows10.md)를 사용 하 여 VPN 연결에 대 한 조건부 액세스 구성: 이 단계에서는 권한 있는 VPN 사용자가 [Azure Active Directory (AZURE AD) 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)를 사용 하 여 리소스에 액세스 하는 방법을 미세 조정할 수 있습니다. Vpn (가상 사설망) 연결에 대 한 Azure AD 조건부 액세스를 사용 하 여 VPN 연결을 보호할 수 있습니다. 조건부 액세스는 Azure AD(Azure Active Directory)에 연결된 응용 프로그램에 대한 액세스 규칙을 만드는 데 사용되는 정책 기반 평가 엔진입니다.         |
|고급 VPN 기능에 대 한 자세한 정보  |[고급 VPN 기능](always-on-vpn-adv-options.md#advanced-vpn-features): 이 페이지에서는 VPN 트래픽 필터를 사용 하도록 설정 하는 방법, 앱 트리거를 사용 하 여 자동 VPN 연결을 구성 하는 방법 및 Azure AD에서 발급 한 인증서를 사용 하 여 클라이언트에서 VPN 연결만 허용 하도록 NPS를 구성 하는 방법을 안내 합니다.        |
