---
title: "마이그레이션 ADFS 2.0 federation 서버 SQL 농장"
description: "Windows Server 2012 ADFS 2.0 서버 SQL 농장 마이그레이션에 정보를 제공 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8433219850793aa34b646a3bf14cba42d3de4988
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>마이그레이션 AD 2.0 FS WID 농장  
이 문서 Windows Server 2012 AD 2.0 FS SQL 농장 마이그레이션에 세부 정보를 제공 합니다.


## <a name="migrate-a-sql-server-farm"></a>마이그레이션 SQL Server 농장  
 Windows Server 2012 SQL Server 팜 마이그레이션할 다음 절차를 수행 합니다.  
  
1.  각 서버용 SQL Server 팜 검토 하 고에 절차를 수행 [SQL Server 팜 마이그레이션을](prepare-to-migrate-a-sql-server-farm.md)합니다.  
  
2.  모든 서버 SQL Server 팜 부하 분산에서 제거 합니다.  
  
3.  Windows Server 2012이 서버 SQL Server 팜에서 운영 체제 Windows Server 2008 R2 또는 Windows Server 2008에서 업그레이드 합니다. 자세한 내용은 참조 [Windows Server 2012를 설치](https://technet.microsoft.com/library/jj134246.aspx)합니다.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드 결과이 서버의 ADFS 구성 삭제 되 고 ADFS 2.0 서버 역할은 제거 됩니다. Windows Server 2012 ADFS 서버 역할 대신 설치 되어 있지만 구성 되어 있지 않습니다. 수동으로 만들 원래 ADFS 구성 하 고 federation 서버 마이그레이션을 완료 하 나머지 ADFS 설정으로 복원 해야 합니다.  
  
4.  서버 기존 그룹에 추가 하려면 AD FS Windows PowerShell cmdlet를 사용 하 여 원래 ADFS 구성 SQL Server 팜에서이 서버의 만들기  
  
> [!IMPORTANT]
>  Windows PowerShell SQL Server ADFS 구성 데이터베이스에 저장 하려면 사용 중인 경우 원래 ADFS 구성을 만드는 데 사용 해야 합니다.  

  - 다음 명령을 실행를 Windows PowerShell 열고: `$fscredential = Get-Credential`합니다.  
  - 이름 및 SQL Server 팜 마이그레이션에 대 한 준비 하는 동안 기록 서비스 계정의 암호를 입력 합니다.  
  - 다음 명령을 실행: `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`, 여기서 `Data Source` 데이터 소스 값 정책 스토어 연결 문자열 값 다음 파일에에서: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`합니다.  
  
5.  서버 방금 업그레이드에 Windows Server 2012 부하 분산에 추가 합니다.  
  
6.  SQL Server 발전소의 나머지 노드의 2-6 단계를 반복 합니다.  
  
7.  Windows Server 2012로 업그레이드 된 모든 서버 SQL Server 팜에를 사용자 지정 된 특성 스토어 등 모든 나머지 ADFS 사용자 지정 복원 됩니다.  

## <a name="next-steps"></a>다음 단계
 [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)



