---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: "설치 광고 FS 역할 서비스"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9851134d1ad73092ee44c34c99bc2d873d20ca07
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="install-the-ad-fs-role-service"></a>설치 광고 FS 역할 서비스

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

다음 절차 ADFS 역할 서비스에서 기존 federation 서버 팜 federation 서버 또는 Windows Server 2012 r 2 federation 서버 발전소의 첫 번째 federation 서버를 실행 하는 컴퓨터에 설치에 사용할 수 있습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 최소 요구 사항을 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>추가 기능 및 역할 마법사를 통해 ADFS 서버 역할을 설치 하려면  
  
1.  서버 관리자를 엽니다. 서버 관리자를 열을 클릭 **서버 관리자** 에 **시작** 화면 또는 **서버 관리자** 바탕 화면 작업 표시줄에 있습니다. 에 **빠른 시작** 탭에서 **시작** 타일에 **대시보드** 페이지, 클릭 **역할 및 기능을 추가**합니다. 클릭 수 있습니다 **역할 추가 및 기능** 에 **관리** 메뉴 합니다.  
  
2.  에 **시작 하기 전에** 페이지, 클릭 **다음**합니다.  
  
3.  에 **설치 유형을 선택** 페이지, 클릭 **Role\ 또는 Feature\ 기반 설치**을 차례로 클릭 하 고 **다음**합니다.  
  
4.  에 **선택 대상 서버** 페이지, 클릭 **서버 풀에서 서버를 선택**, 대상 컴퓨터를 선택한 다음 클릭 확인 **다음**합니다.  
  
5.  에 **서버 역할 선택** 페이지, 클릭 **Active Directory Federation Services**, 클릭 한 다음 **다음**합니다.  
  
6.  에 **기능 선택** 페이지, 클릭 **다음**합니다. 필수 사용자에 대 한 미리 선택 됩니다. 다른 기능을 선택할 필요가 없습니다.  
  
7.  에 **Active Directory Federation 서비스 \(AD FS\)** 페이지, 클릭 **다음**합니다.  
  
8.  정보를 확인 한 후는 **설치 선택을 확인** 페이지, 클릭 **설치**합니다.  
  
9. 에 **설치 진행률** 페이지 모든 올바르게 설치 되었는지 확인 한 다음 클릭 **닫기**합니다.  
  
### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>Windows PowerShell를 통해 ADFS 서버 역할을 설치 하려면  
  
1.  Federation 서버 구성 하려면 컴퓨터에서 Windows PowerShell 명령 창을 연 다음 명령을 실행: `Install-windowsfeature adfs-federation –IncludeManagementTools`합니다.  
  
## <a name="see-also"></a>참조 하십시오 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[지침에 따라 Windows Server 2012 r 2 광고 FS 배포](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Federation 서버 농장 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

