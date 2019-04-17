---
title: 네트워크 셸 (Netsh)
description: 이 항목에서는 Windows Server 2016에는 네트워크 셸 (netsh) 명령줄 유틸리티 개요를 제공 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0a23d60bc3f181fee62ade105e546bbb7161c133
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-shell-netsh"></a>네트워크 셸 \(Netsh\)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

네트워크 셸 (netsh)는 명령줄 유틸리티 구성 하 고 Windows Server 2016을 실행 하는 컴퓨터에 설치 된 후 다양 한 네트워크 communications server 역할 및 구성 요소의 상태를 표시할 수 있습니다.

>[!NOTE]
>이 항목에서는 뿐만 아니라 다음 네트워크 셸 콘텐츠를 사용할 수 있습니다.
>
> - [Netsh 명령 구문을, 컨텍스트 및 포맷](netsh-contexts.md)
> - [네트워크 셸 (Netsh) 예 배치 파일](netsh-wins.md)
> - [Netsh 기술 참조](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc) 

일부 클라이언트 기술을 BranchCache, Dynamic Host Configuration Protocol \(DHCP\) 클라이언트 등 Windows 10을 실행 하는 클라이언트 컴퓨터를 구성할 수 있도록 netsh 명령을 제공 합니다.

Netsh 명령은 대부분의 경우 Microsoft Management Console \(MMC\) snap\ 사용 하는 경우 사용할 수 있는 같은 기능을 제공-에서 각 네트워킹 서버 역할 또는 네트워킹 기능에 대해 합니다. 예를 들어, NPS MMC 스냅인 또는 netsh 명령에 사용 하 여 네트워크 정책 서버 \(NPS\)를 구성할 수 있습니다의 **netsh nps** 컨텍스트가 합니다.

또한 MMC 스냅인와 Windows Server에서 사용할 수 없는 IPv6, 네트워크 다리 및 \(RPC\) 원격 프로시저 호출와 같은 네트워크 기술에 대 한 명령 netsh 가지가 있습니다.

>[!IMPORTANT]
>Windows PowerShell 네트워킹 기술에 관리를 사용 하는 것이 좋습니다 [Windows 10 및 Windows Server 2016](https://technet.microsoft.com/library/mt156917.aspx) 네트워크 셸 아니라 합니다. 그러나 네트워크 셸 사용자 스크립트와의 호환성에 대 한 포함 되어 있으며 용도인 지원 됩니다.

## <a name="network-shell-netsh-technical-reference"></a>네트워크 (Netsh) 셸 기술 참조

Netsh 기술 참조 구문을, 매개 변수를 netsh 명령에 대해 예제 등 netsh 명령 참조를 제공 합니다. Netsh 기술 참조 스크립트와 배치 파일 네트워크 기술 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 로컬 또는 원격 관리 netsh 명령을 사용 하 여 빌드를 사용할 수 있습니다.  
  
### <a name="content-availability"></a>콘텐츠 공급 일  
  
네트워크 셸 기술 참조 TechNet 갤러리에서 \(*.chm\) 형식 Windows 도움말에서 다운로드할 수는: [Netsh 기술 참조](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  

