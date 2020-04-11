---
title: RDS 클라이언트 액세스 라이선스 설치
description: RD 클라이언트에 대해 CAL을 설치하는 방법을 알아봅니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: 3a9f73418bd4da67c97db30a3272588afc287b95
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860446"
---
# <a name="install-rds-client-access-licenses-on-the-remote-desktop-license-server"></a>원격 데스크톱 라이선스 서버에 RDS 클라이언트 액세스 라이선스 설치

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

다음 정보를 사용하여 라이선스 서버에 원격 데스크톱 서비스 CAL(클라이언트 액세스 라이선스)을 설치합니다. CAL이 설치되면 라이선스 서버가 사용자에게 라이선스를 적절히 발급합니다.

원격 데스크톱 라이선스 관리자를 실행하는 컴퓨터에서는 인터넷 연결이 필요하지만, 라이선스 서버를 실행하는 컴퓨터에서는 필요하지 않습니다.

1. 라이선스 서버(일반적으로 첫 번째 RD 연결 브로커)에서 원격 데스크톱 라이선스 관리자를 엽니다.
2. 라이선스 서버를 마우스 오른쪽 단추로 클릭한 다음, **라이선스 설치**를 클릭합니다.
3. 시작 페이지에서 **다음**을 클릭합니다.
4. RDS CAL을 구입할 때 사용한 프로그램을 선택하고 **다음**을 클릭합니다. 서비스 공급자인 경우 **서비스 공급자 사용권 계약**을 선택합니다.
5. 라이선스 프로그램에 대한 정보를 입력합니다. 대부분의 경우 라이선스 코드 또는 계약 번호가 여기에 해당하지만, 사용 중인 라이선스 프로그램에 따라 달라집니다.
6. **다음**을 클릭합니다.
7. 제품 버전, 라이선스 유형 및 작업 환경의 라이선스 수를 선택하고 **다음**을 클릭합니다. 라이선스 관리자는 Microsoft Clearinghouse에 연결하여 라이선스가 유효한지 검사하고 검색합니다.
8.  **마침**을 클릭하여 프로세스를 완료합니다.