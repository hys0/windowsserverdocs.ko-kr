---
title: HGS 구성 확인
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 8f01df37-f18e-4386-ae73-ecf84feaa9df
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: d219b7aa9ca1e17df3281fd756106a6f07864116
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386352"
---
# <a name="verify-the-hgs-configuration"></a>HGS 구성 확인

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016


다음으로, 작업이 예상 대로 작동 하는지 확인 해야 합니다. 이렇게 하려면 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행 합니다.

```powershell
Get-HgsTrace -RunDiagnostics
```

HGS 구성에는 보호 된 패브릭에 있는 호스트에 대 한 정보가 아직 포함 되어 있지 않기 때문에 진단에서 아직 호스트를 증명할 수 없다는 메시지가 표시 됩니다. 이 결과를 무시 하 고 진단에서 제공 하는 다른 정보를 검토 합니다.

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

HGS 클러스터의 각 노드에서 진단을 실행 합니다.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [보호된 호스트 배포](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)

