---
title: "원격 컴퓨터에 연결"
description: "이 문서에서는 원격 컴퓨터에 연결하여 파일 서버 리소스 관리자에서 저장소 리소스를 관리하는 방법을 설명합니다."
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 93d2be926437b65ed8eb84a828ea0d7da6a51086
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="connect-to-a-remote-computer"></a>원격 컴퓨터에 연결 

> 적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

원격 컴퓨터에서 저장소 리소스를 관리하기 위해 파일 서버 리소스 관리자에서 컴퓨터에 연결할 수 있습니다. 연결되면 파일 서버 리소스 관리자를 사용하여 할당량을 관리하고, 파일을 차단하고, 분류를 관리하고, 파일 관리 작업을 예약하고, 이러한 원격 리소스로 보고서를 생성할 수 있습니다.

> [!Note]
> 파일 서버 리소스 관리자는 로컬 컴퓨터나 원격 컴퓨터의 리소스를 관리할 수 있지만 동시에 두 리소스를 관리할 수는 없습니다.

## <a name="to-connect-to-a-remote-computer-from-file-server-resource-manager"></a>파일 서버 리소스 관리자에서 원격 컴퓨터에 연결하려면

1.  **관리 도구**에서 **파일 서버 리소스 관리자**를 클릭합니다.

2.  콘솔 트리에서 **파일 서버 리소스 관리자**를 마우스 오른쪽 단추로 클릭하고 **다른 컴퓨터에 연결**을 클릭합니다.

3.  **다른 컴퓨터에 연결** 대화 상자에서 **다른 컴퓨터**를 클릭합니다. 그런 다음 연결하려는 서버의 이름을 입력(또는 **찾아보기**를 클릭하여 원격 컴퓨터 검색)합니다.

4.  **확인**을 클릭합니다.

> [!Important]
> **다른 컴퓨터에 연결** 명령은 파일 서버 리소스 관리자를 **관리 도구**에서 열었을 때만 사용할 수 있습니다. 서버 관리자에서 파일 서버 리소스 관리자에 액세스한 경우 명령을 사용할 수 없습니다.

## <a name="additional-considerations"></a>추가 고려 사항

파일 서버 리소스 관리자로 원격 리소스를 관리:

-   로컬 컴퓨터에서 원격 컴퓨터의 **Administrators** 그룹의 구성원인 도메인 계정으로 로그온해야 합니다.
-   원격 컴퓨터는 Windows Server를 실행 중이어야 하며 파일 서버 리소스 관리자가 설치되어 있어야 합니다.
-   원격 컴퓨터에서 **원격 파일 서버 리소스 관리자 관리** 예외를 사용하도록 설정되어 있어야 합니다. 이 예외는 제어판의 Windows 방화벽을 통해 사용하도록 설정합니다.

## <a name="see-also"></a>참고 항목

-   [원격 저장소 리소스 관리](managing-remote-storage-resources.md)