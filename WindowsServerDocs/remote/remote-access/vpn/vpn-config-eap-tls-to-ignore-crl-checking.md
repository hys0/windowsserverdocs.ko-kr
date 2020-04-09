---
title: EAP-TLS를 사용하여 CRL(인증서 해지 목록) 확인 무시
description: NPS 서버가 클라이언트의 인증서 체인 (루트 인증서 포함)에 대 한 해지 검사를 완료 하 고 인증서가 해지 되었는지 확인 하지 않는 한 EAP-TLS 클라이언트는 연결할 수 없습니다.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 07/13/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: db85d71ed1b7d8d5b3c14ac8ea603789422ea2cb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818886"
---
# <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>7\.1단계. EAP-TLS를 사용하여 CRL(인증서 해지 목록) 확인 무시

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** 7 단계. 필드 Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스](ad-ca-vpn-connectivity-windows10.md)
- [**다음:** 7.2 단계. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>이 레지스트리 변경을 구현 하지 못하면 PEAP를 사용 하는 클라우드 인증서를 사용 하는 IKEv2 연결이 실패 하지만, 온-프레미스 CA에서 발급 한 클라이언트 인증 인증서를 사용 하는 IKEv2 연결은 계속 작동 합니다.

이 단계에서는 **Ignorenorevocationcheck** 를 추가 하 고 인증서에 CRL 배포 지점이 포함 되지 않은 경우 클라이언트 인증을 허용 하도록 설정할 수 있습니다. 기본적으로 IgnoreNoRevocationCheck는 0 (사용 안 함)으로 설정 됩니다.

>[!NOTE]
>Windows RRAS (라우팅 및 원격 액세스 서버)에서 NPS를 사용 하 여 두 번째 NPS에 대 한 RADIUS 호출을 프록시 하는 경우 두 서버 모두에서 **Ignorenorevocationcheck = 1** 을 설정 해야 합니다.

인증서 체인 (루트 인증서 포함)의 해지 검사를 수행 하지 않는 한 EAP-TLS 클라이언트는 연결할 수 없습니다. Azure AD에서 사용자에 게 발급 한 클라우드 인증서는 수명이 1 시간인 수명이 짧은 인증서 이기 때문에 CRL이 없습니다. NPS의 EAP는 CRL이 없음을 무시 하도록 구성 해야 합니다. 기본적으로 IgnoreNoRevocationCheck는 0 (사용 안 함)으로 설정 됩니다. IgnoreNoRevocationCheck를 추가 하 고 인증서에 CRL 배포 지점이 포함 되지 않은 경우 클라이언트에 대 한 인증을 허용 하도록 1로 설정 합니다. 

인증 방법이 EAP-TLS 이므로이 레지스트리 값은 EAP\13. 에서만 필요 합니다. 다른 EAP 인증 방법을 사용 하는 경우 레지스트리 값도 그 아래에 추가 해야 합니다. 

**여기서**

1. NPS 서버에서 **regedit.exe** 를 엽니다.

2. **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\rasman\ppp\eap\13**로 이동 합니다.

3. **편집 > 새로 만들기** 를 선택 하 고 **DWORD (32 비트) 값** 을 선택 하 고 **Ignorenorevocationcheck**를 입력 합니다.

4. **Ignorenorevocationcheck** 를 두 번 클릭 하 고 값 데이터를 **1**로 설정 합니다.

5. **확인** 을 선택 하 고 서버를 다시 부팅 합니다. RRAS와 NPS 서비스를 다시 시작 해도 충분 하지 않습니다.

자세한 내용은 [클라이언트에서 CRL (인증서 해지 확인)을 사용 하거나 사용 하지 않도록 설정 하는 방법](https://technet.microsoft.com/library/bb680540.aspx)을 참조 하세요.


|레지스트리 경로  |EAP 확장  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP-MSCHAP v2         |

## <a name="next-steps"></a>다음 단계

[7.2 단계. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md):이 단계에서는 테 넌 트에서 Vpn 서버 클라우드 앱을 자동으로 만드는 AZURE ad를 사용 하 여 vpn 인증에 대 한 조건부 액세스 루트 인증서를 구성 합니다.
