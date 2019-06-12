---
title: EAP-TLS를 사용하여 CRL(인증서 해지 목록) 확인 무시
description: NPS 서버는 클라이언트의 (루트 인증서 포함) 인증서 체인의 해지 검사를 완료 하 고 인증서가 해지 된 확인 하지 않는 한 EAP-TLS 클라이언트를 연결할 수 없습니다.
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
ms.openlocfilehash: 781239f45b9b260b7d374c2a6972cdb8faad2879
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749597"
---
# <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>7.1단계. EAP-TLS를 사용하여 CRL(인증서 해지 목록) 확인 무시

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**이전:** 7단계. (선택 사항) Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스](ad-ca-vpn-connectivity-windows10.md)
- [**다음:** 7.2단계. Azure AD를 사용하여 VPN 인증에 대한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>이 레지스트리 변경 내용을 구현 하지 않으면 IKEv2 연결 실패 시 PEAP와 함께 클라우드 인증서를 사용 하 여 시키지만 온-프레미스 CA에서 발급 한 클라이언트 인증 인증서를 사용 하 여 IKEv2 연결은 계속 작동 합니다.

이 단계에서 추가할 수 있습니다 **IgnoreNoRevocationCheck** 인증서에 CRL 배포 지점 포함 되지 않은 경우 클라이언트 인증을 허용 하도록 설정 합니다. 기본적으로 IgnoreNoRevocationCheck 0 (해제)으로 설정 됩니다.

>[!NOTE]
>Windows RRAS (라우팅 및 원격 액세스 서버) NPS를 사용 하는 경우 프록시에는 두 번째 NPS를 RADIUS 호출을 설정 해야 합니다 **IgnoreNoRevocationCheck = 1** 두 서버 모두에서.

NPS 서버 (루트 인증서 포함)의 인증서 체인의 해지 확인을 완료 하지 않으면 EAP-TLS 클라이언트를 연결할 수 없습니다. 1 시간 동안 유지를 사용 하 여 단기 인증서 이기 때문에 클라우드 인증서를 Azure AD에서 사용자에 게 발급 된 CRL을 갖지 않습니다. NPS에서 EAP CRL의 부재를 무시 하도록 구성 해야 합니다. 기본적으로 IgnoreNoRevocationCheck 0 (해제)으로 설정 됩니다. IgnoreNoRevocationCheck를 추가 하 고 인증서에 CRL 배포 지점 포함 되지 않은 경우 클라이언트 인증을 허용 하는 1로 설정 합니다. 

EAP-TLS 인증 방법 이므로이 레지스트리 값은 EAP\13에서 필요한만 합니다. 다른 EAP 인증 방법을 사용 하는 경우 다음 레지스트리 값을 추가 해야 해당 아래도 합니다. 

**프로시저**

1. 오픈 **regedit.exe** NPS 서버에서.

2. 이동할 **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13**합니다.

3. 선택 **편집 > 새로 만들기** 선택한 **(32 비트) Dword** 입력 **IgnoreNoRevocationCheck**합니다.

4. 두 번 클릭 **IgnoreNoRevocationCheck** 값 데이터를 설정 하 고 **1**합니다.

5. 선택 **확인** 하 고 서버를 다시 부팅 합니다. NPS 및 RRAS 서비스를 다시 시작 충분 하지 않습니다.

자세한 내용은 [을 사용 하도록 설정 하거나 클라이언트에서 인증서 해지 확인 하는 중 (CRL)를 사용 하지 않도록 설정 하는 방법을](https://technet.microsoft.com/library/bb680540.aspx)합니다.


|레지스트리 경로  |EAP 확장  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP-MSCHAP v2         |

## <a name="next-steps"></a>다음 단계

[7.2단계. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md): 이 단계에서는 자동으로 테 넌 트에서 VPN 서버 클라우드 앱을 만드는 Azure AD와 VPN 인증에 대 한 조건부 액세스 루트 인증서를 구성 합니다.
