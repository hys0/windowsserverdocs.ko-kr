---
title: Microsoft Hyper-V Server 2016
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: KBDAzure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: 9a1b6ea7b9abc94f63a1390b6fa18e4c8d4a1822
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839374"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-v Server 2016은 독립\-만 Windows 하이퍼바이저, Windows Server 드라이버 모델 및 가상화 구성 요소를 포함 하는 단독으로 제품입니다. 에 서버 사용률을 높이고 비용을 절감할 수 있도록 간단 하 고 신뢰할 수 있는 가상화 솔루션을 제공 합니다.

Microsoft Hyper-v Server 2016의 Windows 하이퍼바이저 기술 같습니다 Hyper에 새로운\-Windows Server 2016에서 V 역할입니다. 따라서 대부분의 사용 가능한 Hyper에 대 한 콘텐츠\-V 역할 Windows Server 2016에서 Microsoft Hyper-v Server 2016에도 적용 됩니다.

## <a name="hyper-v-server-resources-for-it-pros"></a>하이퍼\-IT 전문가 위한 V 서버 리소스

|태스크|리소스|
|-|-|
|![기호 요구 사항 충족](media/All_Symbols_MeetsRequirements.png)|**Hyper-v가 설치를 평가 합니다.**<br /><br />-   [Hyper-v 기술 개요](hyper-v-technology-overview.md)<br />- [Windows Server 2016에서 Hyper-v의 새로운 기능](what-s-new-in-hyper-v-on-windows.md)<br />-   [Windows Server 2016에서 Hyper-v에 대 한 시스템 요구 사항](system-requirements-for-hyper-v-on-windows.md)<br />-   [Hyper-v에 대 한 지원 되는 Windows 게스트 운영 체제](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)<br />-   [지원 되는 Linux 및 FreeBSD Virtual Machines](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />-   [생성 및 게스트 별 기능 호환성](hyper-v-feature-compatibility-by-generation-and-guest.md)<br /><br />**Hyper-v에 대 한 계획**<br /><br />-결정할 [가상 머신 세대](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md) 요구 사항을 충족 합니다. <br/>-사용자가 이동 하거나 가상 컴퓨터를 가져오기, 경우를 결정 하는 경우 [버전을 업그레이드](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)합니다. <br />- [확장성](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [Networking](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [보안](plan/plan-hyper-v-security-in-windows-server.md)|
|![시작된 기호 가져오기](media/All_Symbols_GetStarted.png)|**Hyper-v Server 시작**<br /><br />[다운로드 및 설치 Microsoft 하이퍼\-V Server 2016](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016)합니다. 이 Windows 하이퍼바이저, Windows Server 드라이버 모델 및 가상화 구성 요소를 설치합니다. Windows Server 2016 및 Hyper의 Server Core 설치 옵션을 실행 하는 것과 비슷합니다\-V 역할입니다.|
|![기호를 관리 합니다.](media/All_Symbols_Administrator.png)|**구성 및 Hyper-v 서버를 관리 합니다.**<br /><br />하이퍼\-V Server 그래픽 사용자 인터페이스가 없는 \(GUI\)합니다. 다음 도구를 사용 하 여 구성 하 고 하이퍼 관리할\-V 서버.<br /><br />-   [Sconfig.cmd로 Windows Server 2016의 Server Core 설치 구성](../../get-started/sconfig-on-ws2016.md) 도메인 또는 작업 그룹 설정을 업데이트 하려면 Windows 업데이트 설정, 원격 관리를 사용 하는, 및 기타 변경 합니다.<br />--일반적인을 사용 하는 중 [명령 프롬프트](../../administration/windows-commands/windows-commands.md) Sconfig에서 사용할 수 없는 명령에 대 한 합니다.<br />-사용 [하이퍼\-V 관리자](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/remote_host_management) 하거나 [Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm) 하이퍼를 관리할 수\-V 서버. 사용할 하이퍼\-V 관리자 [하이퍼를 설치할\-Windows 10에서 V 역할](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) 또는 [Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md).<br />-참조 [Server Core 설치](../../get-started/getting-started-with-server-core.md) 하이퍼 관련이 없는 기본 서버 기능에 대 한 추가 관리 옵션에 대 한\-V. 또한 하이퍼 있습니다 문서화 관리 메서드 중 대부분은와 함께\-V 서버.<br /><br />**구성 및 관리 하이퍼\-가상 머신**<br /><br />-   [Hyper-v 가상 컴퓨터에 대 한 가상 스위치 만들기](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />-   [Hyper-v에서 가상 머신 만들기](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [표준 또는 프로덕션 검사점 간의 선택](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)<br />-   [검사점을 사용할지 설정 합니다.](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />-   [PowerShell Direct를 사용 하 여 Windows virtual machines 관리](manage/manage-windows-virtual-machines-with-powershell-direct.md) <br /><br />**배포**<br /><br />-   [장애 조치 클러스터링이 없는 실시간 마이그레이션에 대해 호스트 설정](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [Windows Server 클러스터 노드를 업그레이드 합니다.](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />- [가상 머신 버전 업그레이드](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)<br />|
