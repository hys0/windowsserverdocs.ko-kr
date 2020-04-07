---
title: 1 단계-WSUS 서버 역할 설치
description: WSUS(Windows Server Update Service) 항목 - 서버 관리자를 사용하여 서버 역할을 설치하는 방법 설명
ms.prod: windows-server
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: article
ms.assetid: fabc8619-350e-403b-96f8-116424931300
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d71a26cbe889f5de11934b2af411ac407fc5e75
ms.sourcegitcommit: 3c3dfee8ada0083f97a58997d22d218a5d73b9c4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80639857"
---
# <a name="step-1-install-the-wsus-server-role"></a>1단계: WSUS 서버 역할 설치

>적용 대상: Windows Server 2019, Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

WSUS 서버 배포의 다음 단계는 WSUS 서버 역할을 설치하는 것입니다. 다음 절차에서는 서버 관리자를 사용하여 WSUS 서버를 설치하는 방법을 설명합니다.

> [!IMPORTANT]
> 이 설치 절차에서는 WID(Windows 내부 데이터베이스)를 사용하여 WSUS를 설치하는 방법에 대해서만 다룹니다. Microsoft SQL Server를 사용하여 WSUS를 설치하는 절차는 [이 문서](https://social.technet.microsoft.com/wiki/contents/articles/10020.installing-wsus-server-role-on-windows-server-2012-with-microsoft-sql-database.aspx)에 설명되어 있습니다.

### <a name="to-install-the-wsus-server-role"></a>WSUS 서버 역할을 설치하려면

1.  로컬 관리자 그룹의 구성원인 계정을 사용하여 WSUS 서버 역할을 설치할 서버에 로그온합니다.

2.  **서버 관리자**에서 **관리**, **역할 및 기능 추가**를 차례로 클릭합니다.

3.  **시작하기 전** 페이지에서 **다음**을 클릭합니다.

4.  **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치** 옵션이 선택되어 있는지 확인하고 **다음**을 클릭합니다.

5.  **대상 서버 선택** 페이지에서는 서버 위치(서버 풀 또는 가상 하드 디스크에서)를 선택합니다 위치를 선택한 후 WSUS 서버 역할을 설치할 서버를 선택하고 **다음**을 클릭합니다.

6.  **서버 역할 선택** 페이지에서 **Windows Server Update Services**를 선택합니다.  **Windows Server Update Services에 필요한 기능 추가** 가 열립니다. **기능 추가**를 클릭한 후 **다음**을 클릭합니다.

7.  **기능 선택**페이지에서 기본 선택 항목을 유지하고 **다음**을 클릭합니다.

    > [!IMPORTANT]
    > WSUS에는 기본 웹 서버 역할 구성만 필요합니다. WSUS를 설정하는 동안 추가 웹 서버 역할 구성에 대한 메시지가 표시되면 기본값을 안전하게 허용하고 계속해서 WSUS를 설정할 수 있습니다.

8.  **Windows Server Update Services** 페이지에서 **다음**을 클릭합니다.

9. **역할 서비스 선택** 페이지에서 기본 선택 항목을 그대로 사용하고 **다음**을 클릭합니다.

    > [!TIP]
    > 데이터베이스 유형을 하나 선택해야 합니다. 데이터베이스 옵션이 모두 선택 취소된 경우(선택되지 않음) 설치 후 작업이 실패합니다.

10. **콘텐츠 위치 선택** 페이지에서 업데이트를 저장할 올바른 위치를 입력합니다. 예를 들어 특별히 이 용도로 K 드라이브의 루트에 WSUS_database라는 폴더를 만들고 유효한 위치로 **k:\WSUS_database** 를 입력할 수 있습니다.

11. **다음**을 클릭합니다. **웹 서버 역할(IIS)** 페이지가 열립니다. 정보를 검토하고 **다음**을 클릭합니다. **웹 서버(IIS)에 설치할 역할 서비스 선택**에서 기본값을 유지하고 **다음**을 클릭합니다.

12. **설치 선택 확인** 페이지에서 선택한 옵션을 검토한 후 **설치**를 클릭합니다. WSUS 설치 마법사가 실행됩니다. 이 작업을 완료하는 데 몇 분 정도 걸릴 수 있습니다.

13. WSUS 설치가 완료되면 **설치 진행률** 페이지의 요약 창에서 **사후 설치 작업 시작**을 클릭합니다. 텍스트가 변경되고 다음을 요청합니다. **서버가 구성되는 동안 잠시 기다려 주세요**. 작업이 완료되면 텍스트가 다음과 같이 변경됩니다. **구성이 완료되었습니다**. **닫기**를 클릭합니다.

14. **서버 관리자**에서 다시 시작해야 함을 알리는 메시지가 표시되는지 확인합니다. 이는 설치된 서버 역할에 따라 다를 수 있습니다. 다시 시작해야 하는 경우 서버를 다시 시작해야 설치가 완료됩니다.

> [!IMPORTANT]
> 설치 과정은 이 시점에서 끝나지만 WSUS를 사용하려면 계속해서 [2단계: WSUS 구성](2-configure-wsus.md) 과정을 진행해야 합니다.

