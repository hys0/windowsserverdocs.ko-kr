---
ms.assetid: 4deff06a-d0ef-4e5a-9701-5911ba667201
title: AD FS 신속 복원 도구
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/02/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fc924f5e5bdd7dabecac4fdd6805ad261a0fc634
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866171"
---
# <a name="ad-fs-rapid-restore-tool"></a>AD FS 신속 복원 도구

## <a name="overview"></a>개요
오늘날 AD FS는 항상 사용 가능 하 여 AD FS 팜을 설정 하 여 합니다. 일부 조직에서는 단일 서버 AD FS 배포 하는 방법을 싶습니다, 그리고 여러 AD FS 서버 및 네트워크 부하 않고 일부 인프라를 분산 하지 않아도 서비스 보증 경우 복원할 수 신속 하 게 문제가 있습니다.
새 AD FS 신속 하 게 복원 도구를 전체 백업 및 복원의 운영 체제 또는 시스템 상태를 요구 하지 않고 AD FS 데이터를 복원 하는 방법을 제공 합니다. Azure 또는 온-프레미스 위치에 AD FS 구성을 내보내려면 새로운 도구를 사용할 수 있습니다.  그런 다음 다시 만들거나 AD FS 환경을 복제 내보낸된 데이터 새로 AD FS 설치를 적용할 수 있습니다. 

## <a name="scenarios"></a>시나리오
다음과 같은 시나리오에서 AD FS 신속 하 게 복원 도구를 사용할 수 있습니다.

1. 문제가 후 AD FS 기능을 신속 하 게 복원
    - 온라인 AD FS 서버 대신 신속 하 게 배포할 수 있는 AD FS의 콜드 대기 설치를 만드는 도구를 사용 합니다.
2. 동일한 테스트 및 프로덕션 환경에 배포
    - 신속 하 게 테스트 환경에서 프로덕션 AD FS의 정확한 복사본을 만들려면 또는 신속 하 게 유효성을 검사 하는 테스트 구성을 프로덕션에 배포 하는 도구를 사용 하 여

>[!NOTE] 
>SQL 병합 복제 또는 Always on 가용성 그룹을 사용 하는 경우 빠른 복원 도구가 지원 되지 않습니다. 대신 SQL 기반 백업과 SSL 인증서의 백업을 사용 하는 것이 좋습니다.

## <a name="what-is-backed-up"></a>백업 항목
도구는 다음과 같은 AD FS 구성 백업
    
- AD FS 구성 데이터베이스 (SQL 또는 WID)
- 구성 파일 (AD FS 폴더에 있음)
- 토큰 서명 및 인증서와 프라이빗 키 (에서 Active Directory DKM 컨테이너)를 암호 해독을 자동으로 생성
- SSL 인증서와 외부에서 등록한 인증서 (토큰 서명, 토큰 암호 해독 및 서비스 통신)와 해당 프라이빗 키(참고: 프라이빗 키를 내보낼 수 있어야 하고 스크립트를 실행하는 사용자에 대한 액세스 권한이 있어야 합니다.)
- 사용자 지정 인증 공급자, 특성 저장소 및 로컬 클레임 공급자의 목록이 설치 되어 있는 것을 신뢰 합니다.

## <a name="how-to-use-the-tool"></a>이 도구를 사용 하는 방법
첫째, [다운로드](https://go.microsoft.com/fwlink/?LinkId=825646) 및 AD FS 서버에 MSI를 설치 합니다.  

PowerShell 프롬프트에서 다음 명령을 실행 합니다.

```powershell
import-module 'C:\Program Files (x86)\ADFS Rapid Recreation Tool\ADFSRapidRecreationTool.dll'
```

>[!NOTE] 
>통합 데이터베이스 WID (Windows)를 사용 하는 경우이 도구는 기본 AD FS 서버에서 실행 되도록 해야 합니다.  사용할 수는 `Get-AdfsSyncProperties` 주 서버 인지 여부는 서버에 있는 확인 하려면 PowerShell cmdlet.

### <a name="system-requirements"></a>시스템 요구 사항

- 이 도구는 Windows Server 2012 R2 이상 AD FS에 대 한 작동합니다. 
- 필요한.NET framework에는 적어도 4.0입니다. 
- 백업으로 동일한 버전의 AD FS 서버에서 실행 되어야 하는 복원 하 고 AD FS 서비스 계정으로 동일한 Active Directory 계정을 사용 하 합니다.

## <a name="create-a-backup"></a>백업 만들기
백업을 만들 백업 ADFS cmdlet을 사용 합니다. 이 cmdlet은 AD FS 구성, 데이터베이스, SSL 인증서 등을 백업합니다. 

사용자가이 cmdlet을 실행 하려면 최소한 로컬 관리자 여야 합니다. Active Directory DKM 컨테이너 (기본 AD FS 구성에 필요)를 백업 하려면 사용자가 도메인 관리자 이거나 AD FS 서비스 계정 자격 증명을 전달 하거나 DKM 컨테이너에 액세스할 수 있어야 합니다.  GMSA 계정을 사용 하는 경우 사용자는 도메인 관리자 이거나 컨테이너에 대 한 사용 권한이 있어야 합니다. gMSA 자격 증명을 제공할 수 없습니다. 

"AdfsBackup_ID_Date" 패턴에 따라 백업 이름이 지정 됩니다. 버전 번호, 날짜 및 시간에 백업이 수행 된 포함 됩니다.
Cmdlet은 다음 매개 변수를 사용 합니다.
    
매개 변수 집합

![AD FS 신속 복원 도구](media/AD-FS-Rapid-Restore-Tool/parameter1.png)

### <a name="detailed-description"></a>자세한 설명

- **BackupDKM** -기본 구성 (자동으로 생성 된 토큰 서명 및 인증서를 암호 해독)에서 AD FS 키를 포함 하는 Active Directory DKM 컨테이너를 백업 합니다. 이는 ad 도구 ' ldifde '를 사용 하 여 AD 컨테이너와 해당 하위 트리를 모두 내보냅니다.

- -**Storagetype &lt;문자열&gt;**  -사용자가 사용 하려는 저장소의 유형입니다. "FileSystem"은 사용자가 로컬 또는 "Azure" 네트워크에서 해당 파일을 저장 하려는 경우 사용자가 백업을 수행할 때 사용자가 Azure Storage 컨테이너에 저장 하려는 경우 백업 위치 (파일 시스템 또는 pnrp. 사용할 Azure에 대 한 Azure 저장소 자격 증명을 cmdlet으로 전달 되어야 합니다. 저장소 자격 증명의 계정 이름 및 키를 포함 합니다. 또한이 컨테이너 이름에 전달 합니다. 컨테이너가 존재 하지 않는 경우 백업 중에 생성 됩니다. 사용할 파일 시스템에 대 한 저장소 경로 제공 합니다. 해당 디렉터리에 각 백업에 대해 새 디렉터리가 생성 됩니다. 만든 각 디렉터리에는 백업된 파일이 포함 됩니다. 

- **EncryptionPassword &lt;문자열&gt;** -백업된 된 모든 파일을 저장 하기 전에 암호화 하는 데 사용 될 것 이라고 암호

- **AzureConnectionCredentials &lt;pscredential&gt;** -계정 이름 및 Azure 저장소 계정에 대 한 키

- **AzureStorageContainer &lt;문자열&gt;** -백업이 Azure에 저장 될 저장소 컨테이너

- **StoragePath &lt;문자열&gt;** -위치에 백업을 저장 됩니다

- **Serviceaccountcredential &lt;pscredential&gt;**  -현재 실행 중인 AD FS 서비스에 사용 되는 서비스 계정을 지정 합니다. 이 매개 변수는 사용자가 DKM을 백업 하 고 도메인 관리자가 아니거나 컨테이너의 콘텐츠에 대 한 액세스 권한이 없는 경우에만 필요 합니다. 

- **BackupComment &lt;string&gt;** -Hyper-v가 검사점 이름을 지정 하는 개념과 비슷합니다 복원 되는 동안 표시 되는 백업에 대 한 정보는 문자열입니다. 기본값은 빈 문자열

 
## <a name="backup-examples"></a>백업 예제
AD FS 빠른 복원 도구를 사용 하는 백업 예제는 다음과 같습니다.

### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-and-has-access-to-the-dkm-container-contents-either-domain-admin-or-delegated"></a>DKM을 사용 하 여 파일 시스템에 AD FS 구성을 백업 하 고 DKM 컨테이너 내용 (도메인 관리자 또는 위임 된 항목)에 액세스할 수 있습니다.

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM
```
 
### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-with-the-service-account-credential-running-as-local-admin"></a>로컬 관리자로 실행 되는 서비스 계정 자격 증명을 사용 하 여 DKM을 사용 하 여 파일 시스템에 AD FS 구성을 백업 합니다.

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM -ServiceAccountCredential $cred
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-azure-storage-container"></a>Azure Storage 컨테이너에 대해 DKM을 사용 하지 않고 AD FS 구성을 백업 합니다.

```powershell
Backup-ADFS -StorageType "Azure" -AzureConnectionCredentials $cred -AzureStorageContainer "adfsbackups"  -EncryptionPassword "password" -BackupComment "Clean Install of ADFS"
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-file-system"></a>파일 시스템에 대 한 DKM 없이 AD FS 구성 백업

```powershell   
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)"
```

## <a name="restore-from-backup"></a>백업에서 복원
새 AD FS 설치 백업 ADFS를 사용 하 여 만든 구성 적용 복원 ADFS cmdlet을 사용 합니다.

이 cmdlet은 cmdlet을 사용 하 여 새 AD FS 팜을 만듭니다 `Install-AdfsFarm` 되 고 AD FS 구성, 데이터베이스, 인증서 등을 복원 합니다.  AD FS 역할 서버에 설치 되지 않은, 경우 cmdlet를 설치 합니다.  Cmdlet는 기존 백업 복원 위치를 확인 하 고는 적절 한 백업을 수행 된 날짜/시간 및 백업 주석을 백업에 사용자 연결 수에 따라 선택 하 라는 메시지. 다른 페더레이션 서비스 이름으로 여러 AD FS 구성의 경우 다음 사용자가 선택 하 라는 메시지가 먼저 적절 한 AD FS 구성 합니다.
사용자가이 cmdlet을 실행 하려면 로컬 및 도메인 관리자 여야 합니다.


>[!NOTE] 
>AD FS 신속한 복구 도구를 사용 하기 전에 서버 백업을 복원 하기 전에 도메인에 가입 되어 있는지 확인 합니다. 

Cmdlet은 다음 매개 변수를 사용 합니다. 

![AD FS 신속 복원 도구](media/AD-FS-Rapid-Restore-Tool/parameter2.png)

### <a name="detailed-description"></a>자세한 설명

- **StorageType &lt;문자열&gt;** -사용자가 사용 하려는 저장소 유형입니다.
 "FileSystem"은 사용자가 로컬 또는 "Azure" 네트워크에 저장 하려는 사용자가 Azure Storage 컨테이너에 저장 하려고 함을 나타냅니다.

- **DecryptionPassword &lt;문자열&gt;** -백업된 된 모든 파일 암호화에 사용 된 암호 

- **AzureConnectionCredentials &lt;pscredential&gt;** -계정 이름 및 Azure 저장소 계정에 대 한 키

- **AzureStorageContainer &lt;문자열&gt;** -백업이 Azure에 저장 될 저장소 컨테이너

- **StoragePath &lt;문자열&gt;** -위치에 백업을 저장 됩니다

- **ADFSName &lt; 문자열 &gt;** -백업 및 복원 하려고 하는 페더레이션의 이름입니다. 이 제공 되지 않았고는 하나의 페더레이션 서비스 이름 다음에 사용 됩니다. 있는 경우에 둘 이상의 페더레이션 서비스 위치에 백업 후 사용자는 페더레이션 서비스 백업 중 하나를 선택 하 라는 메시지가 표시 됩니다.

- **Serviceaccountcredential &lt; pscredential &gt;**  -복원 중인 새 AD FS 서비스에 사용 되는 서비스 계정을 지정 합니다. 

- **GroupServiceAccountIdentifier&lt;string&gt;** -사용자가 복원 중인 새 AD FS 서비스에 사용 하려는 GMSA입니다. 기본적으로, 둘 중 아무것도 제공 다음 백업를 계정 이름이 사용 됩니다 GMSA를 다른 서비스 계정에 넣을 묻는 것

- **DBConnectionString &lt;문자열&gt;** -은 전달 해야 SQL 연결 문자열 또는 형식 WID WID.에 대 한 다음 다른 데이터베이스에 복원에 사용 하 여 사용자가 원하는 경우

- **Force &lt;bool&gt;** -도구는 백업을 선택 하 고 나면 가질 수 있는 프롬프트를 건너뛰고

- **RestoreDKM &lt;bool&gt;** -복원 DKM 컨테이너 AD로 새 광고를 하려는 경우 설정 해야 하 고는 DKM 처음 백업 합니다.

## <a name="restore-examples"></a>복원 예제

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-azure-storage-container"></a>Azure Storage 컨테이너에서 DKM을 사용 하지 않고 AD FS 구성을 복원 합니다.

```powershell
Restore-ADFS -StorageType "Azure" -AzureConnectionCredential $cred -DecryptionPassword "password" -AzureStorageContainer "adfsbackups"
```

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-file-system"></a>파일 시스템에서 DKM을 사용 하지 않고 AD FS 구성을 복원 합니다.
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password"
```

### <a name="restore-the-ad-fs-configuration-with-the-dkm-to-the-file-system"></a>DKM을 사용 하 여 파일 시스템으로 AD FS 구성을 복원 합니다. 
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -RestoreDKM
```

### <a name="restore-the-ad-fs-configuration-to-wid"></a>WID에 AD FS 구성을 복원 합니다.

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "WID"
``` 

### <a name="restore-the-ad-fs-configuration-to-sql"></a>AD FS 구성을 SQL로 복원

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "Data Source=TESTMACHINE\SQLEXPRESS; Integrated Security=True"
```

### <a name="restores-the-ad-fs-configuration-with-the-specified-gmsa"></a>지정 된 GMSA를 사용 하 여 AD FS 구성을 복원 합니다.

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -GroupServiceAccountIdentifier "mangupd1\adfsgmsa$"
```
### <a name="restore-the-ad-fs-configuration-with-the-specified-service-account-creds"></a>지정 된 서비스 계정 자격 증명을 사용 하 여 AD FS 구성을 복원 합니다.

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -ServiceAccountCredential $cred
```

## <a name="encryption-information"></a>암호화 정보
모든 백업 데이터는 클라우드로 푸시하 또는 파일 시스템에 저장 하기 전에 암호화 됩니다.  

백업의 일부로 생성 하는 각 문서는 S-256을 사용 하 여 암호화 됩니다. 이 도구에 전달 된 암호 Rfc2898DeriveBytes 클래스를 사용 하 여 새 암호를 생성 하는 전달 구를으로 사용 됩니다. 

RngCryptoServiceProvider는 AES 및 Rfc2898DeriveBytes 클래스에서 사용 하는 솔트를 생성 하는 데 사용 됩니다. 

## <a name="log-files"></a>로그 파일
백업 또는 복원을 수행할 때마다 로그 파일이 생성 됩니다. 다음 위치에서 찾을 수 있습니다.

- **%localappdata%\ADFSRapidRecreationTool**

>[!NOTE]
> 복원을 수행할 때 AD FS 서비스를 시작 하기 전에 수동으로 설치할 추가 인증 공급자, 특성 저장소 및 로컬 클레임 공급자 트러스트에 대 한 개요를 포함 하는 PostRestore_Instructions 파일이 만들어질 수 있습니다.

## <a name="version-release-history"></a>버전 릴리스 기록

### <a name="version-10820"></a>버전 1.0.82.0
릴리스 7 월 2019

**해결 된 문제:**
- LDAP 이스케이프 문자를 포함 하는 AD FS 서비스 계정 이름에 대 한 버그 수정


### <a name="version-10810"></a>버전: 1.0.81.0
릴리스 2019년 4월

**해결 된 문제:**


- 인증서 백업 및 복원에 대 한 버그 수정
- 로그 파일에 대 한 추가 추적 정보


### <a name="version-10750"></a>버전: 1.0.75.0
릴리스 2018년 8월

**해결 된 문제:**
* 백업 업데이트--BackupDKM 스위치를 사용 하는 경우 ADFS  이 도구는 현재 컨텍스트가 DKM 컨테이너에 액세스할 수 있는지 여부를 확인 합니다.  그렇다면 도메인 관리자 권한 또는 서비스 계정 자격 증명이 필요 하지 않습니다.  이렇게 하면 명시적으로 자격 증명을 제공 하거나 도메인 관리자 계정으로 실행 하지 않고도 자동화 된 백업이 수행 될 수 있습니다.

### <a name="version-10730"></a>버전: 1.0.73.0
릴리스 2018년 8월

**해결 된 문제:**
* 응용 프로그램이 FIPS를 준수 하도록 암호화 알고리즘을 업데이트 합니다.
    
    >[!NOTE]
    > FIPS 규정 준수에의 한 암호화 알고리즘의 변경으로 인해 이전 백업은 새 버전에서 작동 하지 않습니다.
    
* 병합 복제를 사용 하는 SQL 클러스터에 대 한 지원 추가

### <a name="version-10720"></a>버전: 1.0.72.0
릴리스 2018 년 7 월

**해결 된 문제:**

   - 버그 수정: 를 수정 했습니다. 전체 업그레이드를 지 원하는 MSI 설치 관리자 

### <a name="10180"></a>1.0.18.0
릴리스 2018 년 7 월

**해결 된 문제:**

   - 버그 수정: 특수 문자를 포함 하는 서비스 계정 암호를 처리 합니다 (ie, ' & ').
   - 버그 수정: 다른 프로세스에서 IdentityServer을 사용 하 고 있으므로 복원에 실패 합니다.


### <a name="1000"></a>1.0.0.0
릴리스 날짜: 2016년 10월

AD FS 빠른 복원 도구의 초기 릴리스
