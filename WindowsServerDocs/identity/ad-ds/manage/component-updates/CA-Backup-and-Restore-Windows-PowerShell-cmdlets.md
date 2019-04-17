---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: "캘리포니아 백업 및 복원 Windows PowerShell cmdlet"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: aba86ed080cc0b4043805531f0a2138b1b1d3cf8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>캘리포니아 백업 및 복원 Windows PowerShell cmdlet

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
>
**작성자**: Windows 그룹과 조자룡 Turner, 선임 지원 엔지니어로  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 담당자가 작성 하며 경험이 관리자와 technet 항목 일반적으로 제공 하는 것 보다에 대 한 보다 긴밀 기술 설명은 기능 및 Windows Server 2012 r 2에 대 한 해결 방법을 찾는 누가 시스템 개발자를 위한 것입니다. 그러나 받지 않았습니다 동일한 편집 가공 일부 언어 일반적으로 technet 찾을 수 보다 세련 된 적게 보일 수 있도록 합니다.  
  
## <a name="overview"></a>개요  
창 Server 2012에서 ADCSAdministration Windows PowerShell 모듈 도입 되었습니다.  백업 및 복원은 캐나다의 지원 하기 위해 창 Server 2012 r 2에이 모듈에 두 가지 새로운 cmdlet 추가 되었습니다.  
  
-   백업 CARoleService  
  
-   복원 CARoleService  
  
## <a name="backup-caroleservice"></a>백업 CARoleService  
**테이블 SEQ 테이블 \\\ * 아랍어 17: 백업 및 복원 Windows PowerShell Cmdlet**  
  
**ADCSAdministration Cmdlet: 백업 CARoleService**  
  
|인수- **굵게** 인수가 필요|설명|  
|------------------------------------------------|---------------|  
|**경로**|-문자열-백업을 저장할 위치를<br />-이 경우에 매개 이름 없습니다<br />-위치 매개<br /><br />**예:**<br /><br />백업-CARoleService.-경로 c:\adcsbackup1<br /><br />백업 CARoleService c:\adcsbackup2|  
|-KeyOnly|-데이터베이스를 않고도 인증서를 백업 합니다.<br /><br />**예:**<br /><br />백업 CARoleService c:\adcsbackup3 KeyOnly|  
|암호|-캐나다 인증서와 개인 키를 보호 하기 위해 암호를 지정 합니다.<br />-여야 보안 문자열<br />-잘못-DatabaseOnly 매개<br /><br />예:<br /><br />백업 CARoleService c:\adcsbackup4-암호 (읽기 호스트-프롬프트 "암호:"-AsSecureString)<br /><br />백업 CARoleService c:\adcsbackup5-암호 (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText-포스)|  
|-DatabaseOnly|백업에서 선택 된 인증서를 않고도 데이터베이스<br /><br />백업 CARoleService c:\adcsbackup6 DatabaseOnly|  
|힘|1. 수 있도록 지정 된 위치에서 preexists 백업을 덮어쓰지-경로 매개에서<br /><br />백업 CARoleService c:\adcsbackup1-힘|  
|증분|-증분 백업을 수행 합니다.<br /><br />백업 CARoleService c:\adcsbackup7-증분|  
|-KeepLog|1. 로그 파일을 유지할지 명령을 하도록 합니다. 로그 파일을 제외 하 고 증분 시나리오에서 기본적으로 잘립니다 스위치를 지정 하지 않은 경우<br /><br />백업 CARoleService c:\adcsbackup7 KeepLog|  
  
### <a name="-password-secure-string"></a>암호<Secure String>  
하는 경우 암호-매개 변수를 사용, 제공된 암호 보안 문자열 여야 합니다.  사용 하 여는 **읽기 호스트** cmdlet 보안 암호 항목에 대 한 대화형 프롬프트를 실행 하거나 사용 하는 **ConvertTo SecureString** cmdlet은 암호 인라인 지정할 수 있습니다.  
  
다음은 검토  
  
**읽기 호스트를 사용 하 여 암호 매개에 대 한 보안 문자열을 지정**  
  
```powershell  
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)  
```  
  
**ConvertTo SecureString를 사용 하 여 암호 매개에 대 한 보안 문자열을 지정**  
  
```powershell  
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)  
```  
  
## <a name="restore-caroleservice"></a>복원 CARoleService  
**ADCSAdministration Cmdlet: 복원 CARoleService**  
  
|인수- **굵게** 인수가 필요|설명|  
|------------------------------------------------|---------------|  
|**경로**|-문자열-위치에서 백업을 복원 하려면<br />-이 경우에 매개 이름 없습니다<br />-위치 매개<br /><br />**예:**<br /><br />복원-CARoleService.-경로 c:\adcsbackup1-힘<br /><br />복원 CARoleService c:\adcsbackup2-힘|  
|-KeyOnly|-데이터베이스를 않고도 인증서 복원<br />-사람은-KeyOnly 옵션으로 백업 하는 경우<br /><br />**예:**<br /><br />복원 CARoleService c:\adcsbackup3 KeyOnly-힘|  
|암호|-캐나다 인증서와 개인 키의 암호를 지정합니다.<br />-여야 보안 문자열<br /><br />**예:**<br /><br />복원 CARoleService c:\adcsbackup4-암호 (읽기 호스트-프롬프트 "암호:"-AsSecureString)-힘<br /><br />복원 CARoleService c:\adcsbackup5-암호 (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText-포스)-힘|  
|-DatabaseOnly|-데이터베이스는 선택 된 인증서를 않고도 복원<br /><br />복원 CARoleService c:\adcsbackup6 DatabaseOnly|  
|힘|-수 있습니다. 기존 키 덮어쓰기를<br />-선택적 매개 이지만 할 필요는 위치, 복원 하는 경우<br /><br />복원 CARoleService c:\adcsbackup1-힘|  
  
### <a name="issues"></a>문제  
백업 CARoleService 사용 하는 동안 ConvertTo SecureString 기능이 실패 하는 경우 암호 비 보호 된 백업이 수행-암호 매개 변수를 합니다.  
  
![캘리포니아 백업 및 복원](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)  
  
**테이블 SEQ 테이블 \\\ * 아랍어 18: 일반적인 오류**  
  
|알림|오류|메모|  
|----------|---------|-----------|  
|**복원 CARoleService C:\ADCSBackup**|복원 CARoleService: 프로세스에 액세스할 수 없는 파일 다른 프로세스에서 사용 되 고 있으므로 합니다. (HRESULT에서:<br /><br />0x80070020)|복원 CARoleService cmdlet 실행 하기 전에 Active Directory 인증서 서비스 서비스 중지|  
|**복원 CARoleService C:\ADCSBackup**|복원 CARoleService: 디렉터리가 비어있지 않습니다. (HRESULT에서: 0x80070091)|사용 하 여-힘 매개 변수를 덮어씁니다 기존 키|  
|**백업 CARoleService C:\ADCSBackup-암호 (읽기 호스트-프롬프트 "암호:"-AsSecureString)-DatabaseOnly**|백업 CARoleService: 매개 설정 해결할 수 없는 사용 하 여 매개 라는 합니다.|매개-암호 개인 키를 보호 하 고 유효 하지 따라서를 백업 하지는 경우에 암호를 사용|  
|**복원 CARoleService C:\ADCSBack15-암호 (읽기 호스트-프롬프트 "암호:"-AsSecureString)-DatabaseOnly**|복원 CARoleService: 매개 설정 해결할 수 없는 사용 하 여 매개 라는 합니다.|매개-암호 개인 키를 보호 하 고 유효 하지 따라서 복원 하지 않는 경우에 암호를 사용 합니다.|  
|**복원 CARoleService C:\ADCSBack14-암호 (읽기 호스트-프롬프트 "암호:"-AsSecureString)**|복원 CARoleService: 시스템 지정 된 파일을 찾을 수 없습니다. (HRESULT에서: 0x80070002)|다른 경로 유효한 데이터베이스 백업을 포함 되지 않습니다.  아마도 경로 유효 하지 않거나-KeysOnly 옵션으로 백업 하나요?|  
  
## <a name="additional-resources"></a>추가 리소스  
[Active Directory 인증서 서비스 마이그레이션 가이드](https://technet.microsoft.com/library/ee126170(v=ws.10).aspx)  
  
[캘리포니아 데이터베이스와 개인 키를 백업](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_BackUpDB)  
  
[캘리포니아 데이터베이스와 구성 대상 서버에서 복원](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_RestoreCA)  
  
## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>Windows PowerShell를 사용 하 여 랩에서 캘리포니아 백업 시도해 보기:  
  
1.  이과 명령을 사용 하 여 캘리포니아 데이터베이스와 개인 키와 암호로 보호를 백업 합니다.  
  
2.  이 이번에는 캐나다의 복원을에 보관 합니다.  
  


