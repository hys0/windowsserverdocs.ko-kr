---
title: Microsoft Hyper-V Server 2016
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: KBDAzure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: c9e1b5e2d30276bf89bc2d56482ec76d1c2241a2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365579"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-V Server 2016는 Windows 하이퍼바이저, Windows Server 드라이버 모델 및 가상화 구성 요소만 포함 하는 독립형 @ no__t-0alone 제품입니다. 서버 사용률을 개선 하 고 비용을 절감 하는 데 도움이 되는 간단 하 고 신뢰할 수 있는 가상화 솔루션을 제공 합니다.

Microsoft Hyper-V Server 2016의 Windows 하이퍼바이저 기술은 Windows Server 2016의 하이퍼 @ no__t-0V 역할에 있는 것과 동일 합니다. 따라서 Windows Server 2016의 하이퍼 @ no__t-0V 역할에 사용 가능한 대부분의 콘텐츠는 Microsoft Hyper-V Server 2016에도 적용 됩니다.

## <a name="hyper-v-server-resources-for-it-pros"></a>IT 전문가를 위한 하이퍼 @ no__t-0V 서버 리소스

|태스크|리소스|
|-|-|
|![요구 사항에 맞는 기호](media/All_Symbols_MeetsRequirements.png)|**Hyper-v 평가**<br /><br />-   [Hyper-v 기술 개요](hyper-v-technology-overview.md)<br />- [Windows Server 2016에서 제공 되는 hyper-v의 새로운](what-s-new-in-hyper-v-on-windows.md) 기능<br />@no__t-[Windows Server 2016의 hyper-v에 대 한 시스템 요구 사항](system-requirements-for-hyper-v-on-windows.md) 0<br />@no__t-[hyper-v에 대해 지원 되는 Windows 게스트 운영 체제](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md) 0<br />@no__t[지원 되는 Linux 및 FreeBSD Virtual Machines](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />@no__t-[세대 및 게스트 별 기능 호환성](hyper-v-feature-compatibility-by-generation-and-guest.md)<br /><br />**Hyper-v 계획**<br /><br />-사용자의 요구를 충족 하는 [가상 머신 생성](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md) 을 결정 합니다. <br/>-가상 컴퓨터를 이동 하거나 가져오는 경우 [버전을 업그레이드할](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)시기를 결정 합니다. <br />- [확장성](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [네트워킹](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [보안](plan/plan-hyper-v-security-in-windows-server.md)|
|![시작 기호](media/All_Symbols_GetStarted.png)|**Hyper-v 서버 시작**<br /><br />[Microsoft 하이퍼 @ no__t-1V Server 2016를 다운로드 하 여 설치](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016)합니다. 그러면 Windows 하이퍼바이저, Windows Server 드라이버 모델 및 가상화 구성 요소가 설치 됩니다. Windows Server 2016 및 하이퍼 @ no__t-0V 역할의 Server Core 설치 옵션을 실행 하는 것과 유사 합니다.|
|![기호 관리](media/All_Symbols_Administrator.png)|**Hyper-v 서버 구성 및 관리**<br /><br />하이퍼 @ no__t-0V 서버에 \(GUI @ no__t-2의 그래픽 사용자 인터페이스가 없습니다. 다음 도구를 사용 하 여 하이퍼 @ no__t-0V 서버를 구성 하 고 관리할 수 있습니다.<br /><br />-    도메인 또는 작업 그룹 설정을 업데이트 하 고, Windows 업데이트 설정을 변경 하 고, 원격 관리를 사용 하도록 설정 하려면[Windows server 2016의 Server Core 설치를 구성 합니다.](../../get-started/sconfig-on-ws2016.md)<br />-Sconfig에서 사용할 수 없는 명령에 일반적인 [명령 프롬프트](../../administration/windows-commands/windows-commands.md) 를 사용 합니다.<br />-하이퍼 [@ no__t-1V 관리자](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/remote_host_management) 또는 [Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm) 를 사용 하 여 원격으로 hyper-v no__t hyper-v 서버를 관리 합니다. 하이퍼 @ no__t-0V Manager를 사용 하려면 Windows 10 또는 [Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md) [에 hyper-v 역할을 설치](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) 합니다.<br />-Hyper-v와 관련 없는 기본 서버 기능에 대 한 추가 관리 옵션은 [Server Core 설치](../../get-started/getting-started-with-server-core.md) 를 참조 하세요. 문서화 된 대부분의 관리 방법은 하이퍼 @ no__t-0V 서버 에서도 작동 합니다.<br /><br />**하이퍼 @ no__t-1V 가상 컴퓨터 구성 및 관리**<br /><br />-   [hyper-v 가상 컴퓨터에 대 한 가상 스위치 만들기](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />-   [hyper-v에서 가상 컴퓨터 만들기](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [표준 또는 프로덕션 검사점 중에서 선택](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)<br />-   [검사점 사용 또는 사용 안 함](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />-   [PowerShell Direct를 사용 하 여 Windows 가상 머신 관리](manage/manage-windows-virtual-machines-with-powershell-direct.md) <br /><br />**배포**<br /><br />-   [장애 조치 (Failover) 클러스터링이 없는 실시간 마이그레이션에 대 한 호스트 설정](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [Windows Server 클러스터 노드 업그레이드](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />- [업그레이드 가상 컴퓨터 버전](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)<br />|
