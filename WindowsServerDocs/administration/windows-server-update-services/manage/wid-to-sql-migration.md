---
title: WSUS 데이터베이스 (Windows 내부 데이터베이스)로 마이그레이션 WID to SQL
description: Windows Server Update Service (WSUS) 항목-SQL Server의 로컬 또는 원격 인스턴스에 Windows 내부 데이터베이스 인스턴스에서 WSUS 데이터베이스 (SUSDB)를 마이그레이션하는 방법입니다.
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09g7dr
author: coreyp-at-msft
ms.author: coreyp
manager: dougkim
ms.date: 07/25/2018
ms.openlocfilehash: 9015bbc54a4c4bda0f691b79dbb7d3ba8ddbc4a1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439896"
---
>적용 대상: Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

# <a name="migrating-the-wsus-database-from-wid-to-sql"></a>WID에서 SQL로 WSUS 데이터베이스를 마이그레이션

SQL Server의 로컬 또는 원격 인스턴스에 WSUS 데이터베이스 (SUSDB)를 마이그레이션하려면 Windows 내부 데이터베이스 인스턴스에서 다음 단계를 사용 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- SQL 인스턴스입니다. 이 기본값을 수 있습니다 **MSSQLServer** 또는 사용자 지정 인스턴스.
- SQL Server Management Studio
- WID 역할이 설치 된 WSUS
- IIS (이 일반적으로 포함 된 WSUS 서버 관리자를 통해 설치한 경우). 아직 설치 되지 않은, 되도록 해야 합니다.

## <a name="migrating-the-wsus-database"></a>WSUS 데이터베이스 마이그레이션

### <a name="stop-the-iis-and-wsus-services-on-the-wsus-server"></a>WSUS 서버에서 IIS 및 WSUS 서비스를 중지 합니다.

(관리자 권한) PowerShell에서 다음을 실행 합니다.

```powershell
    Stop-Service IISADMIN
    Stop-Service WsusService
```

### <a name="detach-susdb-from-the-windows-internal-database"></a>Windows 내부 데이터베이스에서 SUSDB를 분리 합니다.

#### <a name="using-sql-management-studio"></a>SQL Management Studio를 사용 하 여

1. 마우스 오른쪽 단추로 클릭 **SUSDB** - &gt; **태스크** - &gt; 클릭 **분리**: ![image1](images/image1.png)
2. 확인할 **기존 연결 삭제** 누릅니다 **확인** (선택 사항에 대 한 활성 연결이 있는 경우).
    ![image2](images/image2.png)

#### <a name="using-command-prompt"></a>명령 프롬프트 사용

> [!IMPORTANT]
> 다음이 단계를 사용 하 여 WSUS 데이터베이스 (SUSDB)를 분리 하는 방법 Windows 내부 데이터베이스 인스턴스를 표시 합니다 **sqlcmd** 유틸리티입니다. 에 대 한 자세한 내용은 합니다 **sqlcmd** 유틸리티를 참조 하십시오 [sqlcmd 유틸리티](https://go.microsoft.com/fwlink/?LinkId=81183)합니다.
> 1. 관리자 권한 명령 프롬프트를 열으십시오
> 2. 사용 하 여 Windows 내부 데이터베이스 인스턴스에서 WSUS 데이터베이스 (SUSDB)를 분리 하려면 다음 SQL 명령을 실행 합니다 **sqlcmd** 유틸리티.

```batchfile
        sqlcmd -S \\.\pipe\Microsoft##WID\tsql\query
        use master
        GO
        alter database SUSDB set single_user with rollback immediate
        GO
        sp_detach_db SUSDB
        GO
```

### <a name="copy-the-susdb-files-to-the-sql-server"></a>SQL Server에 SUSDB 파일을 복사 합니다.

1. 복사본 **SUSDB.mdf** 하 고 **SUSDB\_log.ldf** WID 데이터 폴더에서 ( **% SystemDrive %** \** Windows\WID\Data * *) SQL 인스턴스 데이터 폴더입니다.

> [!TIP]
> 예를 들어 SQL 인스턴스 폴더 **C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL**, WID 데이터 폴더 이며 **C:\Windows\WID\Data 합니다** SUSDB 파일을 복사할 **C:\Windows\WID\Data** 에 **C:\Program Files\Microsoft SQL Server \MSSQL12 합니다. MSSQLSERVER\MSSQL\Data**

### <a name="attach-susdb-to-the-sql-instance"></a>SUSDB SQL 인스턴스에 연결

1. **SQL Server Management Studio**아래에 있는 합니다 **인스턴스** 노드를 마우스 오른쪽 단추로 클릭 **데이터베이스**를 클릭 하 고 **연결**합니다.
    ![image3](images/image3.png)
2. 에 **데이터베이스 연결** 상자의 **연결할 데이터베이스**, 클릭 합니다 **추가** 단추를 찾습니다는 **SUSDB.mdf** 파일 (에서 복사를 WID 폴더)를 클릭 하 고 **확인**합니다.
    ![image4](images/image4.png) ![image5](images/image5.png)

> [!TIP]
> 이 수행할 수 있습니다 Transact Sql을 사용 합니다.  참조 하십시오 합니다 [데이터베이스 연결에 대 한 SQL 설명서](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) 해당 명령에 대 한 합니다.
>
> 예제 (이전 예제에서 경로 사용):
> ```sql
>    USE master;
>    GO
>    CREATE DATABASE SUSDB
>    ON
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data\SUSDB.mdf'),
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SUSDB_Log.ldf')
>        FOR ATTACH;
>    GO
>```

### <a name="verify-sql-server-and-database-logins-and-permissions"></a>SQL Server 및 데이터베이스 로그인 및 사용 권한을 확인 합니다.

#### <a name="sql-server-login-permissions"></a>SQL Server 로그인 사용 권한

확인 후 SUSDB를 연결할 **NT AUTHORITY\NETWORK SERVICE** 다음을 수행 하 여 SQL Server 인스턴스의 로그인 권한이:

1. SQL Server Management Studio로 이동
2. 인스턴스 열기
3. 클릭 **보안**
4. 클릭 **로그인**

합니다 **NT AUTHORITY\NETWORK SERVICE** 계정 나열 되어야 합니다. 없는 경우 새 로그인 이름을 추가 하 여 추가 해야 합니다.

> [!IMPORTANT]
> WSUS 서버의 컴퓨터 계정 형식에 나열 되어야 합니다 SQL 인스턴스를 다른 컴퓨터에서 WSUS에 있으면 **[FQDN]\\[WSUSComputerName] $** 합니다.  그렇지 않은 추가 하려면 아래 단계를 사용할 수 있는, 경우 교체 **NT AUTHORITY\NETWORK SERVICE** WSUS 서버의 컴퓨터 계정을 사용 하 여 ( **[FQDN]\\[WSUSComputerName] $** )이 됩니다 ***외에*** 권리를 부여 **NT AUTHORITY\NETWORK SERVICE**

##### <a name="adding-nt-authoritynetwork-service-and-granting-it-rights"></a>NT AUTHORITY\NETWORK SERVICE를 추가 하 고 부여 권한

1. 마우스 오른쪽 단추로 클릭 **로그인** 를 클릭 하 고 **새 로그인...**
    ![image6](images/image6.png)
2. 에 **일반** 페이지에 정보를 입력 합니다 **로그인 이름** (**NT AUTHORITY\NETWORK SERVICE**), 설정 및는 **기본 데이터베이스** SUSDB를.
    ![image7](images/image7.png)
3. 에 **서버 역할** 페이지에서 **공용** 하 고 **sysadmin** 선택 됩니다.
    ![image8](images/image8.png)
4. 에 **사용자 매핑** 페이지:
    - 아래 **사용자가이 로그인으로 매핑된**: 선택 **SUSDB**
    - 아래 **데이터베이스 역할 멤버 자격: SUSDB**을 다음 선택 되어야 합니다.
        - **public**
        - **webService** ![image9](images/image9.png)
5. **확인**을 클릭합니다.

이제 **NT AUTHORITY\NETWORK SERVICE** 에서 로그인 합니다.
![image10](images/image10.png)

#### <a name="database-permissions"></a>데이터베이스 권한

1. SUSDB를 마우스 오른쪽 단추로 클릭
2. 선택 **속성**
3. 클릭 **권한**

합니다 **NT AUTHORITY\NETWORK SERVICE** 계정 나열 되어야 합니다.

1. 없는 경우 계정을 추가 합니다.
2. 로그인 이름 텍스트 상자에서 다음 형식으로 WSUS 컴퓨터를 입력 합니다.
    > [**FQDN]\\[WSUSComputerName]$**
3. 있는지 확인 합니다 **기본 데이터베이스** 로 설정 된 **SUSDB**합니다.

    > [!TIP]
    > 다음 예제에서는 FQDN이 **Contosto.com** WSUS 컴퓨터 이름은 **WsusMachine**:
    >
    > ![image11](images/image11.png)

4. 에 **사용자 매핑** 페이지에서 선택 합니다 **SUSDB** 아래에 있는 데이터베이스 **"이이 로그인으로 매핑된 사용자"**
5. 확인할 **webservice** 아래에서 **"데이터베이스 역할 멤버 자격: SUSDB"** :  ![image12](images/image12.png)
6. 클릭 **확인** 설정을 저장 합니다.
    > [!NOTE]
    > 변경 내용을 적용 하려면 SQL 서비스를 다시 시작 해야 합니다.

### <a name="edit-the-registry-to-point-wsus-to-the-sql-server-instance"></a>SQL Server 인스턴스로 지점 wsus 레지스트리 편집

> [!IMPORTANT]
> 이 섹션의 단계를 신중 하 게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정 하기 전에 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756) 문제가 발생할 경우.

1. **시작**을 클릭하고, **실행**을 클릭하고, **regedit**를 입력한 후 **확인**을 클릭합니다.
2. 다음 키를 찾습니다. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\UpdateServices\Server\Setup\SqlServerName**
3. 에 **값** 텍스트 상자에서 **[ServerName]\\[InstanceName]** 를 클릭 하 고 **확인**합니다. 인스턴스 이름은 기본 인스턴스의 경우 입력 **[ServerName]** 합니다.
4. 다음 키를 찾습니다. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update Services\Server\Setup\Installed 역할 Services\UpdateServices WidDatabase** ![image13](images/image13.png)
5. 키 이름 바꾸기 **UpdateServices 데이터베이스** ![image41](images/image14.png)

    > [!NOTE]
    > 그런 다음이 키를 업데이트 하지 않으면 하는 경우 **WsusUtil** 마이그레이션된 SQL 인스턴스 대신 WID 서비스 하려고 합니다.

### <a name="start-the-iis-and-wsus-services-on-the-wsus-server"></a>WSUS 서버에서 IIS 및 WSUS 서비스를 시작 합니다.

(관리자 권한) PowerShell에서 다음을 실행 합니다.

```powershell
    Start-Service IISADMIN
    Start-Service WsusService
```

> [!NOTE]
> WSUS 콘솔을 사용 하는 경우 닫고 다시 시작 합니다.

## <a name="uninstalling-the-wid-role-not-recommended"></a>(권장 하지 않음) WID 역할 제거

> [!WARNING]
> 데이터베이스 폴더 제거 WID 역할을 제거 ( **%SystemDrive%\Program Files\Update Services\Database**) WSUSUtil.exe 사후 설치 작업에 대 한 필요한 스크립트를 포함 하는 합니다. WID 역할을 제거 하려는 경우 했는지를 백업 합니다 **%SystemDrive%\Program Files\Update Services\Database** 미리 폴더.

PowerShell을 사용합니다.

```powershell
Uninstall-WindowsFeature -Name 'Windows-Internal-Database'
```

WID 역할을 제거한 후 다음 레지스트리 키가 있는지 확인 합니다. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update Services\Server\Setup\Installed 역할 Services\UpdateServices 데이터베이스**