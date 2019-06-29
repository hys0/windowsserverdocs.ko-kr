---
title: HGS 구성 확인
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 8f01df37-f18e-4386-ae73-ecf84feaa9df
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8098edd1eea475cea1face5541459b262364a07b
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469551"
---
# <a name="verify-the-hgs-configuration"></a>HGS 구성 확인

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019


다음으로, 작업 예상 대로 작동 하는지 유효성을 검사 해야 합니다. 이렇게 하려면 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행 합니다.

```powershell
Get-HgsTrace -RunDiagnostics
```

HGS 구성은 아직 보호 된 패브릭 포함에서 될 호스트에 대 한 정보를 포함 하지 않으므로 호스트가 없습니다 아직 성공적으로 증명할 수는 진단 표시 됩니다. 이 결과 무시 하 고 진단에 의해 제공 된 다른 정보를 검토 합니다.

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

HGS 클러스터의 각 노드에서 진단 유틸리티를 실행 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [보호된 호스트 배포](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)

