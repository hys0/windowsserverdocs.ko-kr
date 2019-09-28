---
ms.assetid: 13210461-1e92-48a1-91a2-c251957ba256
title: 드라이브 펌웨어 업데이트 문제 해결
ms.prod: windows-server
ms.author: toklima
ms.manager: masriniv
ms.technology: storage
ms.topic: article
author: toklima
ms.date: 04/18/2017
ms.openlocfilehash: 9c9c1083def53e09b063a0ca9879e4d4527e98c0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365890"
---
# <a name="troubleshooting-drive-firmware-updates"></a>드라이브 펌웨어 업데이트 문제 해결

>적용 대상: Windows 10, Windows Server (반기 채널)

Windows 10, 버전 1703 이후 버전 및 Windows Server(반기 채널)에는 PowerShell을 통해 펌웨어 업그레이드 가능 추가 한정자(Firmware Upgradeable AQ) 인증을 받은 HDD 및 SSD의 펌웨어를 업데이트하는 기능이 포함되어 있습니다.

다음 웹 사이트에서 이 기능에 대한 자세한 정보를 확인할 수 있습니다.

- [Windows Server 2016에서 드라이브 펌웨어 업데이트](update-firmware.md)
- [스토리지 공간 다이렉트에서 가동 중지 시간 없이 드라이브 펌웨어 업데이트](https://channel9.msdn.com/Blogs/windowsserver/Update-Drive-Firmware-Without-Downtime-in-Storage-Spaces-Direct)

펌웨어 업데이트가 잘못되는 이유는 매우 다양합니다. 이 글은 고급 단계 문제 해결에 도움을 드리기 위해 작성되었습니다.

  > [!Note]
  > 문제에 따라 가능한 모든 실패 사례를 해결하기에는 이 글의 내용으로 충분치 않을 수 있습니다.

## <a name="common-issues"></a>일반적인 문제
구조적으로 이 새 기능은 PowerShell에서 호출하는 Windows 저장소 스택에 구현된 API를 사용합니다. 저장소 스택은 산업적으로 정의된 명령을 올바로 구현하기 위해 드라이버와 하드웨어에 의지합니다. 여기서 오류가 발생할 수 있는 몇 가지 지점이 노출됩니다. 가장 일반적으로 관찰되는 문제점은 다음과 같습니다.

1.  해당 드라이브가 산업 표준 명령을 올바로 구현하지 않는 경우(AQ가 없음)
2.  업데이트를 수행하는 데 필요한 API가 구현되지 않았거나 결함이 있는 경우(타사 드라이버가 사용된 경우)
3.  API는 제대로 작동하지만 펌웨어 자체에 문제가 있는 경우(이미지 결함/손상 등등)

이하에서는 문제 해결 정보를 Microsoft 드라이버를 사용한 경우와 타사 드라이버를 사용한 경우에 따라 나눠 개괄적으로 설명합니다.

## <a name="identifying-inappropriate-hardware"></a>부적합한 하드웨어 확인
어떤 장치가 올바른 명령 집합을 지원하는지 확인하는 가장 빠른 방법은 간단히 PowerShell을 실행하여 디스크를 나타내는 PhysicalDisk 객체를 Get-StorageFirmwareInfo cmdlet에 전달하는 것입니다. 다음 예를 참조하세요.

```powershell
Get-PhysicalDisk -SerialNumber 15140F55976D | Get-StorageFirmwareInformation
```
그리고 다음은 예제의 실행 결과입니다.

```
PhysicalDisk          : MSFT_PhysicalDisk (ObjectId = "{1}\\TOKLIMA-DL380\root/Microsoft/Windo...)
SupportsUpdate        : True
NumberOfSlots         : 1
ActiveSlotNumber      : 0
SlotNumber            : {0}
IsSlotWritable        : {True}
FirmwareVersionInSlot : {0013}
```

SupportsUpdate 필드는 최소한 SATA 및 NVMe 장치에 대해서는 자체 내장된 PowerShell 기능을 펌웨어 업데이트에 사용할 수 있는지 나타내 주게 됩니다.

산업 표준 명령으로는 적절한 명령 지원에 대한 쿼리가 불가능하기 때문에 SupportsUpdate 필드는 SAS 연결 장치에 대해 항상 “True” 값을 보고할 것입니다.

필요한 명령 집합을 SAS 장치가 지원하는지 확인하는 데는 두 가지 옵션이 있습니다.
1.  적절한 펌웨어 이미지와 함께 Update-StorageFirmware cmdlet을 통해 시험해 보는 방법, 또는
2.  Windows Server 카탈로그를 참조 하 여 FW 업데이트 AQ을 성공적으로 획득 한 SAS 장치를 확인 합니다 (https://www.windowsservercatalog.com/)

### <a name="remediation-options"></a>재구성 옵션
테스트 중인 장치가 적절한 명령 집합을 지원하지 않을 경우, 판매업체에 문의해서 필요한 명령 집합을 제공하는 업데이트된 펌웨어가 있는지 확인하거나 Windows Server 카탈로그를 조회해서 적절한 명령 집합을 구현한 소싱 대상 장치가 있는지 확인합니다.

## <a name="troubleshooting-with-3rd-party-drivers-sas"></a>타사 드라이버(SAS) 관련 문제 해결
하드웨어와 가장 가깝게 상호작용하는 소프트웨어 구성 요소는 Windows 저장소 스택의 미니포트 드라이버입니다. SATA 및 NVMe와 같은 일부 저장소 프로토콜에 대해 Microsoft는 기본 Windows 드라이버를 제공합니다. 이러한 드라이버들에는 추가로 디버그 정보를 넣을 수 있습니다. 그러나 타사 하드웨어 및 소프트웨어 판매업체들은 자체 장치를 위한 고유의 미니포트 드라이버를 자유롭게 만들 수 있으며 디버그 정보 지원 수준도 제각각입니다.

펌웨어 다운로드가 어떻게 됐는지 확인하고 저장소 스택 아래쪽으로 전송된 API를 활성화하려면 미니포트 드라이버에 관계없이 다음과 같은 이벤트 로그 채널을 조회합니다.

이벤트 뷰어 - 응용 프로그램 및 서비스 로그 - Microsoft - Windows - StorDiag - **Microsoft-Windows-Storage-ClassPnP/Operational**

이 채널에는 미니포트 드라이버에 전송된 Windows API와 그 반응에 관한 정보가 기록됩니다. 예를 들어 바로 아래 제시된 오류 조건은 SAS에서 SATA로 가는 데 필요한 변환을 올바로 구현하지 않은 SAS HBA를 통해 연결된 SATA 장치에 펌웨어 이미지를 다운로드하려 할 때 나타납니다.

```powershell
Get-PhysicalDisk -SerialNumber 44GS103UT5EW | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.enc -SlotNumber 0
```
출력 예는 다음과 같습니다.

```
Update-StorageFirmware : Failed

Extended information:
A warning or error has been encountered during storage firmware update.
Incorrect function.

Activity ID: {1224482b-2315-4a38-81eb-27bb7de19c00}
At line:1 char:47
+ ... S103UT5EW | Update-StorageFirmware -ImagePath C:\Firmware\J3E160@3.en ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo          : NotSpecified: (:) [Update-StorageFirmware], CimException
+ FullyQualifiedErrorId : StorageWMI 4,Microsoft.Management.Infrastructure.CimCmdlets.InvokeCimMethodCommand,Update-StorageFirmware
```
    
PowerShell은 오류를 낼 것이며 호출된 함수(즉, Kernel API)가 잘못되었다는 정보를 접수했습니다. 이는 해당 API가 해당 타사 SAS 미니포트 드라이버에 의해 구현된 것이 아니거나(이 경우에는 True), 다운로드 세그먼트의 불일치 등과 같은 다른 이유로 API가 오류를 일으켰음을 의미할 수 있습니다.

```
EventData
DeviceGUID  {132EDB55-6BAC-A3A0-C2D5-203C7551D700}
DeviceNumber    1
Vendor  ATA 
Model   TOSHIBA THNSNJ12
FirmwareVersion 6101
SerialNumber    44GS103UT5EW
DownLevelIrpStatus  0xc0000185
SrbStatus   132
ScsiStatus  2
SenseKey    5
AdditionalSenseCode 36
AdditionalSenseCodeQualifier    0
CdbByteCount    10
CdbBytes    3B0E0000000001000000
NumberOfRetriesDone 0
```

채널의 ETW 이벤트 507는 SCSI SRB 요청이 실패 한 것을 보여 주고,이에 대 한 추가 정보를 제공 합니다 .이 정보는 ' 5 ' (잘못 된 요청)이 고, AdditionalSense 정보는 ' 36 ' (CDB의 잘못 된 필드)입니다.

   > [!Note]
   > 이 정보는 문제의 미니포트에서 직접 제공되며 그 정확성은 해당 미니포트가 제대로 정교하게 구현되었는가에 달려 있습니다.

미니포트 드라이버에 의해 명확히 구분되지 않을 경우 서로 다른 오류 조건이 동일한 오류 코드로 표현될 수도 있습니다. 예를 들어 잘못된 펌웨어 이미지를 SAS HBA를 통해 SATA 장치로 다운로드하려는 작업(해당 장치가 처리에 실패할 것으로 예상되는 작업)은 동일한 오류 코드로 변환될 수 있습니다.

프로토콜이 섞여 있어 변환이 이루어지는 경우, 즉 SAS 뒤에 SATA가 있는 경우 해당 SATA 장치를 SATA 컨트롤러에 직접 연결해서 테스트함으로써 문제 가능성에서 원천적으로 배제하는 것이 최선입니다.

### <a name="remediation-options"></a>재구성 옵션
해당 타사 드라이버가 필요한 API 또는 변환을 구현하지 않은 것으로 확인되는 경우에는 Microsoft에서 SATA용 및 NVMe용으로 제공한 대안(각각, StorAHCI.sys 및 StorNVMe.sys)으로 교체하거나 해당 SAS 드라이버를 공급한 OEM 또는 HBA 판매업체에 연락해서 올바로 지원되는 새 버전이 있는지 확인하는 방법을 택할 수 있습니다.

## <a name="additional-troubleshooting-with-microsoft-drivers-satanvme"></a>Microsoft 드라이버(SATA/NVMe) 관련 추가적 문제 해결 방법
StorAHCI.sys 또는 StorNVMe.sys 등과 같은 Windows 기본 드라이버를 사용해서 저장소 장치를 구동하는 경우에는 펌웨어 업데이트 작업 중 발생할 수 있는 오류 사례에 관한 추가 정보를 구할 수 있습니다.

ClassPnP 작동 채널 외에도 StorAHCI 및 Storahci는 다음 ETW 채널에서 장치의 프로토콜 특정 반환 코드를 기록 합니다.

이벤트 뷰어 - 응용 프로그램 및 서비스 로그 - Microsoft - Windows - StorDiag - **Microsoft-Windows-Storage-StorPort/Diagnose**

이 진단 로그는 기본적으로 표시되지는 않으며 이벤트뷰어에서 “보기”를 클릭하고 드롭다운 메뉴에서 “Show Analytics and Debug Logs”를 선택하여 활성화/표시할 수 있습니다.

이러한 고급 로그 항목을 수집하려면 로그를 사용 설정하고 해당 펌웨어 업데이트 오류를 재현한 다음, 진단 로그를 저장합니다.

다음은 다운로드할 이미지가 잘못 되었기 때문에 실패 한 SATA 장치의 펌웨어 업데이트 예입니다 (이벤트 ID: 258):

``` 
EventData
MiniportName    storahci
MiniportEventId 19
MiniportEventDescription    Firmware Activate Completion
PortNumber  0
Bus 2
Target  0
LUN 0
Irp 0xffff8c84cd45aca0
Srb 0xffffab0024030bc0
Parameter1Name  SrbStatus
Parameter1Value 130
Parameter2Name  ReturnCode
Parameter2Value 0
Parameter3Name  FeaturesReg
Parameter3Value 15
Parameter4Name  SectorCountReg
Parameter4Value 0
Parameter5Name  DriveHeadReg
Parameter5Value 160
Parameter6Name  CommandReg
Parameter6Value 146
Parameter7Name  NULL
Parameter7Value 0
Parameter8Name  NULL
Parameter8Value 0
```

위 이벤트는 매개 변수 2~6에 상세한 장치 정보를 담고 있습니다. 여기서는 다양한 ATA 레지스터 값이 보입니다. ATA ACS 명세서는 마이크로코드 다운로드 명령의 실패에 대한 아래의 값을 디코딩하는 데 사용될 수 있습니다.
- 반환 코드: 0 (0000 0000) (페이로드가 전송 되지 않았기 때문에 의미가 없음)
- 기능: 15 (0000 1111) (비트 1은 ' 1 '로 설정 되 고 "abort"를 나타냄)
- SectorCount: 0 (0000 0000) (해당 없음)
- 드라이브 헤드: 160 (1010 0000) (해당 없음-사용 되지 않는 비트만 설정 됨)
- 명령 146 (1001 0010) (비트 1은 sense 데이터의 가용성을 나타내는 ' 1 '로 설정 됨)

이를 통해 펌웨어 업데이트 작업이 해당 장치에 의해 중단되었음을 알 수 있습니다.

Windows 기본 NVMe 드라이버(StorNVMe.sys)로 NVMe 장치를 사용할 때도 이 채널에서 비슷한 수준의 디버그 정보를 찾을 수 있습니다.
