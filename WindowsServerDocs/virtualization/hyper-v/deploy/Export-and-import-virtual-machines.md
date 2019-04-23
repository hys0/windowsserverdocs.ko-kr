---
title: 가상 컴퓨터 내보내기 및 가져오기
description: Hyper-v 관리자 또는 Windows PowerShell을 사용 하 여 가상 컴퓨터를 내보내고 하는 방법을 보여 줍니다.
ms.prod: windows-server-threshold
author: KBDAzure
ms.author: kathydav
manager: dongill
ms.technology: compute-hyper-v
ms.date: 12/13/2016
ms.topic: article
ms.assetid: 7fd996f5-1ea9-4b16-9776-85fb39a3aa34
ms.openlocfilehash: b326fe8d7ff05ba73fc94225fa38921b42eb3fc6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844324"
---
>적용 대상: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

# <a name="export-and-import-virtual-machines"></a>가상 컴퓨터 내보내기 및 가져오기

이 문서에서는 내보내기 및 가져오기는 가상 컴퓨터를 신속 하 게 이동 하거나 복사 하는 방법을 보여 줍니다. 또한이 문서에서는 가져오기 또는 내보내기를 수행 하는 경우를 확인 하려면 선택 항목 중 일부를 설명 합니다.

## <a name="export-a-virtual-machine"></a>가상 컴퓨터 내보내기

내보내기는 하나의 단위-가상 하드 디스크 파일, 가상 머신 구성 파일 및 검사점 파일에 필요한 모든 파일을 수집합니다. 시작 또는 중지 된 상태의 가상 컴퓨터에서이 수행할 수 있습니다.

### <a name="using-hyper-v-manager"></a>Hyper-V 관리자 사용

가상 컴퓨터 내보내기를 만들려면

1. Hyper-v 관리자에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 선택 **내보내기**합니다.

2. 클릭 하 여 내보낸된 파일을 저장할 위치를 선택 **내보내기**합니다.

내보내기가 완료 되 면 내보내기 위치 아래에 있는 모든 내보낸된 파일을 볼 수 있습니다.

### <a name="using-powershell"></a>PowerShell 사용

관리자 권한으로 세션을 열고 바꾼 후 다음과 같은 명령을 실행 \<vm 이름\> 하 고 \<경로\>:

```powershell
Export-VM -Name \<vm name\> -Path \<path\>
```

자세한 내용은 참조 하세요 [EXPORT-VM](https://docs.microsoft.com/powershell/module/hyper-v/export-vm)합니다.

## <a name="import-a-virtual-machine"></a>가상 컴퓨터 가져오기 

가상 컴퓨터 가져오기는 Hyper-V 호스트를 사용하여 가상 컴퓨터를 등록합니다. 새 호스트를 호스트에 다시 가져올 수 있습니다. 동일한 호스트를 가져오려는 경우 필요가 없습니다 먼저 가상 머신을 내보낼 Hyper-v에서 사용 가능한 파일에서 가상 머신을 다시 하려고 하기 때문에 합니다. Hyper-v 호스트에서 사용할 수 있도록 등록 가상 머신 가져오기 됩니다.

또한 가상 머신 가져오기 마법사를 하나의 호스트에서 다른 호스트로 이동할 때 존재할 수 있는 호환성 문제를 해결할 수 있습니다. 이 일반적으로 메모리, 가상 스위치, 가상 프로세서 등의 물리적 하드웨어와의 차이점입니다.

### <a name="import-using-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 가져오기

가상 머신을 가져오려면:

1. **동작** Hyper-v 관리자의 메뉴 클릭 **가상 머신 가져오기**합니다.

2. **다음**을 클릭합니다.

3. 내보낸된 파일을 포함 하는 폴더를 선택 하 고 클릭 **다음**합니다.

4. 가져올 가상 컴퓨터를 선택 합니다.

5. 가져오기 유형 선택 및 클릭 **다음**합니다. (설명을 보려면 [형식을 가져오도록](#import-types)아래.)

6. **마침**을 클릭합니다.

### <a name="import-using-powershell"></a>PowerShell을 사용 하 여 가져오기

사용 합니다 **IMPORT-VM** cmdlet을 다음 원하는 가져오기의 형식에 대 한 예제입니다. 형식의 설명을 보려면 [형식을 가져오도록](#import-types)아래. 

#### <a name="register-in-place"></a>등록 준비

이 유형의 가져오기는 가져오기 시 저장 된 파일을 사용 하 고 가상 컴퓨터의 id입니다. 유지 다음 명령을 가져오기 파일의 예를 보여 줍니다. 사용자 고유의 값을 사용 하 여 비슷한 명령을 실행 합니다.

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' 
```

#### <a name="restore"></a>복원

가상 머신 파일에 대 한 고유한 경로 지정 하는 가상 컴퓨터를 가져오려면 예제 값으로 바꿉니다 같이 명령을 실행 합니다.

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -VhdDestinationPath 'D:\Virtual Machines\WIN10DOC' -VirtualMachinePath 'D:\Virtual Machines\WIN10DOC'
```

#### <a name="import-as-a-copy"></a>복사본으로 가져오기

복사본 가져오기를 완료 하 고 기본 Hyper-v 위치로 가상 컴퓨터 파일을 이동 하려면 예제 값을 사용 하 여 대체 같이 명령을 실행:

``` PowerShell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -GenerateNewId
```

자세한 내용은 참조 하세요 [IMPORT-VM](https://docs.microsoft.com/powershell/module/hyper-v/import-vm)합니다.

### <a name="import-types"></a>가져오기 형식

Hyper-v는 3 개의 가져오기 유형이 제공합니다.

- **바로 등록** – 저장 하 고 가상 머신을 실행할 수 있는 위치에 내보내기 파일은이 유형을 가정 합니다. 가져온된 가상 컴퓨터 내보내기 시 수행한 것 처럼 동일한 ID가 있습니다. 이 인해 Hyper-v가 설치 된 가상 컴퓨터가 이미 등록 되어 있으면 해야 가져오기 작동 하기 전에 삭제 합니다. 내보낼 파일이 실행 될 가져오기가 완료 되 면 상태 파일 이므로 제거할 수 없습니다.

- **가상 머신을 복원** – 원하는 위치로 가상 컴퓨터를 복원 하거나 Hyper-v로 기본값을 사용 합니다. 이 가져오기 형식은 내보낸된 파일의 복사본을 만들고 선택한 위치로 이동 합니다. 가져올 때 가상 컴퓨터는 내보내기할 때와 동일한 ID를 가집니다. 이 때문에 가상 머신을 Hyper-v에서 이미 실행 중인 경우 해야는 가져오기를 완료 하기 전에 삭제 합니다. 가져오기가 완료 되 면 내보낸된 파일이 그대로 유지 및 수 제거 하거나 다시 가져올 합니다.

- **가상 머신 복사** – 이것은 파일의 위치를 선택 하는 복원 형식과 비슷합니다. 가져온된 가상 컴퓨터에 여러 번 같은 호스트로 가상 컴퓨터를 가져올 수 있습니다 즉 새 고유 ID는 다릅니다.

