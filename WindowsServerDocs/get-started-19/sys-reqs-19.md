---
title: Windows Server 2019 시스템 요구 사항
description: Windows Server 2019의 새로 설치 시 스토리지, CPU, 네트워크, 메모리 및 RAM에 대한 최소 요구 사항입니다.
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
ms.assetid: 4a8b42d7-9fe5-4efe-9ea1-ace2131f860e
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: eb328b9a80eb9d73b7230e0eaa7f820307baf294
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391936"
---
# <a name="system-requirements"></a>시스템 요구 사항

> 적용 대상: Windows Server 2019

이 항목에서는 Windows Server&reg; 2019를 실행하기 위한 최소 시스템 요구 사항을 설명합니다.

## <a name="review-system-requirements"></a>시스템 요구 사항 검토  

다음은 Windows Server 2019 설치를 위한 예상되는 시스템 요구 사항입니다. 컴퓨터의 사양이 "최소" 요구 사항보다 낮으면 이 제품을 제대로 설치할 수 없습니다. 실제 요구 사항은 사용자가 설치하는 응용 프로그램과 기능 및 시스템 구성에 따라 달라질 수 있습니다.

달리 지정되지 않는 경우 이러한 최소 시스템 요구 사항은 모든 설치 옵션(Server Core, 데스크톱 환경 포함 서버, Nano 서버)과 Standard 및 Datacenter 버전에 적용됩니다.  

> [!IMPORTANT]  
> 매우 다양한 잠재적인 배포 범위로 인해 일반적으로 적용되는 "권장" 시스템 요구 사항이 비현실적일 수 있습니다. 특정 서버 역할에 필요한 리소스에 대한 자세한 내용은 배포하려는 각 서버 역할에 대한 설명서를 참조하세요. 최상의 결과를 얻으려면 테스트 배포를 수행하여 특정 배포 시나리오에 적합한 시스템 요구 사항을 확인하세요.  

## <a name="processor"></a>프로세서  

프로세서 성능은 프로세서의 클록 주파수뿐만 아니라 프로세서 코어의 수와 프로세서 캐시의 크기에 따라 달라집니다. 다음은 이 제품을 설치하기 위한 프로세서 요구 사항입니다.  

**최소**:  
- 1.4GHz 64비트 프로세서  
- X64 호환 명령 집합  
- NX 및 DEP 지원  
- CMPXCHG16b, LAHF/SAHF 및 PrefetchW 지원  
- 두 번째 수준 주소 변환(EPT 또는 NPT) 지원  

[Coreinfo](https://technet.microsoft.com/sysinternals/cc835722.aspx)는 CPU가 가진 이러한 기능을 확인하는데 사용할 수 있는 도구입니다.

## <a name="ram"></a>RAM

다음은 이 제품 설치를 위해 예상되는 RAM 관련 요구 사항입니다.  

**최소**:  
- 512MB(데스크톱 환경 포함 서버 설치 옵션인 경우 2GB)
- 물리적 호스트 배포를 위한 ECC(오류 수정 코드) 형식 또는 유사한 기술

> [!IMPORTANT]  
> 지원되는 최소 하드웨어 매개 변수(프로세서 코어 1개, 512MB RAM)를 사용하여 가상 컴퓨터를 만든 다음 가상 컴퓨터에서 이 릴리스를 설치하려고 하면 설치가 실패합니다.  
>   
> 이 문제를 방지하려면 다음 중 하나를 수행합니다.  
>   
> -   이 릴리스를 설치하려는 가상 머신에 800MB를 초과하는 RAM을 할당합니다. 설치가 완료되면 실제 서버 구성에 따라 할당 크기를 512MB RAM 정도로 변경할 수 있습니다. 추가 언어 및 업데이트를 사용하여 설치용 부팅 이미지를 수정한 경우 설치를 완료하려면 800MB가 넘는 RAM을 할당해야 할 수 있습니다.  
> -   Shift+F10을 사용하여 가상 컴퓨터에서 이 릴리스의 부팅 프로세스를 중단합니다. 명령 프롬프트가 열리면 Diskpart.exe를 사용하여 설치 파티션을 만들고 포맷합니다. **Wpeutil createpagefile /path=C:\pf.sys** 를 실행합니다(만든 설치 파티션이 C:인 경우 예제). 명령 프롬프트를 닫고 설치를 계속 진행합니다.  

## <a name="storage-controller-and-disk-space-requirements"></a>저장소 컨트롤러 및 디스크 공간 요구 사항  
Windows Server 2019를 실행하는 컴퓨터에는 PCI Express 아키텍처 사양과 호환되는 스토리지 어댑터가 포함되어 있어야 합니다. 서버에서 하드 디스크 드라이브로 분류된 영구 저장 장치는 PATA가 아니어야 합니다. Windows Server 2019에서는 부팅, 페이지 또는 데이터 드라이브에 ATA/PATA/IDE/EIDE를 사용할 수 없습니다.  

다음은 시스템 파티션을 위한 **최소** 예상 디스크 공간 요구 사항입니다.  

**최소**: 32GB  

> [!NOTE]
> 32GB는 성공적인 설치의 *최소 절대*값으로 간주됩니다. 이 최소 설치를 사용하여 웹 서비스(IIS) 서버 역할을 포함하는 Server Core 모드에서 Windows Server 2019를 설치할 수 있습니다. Server Core 모드의 서버는 GUI 포함 서버 모드의 동일한 서버보다 약 4GB 작습니다. 
> 
> 시스템 파티션은 다음의 환경에서 추가 공간을 필요로 합니다.  
> 
> -   네트워크에 시스템을 설치한 경우  
> -   RAM이 16GB를 넘는 컴퓨터에서는 페이징, 최대 절전 모드 및 덤프 파일을 위해 더 많은 디스크 공간이 필요합니다.  

## <a name="network-adapter-requirements"></a>네트워크 어댑터 요구 사항  

이 릴리스에서 사용되는 네트워크 어댑터는 다음 기능을 포함해야 합니다.  

**최소 요구 사항**:  
- 최소 기가비트 처리량을 지원하는 이더넷 어댑터  
- PCI Express 아키텍처 사양 준수  

네트워크 디버깅을 지원하는 네트워크 어댑터(KDNet)는 유용하지만 최소 요구 사항이 아닙니다.   

PXE(Pre-boot Execution Environment)를 지원하는 네트워크 어댑터는 유용하지만 최소 요구 사항은 아닙니다.

## <a name="other-requirements"></a>기타 요구 사항  
이 릴리스를 실행하는 컴퓨터에는 다음 항목도 있어야 합니다.  

-   DVD 드라이브(DVD 미디어에서 운영 체제를 설치하려는 경우)  

다음 항목은 반드시 필요한 것은 아니지만 특정 기능에 필요합니다.  

- 보안 부팅을 지원하는 UEFI 2.3.1c 기반 시스템 및 펌웨어  
- 신뢰할 수 있는 플랫폼 모듈  

-   Super VGA(1024 x 768) 이상의 해상도를 지원하는 그래픽 디바이스 및 모니터  

-   키보드 및 Microsoft&reg; 마우스(또는 기타 호환 가능 포인팅 디바이스)  

-   인터넷 액세스(사용 요금 부과 가능)  

> [!NOTE]  
> TPM(신뢰할 수 있는 플랫폼 모듈) 칩은 이 릴리스를 설치하는 데 반드시 필요한 것은 아니지만 BitLocker 드라이브 암호화와 같은 특정 기능을 사용하는 데 필요합니다. 컴퓨터에서 TPM을 사용하는 경우 다음 요구 사항을 충족해야 합니다.  
>  
> - 하드웨어 기반 TPM은 TPM 사양 버전 2.0를 구현해야 합니다.  
> - 버전 2.0을 구현하는 TPM에는 하드웨어 공급업체에서 TPM에 미리 프로비전했거나 처음 부팅하는 동안 디바이스에서 검색할 수 있는 EK 인증서가 있어야 합니다.  
> - 버전 2.0을 구현하는 TPM은 SHA-256 PCR 뱅크와 함께 제공되고 SHA-256용 PCR 0~23을 구현해야 합니다. SHA-1 및 SHA-256 측정 둘 다에 사용할 수 있는 전환 가능한 단일 PCR 뱅크가 포함된 TPM을 사용할 수 있습니다.  
> - TPM을 해제하는 UEFI 옵션은 요구 사항이 아닙니다.  
