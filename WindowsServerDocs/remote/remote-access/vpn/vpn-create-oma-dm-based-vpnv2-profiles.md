---
title: Windows 10 디바이스에 대한 OMA-DM 기반 VPNv2 프로필 만들기
description: '두 가지 방법 중 하나를 사용 하 여 OMA DM 기반 VPNv2 프로필을 만들 수 있습니다. '
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 07/13/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: b1316fe2feba674beb915b6ea22b1c0361ae1243
ms.sourcegitcommit: 7116460855701eed4e09d615693efa4fffc40006
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2020
ms.locfileid: "83433157"
---
# <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>7.5단계. Windows 10 장치에 대 한 OMA DM 기반 VPNv2 프로필 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** 7.4 단계. 온-프레미스 AD에 조건부 액세스 루트 인증서 배포](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)
- [**다음:** VPN에 대 한 조건부 액세스가 작동 하는 방법 알아보기](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

이 단계에서는 Intune을 사용 하 여 VPN 장치 구성 정책을 배포 하는 OMA DM 기반 VPNv2 프로필을 만들 수 있습니다. Microsoft Endpoint Configuration Manager 또는 PowerShell 스크립트를 사용 하 여 VPNv2 프로필을 만들려면 [VPNV2 CSP 설정](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) 에서 자세한 내용을 참조 하세요. 

## <a name="managed-deployment-using-intune"></a>Intune을 사용 하 여 관리 되는 배포

이 섹션에서 설명 하는 모든 내용은 조건부 액세스를 사용 하 여 VPN 작업을 수행 하는 데 필요한 최소입니다. 또한 분할 터널링, WIP를 사용 하 여 사용자 지정 Intune 장치 구성 프로필을 만들어 AutoVPN 작동 또는 SSO에 대해 다루지 않습니다. 아래 설정을 5 단계에서 만든 VPN 프로필에 통합 합니다 [. Windows 10 클라이언트 Always On VPN 연결을 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)합니다.이 예제에서는 [Intune 정책을 사용 하 여 VPN 클라이언트 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune) 에 통합 합니다. 

**인지**

Windows 10 클라이언트 컴퓨터는 이미 Intune을 사용 하 여 VPN 연결로 구성 되었습니다.   


**여기서**

1. Azure Portal에서 **intune**  >  **장치 구성**  >  **프로필** 을 선택 하 고 [intune을 사용 하 여 vpn 클라이언트 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)에서 이전에 만든 vpn 프로필을 선택 합니다.
    
2. 정책 편집기에서 **속성**  >  **설정**  >  **기본 VPN**을 선택 합니다. 검색 된 첫 번째 인증서를 사용할 수 있도록 허용 하는 대신 사용자의 인증서 저장소에서 AAD 조건부 액세스 인증서를 검색 하는 데 필요한 논리를 VPN 클라이언트에 부여 하는 필터를 포함 하도록 기존 **EAP Xml** 을 확장 합니다.

    >[!NOTE]
    >이를 사용 하지 않으면 VPN 클라이언트가 온-프레미스 인증 기관에서 발급 된 사용자 인증서를 검색 하 여 VPN 연결이 실패할 수 있습니다.

    ![Intune 포털](../../media/Always-On-Vpn/intune-eap-xml.png)

3. ** \< /Semservername>\< rrtype>** 로 끝나는 섹션을 찾아이 두 값 사이에 다음 문자열을 삽입 하 여 VPN 클라이언트에 AAD 조건부 액세스 인증서를 선택 하는 논리를 제공 합니다.

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. **조건부 액세스** 블레이드를 선택 하 고 **이 VPN 연결에 대 한 조건부 액세스** 를 mtd **설정**합니다.
   
   이 설정을 사용 하도록 설정 하면 VPNv2 Profile XML에서 ** \< DeviceCompliance>\< enabled>true \< /enabled>** 설정이 변경 됩니다.

    ![Always On VPN에 대 한 조건부 액세스-속성](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

5. **확인**을 선택합니다.

6. **할당**을 선택 하 고 포함에서 **포함할 그룹 선택**을 선택 합니다.

7. 이 정책을 받는 **VPN 사용자** 그룹을 선택 하 고 **저장**을 선택 합니다.

    ![자동 VPN 사용자-할당에 대 한 상한](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## <a name="force-mdm-policy-sync-on-the-client"></a>클라이언트에서 MDM 정책 동기화 강제 적용

VPN 프로필이 클라이언트 장치에 표시 되지 않는 경우 설정 \\ 네트워크 & 인터넷 \\ VPN에서 MDM 정책을 강제로 동기화 할 수 있습니다.

1. 도메인에 가입 된 클라이언트 컴퓨터에 **VPN 사용자** 그룹의 구성원으로 로그인 합니다.

2. 시작 메뉴에서 **계정**을 입력 하 고 enter 키를 누릅니다.

3. 왼쪽 탐색 창에서 **회사 또는 학교 액세스**를 선택 합니다.

4. 회사 또는 학교 액세스에서 **< \domain>에 연결 됨**을 선택한 다음 **정보**를 선택 합니다.

5. **동기화** 를 선택 하 고 Vpn 프로필이 설정 \\ 네트워크 & 인터넷 vpn에 표시 되는지 확인 \\ 합니다.


## <a name="next-steps"></a>다음 단계

Azure AD 조건부 액세스를 사용 하도록 VPN 프로필을 구성 하는 작업을 완료 했습니다. 

|다음을 원하는 경우...  |다음을 참조 하세요.  |
|---------|---------|
|Vpn을 사용 하 여 조건부 액세스의 작동 방식에 대 한 자세한 정보  |[Vpn 및 조건부 액세스](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access):이 페이지에서는 vpn에서 조건부 액세스가 작동 하는 방식에 대 한 자세한 정보를 제공 합니다.      |
|고급 VPN 기능에 대 한 자세한 정보  |[고급 Vpn 기능](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features):이 페이지에서는 Vpn 트래픽 필터를 사용 하도록 설정 하는 방법, 앱 트리거를 사용 하 여 자동 vpn 연결을 구성 하는 방법 및 Azure AD에서 발급 한 인증서를 사용 하 여 클라이언트에서 vpn 연결만 허용 하도록 NPS를 구성 하는 방법을 설명 합니다.        |


## <a name="related-topics"></a>관련 항목

- [VPNV2 csp](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp):이 항목에서는 VPNv2 csp에 대 한 개요를 제공 합니다. VPNv2 구성 서비스 공급자는 MDM (모바일 장치 관리) 서버에서 장치의 VPN 프로필을 구성할 수 있도록 허용 합니다.

- [Windows 10 클라이언트 ALWAYS ON VPN 연결 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections):이 항목에서는 프로 파일링 옵션 및 스키마에 대 한 정보와 프로 파일링을 만드는 방법에 대해 설명 합니다. 서버 인프라를 설정한 후에는 VPN 연결을 사용 하 여 해당 인프라와 통신 하도록 Windows 10 클라이언트 컴퓨터를 구성 해야 합니다. 

- [Intune을 사용 하 여 vpn 클라이언트 구성](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune):이 항목에서는 vpn 프로필 Always On Windows 10 원격 액세스를 배포 하는 방법에 대 한 정보를 제공 합니다. 이제 Intune에서 Azure AD 그룹을 사용 합니다. VPN 사용자 그룹을 온-프레미스에서 Azure AD로 동기화 Azure AD Connect 경우에는 Intune을 사용 하 여 VPN 클라이언트를 구성할 필요가 없습니다.
