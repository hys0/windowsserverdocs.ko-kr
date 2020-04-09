---
title: 원격 액세스 서버의 구성 배포 상태 모니터링
description: 이 항목은 Windows Server 2016의 원격 액세스 모니터링 및 계정에 대 한 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: de285d13-9e54-4c46-88f0-607182e5e3dc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 19c3d9c306215c92edb2bf322e722a93f9962738
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854036"
---
# <a name="monitor-the-configuration-distribution-status-of-the-remote-access-server"></a>원격 액세스 서버의 구성 배포 상태 모니터링

>적용 대상: Windows Server(반기 채널), Windows Server 2016

**참고:** Windows Server 2012 DirectAccess 및 원격 액세스 서비스 (RAS)를 단일 원격 액세스 역할로 결합 합니다.  
  
원격 액세스 관리 콘솔에서는 모든 모니터링 대상 서버의 구성 버전을 비교하여 구성 버전이 일치하고 최신 구성 버전을 사용하는지 확인합니다. 여기에는 GPO(그룹 정책 개체)에 지정된 최신 구성 버전이 모든 서버에 배포되었는지 여부 및 서버에서 성공적으로 적용되었는지 여부가 표시됩니다.  
  
### <a name="to-use-the-monitoring-dashboard-to-monitor-the-configuration-distribution"></a>모니터링 대시보드를 사용하여 구성 배포를 모니터링하려면  
  
1.  **서버 관리자**, 클릭 **도구**, 를 클릭 하 고 **원격 액세스 관리**합니다.  
  
2.  **대시보드**를 클릭하여 **원격 액세스 관리 콘솔**의 **원격 액세스 대시보드**로 이동합니다.  
  
3.  모니터링 대시보드의 가운데 위에 **구성 상태** 타일이 있습니다. 이 타일에는 구성 배포의 현재 상태가 표시됩니다.  
  
다음 표에는 **구성 상태** 타일에서 생성되는 메시지, 메시지의 의미 및 필요한 관리 작업(있는 경우)이 나와 있습니다.  
  
|||||  
|-|-|-|-|  
|Severity|메시지|의미|수행할 작업|  
|성공|구성이 분배되었습니다.|GPO의 구성이 서버에 성공적으로 적용되었습니다.|작업이 필요하지 않습니다.|  
|경고|[*server name*] 서버에 대한 구성이 도메인 컨트롤러에서 검색되지 않았습니다. GPO가 연결되어 있지 않습니다.|GPO의 구성이 서버에 아직 전달되지 않았습니다. 이는 GPO가 서버에 연결되지 않았기 때문일 수 있습니다.|GPO를 서버에 적용되는 관리 범위에 연결하거나, 준비 GPO 시나리오의 경우 준비 GPO에서 설정을 수동으로 내보내고 프로덕션 GPO로 가져옵니다. 준비 Gpo에 대 한 자세한 내용은 **원격 액세스 Gpo 관리에서 제한 된 권한으로 원격 액세스 Gpo 관리** -- [--DirectAccess-인프라](../../directaccess/single-server-advanced/Step-1-Plan-the-DirectAccess-Infrastructure.md)를 참조 하세요. GPO 스테이징 단계는 [1 단계: DirectAccess 인프라 구성](../../directaccess/single-server-advanced/Step-1-Configuring-DirectAccess-Infrastructure.md)에서 **제한 된 권한으로 원격 액세스 gpo 구성** 을 참조 하세요.|  
|경고|도메인 컨트롤러에서 [*server name*] 서버에 대한 구성이 아직 검색되지 않았습니다.|GPO의 구성이 서버에 아직 전달되지 않았습니다.<p>새 구성을 전파하는 데 최대 10분이 걸릴 수 있습니다.|서버에서 정책이 업데이트될 때까지 좀 더 기다립니다.|  
|오류|도메인 컨트롤러에서 [*server name*] 서버에 대한 구성을 검색할 수 없습니다.|GPO의 구성이 서버에 전달되지 않았으며 구성이 변경된 후 10분이 넘게 경과했습니다.|이 문제는 다음 시나리오 중 하나에서 발생할 수 있습니다.<p>-서버는 정책을 업데이트 하기 위해 도메인에 연결 되지 않습니다. 서버에서 "gpupdate/force"를 실행 하 여 정책을 강제로 업데이트할 수 있습니다.<br />-GPO 복제가 업데이트 된 구성을 검색 하는 데 필요할 수 있습니다.<br />-원격 액세스 서버의 Active Directory 사이트에 쓰기 가능한 도메인 컨트롤러가 없습니다.<p>GPO가 모든 도메인 컨트롤러에 복제될 때까지 기다린 후 Windows PowerShell cmdlet **Set-DAEntryPointDC**를 사용하여 원격 액세스 서버의 Active Directory에 있는 쓰기 가능 도메인 컨트롤러와 진입점을 연결합니다.|  
|경고|도메인 컨트롤러에서 [*server name*] 서버에 대한 구성이 검색되었지만 아직 적용되지 않았습니다.|GPO의 구성이 서버에 전달되었지만 아직 적용되지 않았습니다.<p>구성이 적용되는 데 최대 15분이 걸릴 수 있습니다.|구성이 서버에 완전히 적용될 때까지 좀 더 기다립니다.|  
|오류|도메인 컨트롤러에서 [*server name*] 서버에 대한 구성이 검색되었지만 적용할 수 없습니다.|GPO의 구성이 서버에 전달되었지만 제대로 적용되지 않았습니다. 구성이 변경된 후 15분이 넘게 경과했습니다.|이 문제는 다음 시나리오 중 하나에서 발생할 수 있습니다.<p>1. 구성이 현재 적용 되 고 있습니다. GPO에서 구성을 검색하는 데 더 오래 걸릴 수 있으므로 오류로 표시된 것입니다.<br />    문제의 원인이 이것인지 확인하려면 **작업 Scheduler**에서 Microsoft\Windows\RemoteAccess로 이동하여 **RAConfigTask**가 현재 실행되고 있는지 확인합니다.<br />2. **RAConfigTask** 가 현재 실행 되 고 있지 않으면 서버에 구성을 적용 하지 못할 수 있습니다.<br />    **이벤트 뷰어**의 원격 액세스 서버 작업 채널(\Applications and Services Logs\Microsoft\Windows\RemoteAccess-RemoteAccessServer) 아래에서 오류를 확인합니다.<br />    원격 액세스 관리 콘솔의 **작업 상태**에서 오류를 확인합니다. 자세한 내용은 [원격 액세스 서버 및 해당 구성 요소의 작동 상태 모니터링](Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components.md)을 참조하세요.|  
|오류|멀티 사이트 서버에 대한 구성이 도메인 컨트롤러에서 검색되었습니다. 구성이 모든 서버에서 일치하지는 않습니다.|멀티 사이트 배포의 서버 GPO 구성 버전이 일치하지 않습니다.<p>모든 진입점에 대한 모든 서버 GPO의 전역 구성이 동일한 것이 가장 좋지만 동기화되지 않는 경우가 있습니다.|이는 구성 변경에 실패하고 구성이 제대로 롤백되지 않은 경우에 발생할 수 있습니다.<p>모든 서버 GPO가 동기화된 백업 상태에서 GPO를 복원해야 합니다. 사용할 수 있는 스크립트에 대한 정보는 [원격 액세스 구성 백업 및 복원](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)을 참조하세요.|  
  


