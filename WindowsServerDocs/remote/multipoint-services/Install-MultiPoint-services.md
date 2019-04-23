---
title: MultiPoint 서비스 설치
description: 설치 및 Windows Server 2016에서 MultiPoint 서비스를 구성 하는 방법을 알아봅니다
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6f8970b-de3f-4255-b2a1-5472a16ed02f
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 52a824bbca3e9f2e1c7823601f6208ae19ae50ef
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866224"
---
# <a name="install-multipoint-services"></a>MultiPoint 서비스 설치
부터 서버를 설치 하는 경우 MultiPoint 서비스를 설치 하려면 다음이 지침을 따릅니다.  

Windows Server 2016를 성공적으로 설치한 후 관리자 권한으로 로그인 합니다. MultiPoint 서비스를 사용 하는 서버 관리자를 사용 합니다. 서버 관리자 시작 시 자동으로 열립니다. 대시보드 선택 **역할 및 기능 추가** MultiPoint 서비스를 사용 하도록 설정 하 여 마법사의 지시를 따릅니다.

설치 유형에 대 한 섹션에서 사용 하 여 이동할 수 있습니다는 
- 역할 기반 또는 기능 기반 설치 또는
- 원격 데스크톱 서비스 설치

표준 MultiPoint 서비스 배포에 대 한 배포 형식에서 MultiPoint 서비스 역할을 간편 하 게 선택할 수 있는 원격 데스크톱 서비스 설치를 선택 하려면이 좋습니다. 역할 기반 설치에 대 한 선택 해야 합니다 **MultiPoint 서비스** 역할 목록에서. 서버는 성공적인 설치 후 다시 부팅 됩니다.  
  
## <a name="configure-your-primary-station"></a>에 기본 스테이션 구성  
  
1.  에 **MultiPoint Server 스테이션 만들기** 페이지, 해당 모니터에 대 한 키보드에서 지정 된 문자를 입력 합니다. 올바른 키 항목에는 키보드 및 마우스 해당 스테이션에 대 한 연결합니다.  
2.  관리자 권한으로 로그인 합니다.  