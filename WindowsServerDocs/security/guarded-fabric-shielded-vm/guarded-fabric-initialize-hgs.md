---
title: HGS 초기화
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 42f76dabbe150f229027909f8b58b843f31ae4e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856596"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>HGS (호스트 보호 서비스)를 초기화 합니다.

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

HGS를 초기화할 때 HGS가 보호 된 호스트의 상태를 측정 하는 데 사용 하는 모드를 지정 합니다. 함께 사용할 수 없는 두 가지 옵션이 있습니다. 선택할 모드에 대 한 배경 정보는 [호스팅 서비스 공급자에 대 한 보호 된 패브릭 및 차폐 VM 계획 가이드](guarded-fabric-planning-for-hosters.md)를 참조 하세요.

다음 항목에서는 각 모드에 대 한 배포 단계를 다룹니다.

- [TPM에서 신뢰할 수 있는 증명 (TPM 모드)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [호스트 키 증명 (키 모드)](guarded-fabric-initialize-hgs-key-mode.md)
- [관리자가 신뢰할 수 있는 증명 (AD 모드)](guarded-fabric-initialize-hgs-ad-mode.md)

실제 서버에서 이러한 단계를 수행 해야 합니다.