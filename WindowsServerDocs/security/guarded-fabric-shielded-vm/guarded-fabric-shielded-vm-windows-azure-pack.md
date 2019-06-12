---
title: 테 넌 트-Windows Azure Pack을 사용 하 여 보호 된 VM을 배포에 대 한 보호 된 Vm
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 095315e4-c4a7-4b80-91d8-528119b62c4c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 600ccd74c379daa281f438b1200179dcae210817
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447356"
---
# <a name="shielded-vms--for-tenants---deploying-a-shielded-vm-by-using-windows-azure-pack"></a>테 넌 트-Windows Azure Pack을 사용 하 여 보호 된 VM을 배포에 대 한 보호 된 Vm

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016

호스팅 서비스 공급자에서 지원할 경우에 보호 된 VM을 배포 하려면 Windows Azure 팩을 사용할 수 있습니다.

다음 단계를 수행 합니다.

<!-- When we have a link to the topic about how tenants subscribe, add that link as an indented item just under step 1 below. -->

1. Windows Azure 팩에서 제공 하는 하나 이상의 계획을 구독 합니다.

2. Windows Azure Pack을 사용 하 여 보호 된 VM을 만듭니다.

    [보호 된 가상 머신을 사용 하 여](https://technet.microsoft.com/library/mt720674.aspx), 다음 항목에 설명 되어 있습니다.

   - [실딩 데이터 작성](https://technet.microsoft.com/library/mt720672.aspx) (및 항목의 두 번째 절차에 설명 된 대로 보호 데이터 파일 업로드) 합니다.
    
     > [!NOTE]
     > 실딩 데이터 만들기의 일환으로, utf-8 형식으로 XML 파일로 될에 보호자 키 파일을 다운로드 합니다. U t F-16으로 파일을 변경 하지 마세요.
    
   - [보호 된 가상 컴퓨터를 만들](https://technet.microsoft.com/library/mt720673.aspx) - **빠른 생성**, 보호 된 템플릿 또는 일반 템플릿.
    
       > [!WARNING]
       > 경우 있습니다 [일반 템플릿을 사용 하 여 보호 된 가상 컴퓨터를 만들](https://technet.microsoft.com/library/mt720673.aspx#Anchor_2), 것에 VM이 프로 비전 하는 유의 해야 *차폐 되지 않은*합니다. 이 의미는 실딩 데이터 파일에서 신뢰할 수 있는 디스크 목록과 비교 하 여 템플릿 디스크 검증 하지도 실딩 데이터 파일의 암호는 VM을 프로 비전을 사용 합니다. 보호 된 템플릿 사용 가능한 경우 엔드-투-엔드 비밀 보호 하기 위해 보호 된 템플릿 사용 하 여 보호 된 VM을 배포 하는 것이 좋습니다.
    
   - [2 세대 가상 컴퓨터 실드 된 가상 컴퓨터 변환](https://technet.microsoft.com/library/mt720670.aspx)
    
       > [!NOTE]
       > 가상 컴퓨터 실드 된 가상 머신을 변환할 기존 검사점 및 백업이 암호화 되지 않습니다. 오래 되 고 암호 해독 된 데이터에 대 한 액세스를 방지 하려면 가능한 경우 이전 검사점을 삭제 해야 합니다.

## <a name="see-also"></a>참조

- [보호 된 호스트 및 차폐 Vm 호스팅 서비스 공급자 구성 단계](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [보호된 패브릭 및 보호된 VM](guarded-fabric-and-shielded-vms-top-node.md)
