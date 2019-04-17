---
title: "Windows Server Essentials 구성원 서버로 추가"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d09dd82f-f7d2-47ce-862d-fd9869f2021c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8fb73f8186d3984c9e93f7a6e39cb72a54db1e58
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="add-windows-server-essentials-as-a-member-server"></a>Windows Server Essentials 구성원 서버로 추가

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

이 항목은 Windows Server Essentials 경험 역할이 설치 된 Windows Server 2012 r 2 표준, Windows Server 2012 R2 Datacenter 또는 Windows Server 2016을 실행 하는 서버에 적용 됩니다. 이 문서의 나머지 부분에 Windows Server Essentials 경험 역할은 라고 Windows Server Essentials 합니다.  
  
> [!NOTE]
>   Windows Server Essentials 도메인 컨트롤러로만 배포 될 수 있습니다. 이 문서에서는 Windows Server Essentials Windows Server Essentials 포함 되지 않습니다.  
  
 Windows Server Essentials는 Windows 도메인 내 주 서버로 필요가 없습니다. 기존 Active Directory 도메인 환경에 Windows Server Essentials 구성원 서버로 추가 하 고 간단한 데이터 보호, 보안 원격 액세스 및 클라우드 통합 기능을 이용할 수 있습니다. 또한 Windows Server Essentials 도메인 컨트롤러를 않고도 기존 Active Directory 환경에 배포할 수 있습니다. 이렇게 하면 저장소 확장 하거나 로컬 저장소와 관리에 대 한 지점 사용할 수 있습니다.  
  
 Windows Server Essentials 다음과 같은 경우에 추가할 수 있습니다.  
  
-   Windows Server Essentials 지점 위치에서 추가 하 고 기본 도구를 사용 하 여 본사 별도 위치에 있는 도메인 컨트롤러에 참여 합니다. 이 구성원 서버의 최적의 대역폭 사용에 대 한 BranchCache 기능을 켤 수 있습니다.  
  
-   Windows Server Essentials 구성원 서버로 구성원 서버에 추가 서버 폴더를 추가 하 여 네트워크의 메모리 연장 하기 위해 Windows Server Essentials 네트워크에 추가 합니다.  
  
-   제 3 자 호스팅에서 주최한 또는 Windows Server Essentials 실행 하는 기본 서버 Microsoft Azure에서 호스트 되는 경우 Windows Server Essentials 구성원 서버 로컬 사무실에 추가 합니다. Windows Server Essentials 대역폭 사용을 최적화 하 여 로컬 office 사이트는 구성원 서버로 것입니다.  
  
## <a name="adding-windows-server-essentials-as-a-member-server"></a>Windows Server Essentials 구성원 서버로 추가  
 Windows Server Essentials 구성원 서버로 주 서버 기존 Active Directory 환경에 Windows Server 2012 R2 또는 Windows Server Essentials 실행을 추가 하려면 다음 단계를 완료 해야 합니다.  
  
1.  Windows Server Essentials 작업 그룹에 실행 하는 서버에 참여 합니다.  
  
2.  Windows Server Essentials 기본 Windows Server Essentials 서버 도메인을 실행 하는 서버에 참여 합니다.  
  
3.  Windows Server Essentials 경험 서버 관리자에서를 구성 합니다.  
  
#### <a name="to-join-windows-server-essentials-to-a-workgroup-or-domain"></a>Windows Server Essentials 도메인 또는 작업 그룹에 연결 하려면  
  
1.  두 번째 서버에 Windows Server Essentials의 설치를 완료 한 후 Windows Server Essentials 구성 마법사 닫습니다.  
  
2.  에 **검색** 상자에 입력 **시스템 설정**, 검색 결과 클릭 하 고 **고급 시스템 설정 보기**합니다.  
  
3.  **시스템 속성**, 클릭 하 고 **컴퓨터 이름** 탭 합니다.  
  
4.  **컴퓨터 이름을**에 **도메인** 섹션에서 클릭 **변경**합니다.  
  
5.  **컴퓨터 도메인 이름/변경**에 **회원** 섹션에 Windows Server Essentials 실행 하는 서버에 참여 하려는 경우를 선택 합니다는 **작업 그룹** 하거나는 **도메인**합니다.  
  
    -   서버를 작업 그룹에 추가 하려면 입력 **작업 그룹**을 차례로 클릭 하 고 **확인**합니다.  
  
    -   이 서버 기존 Active Directory 도메인에 참여 하는 도메인의 이름을 입력 하 고 클릭 한 다음 **확인**합니다.  
  
6.  변경 내용을 적용 하려면 서버를 다시 시작 합니다.  
  
 서버 주 서버의 도메인에 가입한, 후 구성 Windows Server Essentials 마법사 서버 관리자에서 실행 하 여 Windows Server Essentials 구성할 수 계속할 수 있습니다.  
  
#### <a name="to-configure-windows-server-essentials-experience-on-a-member-server"></a>Windows Server Essentials 경험 구성원 서버의 구성 하려면  
  
1.  (선택 사항) 서버 이름 필요한 경우 변경 합니다.  
  
    > [!IMPORTANT]
    >  서버 이름 Windows Server Essentials 환경 구성한 경우 변경할 수 없습니다.  
  
2.  사용자 도메인 관리자 계정을 사용 하 여 서버에 로그인 합니다.  
  
3.  서버 관리자를 엽니다.  
  
4.  플래그 알림 영역에서 **서버 관리자**, 플래그를 클릭 한 다음 클릭 **Windows Server Essentials 구성**합니다.  
  
5.  서버 구성원 서버 구성 하도록 선택 하 고 클릭 한 다음 **다음**합니다.  
  
6.  클릭 **구성** 구성을 시작 합니다. 구성 프로세스를 완료 하려면 10 분 정도 걸립니다.  
  
7.  바탕 화면을 대시보드 서버를 시작 하려면 대시보드 아이콘을 클릭 합니다. 홈 페이지를 완료는 **시작** 에 나열 된 하는 작업은 **설치** 탭 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  

-   [Windows Server Essentials 설치](Install-Windows-Server-Essentials.md)

-   [Windows Server Essentials 설치](../install/Install-Windows-Server-Essentials.md)

