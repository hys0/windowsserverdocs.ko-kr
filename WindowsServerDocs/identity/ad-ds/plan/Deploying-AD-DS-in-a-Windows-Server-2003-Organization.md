---
ms.assetid: e6b72a80-e8b7-4305-be0c-0a290f468d36
title: "Windows Server 2003 조직에서 AD DS 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: df1267ded5ece95dd5a3ab17e4ec6ad5d87a2f12
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploying-ad-ds-in-a-windows-server-2003-organization"></a>Windows Server 2003 조직에서 AD DS 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에서 현재 Windows Server 2003에 대 한 Active Directory를 실행 하는 경우 귀하의 환경에 Windows Server 2008 실행 하는 도메인 컨트롤러를 사용 하 여 또는 중 일부 또는 전부를 Windows Server 2008 도메인 컨트롤러의 운영 체제의 전체 업그레이드를 수행 하 여 Windows Server 2008 Active Directory Domain Services (AD DS) 배포할 수 있습니다.  
  
실행 해야 Windows Server 2008 기존 Windows Server 2003에 대 한 Active Directory 도메인을 실행 하는 도메인 컨트롤러를 추가 하기 전에 **adprep**, 명령줄 도구입니다. Adprep AD DS 스키마를 확장, 업데이트 선택한 개체의 보안 설명자 및 일부 응용 프로그램으로 필요에 따라 새 directory 개체를 추가 합니다. Adprep (\sources\adprep\adprep.exe) Windows Server 2008 설치 디스크에 제공 됩니다. 자세한 내용은 참조 Adprep ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
다음은 Windows Server 2008 AD DS 현재 Windows Server 2003에 대 한 Active Directory를 실행 하는 네트워크 환경에서 배포 하는 단계입니다.  
  
![Windows 2003 조직에서 배포](media/Deploying-AD-DS-in-a-Windows-Server-2003-Organization/900c4eee-1119-4a9a-9310-755597428b71.gif)  
  
> [!NOTE]  
> Windows Server 2008 도메인 또는 숲 기능 수준을으로 설정 하려면 모든 도메인 컨트롤러 귀하의 환경에 Windows Server 2008 운영 체제를 실행 해야 합니다.  
  
리소스 도메인와 Windows Server 2003 환경의 장소에 업그레이드를 Windows Server 2008 AD DS 배포 중 인터포리스트 또는 인트라포리스트 도메인 재구성 필요할 수도 계정 도메인을 통합 합니다. AD DS에서 조직 표현을 간단 하는 데 도움이 재구성 숲 간에 AD DS 도메인 하 고 관련된 관리 비용 절감 하는 데 도움이 됩니다. 숲에 내 AD DS 도메인 재구성 복제 교통 사용자 및, 그룹 관리 양을 줄이는 줄이고 그룹 정책 관리를 간소화 하 여 관리 오버 조직에 대 한을 줄일 수 있습니다. 자세한 내용은 참조 ADMT v3.1 마이그레이션 가이드 ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
계획 하 고 Windows Server 2003에 대 한 Active Directory를 실행 하는 조직의 AD DS 배포 사용할 수 있는 작업 자세한 목록은 [검사: Windows Server 2003 조직에서 AD DS 배포](https://technet.microsoft.com/library/cc771407.aspx)합니다.  
  


