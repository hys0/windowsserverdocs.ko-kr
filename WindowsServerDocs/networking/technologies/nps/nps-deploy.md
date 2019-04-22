---
title: 네트워크 정책 서버 배포
description: 이 항목에서는 Windows Server 2016 용 네트워크 정책 서버 배포 콘텐츠 링크를 제공 하 고 NPS에 대 한 추가 설명서 링크가 포함 되어 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8da8951a9c6ed5022c892bbf01b33614d38abc5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814844"
---
# <a name="deploy-network-policy-server"></a>네트워크 정책 서버 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 정책 서버를 배포 하는 방법은이 항목에서는 사용할 수 있습니다.

>[!NOTE]
>추가 네트워크 정책 서버 설명서에 대 한 다음 라이브러리 섹션을 사용할 수 있습니다.  
>- [네트워크 정책 서버를 사용 하 여 시작](nps-getstart-top.md)
>- [네트워크 정책 서버 계획](nps-plan-top.md)
>- [네트워크 정책 서버 관리](nps-manage-top.md)

계획 및 네트워크 정책 서버 설치 섹션을 포함 하는 Windows Server 2016 핵심 네트워크 가이드 \(NPS\), 및 가이드에 제시 된 기술 Active Directory 도메인에서 NPS를 배포 하기 위한 필수 구성 요소로 사용 합니다. 자세한 내용은 Windows Server 2016에서 "NPS1 배포" 섹션을 참조 하세요 [핵심 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1)합니다.

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>VPN 및 802.1x 액세스에 대 한 NPS 인증서 배포

Extensible Authentication Protocol 같은 인증 방법을 배포 하려는 경우 \(EAP\) 서버를 사용 해야 하는 보호 된 EAP에 NPS에서 인증서를 가이드를 사용 하 여 NPS 인증서를 배포할 수 있습니다 [ 802.1 X 유선 및 무선 배포에 대 한 서버 인증서 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)합니다.

## <a name="deploy-nps-for-8021x-wireless-access"></a>802.1x 무선 액세스에 대 한 NPS 배포

무선 액세스에 대 한 NPS를 배포 하려면이 가이드를 사용할 수 있습니다 [배포 암호 기반 802.1x 인증 무선 액세스](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)합니다.

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Windows 10 VPN 액세스를 위한 NPS 배포

NPS를 사용 하 여 항상에서 가상 개인 네트워크에 대 한 연결 요청을 처리 하는 데 \(VPN\) 컴퓨터 및 Windows 10을 실행 하는 장치를 사용 하는 원격 직원에 대 한 연결 합니다.

자세한 내용은 참조는 [원격 액세스 항상에서 VPN 배포 가이드에 대 한 Windows Server 2016 및 Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)합니다.

