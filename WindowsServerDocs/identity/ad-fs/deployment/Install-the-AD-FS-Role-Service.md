---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: AD FS 역할 서비스 설치
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 46231015ffb91f7c6a1f15615e0eede3fc948be2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408356"
---
# <a name="install-the-ad-fs-role-service"></a>AD FS 역할 서비스 설치

다음 절차를 사용 하 여 Windows Server 2012 r 2를 실행 하는 컴퓨터에 AD FS 역할 서비스를 설치 하 여 페더레이션 서버 팜의 첫 번째 페더레이션 서버 또는 기존 페더레이션 서버 팜의 페더레이션 서버가 될 수 있습니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 로컬 컴퓨터에서 최소한이이 절차를 완료 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>역할 및 기능 추가 마법사를 통해 AD FS 서버 역할을 설치 하려면  
  
1.  서버 관리자를 엽니다. 서버 관리자를 열려면 **시작** 화면에서 **서버 관리자** 를 클릭 하거나 바탕 화면의 작업 표시줄에서 **서버 관리자** 합니다. **대시보드** 페이지의 **시작** 타일에 있는 **빠른 시작** 탭에서 **역할 및 기능 추가**를 클릭합니다. 또는 **관리** 메뉴에서 **역할 및 기능 추가**를 클릭해도 됩니다.  
  
2.  **시작하기 전** 페이지에서 **다음**을 클릭합니다.  
  
3.  **설치 유형 선택** 페이지에서 **역할 @ no__t-2Based 또는 기능 @ no__t-3based 설치**를 클릭 한 후 **다음**을 클릭 합니다.  
  
4.  **대상 서버 선택** 페이지에서 **서버 풀에서 서버 선택**을 클릭하고 대상 컴퓨터가 선택되어 있는지 확인한 후 **다음**을 클릭합니다.  
  
5.  **서버 역할 선택** 페이지에서 **Active Directory Federation Services**를 클릭한 후 **다음**을 클릭합니다.  
  
6.  **기능 선택** 페이지에서 **다음**을 클릭합니다. 필요한 필수 구성 요소는 미리 선택 되어 있습니다. 다른 기능을 선택할 필요가 없습니다.  
  
7.  **Active Directory 페더레이션 서비스 \(AD FS @ no__t-2** 페이지에서 **다음**을 클릭 합니다.  
  
8.  **설치 선택 확인** 페이지에서 정보를 확인 한 후 **설치**를 클릭 합니다.  
  
9. **설치 진행률** 페이지에서 모든 항목이 올바르게 설치되었는지 확인하고 **닫기**를 클릭합니다.  
  
### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>Windows PowerShell을 통해 AD FS 서버 역할을 설치 하려면  
  
1.  페더레이션 서버로 구성 하려는 컴퓨터에서 Windows PowerShell 명령 창을 열고 다음 명령을 `Install-windowsfeature adfs-federation –IncludeManagementTools`실행 합니다.  
  
## <a name="see-also"></a>관련 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

