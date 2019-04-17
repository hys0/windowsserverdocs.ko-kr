---
title: Windows 10 장치에 대한 OMA-DM 기반 VPNv2 프로필 만들기
description: '둘 중 하나를 사용할 수 기반 VPNv2 프로필 만들기 OMA DM 하는 방법. '
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
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031297"
---
# 7.5단계. 만들기 OMA-DM 기반 VPNv2 프로필 Windows 10 장치

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **이전:** 7.4 단계입니다. 온-프레미스에 조건부 액세스 루트 인증서 배포 광고](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)<br>
& #187; [ **다음:** 어떻게 조건부 액세스 VPN 작동에 대 한 자세한](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

이 단계에서는 OMA DM 생성할 수 기반 VPNv2 프로필 Intune을 사용 하 여 VPN 장치 구성 정책 배포 합니다. VPNv2 프로필을 만드는 SCCM 또는 PowerShell 스크립트를 사용 하려는 경우 [VPNv2 CSP 설정](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 에 대 한 자세한 내용은 참조 하세요. 

## Intune을 사용 하 여 관리 되는 배포

이 섹션에 설명 된 모든 VPN 조건부 액세스를 사용 하는 데 필요한 최소 수준입니다. 분할 터널링을 사용 하 여 WIP AutoVPN를 가져오려면 사용자 지정 Intune 장치 구성 프로필을 만들거나 SSO는 적용 되지 않습니다. 아래의 설정을 [5 단계에서 이전에 만든 VPN 프로필에 통합 합니다. Windows 10 클라이언트 Always On VPN 연결 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)합니다.이 예제에서는 [Intune을 사용 하 여 VPN 클라이언트 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune) 정책에 통합은 했습니다. 

**필수 조건:**<p>
이미 Windows 10 클라이언트 컴퓨터를 구성 하 여 Intune을 사용 하 여 VPN 연결을 사용 합니다.   


**절차:**

1. Azure 포털에서 **Intune**를 클릭 > **장치 구성** >  [Intune을 사용 하 여 VPN 클라이언트 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)앞에서 만든**프로필** 및 VPN 프로필을 선택 합니다.
    
2. 정책 편집기에서 **속성**을 선택 > **설정** > **기본 VPN**합니다. VPN 클라이언트 첫 번째 인증서를 사용 하므로 가능성을 두지 말고 대신 사용자의 인증서 저장소에서 AAD 조건부 액세스 인증서를 검색 하는 데 필요한 논리를 제공 하는 필터를 포함 하도록 기존 **EAP Xml** 을 확장합니다 검색 합니다.

    >[!NOTE]
    >이렇게 하지 않으면 VPN 클라이언트 검색할 수 온-프레미스 인증 기관에서 발급 된 사용자 인증서 실패 한 VPN 연결에 발생 합니다.

    ![Intune 포털](../../media/Always-On-Vpn/intune-eap-xml.png)

3. **\_LT_/AcceptServerName>\</EapType>** 로 끝나는 섹션을 찾아 AAD 조건부 액세스 인증서를 선택 하기 위한 논리를 사용 하 여 VPN 클라이언트를 제공 하기 위해 이러한 두 값 간의 다음 문자열을 삽입 합니다.

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. **조건부 액세스** 블레이드 및 toogle **사용**으로 **이 VPN 연결에 대 한 조건부 액세스** 선택 합니다.<p>이 설정을 변경 **\<DeviceCompliance>\<Enabled>true\</Enabled>** VPNv2 프로필 XML에서 설정을 활성화 합니다.

    ![Always On VPN-속성에 대 한 조건부 액세스](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

6. **확인**을 클릭합니다.

6. **할당**포함에서 선택 **그룹을 포함 하도록 선택**을 클릭 합니다.

7. 이 정책을 수신 하 **는 VPN 사용자** 그룹을 선택 하 고 **저장**을 클릭 합니다.

    ![자동 VPN 사용자-할당에 대 한 상한](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## 클라이언트에서 MDM 정책 동기화를 강제 실행.
VPN 프로필 클라이언트 장치 Settings\\Network & Internet\\VPN, 아래에 표시 되지 않으면 동기화 하도록 MDM 정책을 실행할 수 있습니다.

1. **VPN 사용자** 그룹의 구성원으로 도메인에 가입 된 클라이언트 컴퓨터에 로그인 합니다.

2. 시작 메뉴에서 **계정**을 입력 하 고 Enter 키를 누릅니다.

3.  왼쪽된 탐색 창에서 **회사 또는 학교 액세스를**클릭 합니다.

5.  회사 또는 학교 액세스, 아래에서 **<\domain> MDM에 연결** 을 클릭 하 고 **정보**를 클릭 합니다.

6.  **동기화** 를 클릭 하 고 VPN 프로필 Settings\\Network & Internet\\VPN 아래에 표시를 확인 합니다.


## 다음 단계
완료 하면 Azure AD 조건부 액세스를 사용 하 여 VPN 프로필을 구성 합니다. 

|하려는 경우...  |다음을 참조 하십시오.  |
|---------|---------|
|Vpn 어떻게 조건부 액세스 작동에 대 한 자세한 정보  |[VPN 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access):이 페이지는 Vpn과 작동 방식을 조건부 액세스에 대 한 자세한 정보를 제공 합니다.      |
|고급 VPN 기능에 자세히 알아보기  |[VPN 고급 기능](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features): VPN 트래픽 필터를 사용 하는 방법, 앱 트리거를 사용 하 여 자동 VPN 연결을 구성 하는 방법 및 NPS만 Azure에서 발급 한 인증서를 사용 하 여 클라이언트에서 VPN 연결을 허용 하도록 구성 하는 방법에 지침을 제공 하는이 페이지 광고 합니다.        |


---

## 관련 항목
- [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp):이 항목에서는 VPNv2 CSP의 개요를 사용 하 여 제공 합니다. VPNv2 구성 서비스 공급자 모바일 장치 관리 (MDM) 서버를 장치의 VPN 프로필을 구성할 수 있습니다.

- [Windows 10 클라이언트 항상에서 VPN 연결 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections):이 항목에서는 ProfileXML 옵션 및 스키마에 대 한 정보 및 ProfileXML VPN을 만드는 방법을 제공 합니다. 서버 인프라를 설정한 후 VPN 연결을 사용 하 여 해당 인프라와 통신 하는 windows 10 클라이언트 컴퓨터를 구성 해야 합니다. 

- [Intune을 사용 하 여 VPN 클라이언트 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune):이 항목에서는 Windows 10 원격 액세스 Always On VPN 프로필을 배포 하는 방법에 대해 설명 합니다. 이제 Intune은 Azure AD 그룹을 사용 합니다. Azure AD Connect 동기화를 Azure AD에서 온-프레미스 VPN 사용자 그룹을 하는 경우 다음 필요는 없습니다 Intune을 사용 하 여 VPN 클라이언트를 구성 합니다.

---
