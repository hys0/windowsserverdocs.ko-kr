---
title: MultiPoint 서비스 (선택 사항) 도메인에 가입
Description: MultiPoint 서비스 사용자의 도메인에 가입 하는 단계를 제공 합니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 623b7c21-dcbb-402e-8b5a-8e434cd225bd
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: af5dd1f16e011161bbcf72c21c21088721ac1243
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827044"
---
# <a name="join-the-multipoint-services-computer-to-a-domain-optional"></a>MultiPoint 서비스 컴퓨터 (선택 사항) 도메인에 가입
MultiPoint 서비스 컴퓨터에는 Active Directory 도메인에 액세스 하는 경우 다음 단계 도메인에 컴퓨터를 추가 하는 것입니다.  
  
> [!IMPORTANT]  
> 컴퓨터를 도메인에 가입 하기 전에 사용자의 표준 시간대를 확인 해야 합니다. 자세한 내용은 [날짜, 시간 및 표준 시간대 설정](Set-the-date--time--and-time-zone.md)합니다.  
   
1.  **시작** 화면에서 **제어판**을 엽니다. 클릭 **시스템 및 보안**를 클릭 하 고 **시스템**입니다.  
  
2.  **컴퓨터 이름, 도메인 및 작업 그룹 설정**에서 **설정 변경**을 클릭합니다.  
  
3.  에 **컴퓨터 이름** 탭을 클릭 **변경**합니다.  
  
4.  에 **컴퓨터 이름/도메인 변경** 대화 상자에서 **도메인**도메인의 이름을 입력 하 고 클릭 **확인**를 완료 하려면 마법사의 단계를 수행 합니다 프로세스입니다.  
  
5.  컴퓨터 다시 시작 되 면 관리자 권한으로 로그온 하 고 다중 포인트 관리자를 열려면 될 때까지 기다립니다.  
  
> [!IMPORTANT]  
> MultiPoint 서비스 도메인 배포가 제대로 작동 되도록 한 쌍의 그룹 정책 구성 하 고 레지스트리를 업데이트 해야 합니다. 정보를 참조 하세요 [도메인 배포를 위한 그룹 정책 구성](https://technet.microsoft.com/library/dn265982.aspx)합니다.  