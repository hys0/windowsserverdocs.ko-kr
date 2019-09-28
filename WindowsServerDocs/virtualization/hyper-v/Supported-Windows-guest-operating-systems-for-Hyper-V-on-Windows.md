---
title: Windows Server에서 Hyper-v에 대해 지원 되는 Windows 게스트 운영 체제
description: 가상 컴퓨터에서 게스트로 사용 하도록 지원 되는 Windows 운영 체제를 나열 합니다. 또한 이전 버전의 Hyper-v에 대 한 유사한 문서에 대 한 링크도 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 06b35897-2192-48b7-8c2d-125c520b0786
author: lizap
ms.author: elizapo
ms.date: 01/08/2019
ms.openlocfilehash: f491f283861098bbe98e253cb2ff1d5cee2ac57f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365462"
---
# <a name="supported-windows-guest-operating-systems-for-hyper-v-on-windows-server"></a>Windows Server에서 Hyper-v에 대해 지원 되는 Windows 게스트 운영 체제

>적용 대상: Windows Server 2016, Windows Server 2019

Hyper-v는 게스트 운영 체제 처럼 가상 컴퓨터에서 실행할 수 있는 여러 버전의 Windows Server, Windows 및 Linux 배포를 지원 합니다. 이 문서에서는 지원 되는 Windows 서버 및 Windows 게스트 운영 체제에 설명 합니다. Linux 및 FreeBSD 배포에 대 한 참조 [Windows에서 hyper-v 가상 컴퓨터를 지원 되는 Linux 및 FreeBSD](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)합니다.  
    
일부 운영 체제 기본 제공 통합 서비스를 보유합니다. 다른 사용자를 설치 하거나 가상 컴퓨터의 운영 체제를 설정한 후 별도 단계로 통합 서비스를 업그레이드 하는 필요 합니다. 자세한 내용은 아래 섹션을 참조 하 고  [Integration Services](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services)합니다.  
  
## <a name="supported-windows-server-guest-operating-systems"></a>지원 되는 Windows Server 게스트 운영 체제  

Windows server 2016 및 Windows Server 2019에서 Hyper-v에 대 한 게스트 운영 체제로 지원 되는 Windows Server 버전은 다음과 같습니다. 
  
|게스트 운영 체제(서버)|최대 가상 프로세서 수|통합 서비스|참고|  
|-------------------------------------|----------------------------------------|------------------------|---------|  
|Windows Server, 버전 1903 |2 세대의 경우 240;<br>64 세대 1|기본 제공||
|Windows Server, 버전 1809 |2 세대의 경우 240;<br>64 세대 1|기본 제공|| 
|Windows Server 2019 |2 세대의 경우 240;<br>64 세대 1|기본 제공||
|Windows Server, 버전 1803 |2 세대의 경우 240;<br>64 세대 1|기본 제공|| 
|Windows Server 2016 |2 세대의 경우 240;<br>64 세대 1|기본 제공|| 
|Windows Server 2012 R2 |64|기본 제공||  
|Windows Server 2012 |64|기본 제공||  
|Windows Server 2008 R2 SP 1(서비스 팩 1)|64|게스트 운영 체제를 설치한 후 중요 한 Windows 업데이트를 모두 설치 합니다.|Datacenter/Enterprise/Standard/Web Edition.|
|Windows Server 2008 서비스 팩 2(SP2)|8|게스트 운영 체제를 설치한 후 중요 한 Windows 업데이트를 모두 설치 합니다.|Datacenter/Enterprise/Standard/Web Edition(32비트/64비트).|  
  
## <a name="supported-windows-client-guest-operating-systems"></a>지원 되는 Windows 클라이언트 게스트 운영 체제  

Windows Server 2016 및 Windows Server 2019에서 Hyper-v에 대 한 게스트 운영 체제로 지원 되는 Windows 클라이언트 버전은 다음과 같습니다.
  
|게스트 운영 체제(클라이언트)|최대 가상 프로세서 수|통합 서비스|참고|  
|-------------------------------------|----------------------------------------|------------------------|---------|  
|Windows 10|32|기본 제공||  
|Windows 8.1|32|기본 제공||  
|Windows 7 SP 1(서비스 팩 1)|4|게스트 운영 체제를 설정한 후 통합 서비스를 업그레이드 합니다.|Ultimate/Enterprise/Professional Edition(32비트/64비트)|  
  
## <a name="guest-operating-system-support-on-other-versions-of-windows"></a>다른 버전의 Windows에서 게스트 운영 체제 지원  

다음 표에서는 다른 버전의 Windows에서 Hyper-v에 대해 지원 되는 게스트 운영 체제 정보에 대 한 링크를 제공 합니다.  
  
|호스트 운영 체제|항목|  
|-------------------------|---------|  
|Windows 10|[Windows 10의 클라이언트 Hyper-v에 대해 지원 되는 게스트 운영 체제](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/supported-guest-os)|  
|Windows Server 2012 R2 및 Windows 8.1|-   [Windows Server 2012 R2 및 Windows 8.1의 hyper-v에 대해 지원 되는 Windows 게스트 운영 체제](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn792027(v=ws.11))<br />Hyper-v의 -   [Linux 및 FreeBSD Virtual Machines](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)|  
|Windows Server 2012 및 Windows 8|[Windows Server 2012 및 Windows 8에서 Hyper-v에 대해 지원 되는 Windows 게스트 운영 체제](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn792028(v=ws.11))|  
|Windows Server 2008 및 Windows Server 2008 R2|[가상 컴퓨터 및 게스트 운영 체제 정보](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc794868(v=ws.10))|  
  
## <a name="how-microsoft-provides-support-for-guest-operating-systems"></a>Microsoft는 게스트 운영 체제에 대 한 지원에 제공 하는 방법  

Microsoft는 다음과 같은 방식으로 게스트 운영 체제에 대한 지원을 제공합니다.  
  
-   Microsoft 운영 체제 및 통합 서비스에서 발견된 문제는 Microsoft 지원에서 지원됩니다.  
  
-   Hyper-V에서 실행할 운영 체제 공급업체의 인증을 받은 다른 운영 체제에서 발견된 문제는 해당 공급업체가 지원 서비스를 제공합니다.  
  
-   다른 운영 체제에서 발견 된 문제를 Microsoft 제출 여러 공급 업체 지원 커뮤니티인 [TSANet](https://www.tsanet.org/)합니다.  
  
## <a name="see-also"></a>참조  
  
-   [Hyper-v의 Linux 및 FreeBSD Virtual Machines](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  
  
-   [Windows 10의 클라이언트 Hyper-v에 대해 지원 되는 게스트 운영 체제](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/supported-guest-os)  
  



