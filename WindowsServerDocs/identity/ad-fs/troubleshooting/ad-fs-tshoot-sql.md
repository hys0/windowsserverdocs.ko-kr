---
title: AD FS 문제 해결-SQL 연결
description: 이 문서에서는 AD FS의 다양 한 측면을 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 09d61292b91c83466f9770184d431b3e6d627dca
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385442"
---
# <a name="ad-fs-troubleshooting---sql-connectivity"></a>AD FS 문제 해결-SQL 연결
AD FS은 AD FS 팜 데이터에 원격 SQL Server를 사용 하는 기능을 제공 합니다.  팜의 AD FS 서버에서 백 엔드 SQL server와 통신할 수 없는 경우 문제가 표시 됩니다.  다음 문서에서는 백 엔드 서버와의 통신을 테스트 하기 위한 몇 가지 기본 단계를 제공 합니다.

## <a name="acquire-the-sql-database-connection-string"></a>SQL database 연결 문자열을 가져옵니다.
SQL 연결을 확인할 때 가장 먼저 테스트할 사항은 AD FS에 올바른 SQL 연결 정보가 있는 경우입니다.  이렇게 하려면 PowerShell을 사용 합니다.

### <a name="to-acquire-the-sql-connection-string"></a>SQL 연결 문자열을 가져오려면
1.  Windows PowerShell 열기
2. 다음을 입력 하 `$adfs = gwmi -Namespace root/ADFS -Class SecurityTokenService` 입력 하 고 Enter 키를 누릅니다.
3. 다음을 입력 하 `$adfs.ConfigurationDatabaseConnectionString`를 입력 하 고 enter 키를 누릅니다.
4. 연결 문자열 정보가 표시 됩니다.
![](media/ad-fs-tshoot-sql/sql2.png)

## <a name="create-a-universal-data-link-udl-file-to-test-connectivity"></a>연결을 테스트 하기 위한 UDL (Universal Data Link) 파일 만들기
유니버설 데이터 링크 파일 또는 UDL 파일은 기본적으로 데이터베이스 연결 문자열을 포함 하는 텍스트 파일입니다.  위에서 얻은 정보를 사용 하 여 SQL server가 연결에 응답 하는지 여부를 테스트할 수 있습니다.

### <a name="to-create-a-udl-file-to-test-connectivity"></a>Udl 파일을 만들어 연결을 테스트 하려면

1. 메모장을 열고 파일을 test.txt로 저장 합니다.  **저장 위치**의 드롭다운에서 **모든 파일** 을 선택 했는지 확인 합니다.
2. 테스트를 두 번 클릭 합니다.
3. 다음 정보를 입력 합니다. a. **서버 이름 선택 또는 입력:**  B 위의 연결 문자열에서 데이터 원본을 사용 합니다. **서버 로그온 정보 입력:**  AD FS 서비스 계정 또는 원격으로 로그온 할 수 있는 권한이 있는 계정을 사용 합니다.  계정이 windows 계정인 경우 통합 인증을 사용 하 고 그렇지 않으면 사용자 이름 및 암호를 입력 합니다.
    c. **서버에서 데이터베이스를 선택 합니다.** 위의 문자열에서 초기 카탈로그를 사용 합니다.  예: AdfsConfigurationV3.
   ![연결 테스트](media/ad-fs-tshoot-sql/sql4.png)
1. **연결 테스트**를 클릭 합니다.</br>
![성공](media/ad-fs-tshoot-sql/sql3.png)

## <a name="use-sql-server-management-studio-to-test-connectivity"></a>SQL Server Management Studio를 사용 하 여 연결 테스트
SSMS를 [다운로드](https://go.microsoft.com/fwlink/?linkid=864329) 하 고 설치 하 여 데이터베이스 연결을 테스트할 수도 있습니다.

### <a name="to-test-connectivity-with-ssms"></a>SSMS를 사용 하 여 연결을 테스트 하려면
1. SQL Server Management Studio를 다운로드 하 고 설치 합니다.
![설치](media/ad-fs-tshoot-sql/sql5.png)
1. SSMS를 열고 서버 이름을 입력 합니다.  위의 데이터 원본입니다.
2. AD FS 서비스 계정 또는 원격으로 로그온 할 수 있는 권한이 있는 계정을 사용 합니다.  계정이 windows 계정인 경우 통합 인증을 사용 하 고 그렇지 않으면 사용자 이름 및 암호를 입력 합니다.
![연결](media/ad-fs-tshoot-sql/sql6.png)
1. 왼쪽이 채워진 것을 볼 수 있습니다.  데이터베이스를 확장 하 고 AD FS 데이터베이스가 표시 되는지 확인 합니다.
AD FS 데이터베이스를 ![](media/ad-fs-tshoot-sql/sql7.png)

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)