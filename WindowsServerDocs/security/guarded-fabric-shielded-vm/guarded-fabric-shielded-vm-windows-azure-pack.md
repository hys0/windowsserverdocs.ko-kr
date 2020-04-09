---
title: 테 넌 트 용 차폐 vm-Windows Azure 팩를 사용 하 여 보호 된 VM 배포
ms.prod: windows-server
ms.topic: article
ms.assetid: 095315e4-c4a7-4b80-91d8-528119b62c4c
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ce3aac47ea6c44abd1811efc1e23b901f53333bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856466"
---
# <a name="shielded-vms--for-tenants---deploying-a-shielded-vm-by-using-windows-azure-pack"></a>테 넌 트 용 차폐 vm-Windows Azure 팩를 사용 하 여 보호 된 VM 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016

호스팅 서비스 공급자가 지 원하는 경우 Windows Azure 팩를 사용 하 여 보호 된 VM을 배포할 수 있습니다.

다음 단계를 완료 합니다.

1. Windows Azure 팩에서 제공 하는 하나 이상의 계획을 구독 합니다.

2. Windows Azure 팩를 사용 하 여 보호 된 VM을 만듭니다.

    [보호 된 가상 컴퓨터를 사용](https://technet.microsoft.com/library/mt720674.aspx)합니다 .이에 대해서는 다음 항목에서 설명 합니다.

   - 항목의 두 번째 절차에 설명 된 대로 [보호 데이터를 만들고](https://technet.microsoft.com/library/mt720672.aspx) 보호 데이터 파일을 업로드 합니다.
    
     > [!NOTE]
     > 보호 데이터를 만드는 과정의 일부로 보호 키 파일을 다운로드 합니다 .이 파일은 UTF-8 형식의 XML 파일이 됩니다. 파일을 u t f-16으로 변경 하지 마십시오.
    
   - 차폐 템플릿 또는 일반 템플릿을 통해 **빠른 생성**을 사용 하 여 [차폐 가상 머신을 만듭니다](https://technet.microsoft.com/library/mt720673.aspx) .
    
       > [!WARNING]
       > [일반 템플릿을 사용 하 여 보호 된 가상 컴퓨터를 만드는](https://technet.microsoft.com/library/mt720673.aspx#Anchor_2)경우 VM이 *보호 되지 않는*으로 프로 비전 된다는 점에 유의 해야 합니다. 즉, 보호 데이터 파일의 신뢰할 수 있는 디스크 목록에 대해 템플릿 디스크가 확인 되지 않으며, VM을 프로 비전 하는 데 사용 되는 보호 데이터 파일의 비밀이 아닙니다. 차폐 템플릿을 사용할 수 있는 경우 보호 된 템플릿을 사용 하 여 보호 된 VM을 배포 하는 것이 좋습니다 .이를 통해 암호의 종단 간 보호를 제공할 수 있습니다.
    
   - [2 세대 가상 컴퓨터를 보호 된 가상 컴퓨터로 변환](https://technet.microsoft.com/library/mt720670.aspx)
    
       > [!NOTE]
       > 가상 컴퓨터를 보호 된 가상 컴퓨터로 변환 하는 경우 기존 검사점 및 백업은 암호화 되지 않습니다. 이전에 해독 된 데이터에 대 한 액세스를 방지 하기 위해 가능한 경우 오래 된 검사점을 삭제 해야 합니다.

## <a name="see-also"></a>참고 항목

- [보호 된 호스트 및 보호 된 Vm에 대 한 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
