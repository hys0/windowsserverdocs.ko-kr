---
title: MultiPoint 서비스를 도메인에 연결 (선택 사항)
Description: MultiPoint 서비스를 도메인에 조인 하는 단계를 제공 합니다.
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 623b7c21-dcbb-402e-8b5a-8e434cd225bd
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 79bd9e594f94c7b3acd06265891dd646b3853b50
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394735"
---
# <a name="join-the-multipoint-services-computer-to-a-domain-optional"></a>MultiPoint 서비스 컴퓨터를 도메인에 가입 (선택 사항)
Active Directory 도메인을 통해 MultiPoint 서비스 컴퓨터에 액세스 하는 경우 다음 단계는 도메인에 컴퓨터를 추가 하는 것입니다.  
  
> [!IMPORTANT]  
> 컴퓨터를 도메인에 가입 시키기 전에 표준 시간대를 확인 해야 합니다. 자세한 지침은 [날짜, 시간 및 표준 시간대 설정](Set-the-date--time--and-time-zone.md)을 참조 하세요.  
   
1.  **시작** 화면에서 **제어판**을 엽니다. **시스템 및 보안**을 클릭 한 다음 **시스템**을 클릭 합니다.  
  
2.  **컴퓨터 이름, 도메인 및 작업 그룹 설정**에서 **설정 변경**을 클릭합니다.  
  
3.  **컴퓨터 이름** 탭에서 **변경**을 클릭 합니다.  
  
4.  **컴퓨터 이름/도메인 변경** 대화 상자에서 **도메인**을 선택 하 고 도메인 이름을 입력 한 다음 **확인**을 클릭 하 고 마법사의 단계에 따라 프로세스를 완료 합니다.  
  
5.  컴퓨터가 다시 시작 되 면 관리자로 로그온 하 여 MultiPoint 관리자가 열릴 때까지 기다립니다.  
  
> [!IMPORTANT]  
> MultiPoint 서비스 도메인 배포가 제대로 작동 하도록 하려면 몇 가지 그룹 정책을 구성 하 고 레지스트리를 업데이트 해야 합니다. 자세한 내용은 [도메인 배포에 대 한 그룹 정책 구성](https://technet.microsoft.com/library/dn265982.aspx)을 참조 하세요.  