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
ms.openlocfilehash: 954393126333bf04d2aa46a01089d88bc91151cb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447326"
---
# <a name="verify-the-hgs-configuration"></a>HGS 구성 확인

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019


다음으로, 작업 예상 대로 작동 하는지 유효성을 검사 해야 합니다. 이렇게 하려면 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행 합니다.

```powershell
Get-HgsTrace -RunDiagnostics
```

HGS 구성은 아직 보호 된 패브릭 포함에서 될 호스트에 대 한 정보를 포함 하지 않으므로 호스트가 없습니다 아직 성공적으로 증명할 수는 진단 표시 됩니다. 이 결과 무시 하 고 진단에 의해 제공 된 다른 정보를 검토 합니다.

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

<!-- When a link is available for an updated troubleshooting guide, add a sentence like the following and create a link to the troubleshooting guide:
If failures did occur, please review the remediation steps provided or see the Troubleshooting Guide.
-->

HGS 클러스터의 각 노드에서 진단 유틸리티를 실행 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [보호된 호스트 배포](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)

