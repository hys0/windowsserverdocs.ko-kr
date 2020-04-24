---
title: 원격 데스크톱 서비스 라이선스 서버 활성화
description: RD 라이선스 서버 설치 및 활성화
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: eb24ddd2-0361-41fe-bd6b-c7c63427cb71
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: 3eaa999c03c97ad3188d4dcd8514b2705bf0a3b1
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80852976"
---
# <a name="activate-the-remote-desktop-services-license-server"></a>원격 데스크톱 서비스 라이선스 서버 활성화

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

원격 데스크톱 서비스 라이선스 서버는 RD 세션 호스트에 액세스할 때 사용자 및 디바이스에 CAL(클라이언트 액세스 라이선스)을 발급합니다. 원격 데스크톱 라이선스 관리자를 사용하여 라이선스 서버를 활성화할 수 있습니다. 

## <a name="install-the-rd-licensing-role"></a>RD 라이선싱 역할 설치

1. 관리자 계정을 사용하여 라이선스 서버로 사용하려는 서버에 로그인합니다.
2. 서버 관리자에서 **역할 요약**을 클릭한 다음, **역할 추가**를 클릭합니다.
   역할 마법사의 첫 번째 페이지에서 **다음**을 클릭합니다.
3. **원격 데스크톱 서비스**를 선택한 다음, **다음**을 클릭한 다음, 원격 데스크톱 서비스 페이지에서 **다음**을 클릭합니다.
4. **원격 데스크톱 라이선싱**을 선택한 다음, **다음**을 클릭합니다.
5. 도메인 구성 - **이 라이선스 서버에 대한 검색 범위 구성**을 선택하고, **이 도메인**을 클릭한 다음, **다음**을 클릭합니다.
6. **설치**를 클릭합니다.

## <a name="activate-the-license-server"></a>라이선스 서버 활성화

1. 원격 데스크톱 라이선스 관리자 열기: **시작 > 관리 도구 > 원격 데스크톱 서비스 > 원격 데스크톱 라이선스 관리자**를 클릭합니다.
2. 라이선스 서버를 마우스 오른쪽 단추로 클릭한 다음, **서버 활성화**를 클릭합니다.
3. 시작 페이지에서 **다음**을 클릭합니다.
4. 연결 방법의 경우 **자동 연결(권장됨)** 을 선택한 다음, **다음**을 클릭합니다.
5. 회사 정보(사용자 이름, 회사 이름, 지역)를 입력한 다음, **다음**을 클릭합니다.
6. 필요에 따라 다른 회사 정보(예: 이메일 및 회사 주소)를 입력한 다음, **다음**을 클릭합니다. 
7. **지금 라이선스 설치 마법사 시작**이 선택되지 않았는지 확인한 다음(이후 단계에서 라이선스 설치 예정), **다음**을 클릭합니다.

라이선스 서버가 라이선스 발급 및 관리를 시작할 준비가 되었습니다. 