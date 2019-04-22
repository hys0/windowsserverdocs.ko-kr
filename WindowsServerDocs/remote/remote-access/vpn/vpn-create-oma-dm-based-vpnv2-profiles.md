---
title: Windows 10 장치에 대한 OMA-DM 기반 VPNv2 프로필 만들기
description: '두 가지 중 하나를 사용할 수 있습니다 8.1(OMA-DM 만들 메서드 기반 VPNv2 프로 파일입니다. '
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 1ce20d09c304b26e3708429cc45da06d020e5809
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816484"
---
# <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>7.5단계. 만들 8.1(OMA-DM 기반 Windows 10 장치에 대 한 VPNv2 프로필

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

&#171;  [**이전:** 7.4단계. 온-프레미스에 조건부 액세스 루트 인증서를 배포할 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)<br>
&#187;[ **다음:** VPN 작동 방식을 조건부 액세스에 알아봅니다.](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

이 단계에서는 OMA-DM를 만들 수 있습니다 기반 VPN 장치 구성 정책을 배포 하려면 Intune을 사용 하 여 VPNv2 프로 파일입니다. SCCM 또는 PowerShell 스크립트를 사용 하 여 VPNv2 프로필 만들기를 참조 하려는 경우 [VPNv2 CSP 설정이](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 대 한 자세한 내용은 합니다. 

## <a name="managed-deployment-using-intune"></a>Intune을 사용 하 여 관리 되는 배포

이 섹션에 설명 된 모든 조건부 액세스를 사용 하는 VPN을 만드는 데 필요한 최소입니다. 분할 터널링을 사용 하 여 WIP AutoVPN 작업을 가져오려면 사용자 지정 Intune 장치 구성 프로필을 만들거나 SSO는 다루지 않습니다. 아래에서 이전에 만든 VPN 프로필에 아래 설정을 통합 [5 단계. Always On VPN 연결에 Windows 10 클라이언트를 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)합니다.  이 예에서는 통합 하는는 [Intune을 사용 하 여 VPN 클라이언트 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune) 정책입니다. 

**필수 구성 요소:**<p>
Windows 10 클라이언트 컴퓨터에 Intune을 사용 하 여 VPN 연결으로 이미 구성 되었습니다.   


**절차:**

1. Azure 포털에서 클릭 **Intune** > **장치 구성을** > **프로필** 앞부분에서만든VPN프로필선택[ Intune을 사용 하 여 VPN 클라이언트 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)합니다.
    
2. 정책 편집기에서 선택 **속성** > **설정** > **자료 VPN**합니다. 기존 확장 **EAP Xml** 논리는 VPN 클라이언트에 제공 하는 필터를 포함할 수 있도록 첫 번째 사용을 유지 하는 대신 사용자의 인증서 저장소에서 AAD 조건부 액세스 인증서를 검색 해야 인증서를 검색 합니다.

    >[!NOTE]
    >이렇게 하지 않으면 VPN 클라이언트를 검색할 수는 온-프레미스 인증 기관에서 발급 된 사용자 인증서 VPN 연결에 발생 합니다.

    ![Intune 포털](../../media/Always-On-Vpn/intune-eap-xml.png)

3. 로 끝나는 섹션을 찾습니다  **\</AcceptServerName >\</EapType >** AAD 조건부 선택 논리를 사용 하 여 VPN 클라이언트를 제공 하기 위해 이러한 두 값 사이의 다음 문자열을 삽입 하 고 액세스 인증서:

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. 선택 된 **조건부 액세스** 블레이드 및 전환 **이 VPN 연결에 대 한 조건부 액세스** 하 **사용**합니다.<p>설정 변경 내용을 활성화 합니다  **\<DeviceCompliance >\<사용 > true\</활성화 >** VPNv2 프로필 XML의 설정 합니다.

    ![VPN-속성 Always On에 대 한 조건부 액세스](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

6. **확인**을 클릭합니다.

6. 선택 **할당**, Include, 클릭 **포함할 그룹 선택**합니다.

7. 선택 된 **VPN 사용자** 이 고 정책을 수신 하는 그룹 **저장**합니다.

    ![자동 VPN 사용자-할당에 대 한 제한](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## <a name="force-mdm-policy-sync-on-the-client"></a>클라이언트에서 MDM 정책 동기화를 강제 적용
VPN 프로필 설정에서 클라이언트 장치에 표시 되지 않는 경우\\네트워크 및 인터넷\\VPN MDM 정책 동기화를 강제로 지정할 수 있습니다.

1. 멤버인 도메인에 가입 된 클라이언트 컴퓨터에 로그인 합니다 **VPN 사용자** 그룹입니다.

2. 시작 메뉴에서 입력 **계정**, Enter 키를 누릅니다.

3.  왼쪽된 탐색 창에서 클릭 **회사 또는 학교 액세스**합니다.

5.  회사 또는 학교 액세스, 클릭 **< \domain > MDM 연결할** 클릭 **정보**합니다.

6.  클릭 **동기화** 설정에서 VPN 프로필 표시 되는지 확인 하 고\\네트워크 및 인터넷\\VPN.


## <a name="next-step"></a>다음 단계
완료 하면 Azure AD 조건부 액세스를 사용 하 여 VPN 프로필을 구성 합니다. 

|하려는 경우...  |다음을 참조 하는 중...  |
|---------|---------|
|조건부 액세스의 작동 방식 Vpn 사용 하는 방법에 대 한 자세한 정보  |[VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): 이 페이지는 Vpn을 사용 하 여 작동 방식을 조건부 액세스에 대 한 자세한 정보를 제공 합니다.      |
|고급 VPN 기능에 자세히 알아보기  |[고급 VPN 기능](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features): 이 페이지는 VPN 트래픽 필터를 사용 하는 방법, 앱 트리거를 사용 하 여 자동 VPN 연결을 구성 하는 방법만 Azure AD에서 발급 한 인증서를 사용 하 여 클라이언트에서 VPN 연결을 허용 하도록 NPS를 구성 하는 방법에 지침을 제공 합니다.        |


---

## <a name="related-topics"></a>관련 항목
- [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp):  이 항목에서는 VPNv2 CSP의 개요를 제공합니다. VPNv2 구성 서비스 공급자에는 장치의 VPN 프로필을 구성 하려면 모바일 장치 관리 (MDM) 서버를 수 있습니다.

- [Always On VPN 연결에 Windows 10 클라이언트를 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): 이 항목에서는 ProfileXML VPN을 만드는 방법과 ProfileXML 옵션 및 스키마에 대 한 정보를 제공 합니다. 서버 인프라를 설정한 후 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 Windows 10 클라이언트 컴퓨터를 구성 해야 합니다. 

- [Intune을 사용 하 여 VPN 클라이언트 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune): 이 항목에서는 Windows 10 원격 액세스 Always On VPN 프로필을 배포 하는 방법을 설명 합니다. Intune은 이제 Azure AD 그룹을 사용 합니다. Azure AD Connect Intune을 사용 하 여 VPN 클라이언트를 구성 하지 않아도 됩니다 온-프레미스에서 Azure AD에 VPN 사용자 그룹을 동기화 합니다.

---
