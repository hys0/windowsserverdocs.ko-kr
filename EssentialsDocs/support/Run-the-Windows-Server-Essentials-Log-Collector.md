---
title: Windows Server Essentials 로그 수집기 실행
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.openlocfilehash: 5654f28aeda3c231376ed888a8aa04bc0cf3d000
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432495"
---
# <a name="run-the-windows-server-essentials-log-collector"></a>Windows Server Essentials 로그 수집기 실행
네트워크에서 서버 또는 컴퓨터에서 Windows Server Essentials 로그 수집기를 실행할 수 있습니다. 서버에서 로그 수집기를 실행하면 서버에서만 로그를 수집할 수 있습니다. 네트워크 컴퓨터에서 로그 수집기를 실행하면 해당 컴퓨터에 대한 로그 이외에 서버에서 로그를 수집하도록 선택할 수 있습니다.  
  
 로그 수집기를 실행하려면 적절한 관리자 권한이 있어야 합니다. 서버에 대한 로그 파일을 수집하고 있다면 서버 관리자여야 하고, 네트워크 컴퓨터에서 로그 파일을 수집하고 있다면 해당 컴퓨터에 대한 클라이언트 관리자여야 합니다.  
  
#### <a name="to-run-the-log-collector-on-the-server-by-using-the-wizard"></a>마법사를 사용하여 서버에서 로그 수집기를 실행하려면  
  
1. 에 **시작** 페이지 서버의 클릭 **Windows Server Essentials Log Collector**합니다.  
  
   > [!NOTE]
   > - 에 로그 수집기 프로그램이 표시 되지 않는 경우는 **시작** 페이지에서 이동할 **%system%\Program 파일 (x86) \Windows Server Essentials Log Collector**를 차례로 두 번 클릭 **LogCollector** .  
   >   -   관리자 권한으로 서버에 로그온되어 있지 않으면 로그 수집기에서 자격 증명을 입력하라는 메시지가 표시됩니다.  
  
2. 수집된 된 로그 파일을 저장할 위치를 묻는 경우 기본 위치를 선택할 수 있습니다  **\\ \\< 서버 이름\>\logs**, 또는 다른 위치를 지정 합니다. 기본 위치를 적용하려면 **다음**을 클릭합니다. 위치를 변경하려면 **찾아보기**를 클릭하고 로그 파일을 저장하려는 폴더로 이동한 다음 **저장**을 클릭합니다.  
  
   > [!NOTE]
   >  로그 파일에 대한 파일 이름을 제공할 필요가 없습니다. 로그 수집기 컴퓨터 이름 및 파일의 타임 스탬프를 연결 하 여 zip 파일 컬렉션의 이름을 지정 합니다.  
  
3. 로그를 수집하는 동안 진행률 표시줄이 표시됩니다.  
  
4. 로그 컬렉션 파일의 콘텐츠를 보려면 **로그가 저장된 파일 위치 열기** 확인란을 선택하고 **닫기** 를 클릭하여 마법사를 닫은 다음 로그 컬렉션 파일을 엽니다.  
  
#### <a name="to-run-the-log-collector-on-a-network-computer-by-using-the-wizard"></a>마법사를 사용하여 네트워크 컴퓨터에서 로그 수집기를 실행하려면  
  
1.  이동할 **%system%\Program 파일 (x86) \Windows Server Essentials Log Collector**, 다음 파일을 두 번 클릭 하 고 **LogCollector.exe**합니다.  
  
    > [!NOTE]
    >  관리자 권한으로 네트워크 컴퓨터에 로그온되어 있지 않으면 메시지가 표시될 때 사용자 이름과 암호를 입력하고 **다음**을 클릭합니다.  
  
2.  다음과 같이 수집할 로그를 선택합니다.  
  
    1.  **서버 로그 파일** 확인란을 선택하여 서버에서 로그 파일을 수집합니다.  
  
    2.  로그 수집기가 실행 중인 네트워크 컴퓨터에서 로그를 수집할 것임을 나타내는 **클라이언트 컴퓨터 로그 파일(이 컴퓨터)** 확인란이 기본적으로 선택됩니다. 서버 로그만 수집하려면 **클라이언트 컴퓨터 로그 파일(이 컴퓨터)** 확인란을 선택 취소합니다.  
  
    3.  **다음**을 클릭합니다.  
  
3.  메시지가 표시되면 서버 관리자에 대한 사용자 이름 및 암호를 입력하고 **다음**을 클릭합니다.  
  
4.  로그 파일을 저장할 위치를 입력하거나 해당 위치로 이동하고 **다음**을 클릭합니다.  
  
    > [!NOTE]
    >  로그 파일에 대한 파일 이름을 제공할 필요가 없습니다. 로그 수집기 컴퓨터 이름 및 파일의 타임 스탬프를 연결 하 여 zip 파일 컬렉션의 이름을 지정 합니다.  
  
5.  로그를 수집하는 동안 진행률 표시줄이 표시됩니다.  
  
6.  로그 컬렉션 파일의 콘텐츠를 보려면 **로그가 저장된 파일 위치 열기** 확인란을 선택하고 **닫기** 를 클릭하여 마법사를 닫은 다음 로그 컬렉션 파일을 엽니다.  
  
### <a name="running-the-log-collector-manually"></a>수동으로 로그 수집기 실행  
 로그 수집기를 설치하고 나서 도구를 실행하기 위한 예약형 작업이 만들어집니다. 마법사를 시작하는 데 문제가 있으면 마법사를 사용하지 않고 이후 **예약형 작업 관리자** 에서 로그 수집기를 실행할 수 있습니다.  
  
##### <a name="to-manually-run-the-log-collector-on-the-server"></a>서버에서 로그 수집기를 수동으로 실행하려면  
  
1.  직접 또는 원격으로 서버에 로그온합니다.  
  
2.  **작업 스케줄러**를 엽니다.  
  
3.  **작업 Scheduler 라이브러리**의 루트에서 **LogCollector**라는 예약된 작업으로 이동합니다.  
  
4.  **LogCollector**를 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다. 서버의 기본 폴더에 로그를 저장 하는 로그 수집기  **\\ \\< 서버 이름\>\Logs**합니다. 폴더에 대 한 쓰기 권한이 없습니다. 폴더가 존재 하지 않습니다, 경우에 로그에 배치 됩니다 합니다 **< temp\>**  하위 디렉터리입니다.  
  
##### <a name="to-manually-run-the-log-collector-on-a-network-computer"></a>네트워크 컴퓨터에서 로그 수집기를 수동으로 실행하려면  
  
1.  직접 또는 원격으로 네트워크 컴퓨터에 로그온합니다.  
  
2.  **작업 스케줄러**를 엽니다.  
  
3.  **작업 Scheduler 라이브러리**의 루트에서 **LogCollector**라는 예약된 작업으로 이동합니다.  
  
4.  **LogCollector**를 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다. 로그 수집기에서 로그를 저장 합니다 **< temp\>**  네트워크 컴퓨터의 폴더입니다.
