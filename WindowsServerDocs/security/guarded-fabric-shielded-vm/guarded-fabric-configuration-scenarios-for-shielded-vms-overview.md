---
title: 보호된 VM 배포
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 5d1a06c9-24e1-4e14-9c9a-efb2adbfeddd
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f7892dabb028b99cb4cb1c9045764a8e36aba7dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386770"
---
# <a name="deploy-shielded-vms"></a>보호된 VM 배포


>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

다음 항목에서는 테 넌 트가 보호 된 Vm을 사용할 수 있는 방법에 대해 설명 합니다.

1. 필드 [Windows 템플릿 디스크를 만들거나](guarded-fabric-create-a-shielded-vm-template.md) [Linux 템플릿 디스크를 만듭니다](guarded-fabric-create-a-linux-shielded-vm-template.md). 테 넌 트 또는 호스팅 서비스 공급자에서 템플릿 디스크를 만들 수 있습니다. 

2. 필드 [기존 WINDOWS VM을 보호 된 vm으로 변환](guarded-fabric-vm-shielding-helper-vhd.md)합니다. 

3. 보호 [된 VM을 정의 하는 보호 데이터를 만듭니다](guarded-fabric-tenant-creates-shielding-data.md).

    보호 데이터 파일에 대 한 설명 및 다이어그램은 [보호 데이터 란 무엇 이며 필요한 이유는 무엇 인가요?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary) 를 참조 하세요.
    
    차폐 데이터 파일에 포함할 응답 파일을 만드는 방법에 대 한 자세한 내용은 [차폐 vm-ShieldingDataAnswerFile 함수를 사용 하 여 응답 파일 생성](guarded-fabric-sample-unattend-xml-file.md)을 참조 하세요.

4. 차폐 VM 만들기:
 
    - **Windows Azure 팩**사용: [Windows Azure 팩를 사용 하 여 보호 된 VM 배포](guarded-fabric-shielded-vm-windows-azure-pack.md)

    - **Virtual Machine Manager**사용: [Virtual Machine Manager를 사용 하 여 보호 된 VM 배포](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [보호 된 VM 템플릿 만들기](guarded-fabric-create-a-shielded-vm-template.md)

## <a name="see-also"></a>참조

- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
