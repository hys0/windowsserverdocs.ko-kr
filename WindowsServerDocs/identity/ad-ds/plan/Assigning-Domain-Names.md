---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: 도메인 이름 할당
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ba5a7ee8b7d9728c48e2798853aab8d55047e86f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866564"
---
# <a name="assigning-domain-names"></a>도메인 이름 할당

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

계획의 모든 도메인에 이름을 할당 해야 합니다. Active Directory Domain Services (AD DS) 도메인에 두 유형의 이름이 있습니다. 도메인 이름 시스템 (DNS) 이름과 NetBIOS 이름입니다. 일반적으로 두 이름은 최종 사용자에 게 표시 됩니다. Active Directory 도메인의 DNS 이름은 두 부분, 접두사 및 접미사를 포함 합니다. 도메인 이름을 만들 경우 먼저 DNS 접두사를 확인 합니다. 이 도메인의 DNS 이름에서 첫 번째 레이블입니다. 접미사는 포리스트 루트 도메인의 이름을 선택 하면 결정 됩니다. 다음 표에서 DNS 이름에 대 한 명명 규칙 접두사를 나열 합니다.  
  
|규칙|설명|  
|--------|---------------|  
|못할 가능성이 있는 접두사를 선택 합니다.|제품군 또는 나중에 변경 될 수 있는 운영 체제와 같은 이름 하지 마세요. 지리적 이름을 사용 하는 것이 좋습니다.|  
|인터넷 표준 문자만 포함 하는 접두사를 선택 합니다.|(-) 및 A ~ Z, a-z, 0-9, 있지만 완전히 숫자입니다.|  
|15 문자 이하인 접두사입니다.|원하는 접두사 길이가 15 자 이하의 NetBIOS 이름 접두사 동일 합니다.|  
  
자세한 내용은 컴퓨터, 도메인, 사이트 및 Ou에 대 한 Active Directory의 명명 규칙 참조 ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629)).  
  
> [!NOTE]  
>  Windows Server 2008 및 Windows Server 2003의 Dcpromo.exe를 사용하면 단일 레이블 DNS 도메인 이름을 만들 수 있지만, 여러 가지 이유로 도메인에 단일 레이블 DNS 이름을 사용해서는 안 됩니다. Windows Server 2008 R2에서는 Dcpromo.exe를 사용하여 도메인에 단일 레이블 DNS 이름을 만들 수 없습니다. 자세한 내용은 [ https://go.microsoft.com/fwlink/?LinkId=92467합니다.](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
도메인의 현재 NetBIOS 이름을 지역을 나타내는 적절 하지 않으며, 명명 규칙 접두사에 맞게 실패 하는 경우 새 접두사를 선택 합니다. 이 경우 도메인의 NetBIOS 이름 도메인의 DNS 접두사에서 다릅니다.  
  
배포 하는 각 새 도메인에 대 한 명명 규칙 접두사를 충족 하는 지역에 대 한 적절 한 접두사를 선택 합니다. 도메인의 NetBIOS 이름을 동일 하 게 DNS 접두사로 하는 것이 좋습니다.  
  
포리스트의 각 도메인에 대해 선택 된 NetBIOS 이름을 확인 하 고 DNS 접두사를 문서화 합니다. 신규 및 업그레이드 도메인에 대 한 계획을 문서화 하기 위해 만든 "도메인 계획" 워크시트에 DNS 및 NetBIOS 이름 정보를 추가할 수 있습니다. 를 열려면 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 다운로드 ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) "도메인 계획" (DSSLOGI_5.doc)를 엽니다.  
  


