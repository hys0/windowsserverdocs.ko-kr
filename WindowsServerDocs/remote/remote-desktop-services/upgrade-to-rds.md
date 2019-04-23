---
title: Windows Server 2016으로 업그레이드 하는 원격 데스크톱 서비스 배포
description: 이 문서에서는 기존 원격 데스크톱 서비스 배포 Windows Server 2016으로 업그레이드 하는 방법을 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 03/20/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7b1f1f6-57c8-40ab-a235-e36240dcc1f8
author: spatnaik
manager: scottman
notes: https://social.technet.microsoft.com/wiki/contents/articles/22069.remote-desktop-services-upgrade-guidelines-for-windows-server-2012-r2.aspx
ms.openlocfilehash: f683a7d9346494e7f1fb6faf716ca9c90cfef8d3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875754"
---
# <a name="upgrading-your-remote-desktop-services-deployments-to-windows-server-2016"></a>Windows Server 2016으로 업그레이드 하는 원격 데스크톱 서비스 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 역할이 설치 된 OS 업그레이드를 지원
Windows Server 2016으로 업그레이드는 Windows Server 2012 R2 및 Windows Server 2016 에서만 지원 됩니다.

## <a name="flow-for-deployment-upgrades"></a>배포 업그레이드에 대 한 흐름
다운 타임을 최소한으로를 유지 하기 위해 다음 단계를 수행 하는 것이 좋습니다.

1. **RD 연결 브로커 서버** 업그레이드 해야 할 첫 번째 메시지 여야 합니다. 배포에 활성/활성 설정이 있는 경우 배포에서 하나를 제외한 모든 서버를 제거 하 고 현재 위치 업그레이드를 수행 합니다. 나머지 RD 연결 브로커 서버를 오프 라인에서 업그레이드를 수행 하 고 배포에 다시 추가 합니다. RD 연결 브로커 서버 업그레이드 중에 배포는 사용할 수 없습니다.

   > [!NOTE] 
   > RD 연결 브로커 서버를 업그레이드 하는 것이 반드시 합니다. Windows Server 2012 R2 RD 연결 브로커 서버에서 Windows Server 2016 서버를 사용 하 여 혼합된 배포를 지원 하지 않습니다. Windows Server 2016를 실행 하는 RD 연결 브로커 서버는 나머지 배포의 서버는 계속 Windows Server 2012 R2를 실행 하는 경우에 배포 작동 됩니다.

2. **RD 라이선스 서버** RD 세션 호스트 서버를 업그레이드 하기 전에 업그레이드 해야 합니다.
   > [!NOTE] 
   > Windows Server 2016 배포를 사용 하 여 Windows Server 2012 및 2012 R2 RD 라이선스 서버가 작동 하지만 Windows Server 2012 R2에서 오래 된 Cal만 처리할 수 있는 합니다. Windows Server 2016 Cal를 사용할 수 없습니다. 참조 [클라이언트 액세스 라이선스 (Cal)를 사용 하 여 RDS 배포 라이선스](rds-client-access-license.md) RD 라이선스 서버에 대 한 자세한 내용은 합니다.

3. **RD 세션 호스트 서버** 다음 업그레이드할 수 있습니다. 업그레이드 하는 동안 중단을 방지 하려면 관리자는 아래 설명 된 대로 2 단계에서 업그레이드할 서버를 분할할 수 있습니다. 업그레이드 후 기능을 수는 모든. 를 업그레이드 하려면에 설명 된 단계를 사용 하 여 [Windows Server 2016으로 업그레이드 원격 데스크톱 세션 호스트 서버](upgrade-to-rdsh.md)합니다.

4. **RD 가상화 호스트 서버** 다음 업그레이드할 수 있습니다. 를 업그레이드 하려면에 설명 된 단계를 사용 하 여 [Windows Server 2016으로 업그레이드 원격 데스크톱 가상화 호스트 서버](upgrade-to-rdvh.md)합니다.

5. **RD 웹 액세스 서버** 언제 든 지 업그레이드할 수 있습니다.
   > [!NOTE]
   > RD 웹 업그레이드 IIS 속성 (예: 모든 구성 파일)를 다시 설정 될 수 있습니다. 변경 내용을 손실 하지, 메모 또는 IIS에서 RD 웹 사이트에 수행 하는 사용자 지정 항목의 복사본을 확인 합니다.

   > [!NOTE] 
   > Windows Server 2012 및 2012 R2 RD 웹 액세스 서버는 Windows Server 2016 배포를 사용 하 여 작동 합니다.

6. **RD 게이트웨이 서버** 언제 든 지 업그레이드할 수 있습니다.
   > [!NOTE]
   > Windows Server 2016에는 네트워크 액세스 보호 (NAP) 정책이 없는-제거 해야 합니다. 올바른 정책을 제거 하는 가장 쉬운 방법은 업그레이드 마법사를 실행 하 여 됩니다. 삭제 해야 하는 NAP 정책을 업그레이드를 차단 하 고 특정 정책을 포함 하는 바탕 화면에서 텍스트 파일을 만듭니다. NAP 정책을 관리 하려면 네트워크 정책 서버 도구를 엽니다. 클릭을 삭제 한 후 **새로 고침** 업그레이드 프로세스를 계속 설치 도구에서. 

   > [!NOTE] 
   > Windows Server 2012 및 2012 R2 RD 게이트웨이 서버는 Windows Server 2016 배포를 사용 하 여 작동 합니다.

## <a name="vdi-deployment--supported-guest-os-upgrade"></a>VDI 배포-지원 되는 게스트 OS 업그레이드
관리자가 VM 컬렉션을 업그레이드 하려면 다음 옵션 해야 합니다.

### <a name="upgrade-managed-shared-vm-collections"></a>관리 되는 공유 VM 컬렉션 업그레이드 
관리자는 원하는 OS 버전을 사용 하 여 VM 템플릿 만들기 및 풀의 모든 Vm을 패치를 사용 해야 합니다. 

다음 패치 시나리오를 지원합니다.
- Windows 8 또는 Windows 8.1 Windows 7 SP1은 패치할 수 있습니다.
- Windows 8.1 Windows 8은 패치할 수 있습니다.
- Windows 10에 Windows 8.1 패치할 수 있습니다.

### <a name="upgrade-unmanaged-shared-vm-collections"></a>관리 되지 않는 공유 VM 컬렉션 업그레이드 
최종 사용자가 개인 데스크톱을 업그레이드할 수 없습니다. 관리자는 업그레이드를 수행 해야 합니다. 정확한 단계는 결정 해야 하는 계속 됩니다.