---
title: Windows Server의 Hyper-v에 대 한 시스템 요구 사항
description: Windows Server의 Hyper-v에 대 한 하드웨어 및 펌웨어 요구 사항을 나열 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: bc4a4971-f727-40cd-91f5-2ee6d24b54cb
author: kbdazure
ms.author: kathydav
ms.date: 9/30/2016
ms.openlocfilehash: 9bb50448f1ee819b3b886536424ee1556775b78d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857986"
---
# <a name="system-requirements-for-hyper-v-on-windows-server"></a>Windows Server의 Hyper-v에 대 한 시스템 요구 사항

>적용 대상: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Hyper-v는 특정 하드웨어 요구 사항 및 Hyper-v 기능이 몇 가지 추가 요구 사항이 있습니다. 이 문서에서 세부 정보를 사용 하 여 시스템을 계획 하는 방법은 Hyper-v를 사용할 수 있도록 충족 해야 하는 요구 사항을 결정 합니다. 그런 다음 검토는 [Windows Server 카탈로그](https://www.windowsservercatalog.com/)합니다. Hyper-v에 대 한 요구 사항을 가상화 환경에 더 많은 컴퓨팅 리소스가 필요 하기 때문에 Windows Server 2016에 대 한 일반 최소 요구 사항의 초과 하는 것을 염두에 두십시오.

Hyper-v를 이미 사용 중인 경우 기존 하드웨어를 사용할 수 있는 가능성이 있습니다. Windows Server 2012 r 2에서 일반적인 하드웨어 요구 사항이 크게 변경 되지 않은 합니다.  그러나 최신 하드웨어를 사용 하 여 차폐 가상 컴퓨터나 불연속 디바이스 할당 해야 합니다. 이러한 기능은 아래에 설명 된 대로 특정 하드웨어 지원을 사용 합니다. 외에 원하는 하드웨어의 주요 차이점은 두 번째 수준 주소 변환 SLAT ()는 이제 필요한 대신 것이 좋습니다.

Hyper-v를 실행 중인 가상 컴퓨터의 수와 같은 지원 되는 최대 구성에 대 한 자세한 참조 [Windows Server 2016의 Hyper-v 확장성에 대 한 계획](plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)합니다. 가상 컴퓨터에서 실행할 수는 운영 체제의 목록에 대해서는 [Windows 서버에서 Hyper-v에 대 한 지원 되는 Windows 게스트 운영 체제](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)합니다.

## <a name="general-requirements"></a>일반 요구 사항

사용 하려면 Hyper-v 기능에 관계 없이 다음이 필요 합니다.

- 두 번째 수준 주소 변환 (SLAT)와 64 비트 프로세서입니다. Windows 하이퍼바이저 같은 Hyper-v 가상화 구성 요소를 설치 하려면 SLAT을 해야 합니다. 그러나 Windows PowerShell에 대 한 가상 컴퓨터 연결 (VMConnect), Hyper-v 관리자 및 Hyper-v cmdlet와 같은 Hyper-v 관리 도구를 설치 하려면 필요 하지는 합니다. 프로세서 있는지 확인 하려면 SLAT에, 아래 "Hyper-v 요구 사항에 대 한 확인 하는 방법"을 참고 하십시오.

- VM 모드 모니터링 확장

- 계획에 대 한 충분 한 메모리- *적어도* 4GB RAM. 더 많은 메모리가 좋습니다. 호스트와 동시에 실행 해야 하는 모든 가상 컴퓨터에 대 한 충분 한 메모리가 필요 합니다.

- 가상화 지원이 BIOS 또는 UEFI에서 설정 합니다.

  - 하드웨어 지원 가상화. 이 Intel Virtualization Technology (Intel VT) 또는 AMD 가상화 (Amd-v) 기술을 사용 하는 프로세서 구체적으로 가상화 옵션-를 포함 하는 프로세서에서 사용할 수 있습니다.

  - 하드웨어 적용 DEP(데이터 실행 방지)가 제공되고, 사용하도록 설정되어 있어야 합니다. Intel 시스템의 경우이 XD 비트 (execute disable bit). AMD 시스템 NX 비트 (no execute bit)입니다.

## <a name="how-to-check-for-hyper-v-requirements"></a>Hyper-v 요구 사항에 대 한 확인 하는 방법

Windows PowerShell 또는 명령 프롬프트 및 종류를 엽니다.

```cmd
Systeminfo.exe
```

보고서를 검토 하려면 Hyper-v 요구 사항 섹션으로 스크롤하십시오.

## <a name="requirements-for-specific-features"></a>특정 기능에 대 한 요구 사항

개별 디바이스 할당 및 차폐 가상 컴퓨터에 대 한 요구 사항은 다음과 같습니다. 이러한 기능에 대 한 설명은 [Windows Server에서 hyper-v의 새로운](What-s-new-in-Hyper-V-on-Windows.md)기능을 참조 하세요.

### <a name="discrete-device-assignment"></a>개별 디바이스 할당

**호스트** 요구 사항은 Hyper-v에서 SR-IOV 기능에 대 한 기존 요구 사항과 유사 합니다.

- 어느 Intel 테이블 EPT (Extended Page) 또는 AMD의 테이블 NPT (Nested Page) 프로세서가 있어야 합니다.

- 칩셋이 있어야 합니다.

  - 인터럽트 다시 매핑-v T-d Intel의 인터럽트 다시 매핑 기능 (VT d2) 또는 AMD I/O 메모리 관리 장치 I/O MMU ()의 모든 버전.

  - DMA 다시 매핑-큐에 대기 무효화 또는 모든 AMD I/O MMU Intel의 VT 차원입니다.

  - PCI Express 루트 포트에서 액세스 제어 서비스 (ACS).

- 펌웨어 테이블에는 Windows 하이퍼바이저 I/O MMU 노출 해야 합니다. 에 유의 BIOS 또는 UEFI에서이 기능을 해제 될 수 있습니다. 자세한 내용은 하드웨어 설명서를 참조 하거나 하드웨어 제조업체에 문의 합니다.

**장치** GPU 또는 비휘발성 메모리 (NVMe) express 필요 합니다. GPU, 특정 디바이스에만 개별 디바이스 할당을 지원합니다. 을 확인 하려면 하드웨어 설명서를 참조 하거나 하드웨어 제조업체에 문의 합니다. 게시물을 참조 및 고려 사항, 사용 하는 방법을 비롯 하 여이 기능에 대 한 자세한 "[불연속 장치 할당-설명 및 배경](https://blogs.technet.com/b/virtualization/archive/2015/11/19/discrete-device-assignment.aspx)" 가상화 블로그에서입니다.

### <a name="shielded-virtual-machines"></a>실드 된 가상 컴퓨터

이러한 가상 머신은 가상화 기반 보안을 사용 하며 Windows Server 2016부터 사용할 수 있습니다.

**호스트** 요구 사항이 있습니다.

- UEFI 2.3.1c-안전 하 고 측정 된 부팅 지원

  다음 두 가지 가상화 기반 보안에 대 한 선택적 일반적으로 사용 되지만 이러한 기능을 제공 하 여 보호 하는 경우 호스트에 필요한:

- TPM v2.0-플랫폼 보안 자산 보호
- IOMMU (Intel VT 차원)-하이퍼바이저 직접 메모리 액세스 (DMA) 보호를 제공할 수 있도록

**가상 컴퓨터** 요구 사항이 있습니다.

- 2세대
- 게스트 운영 체제의 Windows Server 2012 이상

