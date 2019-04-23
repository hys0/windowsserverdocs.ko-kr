---
title: Hyper-v Vm에 대 한 영구 메모리 장치를 구성 하기 위한 Cmdlet
description: Hyper-v Vm에 대 한 영구 메모리 장치를 구성 하는 방법
ms.prod: windows-server-threshold
ms.service: na
manager: jasgroce
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc08039ba1d
author: coreyp-at-msft
ms.author: coreyp
ms.openlocfilehash: fd1b04ce74f0b8d490529d2a7f65091f5847d0f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878184"
---
# <a name="cmdlets-for-configuring-persistent-memory-devices-for-hyper-v-vms"></a>Hyper-v Vm에 대 한 영구 메모리 장치를 구성 하기 위한 Cmdlet

>적용 대상: Windows Server 2019

이 문서에서는 영구 메모리 (즉, 저장소 클래스 메모리 또는 NVDIMM)를 사용 하 여 Hyper-v Vm을 구성 하는 방법에 대 한 정보를 사용 하 여 시스템 관리자와 IT 전문가 제공 합니다. JDEC 규격 Nvdimm-n 영구 메모리 장치는 Windows Server 2016 및 Windows 10에서 지원 하 고 바이트 수준 매우 짧은 대기 시간과 비휘발성 장치에 대 한 액세스를 제공 합니다. VM 영구 메모리 장치는 Windows Server 2019에서 지원 됩니다. 

## <a name="create-a-persistent-memory-device-for-a-vm"></a>VM에 대 한 영구 메모리 장치를 만들기

사용 합니다 **[NEW-VHD](https://docs.microsoft.com/powershell/module/hyper-v/new-vhd?view=win10-ps)** cmdlet을 VM에 대 한 영구 메모리 장치를 만듭니다. 장치는 기존 NTFS DAX 볼륨에 생성 되어야 합니다.  새 파일 이름 확장명 (.vhdpmem) 영구 메모리 장치를 장치 임을 지정 됩니다. 고정된 VHD 파일 형식만 지원 됩니다.

**예:** `New-VHD d:\VMPMEMDevice1.vhdpmem -Fixed -SizeBytes 4GB`

## <a name="create-a-vm-with-a-persistent-memory-controller"></a>영구 메모리 컨트롤러를 사용 하 여 VM 만들기



사용 하 여 합니다 **NEW-VM cmdlet** VHDX 이미지 경로를 지정 된 메모리 크기와 2 세대 VM을 만들려고 합니다. 사용 하 여 **추가 VMPmemController** VM에 영구 메모리 컨트롤러에 추가 합니다.

**예:** 
    
    New-VM -Name "ProductionVM1" -MemoryStartupBytes 1GB -VHDPath c:\vhd\BaseImage.vhdx

    Add-VMPmemController ProductionVM1x

## <a name="attach-a-persistent-memory-device-to-a-vm"></a>VM에 영구 메모리 장치 연결

사용 하 여 **[Add-vmharddiskdrive](https://docs.microsoft.com/powershell/module/hyper-v/add-vmharddiskdrive?view=win10-ps)** 영구 메모리 장치를 VM에 연결 하려면

**예:** `Add-VMHardDiskDrive ProductionVM1 PMEM -ControllerLocation 1 -Path D:\VPMEMDevice1.vhdpmem`

Hyper-v VM 내에서 영구 메모리 장치가 사용 하 고 게스트 운영 체제에 의해 관리 되는 영구 메모리 장치로 표시 됩니다. 게스트 운영 체제 블록 또는 DAX 볼륨으로 장치를 사용할 수 있습니다. VM 내에서 영구 메모리 장치는 DAX 볼륨으로 사용 되는 경우 대기 시간이 짧은 바이트 수준 주소 능력 호스트 장치 (코드 경로에 없는 I/O 가상화)에서 이익을 얻을 수 있습니다. 

>[!NOTE] 
>Gen2로 Hyper-v Vm에 대 한 영구 메모리 에서만 지원 됩니다. 실시간 마이그레이션 및 저장소 마이그레이션 영구 메모리를 사용 하 여 Vm에 대 한 지원 되지 않습니다. Vm의 프로덕션 검사점 영구 메모리 상태를 포함 하지 않습니다. 