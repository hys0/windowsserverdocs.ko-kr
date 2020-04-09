---
title: Hyper-v Vm에 대 한 영구적 메모리 장치를 구성 하기 위한 cmdlet
description: Hyper-v Vm에 대 한 영구적 메모리 장치를 구성 하는 방법
ms.prod: windows-server
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc08039ba1d
author: coreyp-at-msft
ms.author: coreyp
ms.openlocfilehash: b58e2a4e2f31c5bf3e49b89da912b77060e334ed
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860426"
---
# <a name="cmdlets-for-configuring-persistent-memory-devices-for-hyper-v-vms"></a>Hyper-v Vm에 대 한 영구적 메모리 장치를 구성 하기 위한 cmdlet

>적용 대상: Windows Server 2019

이 문서에서는 시스템 관리자 및 IT 전문가에 게 영구적 메모리로 Hyper-v Vm을 구성 하는 방법에 대 한 정보를 제공 합니다 (즉, 저장소 클래스 메모리 또는 NVDIMM-N). JDEC 규격 NVDIMM-N-N 영구 메모리 장치는 Windows Server 2016 및 Windows 10에서 지원 되 고 대기 시간이 짧은 비휘발성 장치에 바이트 수준의 액세스를 제공 합니다. VM 영구 메모리 장치는 Windows Server 2019에서 지원 됩니다. 

## <a name="create-a-persistent-memory-device-for-a-vm"></a>VM에 대 한 영구 메모리 장치 만들기

**[새 VHD](https://docs.microsoft.com/powershell/module/hyper-v/new-vhd?view=win10-ps)** cmdlet을 사용 하 여 VM에 대 한 영구 메모리 장치를 만듭니다. 기존 NTFS DAX 볼륨에 장치를 만들어야 합니다.  새 파일 이름 확장명 (. vhdpmem)은 장치가 영구적 메모리 장치 임을 지정 하는 데 사용 됩니다. 고정 VHD 파일 형식만 지원 됩니다.

**예:** `New-VHD d:\VMPMEMDevice1.vhdpmem -Fixed -SizeBytes 4GB`

## <a name="create-a-vm-with-a-persistent-memory-controller"></a>영구 메모리 컨트롤러를 사용 하 여 VM 만들기



**새 vm cmdlet** 을 사용 하 여 지정 된 메모리 크기와 VHDX 이미지 경로를 사용 하 여 2 세대 vm을 만듭니다. 그런 다음 **VMPmemController** 를 사용 하 여 영구 메모리 컨트롤러를 VM에 추가 합니다.

**예제:** 
    
    New-VM -Name "ProductionVM1" -MemoryStartupBytes 1GB -VHDPath c:\vhd\BaseImage.vhdx

    Add-VMPmemController ProductionVM1x

## <a name="attach-a-persistent-memory-device-to-a-vm"></a>영구 메모리 장치를 VM에 연결

**[Add-vmharddiskdrive](https://docs.microsoft.com/powershell/module/hyper-v/add-vmharddiskdrive?view=win10-ps)** 를 사용 하 여 영구 메모리 장치를 VM에 연결

**예:** `Add-VMHardDiskDrive ProductionVM1 PMEM -ControllerLocation 1 -Path D:\VPMEMDevice1.vhdpmem`

Hyper-v VM 내의 영구적 메모리 장치는 게스트 운영 체제에서 사용 하 고 관리 하는 영구 메모리 장치로 표시 됩니다. 게스트 운영 체제는 장치를 블록 또는 DAX 볼륨으로 사용할 수 있습니다. VM 내에서 영구적 메모리 장치를 DAX 볼륨으로 사용 하는 경우 호스트 장치에서 대기 시간이 짧은 바이트 수준 주소 (코드 경로에 i/o 가상화 없음)를 사용할 수 있습니다. 

>[!NOTE] 
>영구 메모리는 Hyper-v Gen2 Vm에 대해서만 지원 됩니다. 영구적 메모리가 있는 Vm에 대 한 실시간 마이그레이션 및 저장소 마이그레이션은 지원 되지 않습니다. Vm의 프로덕션 검사점은 영구적 메모리 상태를 포함 하지 않습니다. 