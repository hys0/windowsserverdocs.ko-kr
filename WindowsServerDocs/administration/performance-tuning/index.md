---
title: Windows Server 2016 성능 조정 지침
description: Windows Server 2016에 대한 서버 성능 조정 지침
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: phstee
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: f684a87b091ffd95bb65c0b5f3aa0dfc9f405825
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "71355040"
---
# <a name="performance-tuning-guidelines-for-windows-server-2016"></a>Windows Server 2016에 대한 서버 성능 조정 지침

조직에서 서버 시스템을 실행하면 기본 서버 설정으로 충족되지 않는 비즈니스 요구 사항이 있을 수 있습니다. 예를 들어 서버에서 가능한 한 에너지 소비를 줄이고, 대기 시간을 가능한 한 짧게 하며, 최대 처리량이 필요할 수 있습니다. 이 가이드는 특히 시간이 지나면서 워크로드의 성격이 약간 달라지는 경우 Windows Server 2016에서 서버 설정을 조정하고 성능 또는 에너지 효율성을 높일 수 있는 일련의 지침을 제공합니다.

조정 변경은 하드웨어, 워크로드, 전원 예산 및 서버의 성능 목표를 고려해야 합니다. 이 가이드에서는 시스템, 워크로드, 성능 및 에너지 사용량 목표에 대한 적합 여부를 합리적으로 결정할 수 있도록 각 설정 및 잠재적 효과를 설명합니다.

> [!warning]
> 레지스트리 설정 및 조정 매개 변수가 Windows Server 버전 사이에서 크게 변경됩니다. 예기치 않은 결과를 방지하기 위해 최신 조정 지침을 사용했는지 확인합니다.

## <a name="in-this-guide"></a>이 가이드의 내용
이 가이드는 세 개의 조정 범주에서 Windows Server 2016에 대한 성능 및 조정 지침을 구성합니다.

|서버 하드웨어 | 서버 역할 | 서버 하위 시스템 |
|:---:|:---:|:---:|
|[하드웨어 성능 고려 사항](hardware/index.md) |[Active Directory 서버](role/active-directory-server/index.md) |[캐시 및 메모리 관리](subsystem/cache-memory-management/index.md)|
|[하드웨어 전원 고려 사항](hardware/power.md)|[파일 서버](role/file-server/index.md)|[네트워킹 하위 시스템](../../networking/technologies/network-subsystem/net-sub-performance-top.md)|
||[Hyper-V 서버](role/hyper-v-server/index.md)|[스토리지 공간 다이렉트](subsystem/storage-spaces-direct/index.md)|
||[원격 데스크톱 서비스](role/remote-desktop/session-hosts.md)|[SDN(소프트웨어 정의 네트워킹)](subsystem/software-defined-networking/index.md)|
||[웹 서버](role/web-server/index.md)||
||[Windows Server 컨테이너](role/windows-server-container/index.md)||


## <a name="changes-in-this-version"></a>이 버전의 변경 내용

### <a name="sections-added"></a>추가된 섹션
- [Nano 서버 설치 유형 구성 고려 사항](../../get-started/getting-started-with-nano-server.md)


- [소프트웨어 정의 네트워킹](subsystem/software-defined-networking/index.md)([HNV](subsystem/software-defined-networking/hnv-gateway-performance.md) 및 [SLB 게이트웨이 구성 지침](subsystem/software-defined-networking/slb-gateway-performance.md) 포함)

- [스토리지 공간 다이렉트](subsystem/storage-spaces-direct/index.md)

- [HTTP1.1 및 HTTP2](role/web-server/http-performance.md)

- [Windows Server 컨테이너](role/windows-server-container/index.md)

### <a name="sections-changed"></a>변경된 섹션

- [Active Directory 지침](role/active-directory-server/index.md) 섹션으로 업데이트

- [파일 서버 지침](role/file-server/index.md) 섹션으로 업데이트

- [웹 서버 지침](role/web-server/index.md) 섹션으로 업데이트

- [하드웨어 전원 지침](hardware/power.md) 섹션으로 업데이트

- [PowerShell 조정 지침](powershell/index.md) 섹션으로 업데이트

- [Hyper-V 지침](role/hyper-v-server/index.md) 섹션으로 중요 내용 업데이트

- *워크로드에 대한 성능 조정 제거*, [추가 조정 리소스 문서](additional-resources.md)에 관련 리소스에 대한 포인터 추가

- 새 [스토리지 공간 다이렉트](subsystem/storage-spaces-direct/index.md) 섹션 및 정식 Technet 콘텐츠를 위해 *전용 스토리지 섹션 제거*

- 정식 Technet 콘텐츠를 위해 *전용 네트워킹 섹션 제거*  
