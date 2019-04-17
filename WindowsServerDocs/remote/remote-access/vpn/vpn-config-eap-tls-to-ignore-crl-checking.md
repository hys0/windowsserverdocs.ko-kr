---
title: EAP-TLS를 사용하여 CRL(인증서 해지 목록) 확인 무시
description: NPS 서버는 클라이언트의 인증서 체인 (루트 인증서 포함)의 해지 확인을 완료 하 고 인증서 해지 된 확인 하지 않는 한 EAP-TLS 클라이언트 연결할 수 없습니다.
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
ms.openlocfilehash: ac59c554c69a6138a106a648c3fab3ed4fe05b7b
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067370"
---
# 7.1단계. EAP-TLS를 사용하여 CRL(인증서 해지 목록) 확인 무시

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows 10

& #171;  [ **이전:** 7 단계입니다. (선택 사항) Azure AD를 사용 하 여 VPN 연결에 대 한 조건부 액세스](ad-ca-vpn-connectivity-windows10.md)<br>
& #187; [ **다음:** 7.2 단계입니다. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>이 레지스트리 변경 내용을 구현 실패 하 PEAP를 사용 하 여 클라우드 인증서를 사용 하 여 실패 하며, IKEv2 연결 하지만 IKEv2 연결 온-프레미스 CA에서 발급 한 클라이언트 인증 인증서를 사용 하 여 계속 작동 합니다.

이 단계에서는 **IgnoreNoRevocationCheck** 추가 하 고 인증서 CRL 배포 지점 포함 되지 않은 경우 클라이언트 인증을 허용 하도록 설정할 수 있습니다. 기본적으로 IgnoreNoRevocationCheck (사용 안 함) 0으로 설정 됩니다.

>[!NOTE]
>Windows 라우팅 및 원격 액세스 서버 (RRAS) NPS를 사용 하는 경우 프록시 RADIUS 두 번째 NPS로 호출을 설정 해야 **IgnoreNoRevocationCheck = 1** 두 서버 모두에서.

NPS 서버 인증서 체인 (루트 인증서 포함)의 해지 확인을 완료 하지 않는 한 EAP-TLS 클라이언트 연결할 수 없습니다. 사용자에 게 Azure AD에서 발급 하는 클라우드 인증서 CRL가 없는 1 시간의 수명이 일시적인 인증서 이기 때문입니다. NPS에서 EAP CRL의 부재 무시 하도록 구성 해야 합니다. 기본적으로 IgnoreNoRevocationCheck (사용 안 함) 0으로 설정 됩니다. IgnoreNoRevocationCheck를 추가 하 고 인증서 CRL 배포 지점 포함 되지 않은 경우 클라이언트의 인증을 허용 하는 1로 설정 합니다. 

인증 방법 EAP-TLS 이므로 EAP\13에서이 레지스트리 값만 필요 합니다. 다른 EAP 인증 방법을 사용 하는 경우 다음 레지스트리 값 추가할지에서 이러한도 합니다. 

**절차**

1. NPS 서버에서 **regedit.exe** 엽니다.

2. **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13**로 이동 합니다.

3. 클릭 **편집 > 새** **DWORD (32 비트) 값** 을 선택 하 고 **IgnoreNoRevocationCheck**를 입력 합니다.

4. **IgnoreNoRevocationCheck** 를 두 번 클릭 하 고 값 데이터를 **1**로 설정 합니다.

5. **확인** 을 클릭 하 고 서버를 다시 부팅 합니다. RRAS 및 NPS 서비스를 다시 시작 충분 하지 않습니다.

자세한 내용은 [사용 하도록 설정 하거나 클라이언트 인증서 해지 확인 (CRL)을 사용 하지 않도록 설정 하는 방법을](https://technet.microsoft.com/library/bb680540.aspx)참조 하세요.


|레지스트리 경로  |EAP 확장  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP 있을 v2         |

## 다음 단계

[단계 7.2입니다. Azure AD를 사용 하 여 VPN 인증에 대 한 루트 인증서 만들기](vpn-create-root-cert-for-vpn-auth-azure-ad.md):이 단계에서는 Azure AD 테 넌 트에 자동으로 VPN 서버 클라우드 응용 프로그램을 만드는 사용 하 여 VPN 인증에 대 한 루트 인증서 조건부 액세스 구성 합니다. 

---