---
title: 네트워크 정책 서버를 배포 합니다.
description: 이 항목 Windows Server 2016 대 한 링크 네트워크 정책 서버 배포 콘텐츠를 제공 하 고 NPS에 대 한 추가 지침은에 대 한 링크를 포함 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: daf62e2a593014e16bcb5fd16542b2e9c75b9c1d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-network-policy-server"></a>네트워크 정책 서버를 배포 합니다.

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 정책 서버 배포에 대 한 정보에 대 한이 항목을 사용할 수 있습니다.

>[!NOTE]
>추가 네트워크 정책 서버 설명서 다음 라이브러리 섹션을 사용할 수 있습니다.  
>- [네트워크 정책 서버 시작](nps-getstart-top.md)
>- [네트워크 정책 서버 계획](nps-plan-top.md)
>- [네트워크 정책 서버 관리](nps-manage-top.md)

가이드에 표시 되는 기술 역할을 NPS Active Directory 도메인에 배포 사항 및 Windows Server 2016 Core 네트워크 가이드 섹션 계획 하 고 네트워크 정책 서버 \(NPS\) 설치에 포함 됩니다. 자세한 내용은 Windows Server 2016에에서 "배포 NPS1" 섹션을 참조 [Core 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1)합니다.

## <a name="deploy-nps-server-certificates-for-vpn-and-8021x-access"></a>802.1 X 액세스 및 VPN NPS 서버 인증서를 배포 합니다.

가이드 서버 인증서 NPS NPS 서버에 서버의 인증서 사용 해야 하는 Extensible 인증 프로토콜 \(EAP\) EAP 보호 등 인증 방법을 배포 하려면 배포할 수 있습니다 [802.1 X 유선 및 무선 배포에 대 한 서버 인증서 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)합니다.

## <a name="deploy-nps-for-8021x-wireless-access"></a>802.1 X 무선 액세스 NPS 배포

무선 액세스를 NPS 배포 하려면 가이드를 사용할 수 있습니다 [암호 배포 기반 802.1 X 인증 무선 액세스](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)합니다.

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Windows 10 VPN 액세스 NPS 배포

NPS 연결에 대 한 원격 직원 컴퓨터 및 Windows 10을 실행 하는 디바이스를 사용 하는 항상에서 가상 개인 네트워크 \(VPN\) 연결에 대 한 요청을 처리 하는 데 사용할 수 있습니다.

자세한 내용은 참조는 [원격 액세스 항상에서 VPN 배포 가이드 Windows 10 및 Windows Server 2016 용](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)합니다.

