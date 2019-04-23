---
title: 원격 데스크톱 서비스 라이선스 서버 활성화
description: 설치 하 고 RD 라이선스 서버 활성화
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb24ddd2-0361-41fe-bd6b-c7c63427cb71
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: d28ceac9cde0ee2d4c92867bdd90d5c463a8cd4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888014"
---
# <a name="activate-the-remote-desktop-services-license-server"></a>원격 데스크톱 서비스 라이선스 서버 활성화

>적용 대상: Windows Server (반기 채널), Windows Server 2016

RD 세션 호스트에 액세스할 때 사용자 및 장치에 서버 문제 클라이언트 액세스 라이선스 (Cal)를 사용 하는 원격 데스크톱 서비스. 원격 데스크톱 라이선스 관리자를 사용 하 여 라이선스 서버를 활성화할 수 있습니다. 

## <a name="install-the-rd-licensing-role"></a>RD 라이선싱 역할 설치

1. 관리자 계정을 사용 하 여 라이선스 서버로 사용 하려는 서버에 로그인 합니다.
2. 서버 관리자에서 클릭 **역할 요약**를 클릭 하 고 **역할 추가**합니다.
   클릭 **다음** 역할 마법사의 첫 번째 페이지입니다.
3. 선택 **원격 데스크톱 서비스**를 클릭 하 고 **다음**를 차례로 **다음** 원격 데스크톱 서비스 페이지.
4. 선택 **원격 데스크톱 라이선싱**를 클릭 하 고 **다음**합니다.
5. 도메인 구성-선택 **이 라이선스 서버에 대 한 검색 범위를 구성**, 클릭 **이 도메인**를 클릭 하 고 **다음**합니다.
6. **설치**를 클릭합니다.

## <a name="activate-the-license-server"></a>라이선스 서버 활성화

1. 원격 데스크톱 라이선스 관리자를 엽니다: 클릭 **시작 > 관리 도구 > 원격 데스크톱 서비스 > 원격 데스크톱 라이선스 관리자**합니다.
2. 라이선스 서버를 마우스 오른쪽 단추로 누른 **서버 활성화**합니다.
3. 클릭 **다음** 시작 페이지입니다.
4. 연결 방법 선택 **자동 연결 (권장)** 를 클릭 하 고 **다음**합니다.
5. (사용자 이름, 회사 이름, 지리적 지역을) 회사 정보를 입력 한 다음 클릭 **다음**합니다.
6. 필요에 따라 다른 회사 정보 (예를 들어 전자 메일 및 회사 주소)를 입력 한 다음 클릭 **다음**합니다. 
7. 했는지 **라이선스 설치 마법사 지금 시작** 선택 하지 않으면 (설치 라이선스 이후 단계에서)를 클릭 하 고 **다음**합니다.

라이선스 서버를 발급 하 고 라이선스 관리를 시작할 준비가 되었습니다. 