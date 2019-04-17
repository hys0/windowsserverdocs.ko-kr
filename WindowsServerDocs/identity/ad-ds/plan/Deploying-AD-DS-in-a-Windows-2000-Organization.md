---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: "Windows 2000 조직에서 AD DS 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1c46ff6aee03eee4169dbfe0cdff99febad312d2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Windows 2000 조직에서 AD DS 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에서 현재 Windows 2000 Active Directory를 실행 하는 경우 귀하의 환경에 Windows Server 2008 실행 하는 도메인 컨트롤러를 사용 하 여 또는 중 일부 또는 전부를 Windows Server 2008 도메인 컨트롤러의 운영 체제의 전체 업그레이드를 수행 하 여 Windows Server 2008 Active Directory Domain Services (AD DS) 배포할 수 있습니다.  
  
실행 해야 Windows Server 2008 기존 Windows 2000 Active Directory 도메인을 실행 하는 도메인 컨트롤러를 추가 하기 전에 **adprep**, 명령줄 도구입니다. Adprep AD DS 스키마를 확장, 업데이트 선택한 개체의 보안 설명자 및 일부 응용 프로그램으로 필요에 따라 새 directory 개체를 추가 합니다. Adprep (\sources\adprep\adprep.exe) Windows Server 2008 설치 디스크에 제공 됩니다. 자세한 내용은 참조 Adprep ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
> [!NOTE]  
> Windows Server 2008로 기존 Windows 2000 AD DS 도메인 컨트롤러의 현재 위치에서 업그레이드를 수행 하려면 먼저 Windows Server 2003, 서버를 업그레이드 한 후 Windows Server 2008으로 업그레이드 해야 합니다.  
  
다음은 Windows Server 2008 AD DS에서 현재 Windows 2000 Active Directory를 실행 하는 네트워크 환경에서 배포 하는 단계입니다.  
  
![Windows 2000 조직에서 배포](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)  
  
> [!NOTE]  
> Windows Server 2008 도메인 또는 숲 기능 수준을으로 설정 하려면 모든 도메인 컨트롤러 귀하의 환경에 Windows Server 2008 운영 체제를 실행 해야 합니다.  
  
Windows Server 2008 AD DS의 일환으로 Windows 2000 환경에서 곳에서 업그레이드 리소스와 계정을 도메인을 통합 인터포리스트 또는 인트라포리스트 도메인 재구성 배포 필요할 수 있습니다. 숲 간에 AD DS 도메인 재구성 복잡성 조직 및 관련된 관리 비용을 줄일 수 있습니다. 숲에 내 AD DS 도메인 재구성 복제 교통 사용자 및, 그룹 관리 양을 줄이는 줄이고 그룹 정책 관리를 간소화 하 여 관리 오버 조직에 대 한을 줄일 수 있습니다. 자세한 내용은 참조 ADMT v3.1 마이그레이션 가이드 ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
계획 및 AD DS 조직에서 현재 Windows 2000 Active Directory를 실행 하는 배포 하는 데 사용할 수 있는 작업 자세한 목록은 [검사: AD DS Windows 2000 조직에서 배포](https://technet.microsoft.com/library/cc732737.aspx)합니다.  
  


