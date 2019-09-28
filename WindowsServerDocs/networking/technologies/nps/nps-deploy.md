---
title: 네트워크 정책 서버 배포
description: 이 항목에서는 Windows Server 2016에 대 한 네트워크 정책 서버 배포 콘텐츠에 대 한 링크를 제공 하 고 NPS에 대 한 추가 지침에 대 한 링크를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 6cfb50e0-7088-4295-97c5-14ff8776cbf8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33cada472c314088bc1485bab6d9631226b0ffaf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405421"
---
# <a name="deploy-network-policy-server"></a>네트워크 정책 서버 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

네트워크 정책 서버를 배포 하는 방법에 대 한 자세한 내용은이 항목을 참조 하십시오.

>[!NOTE]
>네트워크 정책 서버에 대 한 추가 설명서를 보려면 다음 라이브러리 섹션을 사용 하십시오.  
>- [네트워크 정책 서버 시작](nps-getstart-top.md)
>- [네트워크 정책 서버 계획](nps-plan-top.md)
>- [네트워크 정책 서버 관리](nps-manage-top.md)

Windows Server 2016 핵심 네트워크 가이드에는 네트워크 정책 서버 \(NPS @ no__t-1을 계획 하 고 설치 하는 섹션이 포함 되어 있으며,이 가이드에 제시 된 기술은 Active Directory 도메인에 NPS를 배포 하기 위한 필수 구성 요소로 제공 됩니다. 자세한 내용은 Windows Server 2016 [Core 네트워크 가이드](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide#BKMK_deployNPS1)의 "Deploy NPS1" 섹션을 참조 하세요.

## <a name="deploy-nps-certificates-for-vpn-and-8021x-access"></a>VPN 및 802.1 X 액세스를 위한 NPS 인증서 배포

NPS에서 서버 인증서를 사용 해야 하는 \(EAP @ no__t-1 및 보호 된 EAP와 같은 인증 방법을 배포 하려는 경우에는 다음 [에 대 한 서버 인증서 배포 가이드를 사용 하 여 nps 인증서를 배포할 수 있습니다. 802.1 x 유선 및 무선 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments).

## <a name="deploy-nps-for-8021x-wireless-access"></a>802.1 X 무선 액세스를 위한 NPS 배포

무선 액세스용 NPS를 배포 하기 위해 [암호 기반 802.1 x 인증 된 무선 액세스](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)가이드를 사용할 수 있습니다.

## <a name="deploy-nps-for-windows-10-vpn-access"></a>Windows 10 VPN 액세스용 NPS 배포

NPS를 사용 하 여 Windows 10을 실행 하는 컴퓨터 및 장치를 사용 하는 원격 직원의 @no__t Always On VPN @ no__t 연결에 대 한 연결 요청을 처리할 수 있습니다.

자세한 내용은 [Windows Server 2016 및 windows 10에 대 한 원격 액세스 ALWAYS ON VPN 배포 가이드](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy)를 참조 하세요.

