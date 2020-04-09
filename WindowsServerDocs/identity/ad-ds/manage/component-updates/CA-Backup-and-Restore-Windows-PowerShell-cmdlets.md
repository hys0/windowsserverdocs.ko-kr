---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: CA 백업 및 복원 Windows PowerShell cmdlet
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d1dd406780dc61e1ce52d423ca6148d2a9dd2c3d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823086"
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>CA 백업 및 복원 Windows PowerShell cmdlet

> 적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> **작성자**: Justin Turner, Windows 그룹이 포함 된 선임 지원 에스컬레이션 엔지니어  
> 
> [!NOTE]
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
## <a name="overview"></a>개요  
ADCSAdministration Windows PowerShell 모듈은 Window Server 2012에서 도입 되었습니다.  두 개의 새로운 cmdlet은 백업 및 복원 ca를 지원 하기 위해 Window Server 2012 r 2에서이 모듈에 추가 되었습니다.  
  
-   Backup-CARoleService  
  
-   Restore-CARoleService  
  
## <a name="backup-caroleservice"></a>Backup-CARoleService  
**표 SEQ 테이블 \\\* 아랍어 17: Windows PowerShell Cmdlet 백업 및 복원**  
  
**ADCSAdministration Cmdlet: 백업-CARoleService**  
  
|인수- **굵게** 인수가 필요|설명|  
|------------------------------------------------|---------------|  
|**-경로**|-문자열-백업을 저장할 위치<br />-이 유일한 매개 변수 이름을 지정 하지 않는<br />-위치 매개 변수<p>**예제:**<p>백업-CARoleService.-경로 c:\adcsbackup1<p>백업 CARoleService c:\adcsbackup2|  
|-KeyOnly|--데이터베이스 없이 CA 인증서를 백업 하는 중<p>**예제:**<p>백업 CARoleService c:\adcsbackup3 KeyOnly|  
|-Password|- CA 인증서와 프라이빗 키를 보호하기 위한 암호를 지정합니다.<br />-보안 문자열 이어야 합니다.<br />-잘못 됨-DatabaseOnly 매개 변수<p>예:<p>백업 CARoleService c:\adcsbackup4-암호 (Read-host-프롬프트 "암호:"-AsSecureString)<p>백업 CARoleService c:\adcsbackup5-암호 (Convertto-securestring "Pa55w0rd!" -AsPlainText-Force)|  
|-DatabaseOnly|-CA 인증서가 없는 데이터베이스를 백업 합니다.<p>백업 CARoleService c:\adcsbackup6 DatabaseOnly|  
|-Force|1.-Path 매개 변수에 지정 된 위치에 사전 존재 하는 백업을 덮어쓸 수 있습니다.<p>백업 CARoleService c:\adcsbackup1-Force|  
|-증분|-증분 백업을 수행 합니다.<p>백업 CARoleService c:\adcsbackup7-증분|  
|-KeepLog|1. 로그 파일을 보관 하도록 명령을 지시 합니다. 증분 시나리오에서를 제외 하 고 기본적으로 로그 파일 잘림 스위치가 지정 되지 않은 경우<p>백업 CARoleService c:\adcsbackup7 KeepLog|  
  
### <a name="-password-secure-string"></a>-Password <Secure String>  
경우-암호 매개 변수는 사용, 제공 된 암호는 보안 문자열 이어야 합니다.  사용 하 여는 **Read-host** 보안 암호 항목에 대 한 대화형 프롬프트를 시작 하거나 사용 하 여 cmdlet는 **Convertto-securestring** cmdlet은 암호 인라인 지정을 사용 합니다.  
  
다음 예제를 검토 합니다.  
  
**읽기-호스트를 사용 하 여 암호 매개 변수에 대 한 보안 문자열 지정**  
  
```powershell  
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)  
```  
  
**Convertto-html를 사용 하 여 암호 매개 변수에 대 한 보안 문자열 지정**  
  
```powershell  
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)  
```  
  
## <a name="restore-caroleservice"></a>Restore-CARoleService  
**ADCSAdministration Cmdlet: 복원-CARoleService**  
  
|인수- **굵게** 인수가 필요|설명|  
|------------------------------------------------|---------------|  
|**-경로**|-문자열-에서 백업을 복원 하는 위치<br />-이 유일한 매개 변수 이름을 지정 하지 않는<br />-위치 매개 변수<p>**예제:**<p>복원-CARoleService.-경로 c:\adcsbackup1-Force<p>복원 CARoleService c:\adcsbackup2-Force|  
|-KeyOnly|--데이터베이스 없이 CA 인증서를 복원 하는 중<br />-사람은-KeyOnly 옵션으로 백업이 수행 된 경우<p>**예제:**<p>복원 CARoleService c:\adcsbackup3 KeyOnly-Force|  
|-Password|- CA 인증서와 프라이빗 키의 암호를 지정합니다.<br />-보안 문자열 이어야 합니다.<p>**예제:**<p>복원 CARoleService c:\adcsbackup4-암호 (읽기-호스트-프롬프트 "암호:"-AsSecureString)-Force<p>복원 CARoleService c:\adcsbackup5-암호 (Convertto-securestring "Pa55w0rd!" -AsPlainText-Force)-Force|  
|-DatabaseOnly|-CA 인증서가 없는 데이터베이스를 복원 합니다.<p>복원 CARoleService c:\adcsbackup6 DatabaseOnly|  
|-Force|-기존 키를 덮어쓸 수 있습니다.<br />-선택적 매개 변수 이지만 전체를 복원할 때 필요한 것<p>복원 CARoleService c:\adcsbackup1-Force|  
  
### <a name="issues"></a>문제  
Convertto-securestring 함수가 백업 CARoleService를 사용 하는 동안 실패 한 경우 상태-암호 보호 된 백업-암호 매개 변수를 사용 합니다.  
  
![CA 백업 및 복원](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)  
  
**표 SEQ 테이블 \\\* 아랍어 18: 일반적인 오류**  
  
|작업|오류|설명|  
|----------|---------|-----------|  
|**복원-CARoleService C:\ADCSBackup**|복원-CARoleService: 프로세스가 액세스할 수 없습니다 파일이 다른 프로세스에서 사용 되 고. (HRESULT에서 예외가 발생했습니다:<p>0x80070020)|복원 CARoleService cmdlet을 실행 하기 전에 Active Directory 인증서 서비스 서비스 중지|  
|**복원-CARoleService C:\ADCSBackup**|복원-CARoleService: 디렉터리가 비어 있지 않습니다. (HRESULT의 예외: 0x80070091)|사용 하 여 기존 키를 덮어쓰려면-Force 매개 변수|  
|**백업-CARoleService C:\ADCSBackup-Password (읽기-호스트-프롬프트 "Password:"-AsSecureString)-DatabaseOnly**|백업-CARoleService: 매개 변수 집합 확인할 수 없으면 지정 된 명명 된 매개 변수입니다.|-암호 매개 변수는 프라이빗 키를 암호로 보호하는 데만 사용되므로 백업하지 않을 때는 유효하지 않습니다.|  
|**복원-CARoleService C:\ADCSBack15-Password (읽기-호스트-프롬프트 "Password:"-AsSecureString)-DatabaseOnly**|복원-CARoleService: 매개 변수 집합 확인할 수 없으면 지정 된 명명 된 매개 변수입니다.|-암호 매개 변수는 프라이빗 키를 암호로 보호하는 데만 사용되므로 복원하지 않을 경우 유효하지 않습니다.|  
|**복원-CARoleService C:\ADCSBack14-Password (읽기-호스트-프롬프트 "Password:"-AsSecureString)**|복원-CARoleService: 시스템이 지정 된 파일을 찾을 수 없습니다. (HRESULT의 예외: 0x80070002)|지정 된 경로 유효한 데이터베이스 백업을 포함 되지 않습니다.  아마도 경로가 잘못 되었거나-KeysOnly 옵션으로 백업한?|  
  
## <a name="additional-resources"></a>추가 리소스  
[Active Directory 인증서 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/ee126170(v=ws.10).aspx)  
  
[CA 데이터베이스 및 프라이빗 키 백업](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_BackUpDB)  
  
[대상 서버에서 CA 데이터베이스 및 구성 복원](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_RestoreCA)  
  
## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 랩에서 CA 백업 다음과 같이 해보십시오.  
  
1.  이 단원의 명령을 사용하여 암호로 보호된 CA 데이터베이스 및 프라이빗 키를 백업합니다.  
  
2.  이 이번에는 CA의 복원에서 저장 합니다.  
  


