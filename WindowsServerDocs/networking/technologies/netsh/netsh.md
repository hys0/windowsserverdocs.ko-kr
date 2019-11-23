---
title: Netsh(네트워크 셸)
description: 이 항목에서는 Windows Server 2016의 네트워크 셸 (netsh) 명령줄 유틸리티에 대 한 개요를 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: ac440c8187424733c0636cf2013342458f08d2f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405542"
---
# <a name="network-shell-netsh"></a>네트워크 셸 \(Netsh\)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Netsh (네트워크 셸)는 Windows Server 2016를 실행 하는 컴퓨터에 다양 한 네트워크 통신 서버 역할 및 구성 요소를 설치한 후이를 구성 하 고 표시 하는 데 사용할 수 있는 명령줄 유틸리티입니다.

동적 호스트 구성 프로토콜 \(DHCP\) 클라이언트 및 BranchCache와 같은 일부 클라이언트 기술에서는 Windows 10을 실행 하는 클라이언트 컴퓨터를 구성할 수 있는 netsh 명령도 제공 합니다.

대부분의 경우 netsh 명령은 Microsoft Management Console \(MMC\-\) 사용할 때 사용할 수 있는 것과 동일한 기능을 제공 합니다. 예를 들어 nps MMC 스냅인 또는 **netsh nps** 컨텍스트의 netsh 명령을 사용 하 여 nps\) \(네트워크 정책 서버를 구성할 수 있습니다.

또한 Windows Server에서 MMC 스냅인으로 사용할 수 없는 i p v 6에 대 한 네트워크 기술 (예: i p v 6에 대 한 네트워크 기술, 네트워크 브리지 및 원격 프로시저 호출\)\()에 대 한 netsh 명령도 있습니다.

>[!IMPORTANT]
>Windows PowerShell을 사용 하 여 네트워크 셸이 아닌 [Windows Server 2016 및 windows 10](https://technet.microsoft.com/library/mt156917.aspx) 에서 네트워킹 기술을 관리 하는 것이 좋습니다. 네트워크 셸이 스크립트와의 호환성을 위해 포함 되어 있으며,이를 사용 하는 것이 지원 됩니다.

## <a name="network-shell-netsh-technical-reference"></a>Netsh (네트워크 셸) 기술 참조

Netsh 기술 참조는 구문, 매개 변수 및 netsh 명령의 예를 포함 하 여 포괄적인 netsh 명령 참조를 제공 합니다. Netsh 기술 참조를 사용 하 여 Windows Server 2016 및 Windows 10을 실행 하는 컴퓨터에서 네트워크 기술의 로컬 또는 원격 관리를 위한 netsh 명령을 사용 하 여 스크립트 및 배치 파일을 빌드할 수 있습니다.  
  
### <a name="content-availability"></a>콘텐츠 가용성  
  
네트워크 셸 기술 참조는 TechNet 갤러리에서 다운로드할 수 있는 Windows 도움말 \(* .chm\) 형식: [Netsh 기술 참조](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc) 를 다운로드할 수 있습니다.  
  
---
