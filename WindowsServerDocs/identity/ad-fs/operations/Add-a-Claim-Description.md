---
ms.assetid: 7d230527-f4fe-4572-8838-0b354ee0b06b
title: 클레임 설명 추가
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0e388ef656d3b690da62b077cb9f9e678a771e64
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851434"
---
# <a name="add-a-claim-description"></a>클레임 설명 추가

>적용 대상: Windows Server 2016, Windows Server 2012 R2

계정 파트너 조직의 관리자가 그룹 또는 역할에서 사용자의 등록을 나타내는 또는 직원 id 번호를 사용자의 예를 들어 사용자에 대 한 일부 데이터를 나타내는 클레임을 만듭니다.

리소스 파트너 조직에서 관리자 그룹 및 리소스 사용자로 인식 될 수 있는 사용자를 나타내는 해당 클레임을 만듭니다. 나가는 클레임을 계정 파트너 조직 지도 들어오는 클레임 리소스 파트너 조직의 리소스 파트너 때문에 자격 증명을 제공 하는 계정 파트너를 받아들일 수 있습니다. 

다음 절차를 사용 하 여 클레임을 추가할 수 있습니다.

로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.

## <a name="to-add-a-claim-description"></a>클레임 설명을 추가 하려면

1. 서버 관리자에서 클릭 **도구**, 를 선택한 다음 **AD FS 관리**합니다. 

2.  확장 **서비스** 에서 마우스 오른쪽 단추로 클릭 하 고 **클레임 설명 추가**합니다.
![클레임 설명 추가](media\Add-a-Claim-Description\claimdesc1.png)

3.  추가 클레임 설명 대화 상자의 **표시 이름**, 그룹 또는이 클레임에 대 한 역할을 식별 하는 고유한 이름을 입력 합니다.

4.  추가 **짧은 이름을**합니다.

5.  **클레임 식별자**, 연결 된 그룹 또는 역할 사용 하는 클레임의 URI를 입력 합니다.

6.  아래에서 **설명**, 를 가장 잘이 클레임의 용도 설명 하는 텍스트를 입력 합니다.

7.  조직의 요구에 따라 페더레이션 메타 데이터를이 클레임을 게시할 수 적절 하 게 다음 확인란 중 하나를 선택 합니다.


    - 이 클레임을이 서버에이 클레임을 수락할 수 있음을 인식 하는 파트너를 게시 하려면 **이 클레임을이 페더레이션 서비스에서 수락할 수 있는 클레임 유형으로 페더레이션 메타 데이터에 게시**합니다.
    - 이 클레임을이 서버가이 클레임을 발급할 수 인식 파트너를 게시 하려면 **이 클레임을이 페더레이션 서비스에 보낼 수 있는 클레임 유형으로 페더레이션 메타 데이터에 게시**합니다.

8.  **확인**을 클릭합니다.

![클레임 설명 추가](media\Add-a-Claim-Description\claimdesc2.png)

  
## <a name="see-also"></a>관련 항목  
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md) 
