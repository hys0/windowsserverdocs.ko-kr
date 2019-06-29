---
title: 클라이언트 액세스 라이선스 관리
description: MultiPoint 서비스에서 Cal을 사용 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 675e089e-d841-401e-bba7-69f3929ef609
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 42b943ed5e0066f1f810efaba9e65a529ac25f00
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469352"
---
# <a name="manage-client-access-licenses"></a>클라이언트 액세스 라이선스 관리
MultiPoint Service를 스테이션으로 사용 되는 실행 중인 컴퓨터를 포함 하 여 MultiPoint 서비스 시스템에 연결 하는 모든 스테이션에 유효한 사용자 원격 데스크톱 있어야 *클라이언트 액세스 라이선스 (CAL)* 합니다.

스테이션 가상 데스크톱 스테이션 실제 대신를 사용 하는 경우 각 스테이션 가상 데스크톱에 대 한 CAL을 설치 해야 합니다.  
  
1.  MultiPoint 서비스 컴퓨터 또는 서버에 연결 된 각 스테이션에 대 한 클라이언트 라이선스를 구입 합니다. Cal을 구입 하는 방법에 대 한 자세한 내용은 원격 데스크톱 라이선스에 대 한 설명서를 참조 하세요. 

2.  **시작** 화면이 열리면서 **다중 포인트 관리자**합니다.  
  
3.  클릭 합니다 **홈** 탭을 클릭 한 다음 **클라이언트 액세스 라이선스 추가**합니다.  CAL 라이선스에 대 한 관리 도구가 열립니다.

# <a name="set-the-licensing-mode-manually"></a>라이선스 모드를 수동으로 설정
그렇지 않은 경우 제대로 구성 MultiPoint 서비스 설정 묻는 알림이 만료 되 고 유예 기간에 대 한 합니다. 라이선스 모드를 설정 하려면 다음이 단계를 수행 합니다.

1. 시작할 **로컬 그룹 정책 편집기** (gpedit.msc).

2. 왼쪽된 창에서로 이동 **로컬 컴퓨터 정책-> 컴퓨터 구성-> 관리 템플릿 Windows-> 구성 요소-> 원격 데스크톱 서비스-> 원격 데스크톱 세션 호스트-라이선스 >** 합니다.

3. 오른쪽 창에서 마우스 오른쪽 단추로 클릭 **지정 된 원격 데스크톱 라이선스 서버를 사용 하 여** 선택한 **편집**:
   - 그룹 정책 편집기 대화 상자에서 선택 **사용**
   - 로컬 컴퓨터 이름을 입력 합니다 **서버를 사용 하 여 라이선스** 필드.
   - 선택 **확인**
  
4. 오른쪽 창에서 마우스 오른쪽 단추로 클릭 **원격 데스크톱 라이선스 모드를 설정할** 선택한 **편집**
   - 그룹 정책 편집기 대화 상자에서 선택 **사용**
   - 설정 된 **라이선스 모드** 를 장치별 / 사용자 당
   - 선택 **확인** 

  
## <a name="see-also"></a>관련 항목  
[MultiPoint 관리자를 사용하여 시스템 작업 관리](Manage-System-Tasks-Using-MultiPoint-Manager.md)
