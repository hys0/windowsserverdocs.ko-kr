---
title: AD FS 2.0 페더레이션 서버 SQL 팜 마이그레이션
description: AD FS 2.0 server SQL 팜을 Windows Server 2012로 마이그레이션하는 방법에 대 한 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3c43d26868f39896ec8632397dc0fce1dfe2dd2a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408279"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>AD FS 2.0 WID 팜 마이그레이션  
이 문서에서는 AD FS 2.0 SQL 팜을 Windows Server 2012로 마이그레이션하는 방법에 대 한 자세한 정보를 제공 합니다.


## <a name="migrate-a-sql-server-farm"></a>SQL Server 팜 마이그레이션  
 SQL Server 팜을 Windows Server 2012로 마이그레이션하려면 다음 절차를 수행 합니다.  
  
1.  SQL Server 팜의 각 서버에 대해 [SQL Server 팜 마이그레이션](prepare-to-migrate-a-sql-server-farm.md)의 절차를 검토 하 고 수행 합니다.  
  
2.  부하 분산 장치에서 SQL Server 팜의 모든 서버를 제거합니다.  
  
3.  SQL Server 팜의이 서버의 운영 체제를 Windows server 2008 R2 또는 Windows server 2008에서 Windows server 2012로 업그레이드 합니다. 자세한 내용은 [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드로 인해 이 서버의 AD FS 구성이 손실되고 AD FS 2.0 서버 역할이 제거됩니다. Windows Server 2012 AD FS 서버 역할이 대신 설치 되지만 구성 되지 않습니다. 수동으로 원래 AD FS 구성을 만들고 나머지 AD FS 설정을 복원하여 페더레이션 서버 마이그레이션을 완료해야 합니다.  
  
4. AD FS Windows PowerShell cmdlet을 사용하여 SQL Server 팜의 이 서버에서 원래 AD FS 구성을 만들어 서버를 기존 팜에 추가합니다.  
  
> [!IMPORTANT]
>  SQL Server를 사용하여 AD FS 구성 데이터베이스를 저장하려면 Windows PowerShell을 사용하여 원래 AD FS 구성을 만들어야 합니다.  

  - Windows PowerShell을 열고 다음 명령을 실행합니다. `$fscredential = Get-Credential`.  
  - SQL Server 팜의 마이그레이션을 준비하는 동안 기록한 서비스 계정의 이름 및 암호를 입력합니다.  
  - 다음 명령을 실행합니다. `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`. 여기서 `Data Source` 는 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`파일의 정책 저장소 연결 문자열 값의 데이터 원본 값입니다.  
  
5. 방금 Windows Server 2012로 업그레이드 한 서버를 부하 분산 장치에 추가 합니다.  
  
6. SQL Server 팜의 나머지 노드에 대해 2~6단계를 반복합니다.  
  
7. SQL Server 팜의 모든 서버를 Windows Server 2012로 업그레이드 하는 경우 사용자 지정 특성 저장소와 같은 나머지 AD FS 사용자 지정 항목을 복원 합니다.  

## <a name="next-steps"></a>다음 단계
 [AD FS 2.0 페더레이션 서버 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시  마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)  
 [AD FS 2.0 페더레이션 서버 마이그레이션](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시  마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)  
 [AD FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)



