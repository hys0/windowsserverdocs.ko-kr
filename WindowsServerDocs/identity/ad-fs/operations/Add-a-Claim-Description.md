---
ms.assetid: 7d230527-f4fe-4572-8838-0b354ee0b06b
title: "클레임 설명을 추가합니다"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0e388ef656d3b690da62b077cb9f9e678a771e64
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-claim-description"></a>클레임 설명을 추가합니다

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

계정 파트너 조직에서 관리자 클레임을 나타내는 그룹이 나 역할에서 사용자의 등록 하거나 일부 데이터는 사용자의 직원 id 번호 예를 들어, 사용자에 대 한 일을 만듭니다.

리소스 파트너 조직에서 관리자가 그룹 및 리소스 사용자가 인식 될 수 있는 사용자를 나타내는 해당 클레임 만듭니다. 리소스 파트너 들어오는 클레임 리소스 파트너 조직에서 계정 파트너 조직 맵의 주장 보내는 때문에 계정 파트너 제공 자격 증명을 받을 수 있습니다. 

다음 절차 클레임 추가를 사용할 수 있습니다.

회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.

## <a name="to-add-a-claim-description"></a>클레임 설명을 추가 하려면

1. 서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다. 

2.  확장 **서비스** 에서 오른쪽 클릭 및 **클레임 설명 추가**합니다.
![클레임 설명을 추가합니다](media\Add-a-Claim-Description\claimdesc1.png)

3.  추가 대 한 주장 대화 상자의 **표시 이름**,이 클레임에 대 한 역할 하나 또는 여러 개의 식별 하는 고유한 이름을 입력 합니다.

4.  추가 한 **짧은 이름**합니다.

5.  **클레임 식별자**, 연결 된 그룹이 나 사용 하는 클레임 역할 URI를 입력 합니다.

6.  아래에서 **설명**, 가장 잘이 클레임 목적을 설명 하는 텍스트를 입력 합니다.

7.  조직의 필요에 따라 해당 federation 메타 데이터에이 청구를 게시 하로 다음 확인란 중 하나를 선택 합니다.


    - 이 서버가이 청구를 사용할 수 있는 인식 파트너를 위해이 청구를 게시 클릭 **이 Federation 서비스를 사용할 수 있는 클레임 형식으로 federation 메타 데이터에이 청구를 게시**합니다.
    - 파트너 인식이 서버가이 클레임을 실행할 수 있도록이 청구를 게시 클릭 **이 Federation 서비스를 보낼 수 있는 클레임 형식으로 federation 메타 데이터에이 청구를 게시**합니다.

8.  클릭 **확인**합니다.

![클레임 설명을 추가합니다](media\Add-a-Claim-Description\claimdesc2.png)

  
## <a name="see-also"></a>참조 하십시오  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
