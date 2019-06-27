---
ms.assetid: 2bab6bf6-90e7-46a7-b917-14a7a8f55366
title: Windows의 저장소 클래스 메모리(NVDIMM-N) 상태 관리
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: JasonGerend
ms.date: 06/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4ebec8618c79c43816680387ae5e495f125b3c54
ms.sourcegitcommit: 545dcfc23a81943e129565d0ad188263092d85f6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67407559"
---
# <a name="storage-class-memory-nvdimm-n-health-management-in-windows"></a>Windows의 저장소 클래스 메모리(NVDIMM-N) 상태 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널), Windows 10

이 문서에서는 시스템 관리자 및 IT 전문가에게 저장소 클래스 메모리와 기존 저장 장치 간의 차이점을 중심으로 Windows의 저장소 클래스 메모리(NVDIMM-N) 장치에 특정한 오류 처리 및 상태 관리에 대한 정보를 제공합니다.

Windows의 저장소 클래스 메모리 장치 지원에 익숙하지 않은 경우 다음의 짧은 비디오에서 개요를 확인할 수 있습니다.
- [Windows Server 2016에서에서 블록 저장소로 비휘발성 메모리 (Nvdimm-n) 사용](https://channel9.msdn.com/Events/Build/2016/P466)
- [Windows Server 2016에서에서 바이트 주소 지정 가능 저장소로 비휘발성 메모리 (Nvdimm-n) 사용](https://channel9.msdn.com/Events/Build/2016/P470)
- [Windows Server 2016에서 영구 메모리로 SQL Server 2016 성능 가속화](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-Windows-Server-2016-SCM--FAST)

도 참조 하세요 [이해 하 고 영구 메모리 저장소 공간 다이렉트 배포](deploy-pmem.md)합니다.

JEDEC 규격 NVDIMM-N 저장소 클래스 메모리 장치는 Windows Server 2016 및 Windows 10(버전 1607)부터 기본 드라이버를 통해 Windows에서 지원됩니다. 이러한 장치는 다른 디스크(HDD 및 SSD)와 유사하게 동작하지만 몇 가지 차이점이 있습니다.

여기에 나열된 모든 조건은 매우 드물게 발생하지만 하드웨어가 사용되는 조건에 따라 다릅니다.

아래의 다양한 사례는 저장소 공간 구성을 나타낼 수도 있습니다. 관심이 있는 특정 구성은 NVDIMM-N 장치가 저장소 공간에서 미러링된 나중 쓰기 캐시로 활용되는 구성입니다. 이러한 구성을 설정하려면 [NVDIMM-N 나중 쓰기 캐시로 저장소 공간 구성](https://msdn.microsoft.com/library/mt650885.aspx)을 참조하세요.

Windows Server 2016에서 저장소 공간 GUI는 NVDIMM-N 버스 유형을 알 수 없음으로 표시합니다. 이로 인한 기능 손실이나 풀, 저장소 VD 만들기에 지장은 없습니다. 다음 명령을 실행하며 버스 유형을 확인할 수 있습니다.

```powershell
PS C:\>Get-PhysicalDisk | fl
```
cmdlet 출력에서 매개 변수 BusType이 버스 유형을 "SCM"으로 올바르게 표시합니다.

## <a name="checking-the-health-of-storage-class-memory"></a>저장소 클래스 메모리의 상태 확인
저장소 클래스 메모리의 상태를 쿼리하려면 Windows PowerShell 세션에서 다음 명령을 사용합니다.

```powershell
PS C:\> Get-PhysicalDisk | where BusType -eq "SCM" | select SerialNumber, HealthStatus, OperationalStatus, OperationalDetails
```

그러면 다음 예와 같은 출력이 생성됩니다.

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | 정상 | 확인 | |
| 802c-01-1602-117cb64f | 경고 | 자동 완성 오류 | {Threshold Exceeded,NVDIMM\_N Error} |

> [!NOTE]
> 이벤트에서 지정된 NVDIMM-N 장치의 물리적 위치를 찾으려면 이벤트 뷰어의 이벤트에 있는 **세부 정보** 탭에서 **EventData** > **위치**로 이동합니다. Windows Server 2016은 NVDIMM-N 장치의 잘못된 위치를 나열하지만 이는 Windows Server, 버전 1709에서 수정되었습니다.

다양한 상태 조건을 이해하는 데 도움이 되도록 다음 섹션을 참조하세요.

## <a name="warning-health-status"></a>"Warning" 상태

이 조건은 저장소 클래스 메모리 장치의 상태를 확인할 때 다음 출력 예와 같이 상태가 **Warning**으로 나열되는 경우에 해당합니다.

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | 정상 | 확인 | |
| 802c-01-1602-117cb64f | 경고 | 자동 완성 오류 | {Threshold Exceeded,NVDIMM\_N Error} |

다음 표에 이 조건에 대한 몇 가지 정보가 나와 있습니다.

| | 설명 |
| --- | --- |
| 가능한 조건 | NVDIMM-N 경고 임계값 위반 |
| 근본 원인 | NVDIMM-N 장치는 온도, NVM 수명 및/또는 에너지원 수명과 같은 여러 임계값을 추적합니다. 이러한 임계값 중 하나가 초과되면 운영 체제에 알림이 제공됩니다. |
| 일반적인 동작 | 장치가 정상적으로 작동합니다. 이는 오류가 아니라 경고입니다. |
| 저장소 공간 동작 | 장치가 정상적으로 작동합니다. 이는 오류가 아니라 경고입니다. |
| 추가 정보 | PhysicalDisk 개체의 OperationalStatus 필드. EventLog – Microsoft-Windows-ScmDisk0101/Operational |
| 수행할 작업 | 위반한 경고 임계값에 따라 NVDIMM-N의 특정 부분 또는 전체를 교체하는 것이 현명할 수 있습니다. 예를 들어 NVM 수명 임계값을 위반한 경우 NVDIMM-N을 교체하는 것이 좋습니다. |

## <a name="writes-to-an-nvdimm-n-fail"></a>NVDIMM-N에 쓰기 실패

이 조건은 저장소 클래스 메모리 장치의 상태를 확인할 때 다음 출력 예와 같이 상태가 **Unhealthy**로 나열되고 작동 상태에 **IO Error**가 표시되는 경우에 해당합니다.

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
| 802c-01-1602-117cb5fc | 정상 | 확인 | |
| 802c-01-1602-117cb64f | Unhealthy | {Stale Metadata, IO Error, Transient Error} | {Lost Data Persistence, Lost Data, NV...} |

다음 표에 이 조건에 대한 몇 가지 정보가 나와 있습니다.

| | 설명 |
| --- | --- |
| 가능한 조건 | 지속성 손실/백업 전원 |
|근본 원인|NVDIMM-N 장치는 지속성을 위해 백업 전원(일반적으로 배터리 또는 수퍼 커패시터)에 의존합니다. 이 백업 전원을 사용할 수 없거나 장치에서 어떤 이유로든(컨트롤러/플래시 오류) 백업을 수행할 수 없는 경우 데이터가 위험에 노출되고 Windows에서 영향을 받는 장치에 대한 추가적인 쓰기를 방지합니다. 읽기는 여전히 가능하므로 데이터를 이동할 수는 있습니다.|
|일반적인 동작|NTFS 볼륨이 분리됩니다.<br>PhysicalDisk Health Status 필드에 영향을 받는 모든 NVDIMM-N 장치의 상태가 “Unhealthy”로 표시됩니다.|
|저장소 공간 동작|하나의 NVDIMM-N만 영향을 받는 경우 저장소 공간은 계속 작동합니다. 여러 장치가 영향을 받는 경우 저장소 공간에 대한 쓰기가 실패합니다. <br>PhysicalDisk Health Status 필드에 영향을 받는 모든 NVDIMM-N 장치의 상태가 “Unhealthy”로 표시됩니다.|
|추가 정보|PhysicalDisk 개체의 OperationalStatus 필드.<br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|수행할 작업|영향을 받는 NVDIMM-N의 데이터를 백업하는 것이 좋습니다. 읽기 권한을 얻으려면 디스크를 수동으로 온라인 상태로 전환하면 됩니다(디스크가 읽기 전용 NTFS 볼륨으로 표시됨).<br><br>이 조건을 완전히 해소하려면 근본 원인을 해결(즉, 문제에 따라 전원 공급 장치를 수리하거나 NVDIMM-N을 교체)하고 NVDIMM-N의 볼륨을 오프라인으로 전환했다가 다시 온라인으로 전환하거나 시스템을 다시 시작해야 합니다.<br><br>저장소 공간에서 NVDIMM-N을 다시 사용할 수 있도록 하려면 **Reset-PhysicalDisk** cmdlet을 사용하여 장치를 다시 통합하고 복구 프로세스를 시작합니다.|

## <a name="nvdimm-n-is-shown-with-a-capacity-of-0-bytes-or-as-a-generic-physical-disk"></a>NVDIMM-N이 "Generic Physical Disk"로 표시되거나 해당 용량이 '0'바이트로 표시됨

이 조건은 저장소 클래스 메모리 장치가 0바이트 용량으로 표시되어 초기화할 수 없거나, 다음 출력 예와 같이 작동 상태가 **Lost Communication**인 "Generic Physical Disk" 개체로 노출되는 경우에 해당합니다.

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
|802c-01-1602-117cb5fc|정상|확인||
||경고|Lost Communication||

다음 표에 이 조건에 대한 몇 가지 정보가 나와 있습니다.

||설명|
|---|---|
|가능한 조건|BIOS가 NVDIMM-N을 OS에 노출하지 않음|
|근본 원인|NVDIMM-N 장치는 DRAM을 기반으로 합니다. 손상된 DRAM 주소가 참조된 경우 대부분의 CPU는 컴퓨터 검사를 시작하고 서버를 다시 시작합니다. 그러면 일부 서버 플랫폼에서는 NVDIMM의 매핑을 해제하여 OS의 액세스를 방지하고 잠재적으로 또 다른 컴퓨터 검사가 실행되도록 합니다. 이는 BIOS에서 NVDIMM-N에 장애가 발생하여 교체해야 함을 감지한 경우에도 발생할 수 있습니다.|
|일반적인 동작|NVDIMM-N이 0바이트 용량으로 초기화되지 않은 것으로 표시되며 읽거나 쓸 수 없게 됩니다.|
|저장소 공간 동작|저장소 공간은 계속 작동합니다(하나의 NVDIMM-N만 영향을 받는 경우).<br>NVDIMM-N PhysicalDisk 개체가 "General Physical Disk"로 표시되고 해당 상태에 Warning이 표시됩니다.|
|추가 정보|PhysicalDisk 개체의 OperationalStatus 필드. <br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|수행할 작업|서버 플랫폼에서 NVDIMM-N 장치를 호스트 OS에 다시 노출할 수 있도록 NVDIMM-N 장치를 교체하거나 삭제해야 합니다. 수정할 수 없는 오류가 추가로 발생할 수 있으므로 장치를 교체하는 것이 좋습니다. 교체 장치를 저장소 공간 구성에 추가하려면 **Add-Physicaldisk** cmdlet을 사용하면 됩니다.|

## <a name="nvdimm-n-is-shown-as-a-raw-or-empty-disk-after-a-reboot"></a>다시 부팅한 후 NVDIMM-N이 RAW 또는 빈 디스크로 표시됨

이 조건은 저장소 클래스 메모리 장치의 상태를 확인할 때 다음 출력 예와 같이 상태가 **Unhealthy**로 표시되고 작동 상태에 **Unrecognized Metadata**가 표시되는 경우에 해당합니다.

| SerialNumber | HealthStatus | OperationalStatus | OperationalDetails |
| --- | --- | --- | --- |
|802c-01-1602-117cb5fc|정상|확인|{Unknown}|
|802c-01-1602-117cb64f|Unhealthy|{Unrecognized Metadata, Stale Metadata}|{Unknown}|

다음 표에 이 조건에 대한 몇 가지 정보가 나와 있습니다.

||설명|
|---|---|
|가능한 조건|백업/복원 실패|
|근본 원인|백업 또는 복원 절차에 실패하면 NVDIMM-N의 모든 데이터가 손실될 수 있습니다. 운영 체제가 로드될 때 파티션 또는 파일 시스템 없는 완전히 새로운 NVDIMM-N으로 인식되어 RAW(파일 시스템이 없음을 의미)로 표시됩니다.|
|일반적인 동작|NVDIMM-N이 읽기 전용 모드로 전환됩니다. 다시 사용하려면 명시적인 사용자 작업이 필요합니다.|
|저장소 공간 동작|하나의 NVDIMM만 영향을 받는 경우 저장소 공간은 계속 작동합니다.<br>NVDIMM-N PhysicalDisk 개체가 "Unhealthy" 상태로 표시되고 저장소 공간에서 사용되지 않습니다.|
|추가 정보|PhysicalDisk 개체의 OperationalStatus 필드.<br>EventLog – Microsoft-Windows-ScmDisk0101/Operational|
|수행할 작업|영향을 받는 장치를 교체하지 않으려는 경우 **Reset-PhysicalDisk** cmdlet을 사용하여 영향을 받는 NVDIMM-N에서 읽기 전용 조건을 해소할 수 있습니다. 이 cmdlet은 저장소 공간 환경에서 NVDIMM-N을 저장소 공간에 다시 통합하고 복구 프로세스를 시작합니다.|

## <a name="interleaved-sets"></a>인터리브 집합

플랫폼의 BIOS에서 인터리브 집합을 만들어 여러 NVDIMM-N 장치가 호스트 운영 체제에 단일 장치로 표시되도록 할 수 있습니다.

Windows Server 2016 및 Windows 10 Anniversary Edition은 NVDIMM-N의 인터리브 집합을 지원하지 않습니다.

이 문서를 작성할 당시에는 호스트 운영 체제가 이러한 집합에서 개별 NVDIMM-N을 올바르게 식별하여 사용자에게 오류를 일으켰을 수 있거나 수리해야 하는 특정 장치를 명확히 알려 줄 수 있는 메커니즘이 없었습니다.


