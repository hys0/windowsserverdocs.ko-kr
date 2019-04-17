---
title: "마이그레이션해야 독립 실행형 ADFS federation 서버 또는 단일 노드 ADFS 농장"
description: "Windows Server 2012 독립 실행형 또는 단일 노드 광고 FS 2.0 서버 마이그레이션하에 정보를 제공 합니다."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 10371349fe19be92fb997c9c28f19def0ecad7e9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>마이그레이션해야 독립 실행형 ADFS federation 서버 또는 단일 노드 ADFS 농장  
이 문서는 ADFS 2.0 독립 실행형 서버 Windows Server 2012에 자세히 설명 합니다.

## <a name="migrate-a-stand-alone-ad-fs-20-server"></a>마이그레이션해야 독립 실행형 광고 FS 2.0 서버

다음 절차 ADFS 2.0 마이그레이션을를 사용 하 여 Windows Server 2012 서버 합니다.
  
1.  검토 하 고 절차를 수행 [마이그레이션해야 독립 실행형 ADFS federation 서버 또는 단일 노드 ADFS 농장 준비](prepare-to-migrate-a-stand-alone-ad-fs-federation-server.md)합니다.  
  
2.  Windows Server 2012를 Windows Server 2008 또는 Windows Server 2008 R2에서 서버 운영 체제의 제자리에 업그레이드를 수행 합니다. 자세한 내용은 참조 [Windows Server 2012를 설치](https://technet.microsoft.com/library/jj134246.aspx)합니다.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드 결과이 서버의 ADFS 구성 삭제 되 고 ADFS 2.0 서버 역할은 제거 됩니다. Windows Server 2012 ADFS 서버 역할 대신 설치 되어 있지만 구성 되어 있지 않습니다. 수동으로 만들 원래 ADFS 구성 하 고 federation 서버 마이그레이션을 완료 하 나머지 ADFS 설정으로 복원 해야 합니다.  
  
3.  원래 ADFS 구성을 만듭니다. 다음 방법 중 하나를 사용 하 여 원래 ADFS 구성을 만들 수 있습니다.  
  
-   사용 하는 **광고 FS Federation 서버 구성 마법사** 새 federation 서버를 만듭니다. 자세한 내용은 참조 [Federation 서버 농장의 첫 번째 Federation 서버를 만들](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)합니다.  
  
마법사를 통해 이동할 때 ADFS federation 서버 다음과 같이 마이그레이션 준비 하는 동안 수집 된 정보 사용.  
  
 |**Federation 서버 구성 마법사 입력된 옵션**|**다음 값을 사용 하 여**| 
|-----|-----| 
|**SSL 인증서** 에 **해당 Federation 서비스 이름을 지정** 페이지|제목 이름과 지문 ADFS federation 서버 마이그레이션에 대 한 준비 하는 동안 기록 SSL 인증서를 선택 합니다.|  
|**서비스 계정을** 및 **암호** 에 **서비스 계정을 지정** 페이지|ADFS federation 서버 마이그레이션에 대 한 준비 하는 동안 기록한 서비스 계정 정보를 입력 합니다. **참고:** 네트워크 서비스 서비스 계정으로 자동으로 사용 마법사의 두 번째 페이지에서 독립형 federation 서버를 선택 합니다.|  
  
> [!IMPORTANT] 
> Windows 내부 데이터베이스 (WID)를 사용 하 여 독립 실행형 federation 서버 또는 단일 노드 ADFS 농장 ADFS 구성 데이터베이스에 저장 하는 경우에이 방법을 사용할 수 있습니다.  
>
>  SQL Server ADFS 구성 데이터베이스 단일 노드 ADFS 농장 저장 하도록를 사용 하는 경우 Windows PowerShell 해당 federation 서버에 원래 ADFS 구성을 만드는 데 사용 해야 합니다.  
  
-   Windows PowerShell 사용  
  
> [!IMPORTANT]
>  독립 실행형 federation 서버 또는 단일 노드 ADFS 농장 ADFS 구성 데이터베이스 저장할 SQL Server를 사용 하는 경우 Windows PowerShell를 사용 해야 합니다.  
  
다음은 Windows PowerShell 단일 노드 SQL Server 발전소의 federation 서버에 원래 ADFS 구성을 만드는 데 사용 하는 방법의 예입니다.  다음 명령을 실행를 Windows PowerShell 모듈 열고: `$fscredential = Get-Credential`합니다. 이름 및 SQL server 팜 마이그레이션에 대 한 준비 하는 동안 기록 서비스 계정의 암호를 입력 합니다. 다음 명령을 실행: `C:\PS> Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"` 어디 `Data Source` 데이터 소스 값 정책 스토어 연결 문자열 값 다음 파일에에서: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`합니다.  
  
4.  나머지 ADFS 서비스 설정으로 복원 하 고 관계 신뢰 합니다. 이 유예 기간이 내보낸 파일과 ADFS 마이그레이션에 대 한 준비 하는 동안 수집 값을 사용할 수 수동 단계입니다. 자세한 내용은 남은 AD FS 팜 구성 복원 참조 합니다.  
  
> [!NOTE]
>  이 단계는만 독립 실행형 federation 서버 또는 단일 노드 WID 농장 마이그레이션하는 필요 합니다.  Federation 서버를 SQL Server 데이터베이스 구성 저장소를 사용 하는 경우 서비스 설정과 관계 신뢰 데이터베이스에 유지 됩니다.  
  
5.  ADFS 웹 페이지를 업데이트 합니다. 수동 단계입니다. 마이그레이션에 대 한 준비 하는 동안 사용자 정의 ADFS 웹 페이지를 백업 백업 데이터를 사용 하 여 기본 ADFS 웹 페이지에서 기본적으로 만들어진 덮어씁니다는 **%systemdrive%\inetpub\adfs\ls** Windows Server 2012에서 ADFS 구성 결과 디렉터리 합니다.  
  
6.  사용자 지정 된 특성 스토어 등 모든 나머지 ADFS 사용자 지정 복원 합니다.  
  
## <a name="restoring-the-remaining-ad-fs-farm-configuration"></a>남은 AD FS 농장 구성 요소가 복원  
  
-   다음과 같이 단일 노드 WID 농장 또는 독립 실행형 federation 서비스에 다음과 같은 ADFS 서비스 설정이 복원 다음과 같습니다.  
  
    -   ADFS management console에서 선택 **서비스** 클릭 **Federation 서비스 편집... **. 각각의 마이그레이션에 대 한 준비 하는 동안 properties.txt 파일로 내보낸 값에 대 한 값을 확인 하 여 federation 서비스 설정을 확인 합니다.  
  
    
|**Get ADFSProperties 들이 보고 federation 서비스 속성 이름**|**AD FS Management console에서 federation 서비스 속성 이름**|  
|-----|-----|
|표시 이름|Federation 서비스 표시 이름|  
|호스트|Federation 서비스 이름|  
|식별자|Federation 서비스 id|  
  
-   ADFS management console에서 선택 **인증서**합니다. 각 마이그레이션에 대 한 준비 하는 동안 certificates.txt 파일로 내보낸 값을 확인 하 여 서비스 통신, 토큰 해독 및 토큰 서명 인증서를 확인 합니다.  
  
토큰 해독 또는 토큰 서명 인증서를 기본 자체 서명된 인증서의 외부 인증서를 변경 하려면 먼저 기본적으로 활성화 되어 있는 인증서 자동 롤오버 기능을 해제 해야 합니다.  이렇게 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다: `PSH: Set-ADFSProperties –AutoCertificateRollover $false`합니다.  
  
-   AD FS Management console에서 **끝점**합니다. 활성화 된 ADFS 끝점 ADFS 마이그레이션에 대 한 준비 하는 동안 내보낸 파일에는 활성화 된 ADFS 끝점 목록에 있는지 확인 합니다.  
  
-   AD FS Management console에서 **클레임 설명을**합니다. ADFS 마이그레이션에 대 한 준비 하는 중 파일 내보낸 클레임 설명 사람 목록 ADFS 클레임 설명의 목록을 확인 합니다. 사용자 파일에 포함 되어 있지만 adfs에서 기본 목록에 포함 되지 않은 모든 사용자 지정 클레임 설명을 추가 합니다.  클레임 식별자 management console에서 파일에 ClaimType 매핑됩니다 note 합니다.  에 대 한 자세한 내용은 클레임 설명을 추가, [주장 설명을 추가](../operations/add-a-claim-description.md)합니다. 자세한 내용은 마이그레이션 AD 준비 단계 1-내보내기 서비스 "설정" 섹션 참조 FS 2.0 Federation 서버 합니다.  
  
-   AD FS Management console에서 **클레임 공급자 신뢰**합니다. 사용 하 여 수동으로 각 청구 공급자 신뢰 다시 만들어야는 **클레임 공급자 추가 보안 마법사**합니다.  내보낸는 ADFS 마이그레이션에 대 한 준비 하는 동안 기록 클레임 제공자 신뢰 목록을 사용 합니다. 기본 구성 Adfs의 일부인 "Active Directory" 클레임 공급자 신뢰 이기 때문에 파일에서 "광고 기관" 식별자와 클레임 공급자 신뢰를 무시 해도 됩니다.  그러나 이전 마이그레이션 Active Directory 신뢰를 추가 하는 모든 사용자 지정 클레임 규칙 확인 합니다. 만드는 방법에 대 한 자세한 내용은 주장 제공자 신뢰를에 대 한 참고 [클레임 공급자 신뢰를 사용 하 여 Federation 메타 데이터를 만들](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-using-federation-metadata) 또는 [한 청구 공급자 신뢰 수동으로 만들](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-manually)합니다.  
  
-   AD FS Management console에서 **파티 신뢰 의존 선택**합니다. 사용 하 여 수동으로 각 의존 파티 신뢰 다시 만들어야는 **추가 의존 파티 신뢰 마법사**합니다. 내보내고 ADFS 마이그레이션에 대 한 준비 하는 동안 녹화를 신뢰 파티 신뢰 목록을 사용 합니다. 신뢰 파티 신뢰를 만드는 방법에 대 한 자세한 내용은 참조 [의존 파티 신뢰를 사용 하 여 Federation 메타 데이터를 만들](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata) 또는 [필요로 하 파티 신뢰 수동으로 만들](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)합니다. 

## <a name="next-steps"></a>다음 단계
 [광고 FS 2.0 Federation 서버 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션을 준비합니다](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [광고 FS 2.0 Federation Server를 마이그레이션해야](migrate-the-ad-fs-fed-server.md)   
 [광고 FS 2.0 Federation 서버 프록시 마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [광고 FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)




-   
-    