---
title: Windows Server의 Hyper-v
description: 체험, 계획, 배포 및 Hyper-v를 관리 하는 방법에 대 한 주요 문서의 링크를 제공
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0baef6b8-598c-4fe0-9f31-5869fc4e0f69
author: KBDAzure
ms.author: kathydav
ms.date: 10/07/2016
ms.openlocfilehash: 1a658b611b68d7ecde64bdf0f8a318cc1af2804c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880264"
---
# <a name="hyper-v-on-windows-server"></a>Windows Server의 Hyper-v

>적용 대상: Windows Server 2016, Windows Server 2019

가상화 된 컴퓨팅 환경을 만들고 가상 컴퓨터를 관리 하는 위치를 만들 Windows Server의 Hyper-v 역할이 있습니다. 하나의 물리적 컴퓨터에서 여러 운영 체제를 실행 하 고 운영 체제를 서로 격리할 수 있습니다. 이 기술을 사용 하 여 컴퓨팅 리소스의 효율성을 향상 시킬 수 있으며 하드웨어 리소스를 확보할 수 있습니다.

Windows Server에서 Hyper-v에 자세히 알아보려면 다음 표의 항목을 참조 하세요.

## <a name="hyper-v-resources-for-it-pros"></a>IT 전문가 위한 Hyper-v 리소스

|태스크 |리소스|
|---|---|
|![확인 요구 사항이 충족 표시할 표시 및 문서 아이콘](media/All_Symbols_MeetsRequirements.png)|**Hyper-v가 설치를 평가 합니다.**<br /><br />- [Hyper-v 기술 개요](Hyper-V-Technology-Overview.md)<br />- [Windows Server에서 Hyper-v의 새로운 기능](What-s-new-in-Hyper-V-on-Windows.md)<br />- [Windows Server에서 Hyper-v에 대 한 시스템 요구 사항](System-requirements-for-Hyper-V-on-Windows.md)<br />- [Hyper-v에 대 한 지원 되는 Windows 게스트 운영 체제](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md) <br />- [지원 되는 Linux 및 FreeBSD 가상 컴퓨터](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)<br />- [생성 및 게스트 별 기능 호환성](Hyper-V-feature-compatibility-by-generation-and-guest.md) <br /><br />**Hyper-v에 대 한 계획**<br /><br />- [Hyper-v에 1 또는 2 세대 가상 머신을 만들어야 하나요?](plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md) <br />- [Windows Server의 Hyper-v 확장성에 대 한 계획](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [Windows Server Hyper-v 네트워킹 계획](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [Windows Server에서 Hyper-v 보안 계획](plan/plan-hyper-v-security-in-windows-server.md)|
|![커서 및 선 버스트 아이콘](media/All_Symbols_GetStarted.png)|**Hyper-v 시작**<br /><br />- [다운로드 하 여 Windows Server 2019 설치](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)<br /><br />**가상 컴퓨터 호스트로 Windows 서버 2019의 있는 server Core 또는 GUI 설치 옵션**<br /><br />- [Windows 서버에 Hyper-v 역할 설치](get-started/Install-the-Hyper-V-role-on-Windows-Server.md)<br />- [Hyper-v 가상 컴퓨터에 대 한 가상 스위치 만들기](get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)<br />- [Hyper-v에서 가상 머신 만들기](get-started/Create-a-virtual-machine-in-Hyper-V.md)|
|![사용자 및 도구 아이콘](media/All_Symbols_Administrator.png)|**Hyper-v 호스트 및 가상 컴퓨터를 업그레이드 합니다.**<br /><br />- [Windows Server 클러스터 노드를 업그레이드 합니다.](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)<br />- [가상 머신 버전 업그레이드](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)<br /><br />**구성 및 Hyper-v 관리**<br /><br />- [장애 조치 클러스터링이 없는 실시간 마이그레이션에 대해 호스트 설정](deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)<br />- [Nano Server를 원격으로 관리](../../get-started/manage-nano-server.md)<br />- [표준 또는 프로덕션 검사점 간의 선택](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)<br />- [검사점을 사용할지 설정 합니다.](manage/Enable-or-disable-checkpoints-in-Hyper-V.md)<br />- [PowerShell Direct를 사용 하 여 Windows virtual machines 관리](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)<br />- [Hyper-v 복제본 설정](manage/Set-up-Hyper-V-Replica.md)|
|![대화 거품 아이콘](media/All_Symbols_Chat.png)|**블로그**<br /><br />Microsoft 가상화 및 Hyper-v 팀의 프로그램 관리자, 제품 관리자, 개발자 및 테스터에서 최신 게시물을 확인 합니다.<br /><br />- [가상화 블로그](https://blogs.technet.com/b/virtualization/)<br />- [Windows Server 블로그](https://blogs.technet.com/b/windowsserver/)<br />- [Ben Armstrong의 가상화 블로그](https://blogs.msdn.com/b/virtual_pc_guy/) (보관)|
|![사용자 그룹 아이콘](media/All_Symbols_Users_Group.png)|**포럼 및 뉴스 그룹**<br /><br />궁금한 점이 있으십니까? 동료, Mvp, 및는 Hyper-v 제품 팀에 설명 합니다.<br /><br />- [Windows Server Community](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)<br />- [Windows Server Hyper-v TechNet 포럼](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverhyperv)|

## <a name="related-technologies"></a>관련 기술

다음 표에서 가상화 컴퓨팅 환경에서 사용 하려는 하는 기술을 보여 줍니다.

|기술|설명|
|--------------|---------------|
|[클라이언트 Hyper-v](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index)|Windows 8, Windows 8.1 및 Windows 10을 통해 설치할 수 있는 포함 된 가상화 기술로 **프로그램 및 기능** 에 **제어판**합니다.|
|[장애 조치 클러스터링](https://docs.microsoft.com/windows-server/failover-clustering/whats-new-in-failover-clustering)|Hyper-v 호스트 및 virtual machines에 대 한 고가용성을 제공 하는 Windows Server 기능입니다.|
|[Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)|가상화 된 데이터 센터 관리 솔루션을 제공 하는 system Center 구성 요소입니다. 구성 하 고 만들고를 사용자가 만든 사설 클라우드에 가상 컴퓨터 및 서비스를 배포할 수 있도록에 가상화 호스트, 네트워크 및 저장소 리소스를 관리할 수 있습니다.|
|[Windows 컨테이너](https://docs.microsoft.com/virtualization/windowscontainers/)|Windows Server 및 Hyper-v 컨테이너를 사용 하 여 개발, 테스트 및 프로덕션 팀에 대 한 표준화 된 환경을 제공 합니다.|