---
title: Netsh(네트워크 셸)
description: 이 항목에서는 Windows Server 2016의 netsh(네트워크 셸) 명령줄 유틸리티에 대한 개요를 제공합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: d9103585d1868f586f169f01096c4d37961e7033
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316683"
---
# <a name="network-shell-netsh"></a>네트워크 셸 \(Netsh\)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

netsh(네트워크 셸)는 Windows Server 2016을 실행하는 컴퓨터에 다양한 네트워크 통신 서버 역할 및 구성 요소를 설치한 후 이들의 상태를 구성하고 표시할 수 있는 명령줄 유틸리티입니다.

동적 호스트 구성 프로토콜 \(DHCP\) 클라이언트 및 BranchCache와 같은 일부 클라이언트 기술은 Windows 10을 실행하는 클라이언트 컴퓨터를 구성할 수 있는 netsh 명령도 제공합니다.

대부분의 경우 netsh 명령은 각 네트워킹 서버 역할 또는 네트워킹 기능에 대해 Microsoft Management Console \(MMC\) snap\-을 사용할 때 사용할 수 있는 기능과 동일한 기능을 제공합니다. 예를 들어 NPS MMC 스냅인 또는 **netsh nps** 컨텍스트에서 netsh 명령을 사용하여 네트워크 정책 서버 \(NPS\)를 구성할 수 있습니다.

또한 Windows Server에서 MMC 스냅인으로 사용할 수 없는 IPv6, 네트워크 브리지 및 원격 프로시저 호출 \(RPC\)와 같은 네트워크 기술에 대한 netsh 명령이 있습니다.

>[!IMPORTANT]
>네트워크 셸 대신 Windows PowerShell을 사용하여 [Windows Server 2016 및 Windows 10](https://technet.microsoft.com/library/mt156917.aspx)에서 네트워킹 기술을 관리하는 것이 좋습니다. 그러나 스크립트와의 호환성을 위해 네트워크 셸이 포함되어 있으며, 사용이 지원됩니다.

## <a name="network-shell-netsh-technical-reference"></a>Netsh(네트워크 셸) 기술 참조

Netsh 기술 참조는 구문, 매개 변수 및 netsh 명령의 예를 포함하여 포괄적인 netsh 명령 참조를 제공합니다. Netsh 기술 참조를 사용하여 Windows Server 2016 및 Windows 10을 실행하는 컴퓨터에서 네트워크 기술의 로컬 또는 원격 관리를 위한 netsh 명령을 통해 스크립트 및 배치 파일을 빌드할 수 있습니다.  
  
### <a name="content-availability"></a>콘텐츠 가용성  
  
네트워크 셸 기술 참조는 TechNet 갤러리에서 Windows 도움말 \(*.chm\) 형식으로 다운로드할 수 있습니다. [Netsh 기술 참조](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  
---
