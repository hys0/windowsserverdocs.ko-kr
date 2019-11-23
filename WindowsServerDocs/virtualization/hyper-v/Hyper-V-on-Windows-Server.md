---
title: Windows Server의 Hyper-V
description: Hyper-v 시도, 계획, 배포 및 관리에 대 한 주요 문서 링크를 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0baef6b8-598c-4fe0-9f31-5869fc4e0f69
author: KBDAzure
ms.author: kathydav
ms.date: 10/07/2016
ms.openlocfilehash: 558733e3472578d1df413fe220f1846debc0f358
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366837"
---
# <a name="hyper-v-on-windows-server"></a>Windows Server의 Hyper-V

>적용 대상: Windows Server 2016, Windows Server 2019

Windows Server의 Hyper-v 역할을 사용 하 여 가상 컴퓨터를 만들고 관리할 수 있는 가상화 된 컴퓨팅 환경을 만들 수 있습니다. 물리적 컴퓨터 한 대에서 여러 운영 체제를 실행 하 고 운영 체제를 서로 격리할 수 있습니다. 이 기술을 사용 하면 컴퓨팅 리소스의 효율성을 향상 시키고 하드웨어 리소스를 확보할 수 있습니다.

Windows Server의 Hyper-v에 대 한 자세한 내용을 보려면 다음 표의 항목을 참조 하십시오.

## <a name="hyper-v-resources-for-it-pros"></a>IT 전문가를 위한 hyper-v 리소스

|태스크 |리소스|
|---|---|
|![표시 및 문서 아이콘을 선택 하 여 요구 사항이 충족 됨을 표시 합니다.](media/All_Symbols_MeetsRequirements.png)|**Hyper-v 평가**<br /><br />- [Hyper-v 기술 개요](Hyper-V-Technology-Overview.md)<br />[Windows Server에서 제공 되는 hyper-v의 새로운 기능](What-s-new-in-Hyper-V-on-Windows.md) - <br />[Windows Server의 hyper-v에 대 한 - 시스템 요구 사항](System-requirements-for-Hyper-V-on-Windows.md)<br />[hyper-v에 대해 지원 되는 Windows 게스트 운영 체제](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md) -  <br />- [지원 되는 Linux 및 FreeBSD 가상 컴퓨터](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)<br />[세대 및 게스트에의 한 - 기능 호환성](Hyper-V-feature-compatibility-by-generation-and-guest.md) <br /><br />**Hyper-v 계획**<br /><br />[hyper-v에서 1 세대 또는 2 세대 가상 머신을 만들어야 - ?](plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md) <br />[Windows Server의 hyper-v 확장성에 대 한 - 계획](plan/plan-hyper-v-scalability-in-windows-server.md) <br />[Windows Server에서 hyper-v 네트워킹 - 계획](plan/plan-hyper-v-networking-in-windows-server.md) <br />[Windows Server의 hyper-v 보안 - 계획](plan/plan-hyper-v-security-in-windows-server.md)|
|![커서 및 선 버스트 아이콘](media/All_Symbols_GetStarted.png)|**Hyper-v 시작**<br /><br />- [Windows Server 2019 다운로드 및 설치](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)<br /><br />**Windows Server 2019의 server Core 또는 GUI 설치 옵션 (가상 머신 호스트)**<br /><br />[Windows Server에 hyper-v 역할을 설치](get-started/Install-the-Hyper-V-role-on-Windows-Server.md) - <br />[hyper-v 가상 컴퓨터에 대 한 가상 스위치를 만드는](get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md) - <br />[hyper-v에서 가상 컴퓨터를 만들](get-started/Create-a-virtual-machine-in-Hyper-V.md) - |
|![사용자 및 도구 아이콘](media/All_Symbols_Administrator.png)|**Hyper-v 호스트 및 가상 컴퓨터 업그레이드**<br /><br />- [Windows Server 클러스터 노드 업그레이드](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)<br />[가상 컴퓨터 버전 - 업그레이드](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)<br /><br />**Hyper-v 구성 및 관리**<br /><br />[장애 조치 (Failover) 클러스터링이 없는 실시간 마이그레이션에 대 한 호스트 설정](deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md) - <br />[원격으로 Nano Server 관리](../../get-started/manage-nano-server.md) - <br />[표준 또는 프로덕션 검사점 중 - 선택](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)<br />[검사점 사용 또는 사용 안 함](manage/Enable-or-disable-checkpoints-in-Hyper-V.md) - <br />[PowerShell Direct를 사용 하 여 Windows 가상 머신 - 관리](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)<br />[Hyper-v 복제본 - 설정](manage/Set-up-Hyper-V-Replica.md)|
|![대화 풍선 아이콘](media/All_Symbols_Chat.png)|**블로그**<br /><br />Microsoft 가상화 및 Hyper-v 팀의 프로그램 관리자, 제품 관리자, 개발자 및 테스터의 최신 게시물을 확인 하세요.<br /><br />- [가상화 블로그](https://blogs.technet.com/b/virtualization/)<br />- [Windows Server 블로그](https://blogs.technet.com/b/windowsserver/)<br />- [이혜준 Armstrong의 가상화 블로그](https://blogs.msdn.com/b/virtual_pc_guy/) (보관)|
|![사용자 그룹 아이콘](media/All_Symbols_Users_Group.png)|**포럼 및 뉴스 그룹**<br /><br />질문이 있으신가요? 동료, Mvp 및 Hyper-v 제품 팀과 의견을 교환할 수 있습니다.<br /><br />- [Windows Server 커뮤니티](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)<br />- [Windows Server Hyper-v TechNet 포럼](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverhyperv)|

## <a name="related-technologies"></a>관련 기술

다음 표에는 가상화 컴퓨팅 환경에서 사용 하려는 기술이 나열 되어 있습니다.

|기술|설명|
|--------------|---------------|
|[클라이언트 Hyper-v](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index)|**제어판**의 **프로그램 및 기능** 을 통해 설치할 수 있는 windows 8, Windows 8.1 및 windows 10에 포함 된 가상화 기술입니다.|
|[장애 조치(failover) 클러스터링](https://docs.microsoft.com/windows-server/failover-clustering/whats-new-in-failover-clustering)|Hyper-v 호스트 및 가상 컴퓨터에 대 한 고가용성을 제공 하는 Windows Server 기능입니다.|
|[Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)|가상화 된 데이터 센터에 대 한 관리 솔루션을 제공 하는 System Center 구성 요소입니다. 사용자가 만든 사설 클라우드에 가상 컴퓨터 및 서비스를 만들고 배포할 수 있도록 가상화 호스트, 네트워크 및 저장소 리소스를 구성 하 고 관리할 수 있습니다.|
|[Windows 컨테이너](https://docs.microsoft.com/virtualization/windowscontainers/)|Windows Server 및 Hyper-v 컨테이너를 사용 하 여 개발, 테스트 및 프로덕션 팀에 표준화 된 환경을 제공 합니다.|