---
title: Windows Server 2016으로 원격 데스크톱 서비스 배포 업그레이드
description: 이 문서에서는 기존 원격 데스크톱 서비스 배포를 Windows Server 2016으로 업그레이드하는 방법을 설명합니다.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 29648db89b61a9d22aad6d5aa814cfe7f425a970
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78370688"
---
# <a name="upgrading-your-remote-desktop-services-deployments-to-windows-server-2016"></a>Windows Server 2016으로 원격 데스크톱 서비스 배포 업그레이드

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 역할이 설치된 지원되는 OS 업그레이드
Windows Server 2016으로의 업그레이드는 Windows Server 2012 R2 및 Windows Server 2016에서만 지원됩니다.

## <a name="flow-for-deployment-upgrades"></a>배포 업그레이드에 대한 흐름
가동 중지 시간을 최소한으로 유지하려면 아래 단계를 수행하는 것이 좋습니다.

1. **RD 연결 브로커 서버**는 가장 먼저 업그레이드해야 합니다. 배포에 활성/활성 설정이 있는 경우 배포에서 서버를 하나만 제외한 모든 서버를 제거하고 현재 위치 업그레이드를 수행합니다. 나머지 RD 연결 브로커 서버에서 오프라인으로 업그레이드를 수행한 다음, 배포에 다시 추가합니다. RD 연결 브로커 서버를 업그레이드하는 동안에는 배포를 사용할 수 없습니다.

   > [!NOTE] 
   > RD 연결 브로커 서버를 업그레이드해야 합니다. Windows Server 2016 서버와의 혼합 배포에서는 Windows Server 2012 R2 RD 연결 브로커 서버를 지원하지 않습니다. RD 연결 브로커 서버가 Windows Server 2016을 실행하면 배포에 포함된 나머지 서버가 여전히 Windows Server 2012 R2를 실행하고 있더라도 배포가 작동합니다.

2. **RD 라이선스 서버**는 RD 세션 호스트 서버를 업그레이드하기 전에 업그레이드해야 합니다.
   > [!NOTE] 
   > Windows Server 2012 및 2012 R2 RD 라이선스 서버는 Windows Server 2016 배포와 함께 작동하지만 Windows Server 2012 R2 이전 버전의 CAL만 처리할 수 있습니다. Windows Server 2016 CAL은 사용할 수 없습니다. RD 라이선스 서버에 대한 자세한 내용은 [CAL(클라이언트 액세스 라이선스)로 RDS 배포 라이선싱](rds-client-access-license.md)을 참조하세요.

3. 다음으로 **RD 세션 호스트 서버**를 업그레이드할 수 있습니다. 업그레이드하는 동안 가동 중지 시간을 방지하기 위해 관리자는 아래 설명된 것처럼 업그레이드할 서버를 2단계로 분할할 수 있습니다. 모든 기능은 업그레이드 후 작동됩니다. 업그레이드하려면 [Windows Server 2016으로 원격 데스크톱 세션 호스트 서버 업그레이드](upgrade-to-rdsh.md)에 설명된 단계를 사용합니다.

4. 다음으로 **RD 가상화 호스트 서버**를 업그레이드할 수 있습니다. 업그레이드하려면 [Windows Server 2016으로 원격 데스크톱 가상화 호스트 서버 업그레이드](upgrade-to-rdvh.md)에 설명된 단계를 사용합니다.

5. **RD 웹 액세스 서버**는 언제든지 업그레이드할 수 있습니다.
   > [!NOTE]
   > RD 웹 업그레이드는 IIS 속성(예: 모든 구성 파일)을 다시 설정할 수도 있습니다. 변경 내용을 잃지 않으려면 IIS의 RD 웹 사이트에 수행된 사용자 지정을 적어두거나 복사본을 만들어두세요.

   > [!NOTE] 
   > Windows Server 2012 및 2012 R2 RD 웹 액세스 서버는 Windows Server 2016 배포와 함께 작동합니다.

6. **RD 게이트웨이 서버**는 언제든지 업그레이드할 수 있습니다.
   > [!NOTE]
   > Windows Server 2016에는 NAP(네트워크 액세스 보호) 정책이 포함되어 있지 않습니다. 제거해야 하는 항목입니다. 올바른 정책을 제거하는 가장 쉬운 방법은 업그레이드 마법사를 실행하는 것입니다. 삭제해야 하는 NAP 정책이 있는 경우, 업그레이드는 데스크톱에서 특정 정책을 포함하는 텍스트 파일을 차단하고 생성합니다. NAP 정책을 관리하려면 네트워크 정책 서버 도구를 엽니다. 삭제한 후, 설정 도구에서 **새로 고침**을 클릭하여 업그레이드 프로세스를 계속 진행합니다. 

   > [!NOTE] 
   > Windows Server 2012 및 2012 R2 RD 게이트웨이 서버는 Windows Server 2016 배포와 함께 작동합니다.

## <a name="vdi-deployment--supported-guest-os-upgrade"></a>VDI 배포 - 지원되는 게스트 OS 업그레이드
관리자는 VM 컬렉션을 업그레이드하기 위해 다음과 같은 옵션을 사용할 수 있습니다.

### <a name="upgrade-managed-shared-vm-collections"></a>관리형 공유 VM 컬렉션 업그레이드 
관리자는 원하는 OS 버전으로 VM 템플릿을 생성하고 이를 사용하여 풀의 모든 VM을 패치해야 합니다. 

다음 패치 시나리오를 지원합니다.
- Windows 7 SP1은 Windows 8 또는 Windows 8.1에 패치할 수 있습니다.
- Windows 8은 Windows 8.1에 패치할 수 있습니다.
- Windows 8.1은 Windows 10에 패치할 수 있습니다.

### <a name="upgrade-unmanaged-shared-vm-collections"></a>비관리형 공유 VM 컬렉션 업그레이드 
최종 사용자가 개인 데스크톱을 업그레이드할 수는 없습니다. 관리자가 업그레이드를 수행해야 합니다. 정확한 단계는 아직 결정되지 않았습니다.