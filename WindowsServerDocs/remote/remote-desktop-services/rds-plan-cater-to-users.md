---
title: 원격 데스크톱 서비스 기능을 다양 한 종류의 사용자 제공
description: RDS의 다양한 사용자 유형에 대해 설명합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da522a18-c33f-468e-b9d6-3ad7d3cfba26
author: spatnaik
ms.author: spatnaik
ms.date: 11/06/2019
manager: scottman
ms.openlocfilehash: dc83d76dbfaded9dadae7c16ae9e1c8df7958a7d
ms.sourcegitcommit: d25e47a54a120b9bc26ff43597518fca58c1cc5b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753825"
---
# <a name="remote-desktop-services---cater-to-different-kinds-of-users"></a>원격 데스크톱 서비스 기능을 다양 한 종류의 사용자 제공

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

원격 데스크톱 서비스는 여러 유형의 워크로드를 지원합니다. 각 유형의 사용자의 예상된 필요에 따라 배포 크기를 조정 합니다.

## <a name="types-of-users"></a>사용자 유형

### <a name="knowledge-user"></a>기술 자료 사용자

기술 자료 사용자는 Microsoft Word, Excel, Outlook 및 Microsoft Edge 브라우저와 같은 경량 생산성 애플리케이션을 사용합니다.

기술 자료 사용자의 경우 가상 CPU(vCPU)당 사용자를 4명 이하로 권장합니다.

### <a name="professional-user"></a>전문 사용자

전문 사용자는 인터넷 브라우저 및 생산성 애플리케이션을 사용하고 소프트웨어 개발 및 멀티미디어 콘텐츠 작성과 같은 보다 집중적인 워크로드를 지원합니다.

전문 사용자의 경우 vCPU당 사용자를 두 명 이하로 권장합니다.

### <a name="power-user"></a>고급 사용자

고급 사용자는 CAD(Computer Users Design) 및 Adobe Photoshop과 같은 엔지니어링 및 그래픽 애플리케이션을 사용합니다. GPU는 종종 비디오 렌더링, 3D 디자인 및 시뮬레이션을 위해 그래픽 집약적 프로그램을 정기적으로 사용하는 사용자에게 적합한 선택입니다.

고급 사용자의 경우 vCPU당 사용자를 한 명 이하로 권장합니다.

그래픽 가속에 대해 자세히 알아보려면 [그래픽 렌더링 기술 선택](rds-graphics-virtualization.md)을 확인하세요.

Azure에는 다른 그래픽 가속 배포 옵션과 사용 가능한 여러 GPU VM 크기가 있습니다. [GPU에 최적화된 가상 머신 크기](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu)에서 이에 대해 알아봅니다.

## <a name="test-workload"></a>워크로드 테스트

스트레스 테스트와 실제 사용 시뮬레이션을 모두 사용하여 배포를 부하 테스트하는 것이 좋습니다. 시뮬레이션 도구를 사용하여 배포를 부하 테스트할 수 있습니다. 시스템이 사용자 요구를 충족할 수 있을 만큼 응답성이 뛰어나고 탄력적인지 확인하고, 부하 크기를 조정하여 당황하지 않도록 합니다.
