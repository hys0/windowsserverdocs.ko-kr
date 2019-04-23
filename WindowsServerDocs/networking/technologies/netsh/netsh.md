---
title: Netsh(네트워크 셸)
description: 이 항목에서는 Windows Server 2016에서 네트워크 셸 (netsh) 명령줄 유틸리티의 개요를 제공합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: 038b21783ef1d27619657ec3f9a472cf3caba68e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849364"
---
# <a name="network-shell-netsh"></a>네트워크 셸 \(Netsh\)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

네트워크 셸 (netsh)는 구성 및 Windows Server 2016을 실행 하는 컴퓨터에 설치 된 후 다양 한 네트워크 통신 서버 역할 및 구성 요소의 상태를 표시할 수 있는 명령줄 유틸리티입니다.

Dynamic Host Configuration Protocol 같은 일부 클라이언트 기술은 \(DHCP\) netsh 명령은 Windows 10을 실행 하는 클라이언트 컴퓨터를 구성할 수 있도록 하는 클라이언트 및 BranchCache를 제공 합니다.

Netsh 명령 대부분의 경우에서 Microsoft Management Console을 사용 하는 경우 사용할 수 있는 동일한 기능을 제공 \(MMC\) 맞춤\-에서 각 네트워킹 서버 역할 또는 네트워킹 기능에 대 한 합니다. 예를 들어, 네트워크 정책 서버를 구성할 수 있습니다 \(NPS\) NPS MMC 스냅인 또는 netsh 명령을 사용 하 여 합니다 **netsh nps** 컨텍스트.

또한 가지 네트워크 기술에 대 한 netsh 명령와 같은 IPv6, 네트워크 연결 및 원격 프로시저 호출 \(RPC\), MMC 스냅인을 사용 하는 Windows Server에서 사용할 수 없는 합니다.

>[!IMPORTANT]
>네트워킹 기술을 관리 하기 위한 Windows PowerShell을 사용 하는 것이 좋습니다 [Windows Server 2016 및 Windows 10](https://technet.microsoft.com/library/mt156917.aspx) 네트워크 셸 대신 합니다. 그러나 네트워크 셸 스크립트를 사용 하 여 호환성을 위해 포함 되어 있으며 해당 사용은 지원.

## <a name="network-shell-netsh-technical-reference"></a>네트워크 셸 (Netsh) 기술 참조

Netsh 기술 참조는 구문, 매개 변수 및 netsh 명령에 대 한 예제를 포함 하 여 포괄적인 netsh 명령 참조를 제공 합니다. 네트워크 기술 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터의 로컬 또는 원격 관리를 위한 netsh 명령을 사용 하 여 배치 파일과 스크립트를 작성 하는 Netsh 기술 참조를 사용할 수 있습니다.  
  
### <a name="content-availability"></a>콘텐츠 가용성  
  
네트워크 셸 기술 참조는 Windows 도움말에서 다운로드할 수 있습니다 \(*.chm\) TechNet 갤러리에서 형식: [Netsh 기술 참조](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  
---
