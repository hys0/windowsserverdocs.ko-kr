---
title: "Windows Server Essentials 로그 수집기 실행"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d340223-fa24-4c75-ba8e-b654feb120ab
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6b49fee7ca4a19d5a501cf96c1ce356f8242c81f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="run-the-windows-server-essentials-log-collector"></a>Windows Server Essentials 로그 수집기 실행
네트워크에서 Windows Server Essentials 로그 수집기 서버 또는 컴퓨터에서 실행할 수 있습니다. 서버에서 로그 수집기를 실행 하는 경우에 서버에서 로그를 수집할 수 있습니다. 네트워크 컴퓨터에서 로그 수집기를 실행 하는 경우 해당 컴퓨터에 대 한 로그 뿐만 아니라 서버에서 로그를 수집을 선택할 수 있습니다.  
  
 로그 컬렉터에 실행 하려면 관리자 적절 한 권한이 있어야 합니다. 서버 관리자 여야 로그 파일 서버에 대해 수집 하는 경우 네트워크 컴퓨터에 파일 로그를 수집 하는 경우 해당 컴퓨터에 대 한 클라이언트 관리자 여야 합니다.  
  
#### <a name="to-run-the-log-collector-on-the-server-by-using-the-wizard"></a>마법사를 사용 하 여 서버에 로그 수집기 실행 하려면  
  
1.  에 **시작** 페이지 서버를 클릭 **Windows Server Essentials 로그 수집기**합니다.  
  
    > [!NOTE]
    >  -   로그 수집기 프로그램에 표시 되지 않으면는 **시작** 페이지를 찾은 **%system%\Program 파일 (x86) \Windows Server Essentials 로그 수집기**, 다음 두 번 클릭 하 고 **LogCollector**합니다.  
    > -   관리자 권한으로 서버에 로그온 하지 않은 경우 로그 수집기 자격 증명을 입력 하 라는 메시지를 표시 합니다.  
  
2.  로그를 수집 된 파일을 저장할 위치에 대 한 메시지가 표시 되는 기본 위치를 선택할 수 있습니다 **\\\ < ServerName\ > \logs**, 하거나 다른 위치를 지정 합니다. 기본 위치를 사용 하려면 클릭 **다음**합니다. 위치를 변경 하려면 클릭 **찾아보기**를 탐색을 로그 파일을 저장할 폴더를 클릭 한 다음 **저장**합니다.  
  
    > [!NOTE]
    >  파일 이름에 대 한 로그 파일 제공 필요가 없습니다. Zip 파일 컬렉션에서 컴퓨터 이름과의 파일 타임 스탬프에 연결 하 여 이름을 지정 로그 수집기 합니다.  
  
3.  진행률 표시줄 로그를 수집 하는 동안 표시 됩니다.  
  
4.  로그 컬렉션 파일의 내용을 보려면 선택는 **로그 저장 된 파일 위치 열기** 확인란을 클릭 한 **닫기** 마법사 닫고 로그 컬렉션 파일을 엽니다.  
  
#### <a name="to-run-the-log-collector-on-a-network-computer-by-using-the-wizard"></a>마법사를 사용 하 여 네트워크 컴퓨터에서 로그 수집기 실행 하려면  
  
1.  찾아보기 **%system%\Program 파일 (x86) \Windows Server Essentials 로그 수집기**, 다음 해당 파일을 두 번 클릭 하 고 **LogCollector.exe**합니다.  
  
    > [!NOTE]
    >  사용자 이름 및 메시지가 표시 되 면 암호를 입력 하 고 클릭 한 다음 네트워크 관리자 권한으로 컴퓨터에 로그온 하지 않은 경우 **다음**합니다.  
  
2.  다음과 같이 수집 하려는 어떤 로그를 선택 합니다.  
  
    1.  선택는 **서버 로그 파일** 서버에서 파일 로그를 수집 하 확인란을 선택 합니다.  
  
    2.  **클라이언트 컴퓨터 로그 파일 (이 컴퓨터)** 나타내는 로그 수집기 실행 하는 네트워크 컴퓨터에서 로그를 수집는 기본적으로 확인란이 선택 되어 있는 합니다. 서버 로그를 수집 하려는 경우 선택을 취소는 **클라이언트 컴퓨터 로그 파일 (이 컴퓨터)** 확인란을 선택 합니다.  
  
    3.  클릭 **다음**합니다.  
  
3.  서버 관리자에 대 한 사용자 이름 및 암호를 입력 한 다음 메시지가 표시 되 면 **다음**합니다.  
  
4.  입력 하거나 로그 파일을 저장 한 클릭 한 다음을 저장할 위치로 **다음**합니다.  
  
    > [!NOTE]
    >  파일 이름에 대 한 로그 파일 제공 필요가 없습니다. Zip 파일 컬렉션에서 컴퓨터 이름과의 파일 타임 스탬프에 연결 하 여 이름을 지정 로그 수집기 합니다.  
  
5.  진행률 표시줄 로그를 수집 하는 동안 표시 됩니다.  
  
6.  로그 컬렉션 파일의 내용을 보려면 선택는 **로그 저장 된 파일 위치 열기** 확인란을 클릭 한 **닫기** 마법사 닫고 로그 컬렉션 파일을 엽니다.  
  
### <a name="running-the-log-collector-manually"></a>로그 수집기 수동으로 실행  
 로그 수집기가 설치 된 후 예약 된 작업이 도구를 실행할 만들어집니다. 이후에에서 로그 수집기 실행할 수 있는 **예약 작업 관리자** 마법사를 시작 하 여 문제가 있을 경우 마법사를 사용 하지 않고 합니다.  
  
##### <a name="to-manually-run-the-log-collector-on-the-server"></a>서버에서 로그 수집기 수동으로 실행 하려면  
  
1.  직접 또는 로그온 원격 서버에 합니다.  
  
2.  열려 있는 **작업 스케줄러**합니다.  
  
3.  루트에는 **작업 스케줄러 라이브러리**, 예약 된 작업에 검색할 **LogCollector**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **LogCollector**을 차례로 클릭 하 고 **실행**합니다. 로그 수집기 서버에서 기본 폴더에 로그 장소 **\\\ < ServerName\ > \Logs**합니다. 폴더를에 대 한 있는 쓰기 권한이 나 폴더가 없습니다, 로그에 배치 됩니다는 **< temp\ >** 하위 합니다.  
  
##### <a name="to-manually-run-the-log-collector-on-a-network-computer"></a>수동으로 네트워크 컴퓨터에서 로그 수집기 실행 하려면  
  
1.  직접 또는 원격으로 컴퓨터에 로그온는 네트워크 합니다.  
  
2.  열려 있는 **작업 스케줄러**합니다.  
  
3.  루트에는 **작업 스케줄러 라이브러리**, 예약 된 작업에 검색할 **LogCollector**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **LogCollector**을 차례로 클릭 하 고 **실행**합니다. 로그 수집기 배치 로그에서는 **< temp\ >** 네트워크 컴퓨터에서 폴더 합니다.
