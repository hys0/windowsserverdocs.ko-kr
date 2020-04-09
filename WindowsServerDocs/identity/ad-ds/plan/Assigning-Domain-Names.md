---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: 도메인 이름 할당
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0d605a2f0d0b98a65848f94be9803122c4492a8b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822846"
---
# <a name="assigning-domain-names"></a>도메인 이름 할당

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

계획의 모든 도메인에 이름을 할당 해야 합니다. Active Directory Domain Services (AD DS) 도메인에는 DNS (Domain Name System) 이름 및 NetBIOS 이름 이라는 두 가지 유형의 이름이 있습니다. 일반적으로 최종 사용자에 게 두 이름이 모두 표시 됩니다. Active Directory 도메인의 DNS 이름에는 접두사와 접미사가 포함 되어 있습니다. 도메인 이름을 만들 때 먼저 DNS 접두사를 확인 합니다. 도메인의 DNS 이름에 있는 첫 번째 레이블입니다. 접미사는 포리스트 루트 도메인의 이름을 선택할 때 결정 됩니다. 다음 표에서는 DNS 이름에 대 한 접두사 명명 규칙을 보여 줍니다.  
  
|규칙|설명|  
|--------|---------------|  
|오래 될 가능성이 없는 접두사를 선택 합니다.|나중에 변경 될 수 있는 제품 라인 또는 운영 체제와 같은 이름을 사용 하지 마십시오. 지리적 이름을 사용 하는 것이 좋습니다.|  
|인터넷 표준 문자만 포함 하는 접두사를 선택 합니다.|A-z, a-z, 0-9 및 (-) 이지만 완전히 숫자로는 그렇지 않습니다.|  
|접두사에 15 자 이하의 값을 포함 합니다.|15 자 이하의 접두사 길이를 선택 하는 경우 NetBIOS 이름은 접두사와 동일 합니다.|  
  
자세한 내용은 컴퓨터, 도메인, 사이트 및 Ou에 대 한 Active Directory의 명명 규칙 ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629))을 참조 하세요.  
  
> [!NOTE]  
>  Windows Server 2008 및 Windows Server 2003의 Dcpromo.exe를 통해 단일 레이블 DNS 도메인 이름을 만들 수 있지만 몇 가지 이유 때문에 도메인에 대한 단일 레이블 DNS 도메인 이름을 사용하면 안 됩니다. Windows Server 2008 R2에서 Dcpromo.exe는 도메인에 대한 단일 레이블 DNS 도메인 이름을 만들 수 없습니다. 자세한 내용은 https://go.microsoft.com/fwlink/?LinkId=92467를 참조 [하세요.](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
도메인의 현재 NetBIOS 이름이 지역을 나타내는 데 적합 하지 않거나 접두사 명명 규칙을 충족 하지 못하는 경우 새 접두사를 선택 합니다. 이 경우 도메인의 NetBIOS 이름은 도메인의 DNS 접두사와 다릅니다.  
  
배포 하는 각 새 도메인에 대해 지역에 적합 하 고 접두사 명명 규칙을 충족 하는 접두사를 선택 합니다. 도메인의 NetBIOS 이름을 DNS 접두사와 동일 하 게 하는 것이 좋습니다.  
  
포리스트의 각 도메인에 대해 선택 하는 DNS 접두사 및 NetBIOS 이름을 문서화 합니다. 새 도메인 및 업그레이드 된 도메인에 대 한 계획을 문서화 하기 위해 만든 "도메인 계획" 워크시트에 DNS 및 NetBIOS 이름 정보를 추가할 수 있습니다. 이 파일을 열려면 Windows Server 2003 배포 키트 ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))에 대 한 작업 지원에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고 "도메인 계획" (DSSLOGI_5 .doc)을 엽니다.  
  


