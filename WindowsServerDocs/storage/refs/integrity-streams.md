---
title: ReFS 무결성 스트림
description: ''
author: gawatu
ms.author: jgerend
manager: dmoss
ms.date: 10/16/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.assetid: 1f1215cd-404f-42f2-b55f-3888294d8a1f
ms.openlocfilehash: 11f0a696fb843f5cd8b4a7ff3318c28d6c1adeb8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871344"
---
# <a name="refs-integrity-streams"></a>ReFS 무결성 스트림
>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (반기 채널), Windows 10

무결성 스트림은 체크섬을 사용하여 데이터 무결성을 검사하고 유지하는 ReFS의 선택적 기능입니다. ReFS는 메타데이터에 대해서는 항상 체크섬을 사용하지만, 기본적으로 파일 데이터에 대해서는 체크섬을 생성하거나 체크섬의 유효성을 검사하지 않습니다. 무결성 스트림은 사용자가 파일 데이터에 대한 체크섬을 활용할 수 있는 선택적 기능입니다. 무결성 스트림을 사용하도록 설정할 경우 ReFS는 데이터가 유효한지 손상되었는지 명확하게 판별할 수 있습니다. 또한 ReFS와 저장소 공간은 공동으로 손상된 메타데이터 및 데이터를 자동 수정할 수 있습니다.

## <a name="how-it-works"></a>작동 방법 

무결성 스트림은 개별 파일, 디렉터리 또는 볼륨 전체에 사용하도록 설정할 수 있으며, 무결성 스트림 설정은 언제든지 전환할 수 있습니다. 또한 파일 및 디렉터리에 대한 무결성 스트림 설정은 상위 디렉터리에서 상속됩니다. 

무결성 스트림을 사용하도록 설정하면 ReFS는 해당 파일의 메타데이터에 지정된 파일에 대한 체크섬을 만들고 유지합니다. 이 체크섬을 통해 ReFS는 데이터에 액세스하기 전에 데이터의 무결성을 확인할 수 있습니다. 무결성 스트림을 사용할 수 있는 모든 데이터를 반환하기 전에 ReFS는 먼저 해당 체크섬을 계산합니다.

![파일 데이터에 대 한 체크섬을 계산](media/compute-checksum.gif)

그런 다음 이 체크섬을 파일 메타데이터에 포함된 체크섬과 비교합니다. 체크섬이 일치하는 경우 데이터가 유효한 것으로 표시되고 사용자에게 반환됩니다. 체크섬이 일치하지 않으면 데이터가 손상된 것입니다. 볼륨의 복원력에 따라 ReFS가 손상에 대응하는 방식이 결정됩니다.

- ReFS가 복원력이 없는 단순 공간 또는 빈 드라이브에 탑재된 경우 ReFS는 사용자에게 손상된 데이터를 반환하지 않고 오류를 반환합니다. 
- ReFS가 복원 미러 또는 패리티 공간에 탑재된 경우 ReFS는 손상 수정을 시도합니다. 
    - 시도가 성공하면 ReFS는 수정 쓰기를 적용하여 데이터 무결성을 복원하고 응용 프로그램에 유효한 데이터를 반환합니다. 그러면 응용 프로그램은 어떠한 손상도 인식하지 않습니다.
    - 시도가 실패하면 ReFS는 오류를 반환합니다. 

ReFS는 모든 손상을 시스템 이벤트 로그에 기록하고 손상의 수정 여부가 로그에 반영됩니다. 

![데이터 무결성을 복원 하는 정정 쓰기](media/corrective-write.gif)

## <a name="performance"></a>성능 

무결성 스트림은 시스템에 더 높은 데이터 무결성을 제공하지만 성능 저하가 수반되기도 합니다. 이에 대한 몇 가지 다른 이유가 있습니다.
- 무결성 스트림을 사용하도록 설정한 경우 모든 쓰기 작업은 쓰기 시 할당 작업이 됩니다. 이는 ReFS가 읽거나 수정할 필요가 없는 기존 데이터에 대한 읽기 수정 쓰기 병목 현상을 방지하지만, 파일 데이터가 자주 조각화되어 읽기가 지연됩니다. 
- 시스템의 워크로드 및 기본 저장소에 따라 컴퓨팅 및 체크섬 유효성 검사의 계산 비용으로 인해 IO 대기 시간이 늘어날 수 있습니다. 

무결성 스트림에는 성능 저하가 수반되므로 성능에 민감한 시스템에서는 무결성 스트림을 사용하지 않도록 설정하는 것이 좋습니다. 

## <a name="integrity-scrubber"></a>무결성 스크러버

위에서 설명한 대로, ReFS는 데이터에 액세스하기 전에 데이터 무결성을 자동으로 확인합니다. ReFS는 낮은 빈도로 액세스하는 데이터를 확인할 수 있는 백그라운드 스크러버도 사용합니다. 이 스크러버는 볼륨을 주기적으로 검사하여 잠재적인 손상을 식별한 다음 모든 손상 데이터에 대한 복구를 사전에 트리거합니다.

  >[!NOTE]
  >데이터 무결성 스크러버는 무결성 스트림을 사용하도록 설정된 파일 데이터만 확인할 수 있습니다.

기본적으로는 스크러버는 4주마다 실행되지만, 이 간격은 Microsoft\Windows\Data Integrity Scan의 작업 스케줄러 내에서 구성할 수 있습니다. 

## <a name="examples"></a>예
파일 데이터 무결성 설정을 모니터링하고 변경하기 위해 ReFS는 **Get-FileIntegrity** 및 **Set-FileIntegrity** cmdlet을 사용합니다.

### <a name="get-fileintegrity"></a>Get-FileIntegrity
파일 데이터에 대해 무결성 스트림이 사용하도록 설정되었는지 확인하려면 **Get-FileIntegrity** cmdlet을 사용합니다. 

```PowerShell
PS C:\> Get-FileIntegrity -FileName 'C:\Docs\TextDocument.txt'
```

또한 **Get-Item** cmdlet을 사용하여 지정된 디렉터리의 모든 파일에 대한 무결성 스트림 설정을 가져올 수도 있습니다. 

```PowerShell
PS C:\> Get-Item -Path 'C:\Docs\*' | Get-FileIntegrity
```

### <a name="set-fileintegrity"></a>Set-FileIntegrity
파일 데이터에 대한 무결성 스트림을 사용하거나 사용하지 않도록 설정하려면 **Set-FileIntegrity** cmdlet을 사용하세요. 

```PowerShell
PS C:\> Set-FileIntegrity -FileName 'H:\Docs\TextDocument.txt' -Enable $True
```

또한 **Get-Item** cmdlet을 사용하여 지정된 폴더의 모든 파일에 대한 무결성 스트림 설정을 설정할 수도 있습니다. 

```PowerShell
PS C:\> Get-Item -Path 'H\Docs\*' | Set-FileIntegrity -Enable $True 
```

**Set-FileIntegrity** cmdlet은 볼륨 및 디렉터리에서 직접 사용할 수도 있습니다. 

```PowerShell
PS C:\> Set-FileIntegrity H:\ -Enable $True
PS C:\> Set-FileIntegrity H:\Docs -Enable $True
```

## <a name="see-also"></a>참조

-   [ReFS 개요](refs-overview.md)
-   [ReFS 블록 복제](block-cloning.md)
-   [저장소 공간 다이렉트 개요](../storage-spaces/storage-spaces-direct-overview.md)
