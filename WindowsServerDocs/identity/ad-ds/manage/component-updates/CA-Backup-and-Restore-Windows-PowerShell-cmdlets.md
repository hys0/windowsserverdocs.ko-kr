---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: CA 백업 및 복원 Windows PowerShell cmdlet
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a4bbeeedfb40e789a799103f9a29a848a2b32324
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877354"
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>CA 백업 및 복원 Windows PowerShell cmdlet

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
>
**작성자**: Windows 그룹과 Justin Turner, 수석 지원 에스컬레이션 엔지니어  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
## <a name="overview"></a>개요  
ADCSAdministration Windows PowerShell 모듈은 Window Server 2012에서 도입 되었습니다.  두 개의 새로운 cmdlet은 백업 및 복원 ca를 지원 하기 위해 Window Server 2012 r 2에서이 모듈에 추가 되었습니다.  
  
-   Backup-CARoleService  
  
-   Restore-CARoleService  
  
## <a name="backup-caroleservice"></a>Backup-CARoleService  
**테이블 SEQ 테이블 \\ \* 아랍어 17: 백업 및 복원 Windows PowerShell Cmdlet**  
  
**ADCSAdministration Cmdlet: Backup-CARoleService**  
  
|인수- **굵게** 인수가 필요|설명|  
|------------------------------------------------|---------------|  
|**-Path**|-문자열-백업을 저장할 위치<br />-이 유일한 매개 변수 이름을 지정 하지 않는<br />-위치 매개 변수<br /><br />**예:**<br /><br />백업-CARoleService.-경로 c:\adcsbackup1<br /><br />백업 CARoleService c:\adcsbackup2|  
|-KeyOnly|--데이터베이스 없이 CA 인증서를 백업 하는 중<br /><br />**예:**<br /><br />백업 CARoleService c:\adcsbackup3 KeyOnly|  
|-암호|- CA 인증서와 프라이빗 키를 보호하기 위한 암호를 지정합니다.<br />-보안 문자열 이어야 합니다.<br />-잘못 됨-DatabaseOnly 매개 변수<br /><br />예:<br /><br />백업 CARoleService c:\adcsbackup4-암호 (Read-host-프롬프트 "암호:"-AsSecureString)<br /><br />백업 CARoleService c:\adcsbackup5-암호 (Convertto-securestring "Pa55w0rd!" -AsPlainText-Force)|  
|-DatabaseOnly|-CA 인증서가 없는 데이터베이스를 백업 합니다.<br /><br />백업 CARoleService c:\adcsbackup6 DatabaseOnly|  
|-Force|1.  지정 된 위치에 이미 백업을 덮어쓸 수 있습니다-Path 매개 변수에서<br /><br />백업 CARoleService c:\adcsbackup1-Force|  
|-증분|-증분 백업을 수행 합니다.<br /><br />백업 CARoleService c:\adcsbackup7-증분|  
|-KeepLog|1.  로그 파일을 보관 하는 명령에 지시 합니다. 증분 시나리오에서를 제외 하 고 기본적으로 로그 파일 잘림 스위치가 지정 되지 않은 경우<br /><br />백업 CARoleService c:\adcsbackup7 KeepLog|  
  
### <a name="-password-secure-string"></a>-Password <Secure String>  
경우-암호 매개 변수는 사용, 제공 된 암호는 보안 문자열 이어야 합니다.  사용 하 여는 **Read-host** 보안 암호 항목에 대 한 대화형 프롬프트를 시작 하거나 사용 하 여 cmdlet는 **Convertto-securestring** cmdlet은 암호 인라인 지정을 사용 합니다.  
  
다음 예제를 검토 합니다.  
  
**읽기-호스트를 사용 하 여 암호 매개 변수에 대 한 보안 문자열 지정**  
  
```powershell  
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)  
```  
  
**Convertto-securestring를 사용 하 여 암호 매개 변수에 대 한 보안 문자열 지정**  
  
```powershell  
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)  
```  
  
## <a name="restore-caroleservice"></a>Restore-CARoleService  
**ADCSAdministration Cmdlet: Restore-CARoleService**  
  
|인수- **굵게** 인수가 필요|설명|  
|------------------------------------------------|---------------|  
|**-Path**|-문자열-에서 백업을 복원 하는 위치<br />-이 유일한 매개 변수 이름을 지정 하지 않는<br />-위치 매개 변수<br /><br />**예:**<br /><br />복원-CARoleService.-경로 c:\adcsbackup1-Force<br /><br />복원 CARoleService c:\adcsbackup2-Force|  
|-KeyOnly|--데이터베이스 없이 CA 인증서를 복원 하는 중<br />-사람은-KeyOnly 옵션으로 백업이 수행 된 경우<br /><br />**예:**<br /><br />복원 CARoleService c:\adcsbackup3 KeyOnly-Force|  
|-암호|- CA 인증서와 프라이빗 키의 암호를 지정합니다.<br />-보안 문자열 이어야 합니다.<br /><br />**예:**<br /><br />복원 CARoleService c:\adcsbackup4-암호 (읽기-호스트-프롬프트 "암호:"-AsSecureString)-Force<br /><br />복원 CARoleService c:\adcsbackup5-암호 (Convertto-securestring "Pa55w0rd!" -AsPlainText-Force)-Force|  
|-DatabaseOnly|-CA 인증서가 없는 데이터베이스를 복원 합니다.<br /><br />복원 CARoleService c:\adcsbackup6 DatabaseOnly|  
|-Force|-기존 키를 덮어쓸 수 있습니다.<br />-선택적 매개 변수 이지만 전체를 복원할 때 필요한 것<br /><br />복원 CARoleService c:\adcsbackup1-Force|  
  
### <a name="issues"></a>문제  
Convertto-securestring 함수가 백업 CARoleService를 사용 하는 동안 실패 한 경우 상태-암호 보호 된 백업-암호 매개 변수를 사용 합니다.  
  
![CA 백업 및 복원](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)  
  
**테이블 SEQ 테이블 \\ \* 아랍어 18: 일반적인 오류**  
  
|작업|Error|설명|  
|----------|---------|-----------|  
|**Restore-CARoleService C:\ADCSBackup**|Restore-CARoleService : 프로세스가 다른 프로세스에서 사용 되는 파일을 액세스할 수 없습니다. (예외가 발생한 HRESULT:<br /><br />0x80070020)|복원 CARoleService cmdlet을 실행 하기 전에 Active Directory 인증서 서비스 서비스 중지|  
|**Restore-CARoleService C:\ADCSBackup**|Restore-CARoleService : 디렉터리가 비어 있지 않습니다. (예외가 발생한 HRESULT: 0x80070091)|사용 하 여 기존 키를 덮어쓰려면-Force 매개 변수|  
|**Backup-CARoleService C:\ADCSBackup -Password (Read-Host -Prompt "Password:" -AsSecureString) -DatabaseOnly**|백업-CARoleService: 매개 변수 집합 확인할 수 없습니다 지정 된 명명 된 매개 변수.|-암호 매개 변수는 프라이빗 키를 암호로 보호하는 데만 사용되므로 백업하지 않을 때는 유효하지 않습니다.|  
|**Restore-CARoleService C:\ADCSBack15 -Password (Read-Host -Prompt "Password:" -AsSecureString) -DatabaseOnly**|Restore-CARoleService : 매개 변수 집합 확인할 수 없습니다 지정 된 명명 된 매개 변수.|-암호 매개 변수는 프라이빗 키를 암호로 보호하는 데만 사용되므로 복원하지 않을 경우 유효하지 않습니다.|  
|**Restore-CARoleService C:\ADCSBack14 -Password (Read-Host -Prompt "Password:" -AsSecureString)**|Restore-CARoleService : 시스템에서 지정한 파일을 찾을 수 없습니다. (예외가 발생한 HRESULT: 0x80070002)|지정 된 경로 유효한 데이터베이스 백업을 포함 되지 않습니다.  아마도 경로가 잘못 되었거나-KeysOnly 옵션으로 백업한?|  
  
## <a name="additional-resources"></a>추가 리소스  
[Active Directory 인증서 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/ee126170(v=ws.10).aspx)  
  
[CA 데이터베이스 및 개인 키 백업](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_BackUpDB)  
  
[대상 서버에서 CA 데이터베이스 및 구성 복원](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_RestoreCA)  
  
## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>다음과 같이 해보십시오. Windows PowerShell을 사용 하 여 랩에서 CA 백업  
  
1.  이 단원의 명령을 사용하여 암호로 보호된 CA 데이터베이스 및 프라이빗 키를 백업합니다.  
  
2.  이 이번에는 CA의 복원에서 저장 합니다.  
  


