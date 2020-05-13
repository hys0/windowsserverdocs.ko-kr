---
title: 가상 머신 내보내기 및 가져오기
description: Hyper-v 관리자 또는 Windows PowerShell을 사용 하 여 가상 컴퓨터를 내보내고 가져오는 방법을 보여 줍니다.
ms.prod: windows-server
author: kbdazure
ms.author: kathydav
manager: dongill
ms.technology: compute-hyper-v
ms.date: 12/13/2016
ms.topic: article
ms.assetid: 7fd996f5-1ea9-4b16-9776-85fb39a3aa34
ms.openlocfilehash: f1b321c04ad0b7541f21b444499b13fd2b4e4a6d
ms.sourcegitcommit: 32f810c5429804c384d788c680afac427976e351
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83203553"
---
# <a name="export-and-import-virtual-machines"></a>가상 컴퓨터 내보내기 및 가져오기

> 적용 대상: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

이 문서에서는 가상 머신을 이동 하거나 복사 하는 빠른 방법인 가상 머신을 내보내고 가져오는 방법을 보여 줍니다. 이 문서에서는 내보내기 또는 가져오기를 수행할 때 선택할 수 있는 몇 가지 방법에 대해서도 설명 합니다.

## <a name="export-a-virtual-machine"></a>가상 컴퓨터 내보내기

내보내기는 필요한 모든 파일을 하나의 단위 (가상 하드 디스크 파일, 가상 컴퓨터 구성 파일 및 모든 검사점 파일)로 수집 합니다. 시작 됨 또는 중지 됨 상태에 있는 가상 컴퓨터에서이 작업을 수행할 수 있습니다.

### <a name="using-hyper-v-manager"></a>Hyper-V 관리자 사용

가상 컴퓨터 내보내기를 만들려면

1. Hyper-v 관리자에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 **내보내기**를 선택 합니다.

2. 내보낸 파일을 저장할 위치를 선택 하 고 **내보내기**를 클릭 합니다.

내보내기가 완료 되 면 내보내기 위치 아래에서 내보낸 모든 파일을 볼 수 있습니다.

### <a name="using-powershell"></a>PowerShell 사용

관리자 권한으로 세션을 열고 \< vm 이름 및 경로를 바꾼 후 다음과 같은 명령을 실행 \> 합니다 \< \> .

```powershell
Export-VM -Name \<vm name\> -Path \<path\>
```

자세한 내용은 [Export-VM](https://docs.microsoft.com/powershell/module/hyper-v/export-vm)을 참조 하세요.

## <a name="import-a-virtual-machine"></a>가상 컴퓨터 가져오기

가상 컴퓨터 가져오기는 Hyper-V 호스트를 사용하여 가상 컴퓨터를 등록합니다. 호스트 또는 새 호스트로 다시 가져올 수 있습니다. 동일한 호스트로 가져오는 경우 Hyper-v는 사용 가능한 파일에서 가상 컴퓨터를 다시 만들기 때문에 먼저 가상 컴퓨터를 내보낼 필요가 없습니다. 가상 컴퓨터를 가져오면 Hyper-v 호스트에서 해당 가상 컴퓨터를 사용할 수 있도록 등록 합니다.

가상 컴퓨터 가져오기 마법사를 사용 하면 호스트 간에 이동할 때 존재 하는 비 호환성 문제를 해결할 수도 있습니다. 이는 일반적으로 메모리, 가상 스위치 및 가상 프로세서와 같은 실제 하드웨어의 차이입니다.

### <a name="import-using-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 가져오기

가상 컴퓨터를 가져오려면:

1. Hyper-v 관리자의 **작업** 메뉴에서 **가상 컴퓨터 가져오기**를 클릭 합니다.

2. **다음**을 클릭합니다.

3. 내보낸 파일이 포함 된 폴더를 선택 하 고 **다음**을 클릭 합니다.

4. 가져올 가상 컴퓨터를 선택 합니다.

5. 가져오기 유형을 선택 하 고 **다음**을 클릭 합니다. 자세한 내용은 아래의 [가져오기 형식](#import-types)을 참조 하세요.

6. **Finish**를 클릭합니다.

### <a name="import-using-powershell"></a>PowerShell을 사용하여 가져오기

원하는 가져오기 유형에 대 한 예제를 따라 **가져오기 VM** cmdlet을 사용 합니다. 형식에 대 한 설명은 아래의 [가져오기 형식](#import-types)을 참조 하세요.

#### <a name="register-in-place"></a>현재 위치의 등록

이 가져오기 유형은 가져오기 시 저장 된 파일을 사용 하 고 가상 머신의 ID를 유지 합니다. 다음 명령은 가져오기 파일의 예를 보여 줍니다. 사용자 고유의 값으로 비슷한 명령을 실행 합니다.

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx'
```

#### <a name="restore"></a>복원

가상 컴퓨터 파일의 고유한 경로를 지정 하 여 가상 컴퓨터를 가져오려면 다음과 같은 명령을 실행 하 여 예제를 값으로 바꿉니다.

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -VhdDestinationPath 'D:\Virtual Machines\WIN10DOC' -VirtualMachinePath 'D:\Virtual Machines\WIN10DOC'
```

#### <a name="import-as-a-copy"></a>복사본으로 가져오기

복사본 가져오기를 완료 하 고 가상 머신 파일을 기본 Hyper-v 위치로 이동 하려면 다음과 같은 명령을 실행 하 여 예제를 값으로 바꿉니다.

``` PowerShell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -GenerateNewId
```

자세한 내용은 [VM 가져오기](https://docs.microsoft.com/powershell/module/hyper-v/import-vm)를 참조 하세요.

### <a name="import-types"></a>가져오기 형식

Hyper-v는 다음과 같은 세 가지 가져오기 유형을 제공 합니다.

- **바로 등록** –이 형식은 내보내기 파일이 가상 컴퓨터를 저장 하 고 실행 하는 위치에 있는 것으로 가정 합니다. 가져온 가상 컴퓨터의 ID는 내보내기 시와 동일 합니다. 따라서 가상 컴퓨터가 Hyper-v에 이미 등록 되어 있으면 가져오기 작업을 수행 하기 전에 해당 가상 컴퓨터를 삭제 해야 합니다. 가져오기가 완료 되 면 내보내기 파일이 실행 중인 상태 파일이 되 고 제거할 수 없습니다.

- **가상 컴퓨터 복원** – 가상 컴퓨터를 선택한 위치로 복원 하거나 기본값을 hyper-v로 사용 합니다. 이 가져오기 유형은 내보낸 파일의 복사본을 만들고 선택한 위치로 이동 합니다. 가져올 때 가상 컴퓨터는 내보내기할 때와 동일한 ID를 가집니다. 따라서 가상 컴퓨터가 Hyper-v에서 이미 실행 중인 경우 가져오기를 완료 하기 전에 삭제 해야 합니다. 가져오기가 완료 되 면 내보낸 파일은 그대로 유지 되며 제거 하거나 다시 가져올 수 있습니다.

- **가상 컴퓨터 복사** – 파일의 위치를 선택 하는의 복원 유형과 비슷합니다. 차이점은 가져온 가상 컴퓨터에는 새 고유 ID가 있기 때문입니다. 즉, 가상 컴퓨터를 동일한 호스트로 여러 번 가져올 수 있습니다.

