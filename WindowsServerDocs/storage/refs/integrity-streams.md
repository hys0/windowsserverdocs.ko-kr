---
title: ReFS 무결성 스트림
author: gawatu
ms.author: jgerend
manager: dmoss
ms.date: 10/16/2018
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.assetid: 1f1215cd-404f-42f2-b55f-3888294d8a1f
ms.openlocfilehash: 55611be13333c36201aad149be87207564d4ac97
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471148"
---
# <a name="refs-integrity-streams"></a>ReFS 무결성 스트림
>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (반기 채널), Windows 10

무결성 스트림은 체크섬을 사용 하 여 데이터 무결성의 유효성을 검사 하 고 유지 관리 하는 ReFS의 선택적 기능입니다. ReFS는 항상 메타 데이터에 대 한 체크섬을 사용 하지만 ReFS는 기본적으로 파일 데이터에 대 한 체크섬을 생성 하거나 유효성 검사를 수행 하지 않습니다. 무결성 스트림은 사용자가 파일 데이터에 대 한 체크섬을 활용할 수 있도록 하는 선택적 기능입니다. 무결성 스트림을 사용 하도록 설정 하면 ReFS에서 데이터가 올바른지 또는 손상 되었는지 명확 하 게 확인할 수 있습니다. 또한 ReFS 및 저장소 공간은 손상 된 메타 데이터 및 데이터를 자동으로 수정할 수 있습니다.

## <a name="how-it-works"></a>작동 방법

무결성 스트림은 개별 파일, 디렉터리 또는 전체 볼륨에 대해 사용 하도록 설정할 수 있으며 무결성 스트림 설정은 언제 든 지 전환할 수 있습니다. 또한 파일 및 디렉터리에 대 한 무결성 스트림 설정은 부모 디렉터리에서 상속 됩니다.

무결성 스트림을 사용 하도록 설정 하면 ReFS는 해당 파일의 메타 데이터에 지정 된 파일에 대 한 체크섬을 만들고 유지 관리 합니다. 이 체크섬은 참조를 사용 하 여 액세스 하기 전에 데이터 무결성의 유효성을 검사할 수 있습니다. 무결성 스트림을 사용 하도록 설정 된 데이터를 반환 하기 전에 ReFS는 먼저 체크섬을 계산 합니다.

![파일 데이터에 대 한 계산 체크섬](media/compute-checksum.gif)

그런 다음이 체크섬을 파일 메타 데이터에 포함 된 체크섬과 비교 합니다. 체크섬이 일치 하면 데이터가 유효한 것으로 표시 되 고 사용자에 게 반환 됩니다. 체크섬이 일치 하지 않으면 데이터가 손상 된 것입니다. 볼륨의 복원 력은 ReFS가 손상에 응답 하는 방식을 결정 합니다.

- ReFS가 복원 력이 없는 단순 공간이 나 완전 한 드라이브에 탑재 된 경우 ReFS는 손상 된 데이터를 반환 하지 않고 사용자에 게 오류를 반환 합니다.
- ReFS가 복원 력 또는 패리티 공간에 탑재 된 경우 ReFS는 손상을 해결 하려고 시도 합니다.
    - 성공적으로 수행 되 면 ReFS는 데이터의 무결성을 복원 하는 수정 쓰기를 적용 하 고 유효한 데이터를 응용 프로그램에 반환 합니다. 응용 프로그램은 어떤 손상도 계속 인식 하지 못합니다.
    - 시도가 실패 하면 ReFS에서 오류를 반환 합니다.

ReFS는 시스템 이벤트 로그에 모든 손상을 기록 하 고 로그에는 손상이 수정 되었는지 여부가 반영 됩니다.

![수정 쓰기는 데이터 무결성을 복원 합니다.](media/corrective-write.gif)

## <a name="performance"></a>성능

무결성 스트림은 시스템에 대해 더 큰 데이터 무결성을 제공 하지만 성능 비용도 발생 합니다. 이에 대 한 몇 가지 다른 이유가 있습니다.
- 무결성 스트림을 사용 하도록 설정 하면 모든 쓰기 작업이 할당 시 쓰기 작업이 됩니다. 이 경우 ReFS는 기존 데이터를 읽거나 수정할 필요가 없기 때문에 읽기-수정-쓰기 병목 현상을 방지 하지만 파일 데이터는 자주 조각화 되어 읽기가 지연 됩니다.
- 시스템의 워크 로드 및 기본 저장소에 따라 체크섬 계산 및 체크섬 유효성 검사로 인해 IO 대기 시간이 늘어날 수 있습니다.

무결성 스트림은 성능 비용을 제공 하므로 성능에 민감한 시스템에서는 무결성 스트림을 사용 하지 않도록 설정 하는 것이 좋습니다.

## <a name="integrity-scrubber"></a>무결성 스크러버

위에서 설명한 것 처럼 ReFS는 데이터에 액세스 하기 전에 자동으로 데이터 무결성의 유효성을 검사 합니다. ReFS는 또한 참조에서 자주 액세스 하지 않는 데이터의 유효성을 검사할 수 있도록 하는 background 스크러버를 사용 합니다. 이 스크러버는 정기적으로 볼륨을 검사 하 고, 잠재적인 손상을 식별 하 고, 손상 된 데이터의 복구를 사전에 트리거합니다.

  >[!NOTE]
  >데이터 무결성 스크러버는 무결성 스트림을 사용 하도록 설정 된 파일에 대 한 파일 데이터의 유효성만 검사할 수 있습니다.

기본적으로 스크러버는 4 주 간격으로 실행 되지만 Microsoft\Windows\Data 무결성 검사 아래 작업 스케줄러 내에서이 간격을 구성할 수 있습니다.

## <a name="examples"></a>예제
ReFS는 파일 데이터 무결성 설정을 모니터링 하 고 변경 하기 위해 **Get fileintegrity** 및 **Set-fileintegrity** cmdlet을 사용 합니다.

### <a name="get-fileintegrity"></a>가져오기-FileIntegrity
파일 데이터에 대 한 무결성 스트림이 설정 되었는지 확인 하려면 **Get fileintegrity** cmdlet을 사용 합니다.

```PowerShell
PS C:\> Get-FileIntegrity -FileName 'C:\Docs\TextDocument.txt'
```

또한 **가져오기-항목** cmdlet을 사용 하 여 지정 된 디렉터리의 모든 파일에 대 한 무결성 스트림 설정을 가져올 수 있습니다.

```PowerShell
PS C:\> Get-Item -Path 'C:\Docs\*' | Get-FileIntegrity
```

### <a name="set-fileintegrity"></a>Set FileIntegrity
파일 데이터에 대 한 무결성 스트림을 설정/해제 하려면 **Set fileintegrity** cmdlet을 사용 합니다.

```PowerShell
PS C:\> Set-FileIntegrity -FileName 'H:\Docs\TextDocument.txt' -Enable $True
```

또한 **가져오기-항목** cmdlet을 사용 하 여 지정 된 폴더의 모든 파일에 대 한 무결성 스트림 설정을 지정할 수 있습니다.

```PowerShell
PS C:\> Get-Item -Path 'H\Docs\*' | Set-FileIntegrity -Enable $True
```

**집합-FileIntegrity** cmdlet은 볼륨 및 디렉터리에서 직접 사용할 수도 있습니다.

```PowerShell
PS C:\> Set-FileIntegrity H:\ -Enable $True
PS C:\> Set-FileIntegrity H:\Docs -Enable $True
```

## <a name="additional-references"></a>추가 참조

-   [ReFS 개요](refs-overview.md)
-   [ReFS 블록 복제](block-cloning.md)
-   [스토리지 공간 다이렉트 개요](../storage-spaces/storage-spaces-direct-overview.md)
