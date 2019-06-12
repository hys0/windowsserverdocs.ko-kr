---
title: 보호된 VM 배포
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 5d1a06c9-24e1-4e14-9c9a-efb2adbfeddd
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9badbfcb709c29451425aaecc56b46ac98837e18
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443807"
---
# <a name="deploy-shielded-vms"></a>보호된 VM 배포


>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

다음 항목은 보호 된 Vm 함께 테 넌 트를 사용 하는 방법을 설명 합니다.

1. (선택 사항) [Windows 템플릿 디스크를 만듭니다](guarded-fabric-create-a-shielded-vm-template.md) 하거나 [Linux 템플릿 디스크 만들기](guarded-fabric-create-a-linux-shielded-vm-template.md)합니다. 테 넌 트 또는 호스팅 서비스 공급자에서 템플릿 디스크를 만들 수 있습니다. 

2. (선택 사항) [보호 된 VM에 기존 Windows VM을 변환](guarded-fabric-vm-shielding-helper-vhd.md)합니다. 

3. [보호 된 VM을 정의 하려면 실딩 데이터 작성](guarded-fabric-tenant-creates-shielding-data.md)합니다.

    설명 및 다이어그램 실딩 데이터 파일의 내용은 [실딩 데이터는 무엇 이며 왜 필요?](guarded-fabric-and-shielded-vms.md#what-is-shielding-data-and-why-is-it-necessary)
    
    보호 된 데이터 파일에 포함 하도록 응답 파일을 만드는 방법에 대 한 자세한 내용은 [보호 된 Vm-New-shieldingdataanswerfile 함수를 사용 하 여 응답 파일 생성](guarded-fabric-sample-unattend-xml-file.md)합니다.

4. 보호 된 VM을 만듭니다.
 
    - 사용 하 여 **Windows Azure 팩**: [Windows Azure Pack을 사용 하 여 보호 된 VM 배포](guarded-fabric-shielded-vm-windows-azure-pack.md)

    - 사용 하 여 **Virtual Machine Manager**: [Virtual Machine Manager 사용 하 여 보호 된 VM 배포](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [보호 된 VM 템플릿 만들기](guarded-fabric-create-a-shielded-vm-template.md)

## <a name="see-also"></a>참조

- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
