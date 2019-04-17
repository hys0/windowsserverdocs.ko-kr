---
ms.assetid: 4deff06a-d0ef-4e5a-9701-5911ba667201
title: "광고 FS 신속한 복원 도구"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/20/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cd1cc8dab07288ba73c507bc551f089bb79502bc
ms.sourcegitcommit: 36d7b1dfd7da8e9f303d007a628e76149de000f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/21/2018
---
# <a name="ad-fs-rapid-restore-tool"></a>광고 FS 신속한 복원 도구

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

## <a name="overview"></a>개요
오늘 ADFS ADFS 농장 설정 하 여 매우 사용할 수 있게 됩니다. 여러 ADFS 서버와 쓰지 여전히 몇 가지를 않고도 인프라 균형 네트워크 로드 않아도 보증 서비스를 복원할 수 빠르게에 문제가 있는 경우, 일부 조직 단일 서버 ADFS 배포 하는 방법을 싶습니다.
새 광고 FS 신속한 복구 도구 전체 백업 및 복원 운영 체제 또는 시스템 상태를 않고도 ADFS 데이터를 복원 하는 방법을 제공 합니다. Azure 또는 온-프레미스 위치 ADFS 구성 내보낼 새로운 도구를 사용할 수 있습니다.  그런 다음 다시 만들거나 ADFS 환경 복제 내보낸된 데이터 ADFS 새로 설치를 적용할 수 있습니다. 

## <a name="scenarios"></a>시나리오
다음과 같은 경우에는 광고 FS 신속한 복구 도구를 사용할 수 있습니다.

1. 신속 하 게 문제 후 ADFS 기능을 복원
    - 온라인 ADFS 서버 대신 신속 하 게 배포 될 수 있는 Adfs의 콜드 대기 설치를 만드는 도구를 사용 하 여
2. 배포 동일한 테스트 및 생산 환경
    - 신속 하 게 만들 프로덕션 Adfs의 정확 하 게 복사본 테스트 환경에서 하거나 유효성을 검사 테스트 구성 프로덕션 신속 하 게 배포 하는 도구를 사용 하 여

## <a name="what-is-backed-up"></a>항목 백업
이 도구는 다음과 같은 ADFS 구성을 백업합니다
    
- 광고 FS 구성 데이터베이스 (SQL 또는 WID)
- 구성 파일 (ADFS 폴더에 있음)
- 토큰 서명 하 고 암호를 해독 인증서 및 (출처: 된 Active Directory DKM 컨테이너) 개인 키를 자동으로 생성
- 및 SSL 인증서 외부 등록 인증서 (토큰 서명, 토큰 암호 해독 한 서비스 통신)와 개인 해당 키 (참고: 개인 키 내보낼 수 있어야 하며 사용자 스크립트를 실행할에 액세스할 수 있는 권한이 있어야 합니다.)
- 설치 되어 있는 신뢰 하는 사용자 지정 인증 공급자, 특성 저장소 및 로컬 클레임 공급자 목록 합니다.

## <a name="how-to-use-the-tool"></a>이 도구를 사용 하는 방법
먼저 [다운로드](https://go.microsoft.com/fwlink/?LinkId=825646) MSI ADFS 서버에 설치 하 고 있습니다.  

>[!NOTE]
>광고 FS 신속한 복원 도구 호환 FIPS 않습니다.

PowerShell 프롬프트에서 다음 명령을 실행 합니다.

```powershell
import-module 'C:\Program Files (x86)\ADFS Rapid Recreation Tool\ADFSRapidRecreationTool.dll'
```

>[!NOTE] 
>Windows 통합 데이터베이스 (WID)를 사용 하는 경우이 도구 주 ADFS 서버의 실행 해야 합니다.  사용할 수 있는 `Get-SyncProperties` 주 서버 되어 여부 서버에 연결 되어 있는지 여부를 PowerShell cmdlet 합니다.

### <a name="system-requirements"></a>시스템 요구 사항

- 이 도구 ADFS 나중에 및 Windows Server 2012 r 2에서에 대해 작동합니다. 
- 필요한.NET framework 4.0 적어도입니다. 
- 백업으로 동일한 버전의 ADFS 서버에서 복원을 수행 해야 하 고 ADFS 서비스 계정으로 동일한 Active Directory 계정을 사용 하는 합니다.

## <a name="create-a-backup"></a>백업
백업을 만드는, 백업 ADFS cmdlet을 사용 합니다. 이 cmdlet ADFS 구성, 데이터베이스, SSL 인증서 등을 백업합니다. 

사용자는 최소 로컬 관리자가이 cmdlet 실행 해야 합니다. Active Directory DKM 컨테이너 (광고 기본 FS 구성에서 필요)을 백업 하는 사용자도 도메인 관리자 여야 합니다 하거나 ADFS 서비스 계정 자격 증명 전달할 필요 합니다.

백업은 "adfsBackup_ID_Date 시간" 패턴에 따라 이름이 지정 됩니다. 버전 번호, 날짜 및 시간 백업을 수행한 포함 됩니다.
다음 형식을 cmdlet 다음과 같습니다.
    
매개 설정

![광고 FS 신속한 복원 도구](media/AD-FS-Rapid-Restore-Tool/parameter1.png)

### <a name="detailed-description"></a>자세한 내용

- **BackupDKM** -기본 구성 (자동으로 생성 된 토큰 서명 인증서의 암호를 해독 및) ADFS 키가 포함 된 Active Directory DKM 컨테이너 백업 합니다. 이 광고 컨테이너 하 고 모든 하위 내보낼 광고 도구 'ldifde' 사용 합니다.

- -**StorageType &lt;문자열&gt; ** -저장소를 사용 하 여 사용자가 입력 합니다. "파일 시스템" 사용자가 폴더 로컬로 또는 네트워크 "Azure" 나타냅니다 백업을 수행할 때 Azure 스토리지 컨테이너에 저장 하는 사용자가, 백업 위치 파일 시스템을 선택 또는 클라우드 저장소를 나타냅니다. 사용할 Azure에 대 한 cmdlet에 Azure 저장소 자격 증명을 전달 합니다. 계정 이름 및 키 저장소 자격 증명 포함 되어 있습니다. 이외에 컨테이너 이름에 전달 합니다. 컨테이너 없으면 백업 하는 동안 만들어집니다. 사용 하려면 파일 시스템, 저장 경로 제공 해야 합니다. 디렉터리에 있는 새 디렉터리 각 백업에 대해 생성 됩니다. 각 디렉터리 만든 백업된 파일이 포함 됩니다. 

- **EncryptionPassword &lt;문자열&gt; ** -암호를 저장 하기 전에 백업된 된 모든 파일을 암호화 하는 데 사용할으로 이동

- **AzureConnectionCredentials &lt;pscredential&gt; ** -계정 이름이 및 Azure 저장소 계정에 대 한 키

- **AzureStorageContainer &lt;문자열&gt; ** -Azure에서 백업의 저장할 저장소 컨테이너

- **StoragePath &lt;문자열&gt; ** -위치는 백업에 저장

- **ServiceAccountCredential &lt;pscredential&gt; ** -현재 실행 중인 ADFS 서비스에 대 한 사용 되는 서비스 계정을 지정 합니다. 이 매개 사용자는 DKM 백업 하려는 경우에 필요 고 도메인 관리자

- **BackupComment &lt;문자열&gt; ** -유사한 검사점 이름 지정 Hyper-v의 개념을 복원 하는 동안 표시 되는 백업에 대 한 정보 문자열 합니다. 기본값은 없으면

 
## <a name="backup-examples"></a>백업 예제
광고 FS 신속한 복구 도구를 사용 하 여 백업 예는 다음과 같습니다.

### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-while-running-as-the-domain-admin"></a>ADFS 구성 된 파일 시스템 도메인 관리자 권한으로 실행 하면서 DKM 백업

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM
```
 
### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-with-the-service-account-credential-running-as-local-admin"></a>로컬 관리자 실행 서비스 계정 자격 증명을 사용 하 여 파일 시스템을 DKM와 백업 광고 FS 구성

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM -ServiceAccountCredential $cred
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-azure-storage-container"></a>Azure Storage 컨테이너 DKM 없이 ADFS 구성을 백업 합니다.

```powershell
Backup-ADFS -StorageType "Azure" -AzureConnectionCredentials $cred -AzureStorageContainer "adfsbackups"  -EncryptionPassword "password" -BackupComment "Clean Install of ADFS"
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-file-system"></a>백업 없이 파일 시스템으로 DKM ADFS 구성

```powershell   
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)"
```

## <a name="restore-from-backup"></a>백업에서 복원
백업 ADFS ADFS 새로 설치에 사용 하 여 만든 구성을 적용 하려면 복원 ADFS cmdlet을 사용 합니다.

이 cmdlet 만들어 cmdlet 사용 하 여 새 ADFS 농장 `Install-AdfsFarm` ADFS 구성, 데이터베이스, 인증서 등을 복원 합니다. ADFS 역할 서버에 설치 되어 있지 cmdlet 설치 됩니다.  Cmdlet에 대 한 기존 백업 복원 위치 확인 하 고 찍은 날짜/시간 및 모든 백업 설명을 사용자는 백업에 연결 될 수 있습니다에 따라에 대해 적절 한 백업을 선택 하 라는 메시지. 다른 federation 서비스 이름 사용 하 여 여러 ADFS 구성을 인 다음 사용자가 선택 하 라는 메시지가 처음 적절 한 ADFS 구성 합니다.
사용자는이 cmdlet 실행 하려면 관리자 로컬 및 도메인 해야 합니다.


>[!NOTE] 
>광고 FS 신속한 Recovery Tool을 사용 하기 전에 서버 백업을 복원 하기 전에 도메인에 가입 되어 있는지 확인 합니다. 

다음 형식을 cmdlet 다음과 같습니다. 

![광고 FS 신속한 복원 도구](media/AD-FS-Rapid-Restore-Tool/parameter2.png)

### <a name="detailed-description"></a>자세한 내용

- **StorageType &lt;문자열&gt; ** -저장소를 사용 하 여 사용자가 입력 합니다.
 사용자가 로컬 폴더에 저장 하려는 또는 네트워크 "Azure" 나타냅니다 Azure 스토리지 컨테이너에 저장 하는 사용자가 원하는. "파일 시스템" 나타냅니다.

- **DecryptionPassword &lt;문자열&gt; ** -백업된 된 모든 파일을 암호화 하는 데 사용 된 암호 

- **AzureConnectionCredentials &lt;pscredential&gt; ** -계정 이름이 및 Azure 저장소 계정에 대 한 키

- **AzureStorageContainer &lt;문자열&gt; ** -Azure에서 백업의 저장할 저장소 컨테이너

- **StoragePath &lt;문자열&gt; ** -위치는 백업에 저장

- **ADFSName &lt; 문자열 &gt; ** -federation 백업 및 복원로 이동 하는 이름입니다. 이 제공 되지 않는 경우 하나만 federation 서비스 이름 다음 있는 사용 됩니다. 있는 경우 둘 이상의 federation 서비스는 위치를 백업 후 사용자 백업 Federation Services 중 하나를 선택 하 라는 메시지가 표시 됩니다.

- **ServiceAccountCredential &lt; pscredential &gt; ** -새 ADFS 서비스 복원 되 고에 사용할 수 있는 서비스 계정을 지정 

- **GroupServiceAccountIdentifier &lt;문자열&gt; ** -새 ADFS 서비스 복원를 사용 하 여 사용자가 The GMSA 합니다. 기본적으로 둘 다이 제공 된 백업한 다음을 계정 이름을 사용 됩니다 GMSA, 다른 사용자가 서비스 계정에 추가 하 라는 메시지가 않은 경우

- **DBConnectionString &lt;문자열&gt; ** -해야 통과 SQL 연결 문자열 또는 형식에 WID WID.에 대 한 다음 다른 DB 복원이 사용 하 여 사용자가 원하는 경우

- **힘 &lt;bool&gt; ** -백업을 수 있다고 표시 되 면 도구가 포함 될 수 있는 프롬프트를 건너뛰는

- **RestoreDKM &lt;bool&gt; ** -DKM 컨테이너 광고를 복원, 새로운 광고를 설정 하 고 있는 DKM 처음 백업 된 합니다.

## <a name="restore-examples"></a>예를 복원

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-azure-storage-container"></a>ADFS 구성에서 DKM 없이 Azure Storage 컨테이너에서 복원

```powershell
Restore-ADFS -StorageType "Azure" -AzureConnectionCredential $cred -DecryptionPassword "password" -AzureStorageContainer "adfsbackups"
```

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-file-system"></a>ADFS 구성에서 DKM 하지 않고 파일 시스템에서 복원
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password"
```

### <a name="restore-the-ad-fs-configuration-with-the-dkm-to-the-file-system"></a>ADFS 구성에서 DKM와 파일 시스템 복원 
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -RestoreDKM
```

### <a name="restore-the-ad-fs-configuration-to-wid"></a>AD FS 구성을 WID 복원

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "WID"
``` 

### <a name="restore-the-ad-fs-configuration-to-sql"></a>AD FS 구성을 SQL 복원

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "Data Source=TESTMACHINE\SQLEXPRESS; Integrated Security=True"
```

### <a name="restores-the-ad-fs-configuration-with-the-specified-gmsa"></a>지정 된 GMSA와 AD FS 구성을 복원합니다

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -GroupServiceAccountIdentifier "mangupd1\adfsgmsa$"
```
### <a name="restore-the-ad-fs-configuration-with-the-specified-service-account-creds"></a>지정 된 서비스 계정 자격 증명으로 AD FS 구성을 복원합니다

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -ServiceAccountCredential $cred
```

## <a name="encryption-information"></a>암호화 정보
클라우드에 밀거나 파일 시스템에 저장 하기 전에 모든 백업 데이터가 암호화 됩니다.  

백업의 일부로 생성 되는 문서 aes-256 사용 암호화 됩니다. 이 도구에 전달 암호 Rfc2898DeriveBytes 클래스 사용 하 여 새 암호를 생성 하는으로 사용 됩니다. 

RngCryptoServiceProvider는 AES 및 Rfc2898DeriveBytes 클래스 사용 되는 소금 생성 하는 데 사용 됩니다. 

## <a name="log-files"></a>로그 파일
백업 및 복원을 수행 때마다 로그 파일이 만들어집니다. 이러한 다음 위치에서 찾을 수 있습니다.

- **%localappdata%\ADFSRapidRecreationTool**

>[!NOTE]
> 추가 인증 공급자 개요 포함 된 PostRestore_Instructions 파일을 만들 수 있습니다 복원을 수행, 특성 저장 하 고 로컬 클레임 공급자 신뢰 하는 ADFS 서비스를 시작 하기 전에 수동으로 설치할 수 때 합니다.
