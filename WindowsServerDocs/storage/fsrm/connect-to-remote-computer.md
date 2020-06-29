---
title: 원격 컴퓨터에 연결
description: 이 문서에서는 원격 컴퓨터에 연결 하 여 파일 서버에서 저장소 리소스를 관리 하는 방법을 설명 리소스 관리자
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 562164b461b4cd5db939b116feeb1bf21f78bad4
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474130"
---
# <a name="connect-to-a-remote-computer"></a>원격 컴퓨터에 연결

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

원격 컴퓨터에서 저장소 리소스를 관리 하려면 파일 서버 리소스 관리자에서 컴퓨터에 연결할 수 있습니다. 연결 되어 있는 동안 파일 서버 리소스 관리자를 사용 하 여 할당량, 화면 파일, 분류 관리를 관리 하 고 파일 관리 작업을 예약 하 고 해당 원격 리소스를 사용 하 여 보고서를 생성할 수 있습니다.

> [!Note]
> 파일 서버 리소스 관리자 로컬 컴퓨터 또는 원격 컴퓨터에서 리소스를 관리할 수 있지만 동시에 둘 다를 관리할 수는 없습니다.

## <a name="to-connect-to-a-remote-computer-from-file-server-resource-manager"></a>파일 서버 리소스 관리자에서 원격 컴퓨터에 연결 하려면

1.  **관리 도구**에서 **파일 서버 리소스 관리자**를 클릭 합니다.

2.  콘솔 트리에서 **파일 서버 리소스 관리자**를 마우스 오른쪽 단추로 클릭 한 다음 **다른 컴퓨터에 연결**을 클릭 합니다.

3.  **다른 컴퓨터에 연결** 대화 상자에서 **다른 컴퓨터**를 클릭 합니다. 그런 다음 연결 하려는 서버의 이름을 입력 하거나 **찾아보기** 를 클릭 하 여 원격 컴퓨터를 검색 합니다.

4.  **확인**을 클릭합니다.

> [!Important]
> **다른 컴퓨터에 연결** 명령은 **관리 도구**에서 파일 서버 리소스 관리자를 연 경우에만 사용할 수 있습니다. 서버 관리자에서 파일 서버 리소스 관리자에 액세스 하는 경우에는 명령을 사용할 수 없습니다.

## <a name="additional-considerations"></a>기타 고려 사항

파일 서버 리소스 관리자를 사용 하 여 원격 리소스를 관리 하려면:

-   원격 컴퓨터에서 **Administrators** 그룹의 구성원 인 도메인 계정을 사용 하 여 로컬 컴퓨터에 로그온 해야 합니다.
-   원격 컴퓨터에서 Windows Server를 실행 하 고 있어야 하며 파일 서버 리소스 관리자를 설치 해야 합니다.
-   원격 컴퓨터에서 **원격 파일 서버 리소스 관리자 관리** 예외를 사용 하도록 설정 해야 합니다. 제어판에서 Windows 방화벽을 사용 하 여이 예외를 사용 하도록 설정 합니다.

## <a name="additional-references"></a>추가 참조

-   [원격 스토리지 리소스 관리](managing-remote-storage-resources.md)