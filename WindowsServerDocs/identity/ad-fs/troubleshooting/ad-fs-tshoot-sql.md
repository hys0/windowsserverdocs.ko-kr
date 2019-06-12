---
title: AD FS 문제 해결-SQL 연결
description: 이 문서에서는 AD FS의 다양 한 측면을 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4b09094b6e305bc85b38e94d11fbc8845d555437
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443929"
---
# <a name="ad-fs-troubleshooting---sql-connectivity"></a>AD FS 문제 해결-SQL 연결
AD FS는 AD FS 팜 데이터에 대 한 원격 SQL Server를 사용 하는 기능을 제공 합니다.  팜의 AD FS 서버에서 백 엔드 SQL 서버와 통신할 수 없는 경우 문제가 표시 됩니다.  다음 문서는 백 엔드 서버와의 통신을 테스트 하는 몇 가지 기본 단계를 제공 합니다.

## <a name="acquire-the-sql-database-connection-string"></a>SQL 데이터베이스 연결 문자열을 획득 합니다.
AD FS에 올바른 SQL 연결 정보가 있는 경우 SQL 연결을 확인 하는 경우 테스트에 가장 먼저 됩니다.  이렇게 하려면 PowerShell을 사용 합니다.

### <a name="to-acquire-the-sql-connection-string"></a>SQL 연결 문자열을 획득 하기
1.  열린 Windows PowerShell
2. 다음을 입력 합니다. `$adfs = gwmi -Namespace root/ADFS -Class SecurityTokenService` Enter를 누릅니다
3. 다음을 입력 합니다. `$adfs.ConfigurationDatabaseConnectionString` 하 고 enter 키를 누릅니다.
4. 연결 문자열 정보를 표시 됩니다.
![](media/ad-fs-tshoot-sql/sql2.png)

## <a name="create-a-universal-data-link-udl-file-to-test-connectivity"></a>연결을 테스트 하려면 유니버설 데이터 링크 (UDL) 파일 만들기
유니버설 데이터 링크 파일 또는 UDL 파일을 포함 하는 텍스트 파일은 기본적으로 데이터베이스 연결 문자열입니다.  위에서 얻은 정보를 사용 하 여 SQL 서버에서 연결에 응답 하는 여부 테스트할 수 있습니다.

### <a name="to-create-a-udl-file-to-test-connectivity"></a>연결을 테스트 하는 udl 파일을 만들려면

1. 메모장을 열고 파일 test.udl로 저장 합니다.  했는지 확인 하십시오 **모든 파일** 에 대 한 드롭다운 목록에서 선택한 **형식으로 저장**합니다.
2. Test.udl 두 번 클릭
3. 다음 정보를 입력 합니다:는 합니다. **선택 하거나 서버 이름을 입력 합니다.**  데이터 소스의 b 위의 연결 문자열을 사용 합니다. **서버 로그온 정보를 입력 합니다.**  AD FS 서비스 계정 또는 원격으로 로그온 할 권한이 있는 계정을 사용 합니다.  통합 windows 계정을 사용 하는 경우 인증이 고 그렇지 사용자 이름 및 암호를 입력 합니다.
    c. **서버에서 데이터베이스를 선택 합니다.** 위 문자열에서 초기 카탈로그를 사용 합니다.  예:  AdfsConfigurationV3.
   ![연결 테스트](media/ad-fs-tshoot-sql/sql4.png)
1. 클릭 **연결 테스트**합니다.</br>
![성공](media/ad-fs-tshoot-sql/sql3.png)

## <a name="use-sql-server-management-studio-to-test-connectivity"></a>SQL Server Management Studio를 사용 하 여 연결을 테스트 하려면
할 수도 있습니다 [다운로드](https://go.microsoft.com/fwlink/?linkid=864329) 및 데이터베이스 연결을 테스트 하는 SSMS를 설치 합니다.

### <a name="to-test-connectivity-with-ssms"></a>SSMS 사용 하 여 연결을 테스트 하려면
1. 다운로드 하 고 SQL Server Management Studio를 설치 합니다.
![설치](media/ad-fs-tshoot-sql/sql5.png)
1. SSMS를 열고, 서버 이름을 입력 합니다.  위의 데이터 소스입니다.
2. AD FS 서비스 계정 또는 원격으로 로그온 할 권한이 있는 계정을 사용 합니다.  통합 windows 계정을 사용 하는 경우 인증이 고 그렇지 사용자 이름 및 암호를 입력 합니다.
![연결](media/ad-fs-tshoot-sql/sql6.png)
1. 왼쪽 입력이 표시 됩니다.  데이터베이스를 확장 하 고 AD FS 데이터베이스에 표시 되는지 확인 합니다.
![AD FS 데이터베이스](media/ad-fs-tshoot-sql/sql7.png)

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)