---
ms.assetid: e6b72a80-e8b7-4305-be0c-0a290f468d36
title: Windows Server 2003 조직에서 AD DS 배포
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 033973ad7a726054f6c47c7154fa54a3767beab4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816364"
---
# <a name="deploying-ad-ds-in-a-windows-server-2003-organization"></a>Windows Server 2003 조직에서 AD DS 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에는 Windows Server 2003 Active Directory 현재 실행 중인 경우에 Windows Server 2008 도메인 컨트롤러의 운영 체제의 일부 또는 전부의 전체 업그레이드를 수행 하거나 또는 사용자 환경에 Windows Server 2008을 실행 하는 도메인 컨트롤러를 도입 하 여 Windows Server 2008 Active Directory 도메인 서비스 (AD DS)를 배포할 수 있습니다.  
  
기존 Windows Server 2003 Active Directory 도메인에 Windows Server 2008을 실행 하는 도메인 컨트롤러를 추가 하기 전에 실행 해야 **adprep**, 명령줄 도구입니다. Adprep AD DS 스키마를 확장 하 고, 선택 된 개체의 기본 보안 설명자를 업데이트, 일부 응용 프로그램에서 필요에 따라 새 디렉터리 개체를 추가 합니다. Adprep는 Windows Server 2008 설치 디스크 (\sources\adprep\adprep.exe)에 있습니다. 자세한 내용은 Adprep을 참조 하세요. ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
다음 그림에는 현재 실행 중인 Windows Server 2003 Active Directory 네트워크 환경에서 Windows Server 2008 AD DS를 배포 하기 위한 단계 보여 줍니다.  
  
![windows 2003 조직에 배포](media/Deploying-AD-DS-in-a-Windows-Server-2003-Organization/900c4eee-1119-4a9a-9310-755597428b71.gif)  
  
> [!NOTE]  
> 도메인 또는 포리스트 기능 수준을 Windows Server 2008로 설정 하려는 경우 모든 도메인 컨트롤러 환경에서 Windows Server 2008 운영 체제를 실행 해야 합니다.  
  
통합 리소스 도메인 및 계정 도메인에 Windows Server 2003 환경에서 업그레이드를 인터포리스트 포리스트 내 도메인 구조 변경 또는 Windows Server 2008 AD DS 배포에 포함 해야 할 수 있습니다. AD DS에 조직의 표현의 복잡성을 줄이고 활용 포리스트 간에 AD DS 도메인 구조 변경 하 고 관련된 관리 비용을 낮추도록 도와 줍니다. 포리스트 내의 AD DS 도메인 구조 변경 하면 복제 트래픽을 줄이고 사용자 및 그룹 관리, 필요한 양을 줄이는의 그룹 정책 관리를 단순화 하 여 조직에 대 한 관리 오버 헤드를 줄일 수 있습니다. 자세한 내용은 ADMT v3.1 마이그레이션 가이드를 참조 하세요. ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
계획 및 Windows Server 2003 Active Directory를 실행 하는 조직에서 AD DS를 배포 하는 데 사용할 수 있는 자세한 작업 목록은 참조 하세요. [검사 목록: Windows Server 2003 조 직에 AD DS 배포](https://technet.microsoft.com/library/cc771407.aspx)합니다.  
  


