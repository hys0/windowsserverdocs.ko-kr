---
title: Windows Server Essentials에서 애플리케이션 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: ae89c46a-0afd-4858-9150-ec97650f45a4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: bc85199849b140aa8d1ef2f98fd009a1d43bb01b
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470858"
---
# <a name="manage-applications-in-windows-server-essentials"></a>Windows Server Essentials에서 애플리케이션 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 Windows server essentials Experience 역할이 설치 된 windows Server Essentials 및 Windows Server 2012 r 2의 서버 대시보드에서 일반적인 관리 작업을 수행할 수 있습니다. 이러한 작업을 수행하려면 다음을 참조하세요.

-   [대시보드의 애플리케이션 관리 작업](Manage-Applications-in-Windows-Server-Essentials.md#BKMK_1)

-   [대시보드를 사용하여 추가 기능 설치 또는 제거](Manage-Applications-in-Windows-Server-Essentials.md#BKMK_2)

##  <a name="application-management-tasks-in-the-dashboard"></a><a name="BKMK_1"></a>대시보드의 응용 프로그램 관리 작업
 대시보드의 **응용 프로그램** 관리 페이지는 다음 정보를 제공합니다.

- 다음을 표시하는 설치된 추가 기능 목록:

  -   온라인 서비스 또는 추가 기능의 이름

  -   추가 기능의 업데이트 상태

  -   추가 기능의 구독 상태

  -   추가 기능을 제공하는 회사 또는 게시자의 이름

- 선택한 추가 기능을 관리하기 위한 작업 집합을 포함하는 작업 창

- Microsoft Pinpoint에서 다운로드하여 설치할 수 있는 추가 기능 목록

  다음 표에서는 서버 대시보드에서 사용할 수 있는 다양한 추가 기능 관리 작업에 대해 설명합니다. 일부 작업은 추가 기능과만 관련되므로 목록에서 추가 기능을 선택할 때만 표시됩니다.

|작업 이름|설명|
|---------------|-----------------|
|추가 기능 제거|서버 및 네트워크의 모든 다른 컴퓨터에서 선택된 추가 기능을 제거합니다.|
|네트워크 컴퓨터에 추가 기능 설치|네트워크의 모든 다른 컴퓨터에서 선택된 추가 기능의 설치를 예약할 수 있습니다.|
|추가 기능 도움말 보기|인터넷 브라우저를 열고 문제의 해결 방법을 검색할 수 있는 웹 사이트로 이동한 다음 선택한 추가 기능에 대해 자세히 알아봅니다.|
|추가 기능 업데이트|서버 및 네트워크 컴퓨터에 설치된 추가 기능에 대한 업데이트를 다운로드하여 설치할 수 있습니다.|
|추가 기능 구독 갱신|인터넷 브라우저를 열고 추가 기능 구독을 갱신할 수 있는 소스 웹 사이트로 이동합니다.|
|추가 기능에 대한 개인 정보 취급 방침 읽기|인터넷 브라우저를 열고 개인 정보 취급 방침을 볼 수 있는 소스 웹 사이트로 이동합니다.|
|추가 기능을 설치 또는 제거하는 방법|인터넷 브라우저를 열고 주제 도움말 항목을 표시하는 웹 페이지로 이동합니다.|

##  <a name="install-or-remove-add-ins-using-the-dashboard"></a><a name="BKMK_2"></a>대시보드를 사용 하 여 추가 기능 설치 또는 제거
 추가 기능은 서버에 대한 추가적인 기능을 제공하는 소프트웨어 애플리케이션입니다. Microsoft 및 기타 ISV(Independent Software Vendor)에서 점점 더 많은 추가 기능을 제공하고 있습니다.

 추가 기능이 제공하는 확장 기능을 사용하려면 먼저 서버에 추가 기능을 설치해야 합니다.

#### <a name="to-install-an-add-in-from-microsoft-pinpoint"></a>Microsoft Pinpoint에서 추가 기능을 설치하려면

1.  서버 대시보드에서 **응용 프로그램**을 클릭 한 다음 **Microsoft의 Microsoft** 에서 탭을 클릭 합니다.  사용 가능한 추가 기능 목록이 표시 됩니다.

2.  설치할 추가 기능을 클릭합니다. 추가 기능 정보 페이지가 표시됩니다.

3.  추가 기능 정보 페이지에서 다운로드를 클릭하고 화면 지침에 따라 추가 기능을 다운로드하여 설치합니다.

4.  마법사의 지침에 따라 추가 기능을 설치합니다.

5.  설치가 완료되면 대시보드를 다시 시작하고 서버 대시보드의 **응용 프로그램** 페이지를 연 다음 목록 뷰에 추가 기능이 표시되는지 확인합니다.

#### <a name="to-install-an-add-in-from-another-provider"></a>다른 공급자의 추가 기능을 설치하려면

1.  Windows 탐색기를 열고 추가 기능 설치 파일이 있는 위치로 이동합니다.

2.  파일을 두 번 클릭하여 설치 마법사를 실행합니다.

3.  마법사의 지침에 따라 추가 기능을 설치합니다.

4.  설치가 완료되면 대시보드를 다시 시작하고 **응용 프로그램** 페이지를 연 다음 목록 뷰에 추가 기능이 표시되는지 확인합니다.

#### <a name="to-remove-an-add-in"></a>추가 기능을 제거하려면

1.  서버 대시보드를 엽니다.

2.  **응용 프로그램** 탭을 클릭합니다.

3.  **추가 기능** 탭에서 제거할 추가 기능을 선택하고 **추가 기능 제거**를 클릭합니다.

4.  **추가 기능 제거** 창에서 **제거**를 클릭합니다.

    > [!NOTE]
    >  추가 기능을 완전히 제거하려면 대시보드를 다시 시작해야 할 수 있습니다.

## <a name="additional-references"></a>추가 참조

-   [대시보드 개요](Overview-of-the-Dashboard-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials 관리](Manage-Windows-Server-Essentials.md)
