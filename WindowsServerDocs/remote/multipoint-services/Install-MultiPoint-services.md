---
title: MultiPoint 서비스 설치
description: Windows Server 2016에서 MultiPoint 서비스를 설치 및 구성 하는 방법을 알아봅니다.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: f6f8970b-de3f-4255-b2a1-5472a16ed02f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: ab82782f4ac1ffa8532dc23ad9340329a65765de
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859216"
---
# <a name="install-multipoint-services"></a>MultiPoint 서비스 설치
서버를 처음부터 설치 하는 경우 다음 지침에 따라 MultiPoint 서비스를 설치 합니다.  

Windows Server 2016을 설치한 후 관리자 권한으로 로그인 합니다. MultiPoint 서비스를 사용 하도록 설정할 수 있는 서버 관리자을 사용 합니다. 서버 관리자 시작 시 자동으로 열립니다. 대시보드에서 **역할 및 기능 추가** 를 선택 하 여 MultiPoint 서비스를 사용 하도록 설정 하 고 마법사의 지침을 따릅니다.

설치 유형에 대 한 섹션에서 다음으로 이동할 수 있습니다. 
- 역할 기반 또는 기능 기반 설치 또는
- 원격 데스크톱 서비스 설치

표준 MultiPoint 서비스 배포의 경우 배포 유형 아래에서 MultiPoint 서비스 역할을 편리 하 게 선택할 수 있는 원격 데스크톱 서비스 설치를 선택 하는 것이 좋습니다. 역할 기반 설치의 경우 역할 목록에서 **MultiPoint 서비스** 를 선택 해야 합니다. 설치가 완료 되 면 서버를 다시 부팅 합니다.  
  
## <a name="configure-your-primary-station"></a>기본 스테이션 구성  
  
1.  **MultiPoint Server 스테이션 만들기** 페이지에서 해당 모니터에 대 한 키보드의 지정 된 문자를 입력 합니다. 올바른 키 항목은 해당 스테이션에 대해 키보드와 마우스를 연결 합니다.  
2.  관리자 권한으로 로그인 합니다.  