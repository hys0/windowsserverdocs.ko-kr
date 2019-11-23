---
title: (Windows 내부 데이터베이스) WID에서 SQL로 WSUS 데이터베이스 마이그레이션
description: WSUS (windows Server Update Service) 항목-Windows 내부 데이터베이스 인스턴스에서 SQL Server의 로컬 또는 원격 인스턴스로 WSUS 데이터베이스 (SUSDB)를 마이그레이션하는 방법입니다.
ms.prod: windows-server
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
ms.openlocfilehash: 0977aa1fd9a6848bd7b85bb592b6a82556277e72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361585"
---
>적용 대상: Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

# <a name="migrating-the-wsus-database-from-wid-to-sql"></a>WID에서 SQL로 WSUS 데이터베이스 마이그레이션

다음 단계를 사용 하 여 WSUS 데이터베이스 (SUSDB)를 Windows 내부 데이터베이스 인스턴스에서 SQL Server의 로컬 또는 원격 인스턴스로 마이그레이션합니다.

## <a name="prerequisites"></a>필수 구성 요소

- SQL 인스턴스. 이는 기본 **MSSQLServer** 또는 사용자 지정 인스턴스일 수 있습니다.
- SQL Server Management Studio
- WID 역할이 설치 된 WSUS
- IIS (일반적으로 서버 관리자를 통해 WSUS를 설치할 때 포함 됨) 아직 설치 되지 않은 경우 여야 합니다.

## <a name="migrating-the-wsus-database"></a>WSUS 데이터베이스 마이그레이션

### <a name="stop-the-iis-and-wsus-services-on-the-wsus-server"></a>WSUS 서버에서 IIS 및 WSUS 서비스를 중지 합니다.

PowerShell (승격)에서 다음을 실행 합니다.

```powershell
    Stop-Service IISADMIN
    Stop-Service WsusService
```

### <a name="detach-susdb-from-the-windows-internal-database"></a>Windows 내부 데이터베이스에서 SUSDB 분리

#### <a name="using-sql-management-studio"></a>SQL Management Studio 사용

1. **SUSDB** -&gt; **작업** -을 마우스 오른쪽 단추로 클릭 하 &gt; **분리**: ![image1를 클릭](images/image1.png)
2. **기존 연결 삭제** 를 선택 하 고 **확인** 을 클릭 합니다 (활성 연결이 있는 경우 선택 사항).
    ![image2](images/image2.png)

#### <a name="using-command-prompt"></a>명령 프롬프트 사용

> [!IMPORTANT]
> 다음 단계는 **sqlcmd** 유틸리티를 사용 하 여 Windows 내부 데이터베이스 인스턴스에서 WSUS 데이터베이스 (SUSDB)를 분리 하는 방법을 보여 줍니다. **Sqlcmd** 유틸리티에 대 한 자세한 내용은 [sqlcmd 유틸리티](https://go.microsoft.com/fwlink/?LinkId=81183)를 참조 하세요.
> 1. 관리자 권한 명령 프롬프트를 엽니다.
> 2. 다음 SQL 명령을 실행 하 여 **sqlcmd** 유틸리티를 사용 하 여 WSUS 데이터베이스 (SUSDB)를 Windows 내부 데이터베이스 인스턴스에서 분리 합니다.

```batchfile
        sqlcmd -S \\.\pipe\Microsoft##WID\tsql\query
        use master
        GO
        alter database SUSDB set single_user with rollback immediate
        GO
        sp_detach_db SUSDB
        GO
```

### <a name="copy-the-susdb-files-to-the-sql-server"></a>SUSDB 파일을 SQL Server에 복사 합니다.

1. SUSDB 및 **SUSDB\_** 를 WID 데이터 폴더 (\* **%** ;)에서 SQL 인스턴스 데이터 폴더로 복사 합니다.

> [!TIP]
> 예를 들어 SQL 인스턴스 폴더가 **C:\Program FILES\MICROSOFT sql Server\MSSQL12. 인 경우 MSSQLSERVER\MSSQL**및 WID 데이터 폴더는 **C:\WINDOWS\WID\DATA** 로 SUSDB 파일을 **C:\WINDOWS\WID\DATA** 에서 **C:\Program Files\Microsoft SQL Server\MSSQL12.로 복사 합니다. MSSQLSERVER\MSSQL\Data**

### <a name="attach-susdb-to-the-sql-instance"></a>SQL 인스턴스에 SUSDB 연결

1. **SQL Server Management Studio**의 **인스턴스** 노드에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭 한 다음 **연결**을 클릭 합니다.
    ![image3](images/image3.png)
2. **데이터베이스 연결** 상자에서 **연결할 데이터베이스**아래에 있는 **추가** 단추를 클릭 하 고 **SUSDB** 파일 (WID 폴더에서 복사 됨)을 찾은 다음 **확인**을 클릭 합니다.
    ![image4.jpg](images/image4.png) ![image5](images/image5.png)

> [!TIP]
> Transact-sql을 사용 하 여이 작업을 수행할 수도 있습니다.  해당 지침에 대 한 [데이터베이스 연결에 대 한 SQL 설명서](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) 를 참조 하십시오.
>
> 예 (이전 예제의 경로 사용):
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

### <a name="verify-sql-server-and-database-logins-and-permissions"></a>SQL Server 및 데이터베이스 로그인 및 사용 권한 확인

#### <a name="sql-server-login-permissions"></a>SQL Server 로그인 권한

SUSDB을 연결한 후 다음을 수행 하 여 **NT AUTHORITY\NETWORK SERVICE** 에 SQL Server 인스턴스에 대 한 로그인 권한이 있는지 확인 합니다.

1. SQL Server Management Studio로 이동
2. 인스턴스 열기
3. **보안** 을 클릭 합니다.
4. **로그인** 클릭

**NT AUTHORITY\NETWORK SERVICE** 계정이 나열 됩니다. 그렇지 않은 경우 새 로그인 이름을 추가 하 여 추가 해야 합니다.

> [!IMPORTANT]
> SQL 인스턴스가 WSUS와 다른 컴퓨터에 있는 경우 WSUS 서버의 컴퓨터 계정이 **[FQDN]\\[WSUSComputerName] $** 형식으로 나열 되어야 합니다.  그렇지 않은 경우 아래 단계를 사용 하 여 추가 하 고 nt **AUTHORITY\NETWORK service** 를 WSUS 서버의 컴퓨터 계정 ( **[FQDN]\\[WSUSComputerName] $** )으로 바꾸면 **nt AUTHORITY\NETWORK service** 에 권한을 부여 하는 것 ***외에도*** 이 작업을 수행할 수 있습니다.

##### <a name="adding-nt-authoritynetwork-service-and-granting-it-rights"></a>NT AUTHORITY\NETWORK SERVICE 추가 및 it 권한 부여

1. **로그인** 을 마우스 오른쪽 단추로 클릭 하 고 **새 로그인** ...을 클릭 합니다.
    ![image6](images/image6.png)
2. **일반** 페이지에서 **로그인 이름** (**NT AUTHORITY\NETWORK SERVICE**)을 입력 하 고 **기본 데이터베이스** 를 SUSDB로 설정 합니다.
    ![image7](images/image7.png)
3. **서버 역할** 페이지에서 **공용** 및 **sysadmin** 이 선택 되어 있는지 확인 합니다.
    ![image8](images/image8.png)
4. **사용자 매핑** 페이지에서 다음을 수행 합니다.
    - **이 로그인으로 매핑된 사용자**에서: **SUSDB** 를 선택 합니다.
    - **데이터베이스 역할 멤버 자격: SUSDB**에서 다음을 확인 합니다.
        - **공개적**
        - **웹 서비스** ![image9](images/image9.png)
5. **확인** 을 클릭합니다.

이제 로그인 아래에 **NT AUTHORITY\NETWORK SERVICE** 가 표시 되어야 합니다.
![image10](images/image10.png)

#### <a name="database-permissions"></a>데이터베이스 권한

1. SUSDB를 마우스 오른쪽 단추로 클릭 합니다.
2. **속성** 선택
3. **권한** 클릭

**NT AUTHORITY\NETWORK SERVICE** 계정이 나열 됩니다.

1. 그렇지 않으면 계정을 추가 합니다.
2. 로그인 이름 텍스트 상자에 다음과 같은 형식으로 WSUS 컴퓨터를 입력 합니다.
    > [**FQDN]\\[WSUSComputerName] $**
3. **기본 데이터베이스가** **SUSDB**로 설정 되어 있는지 확인 합니다.

    > [!TIP]
    > 다음 예에서는 FQDN이 **Contosto.com** 이 고 WSUS 컴퓨터 이름은 **WsusMachine**입니다.
    >
    > ![image11](images/image11.png)

4. **사용자 매핑** 페이지의 **"이 로그인으로 매핑된 사용자"** 에서 **SUSDB** 데이터베이스를 선택 합니다.
5. **"데이터베이스 역할 멤버 자격: SUSDB"** : ![image12](images/image12.png)에서 **webservice** 를 확인 합니다.
6. **확인** 을 클릭 하 여 설정을 저장 합니다.
    > [!NOTE]
    > 변경 내용을 적용 하려면 SQL 서비스를 다시 시작 해야 할 수 있습니다.

### <a name="edit-the-registry-to-point-wsus-to-the-sql-server-instance"></a>WSUS가 SQL Server 인스턴스를 가리키도록 레지스트리를 편집 합니다.

> [!IMPORTANT]
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/en-us/help/322756)해 두세요.

1. **시작**을 클릭하고, **실행**을 클릭하고, **regedit**를 입력한 후 **확인**을 클릭합니다.
2. 다음 키를 찾습니다. **HKEY_LOCAL_MACHINE \software\microsoft\updateservices\server\setup\sqlservername**
3. **값** 텍스트 상자에 **[ServerName]\\[InstanceName]** 을 입력 한 다음 **확인**을 클릭 합니다. 인스턴스 이름이 기본 인스턴스인 경우 **[ServerName]** 을 입력 합니다.
4. 다음 키를 찾습니다. **HKEY_LOCAL_MACHINE \Software\microsoft\update Services\Server\Setup\Installed Role Services\UpdateServices-WidDatabase** ![image13](images/image13.png)
5. 키 이름을 **updateservices-api** ![image41로 바꿉니다](images/image14.png)

    > [!NOTE]
    > 이 키를 업데이트 하지 않으면 **wsusutil.exe** 은 마이그레이션한 SQL 인스턴스 대신 WID를 서비스 하려고 시도 합니다.

### <a name="start-the-iis-and-wsus-services-on-the-wsus-server"></a>WSUS 서버에서 IIS 및 WSUS 서비스를 시작 합니다.

PowerShell (승격)에서 다음을 실행 합니다.

```powershell
    Start-Service IISADMIN
    Start-Service WsusService
```

> [!NOTE]
> WSUS 콘솔을 사용 하는 경우이를 닫고 다시 시작 합니다.

## <a name="uninstalling-the-wid-role-not-recommended"></a>WID 역할 제거 (권장 하지 않음)

> [!WARNING]
> WID 역할을 제거 하면 설치 후 작업에 Wsusutil.exe에 필요한 스크립트가 포함 된 데이터베이스 폴더 ( **%SystemDrive%\Program Files\Update Services\Database**)도 제거 됩니다. WID 역할을 제거 하도록 선택한 경우 **%SystemDrive%\Program Files\Update Services\Database** 폴더를 미리 백업 해야 합니다.

PowerShell 사용:

```powershell
Uninstall-WindowsFeature -Name 'Windows-Internal-Database'
```

WID 역할이 제거 된 후에는 다음 레지스트리 키가 있는지 확인 합니다. **HKEY_LOCAL_MACHINE \Software\microsoft\update Services\Server\Setup\Installed role Services\UpdateServices-Database**