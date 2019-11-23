---
title: 독립 실행형 AD FS 페더레이션 서버 또는 단일 노드 AD FS 팜 마이그레이션
description: 독립 실행형 또는 단일 노드 AD FS 2.0 서버를 Windows Server 2012로 마이그레이션하는 방법에 대 한 정보를 제공 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b8029d67a9f21e5189322692b8f1316306542c96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359376"
---
# <a name="migrate-a-stand-alone-ad-fs-federation-server-or-a-single-node-ad-fs-farm"></a>독립 실행형 AD FS 페더레이션 서버 또는 단일 노드 AD FS 팜 마이그레이션  
이 문서에서는 AD FS 2.0 독립 실행형 서버를 Windows Server 2012로 마이그레이션하는 방법에 대 한 자세한 정보를 제공 합니다.

## <a name="migrate-a-stand-alone-ad-fs-20-server"></a>독립형 AD FS 2.0 서버 마이그레이션

AD FS 2.0 서버를 Windows Server 2012로 마이그레이션하려면 다음 절차를 따르십시오.
  
1.  [독립 실행형 AD FS 페더레이션 서버 또는 단일 노드 AD FS 팜 마이그레이션 준비](prepare-to-migrate-a-stand-alone-ad-fs-federation-server.md)의 절차를 검토 하 고 수행 합니다.  
  
2.  서버 운영 체제를 Windows Server 2008 R2 또는 Windows Server 2008에서 Windows Server 2012로 전체 업그레이드를 수행 합니다. 자세한 내용은 [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx)를 참조하세요.  
  
> [!IMPORTANT]
>  운영 체제 업그레이드로 인해 이 서버의 AD FS 구성이 손실되고 AD FS 2.0 서버 역할이 제거됩니다. Windows Server 2012 AD FS 서버 역할이 대신 설치 되지만 구성 되지 않습니다. 수동으로 원래 AD FS 구성을 만들고 나머지 AD FS 설정을 복원하여 페더레이션 서버 마이그레이션을 완료해야 합니다.  
  
3. 원래 AD FS 구성을 만듭니다. 다음 방법 중 하나를 사용하여 원래 AD FS 구성을 만들 수 있습니다.  
  
-   **AD FS 페더레이션 서버 구성 마법사** 를 사용하여 새 페더레이션 서버를 만듭니다. 자세한 내용은 [페더레이션 서버 팜의 첫 번째 페더레이션 서버 만들기](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)를 참조하세요.  
  
다음과 같이 마법사를 진행하면서 AD FS 페더레이션 서버 마이그레이션을 준비하는 동안 수집한 정보를 사용합니다.  
  
 |**페더레이션 서버 구성 마법사 입력 옵션**|**다음 값을 사용 합니다.**| 
|-----|-----| 
|**페더레이션 서비스 이름 지정** 페이지의 **SSL 인증서**|AD FS 페더레이션 서버 마이그레이션을 준비하는 동안 주체 이름 및 지문을 기록한 SSL 인증서를 선택합니다.|  
|**서비스 계정 지정** 페이지의 **서비스 계정** 및 **암호**|AD FS 페더레이션 서버를 준비하는 동안 기록한 서비스 계정 정보를 입력합니다. **참고:**  마법사의 두 번째 페이지에서 독립 실행형 페더레이션 서버를 선택 하면 네트워크 서비스가 자동으로 서비스 계정으로 사용 됩니다.|  
  
> [!IMPORTANT] 
> WID(Windows 내부 데이터베이스)를 사용하여 독립 실행형 페더레이션 서버 또는 단일 노드 AD FS 팜에 대한 AD FS 구성 데이터베이스를 저장하는 경우에만 이 방법을 사용할 수 있습니다.  
>
>  SQL Server를 사용하여 단일 노드 AD FS 팜에 대한 AD FS 구성 데이터베이스를 저장하려면 Windows PowerShell을 사용하여 페더레이션 서버에서 원래 AD FS 구성을 만들어야 합니다.  
  
-   Windows PowerShell 사용  
  
> [!IMPORTANT]
>  SQL Server를 사용하여 독립 실행형 페더레이션 서버 또는 단일 노드 AD FS 팜에 대한 AD FS 구성 데이터베이스를 저장하려면 Windows PowerShell을 사용해야 합니다.  
  
다음은 Windows PowerShell을 사용하여 페더레이션 서버 또는 단일 노드 SQL Server 팜에서 원래 AD FS 구성을 만드는 방법에 대한 예입니다.  Windows PowerShell 모듈을 열고 다음 명령을 실행합니다. `$fscredential = Get-Credential`. SQL Server 팜의 마이그레이션을 준비하는 동안 기록한 서비스 계정의 이름 및 암호를 입력합니다. 다음 명령을 실행합니다. `C:\PS> Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"` 여기서 `Data Source` 는 `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`파일의 정책 저장소 연결 문자열 값의 데이터 원본 값입니다.  
  
4. 나머지 AD FS 서비스 설정 및 트러스트 관계를 복원합니다. 이 단계는 AD FS 마이그레이션을 준비하는 동안 내보낸 파일과 수집한 값을 사용하여 수동으로 수행할 수 있는 단계입니다. 자세한 지침은 나머지 AD FS 팜 구성 복원을 참조하세요.  
  
> [!NOTE]
>  이 단계는 독립 실행형 페더레이션 서버 또는 단일 노드 WID 팜을 마이그레이션하는 경우에만 필요합니다.  페더레이션 서버에서 SQL Server 데이터베이스를 구성 저장소로 사용하는 경우에는 서비스 설정 및 트러스트 관계가 데이터베이스에서 유지됩니다.  
  
5. AD FS 웹 페이지를 업데이트합니다. 이것은 수동 단계입니다. 마이그레이션을 준비 하는 동안 사용자 지정 된 AD FS 웹 페이지를 백업한 경우 Windows Server 2012에 대 한 AD FS 구성의 결과로, 기본적으로 **%systemdrive%\inetpub\adfs\ls** 디렉터리에 생성 된 기본 AD FS 웹 페이지를 백업 데이터를 사용 하 여 덮어씁니다.  
  
6. 사용자 지정 특성 저장소와 같은 나머지 AD FS 사용자 지정 항목을 복원합니다.  
  
## <a name="restoring-the-remaining-ad-fs-farm-configuration"></a>나머지 AD FS 팜 구성 복원  
  
-   아래와 같이 다음 AD FS 서비스 설정을 단일 노드 WID 팜 또는 독립 실행형 페더레이션 서비스로 복원합니다.  
  
    -   AD FS 관리 콘솔에서 **서비스** 를 선택하고 **페더레이션 서비스 편집...** 을 클릭합니다. 각 값을 마이그레이션을 준비하는 동안 properties.txt 파일로 내보낸 값과 대조하여 페더레이션 서비스 설정을 확인합니다.  
  
    
|**Set-adfsproperties에서 보고 한 속성 이름 페더레이션 서비스**|**AD FS Management console에서 속성 이름 페더레이션 서비스**|  
|-----|-----|
|DisplayName|페더레이션 서비스 표시 이름|  
|HostName|페더레이션 서비스 이름|  
|Identifier|페더레이션 서비스 식별자|  
  
-   ADFS 관리 콘솔에서 **Certificates(인증서)** 를 선택합니다. 마이그레이션을 준비하는 동안 certificates.txt 파일로 내보낸 값과 대조하여 서비스 통신, 토큰 암호 해독 및 토큰 서명 인증서를 확인합니다.  
  
토큰 암호 해독 또는 토큰 서명 인증서를 기본 자체 서명된 인증서에서 외부 인증서로 변경하려면 먼저 기본적으로 사용되는 자동 인증서 롤오버 기능을 사용하지 않도록 설정해야 합니다.  이렇게 하려면 다음 Windows PowerShell 명령을 사용하면 됩니다. `PSH: Set-ADFSProperties –AutoCertificateRollover $false`.  
  
-   AD FS 관리 콘솔에서 **Endpoints(끝점)** 를 선택합니다. AD FS 마이그레이션을 준비하는 동안 파일로 내보낸 사용 가능한 AD FS 끝점 목록과 사용하도록 설정된 AD FS 끝점을 대조합니다.  
  
-   AD FS 관리 콘솔에서 **Claim Descriptions(클레임 설명)** 를 선택합니다. AD FS 마이그레이션을 준비하는 동안 파일로 내보낸 클레임 설명 목록과 AD FS 클레임 설명 목록을 대조합니다. 파일에 포함되어 있지만 AD FS의 기본 목록에 포함되어 있지 않은 모든 사용자 지정 클레임 설명을 추가합니다.  관리 콘솔의 클레임 식별자는 파일의 ClaimType에 매핑됩니다.  클레임 설명을 추가하는 방법에 대한 자세한 내용은 [클레임 설명 추가](../operations/add-a-claim-description.md)를 참조하세요. 자세한 내용은 AD FS 2.0 페더레이션 서버 마이그레이션 준비의 "1단계 - 서비스 설정 내보내기" 섹션을 참조하세요.  
  
-   AD FS 관리 콘솔에서 **클레임 공급자 트러스트**를 선택합니다. **클레임 공급자 트러스트 추가 마법사**를 사용하여 각 클레임 공급자 트러스트를 수동으로 다시 만들어야 합니다.  AD FS 마이그레이션을 준비하는 동안 내보내고 기록한 클레임 공급자 트러스트 목록을 사용합니다. 파일의 "AD AUTHORITY" 식별자는 기본 AD FS 구성의 일부인 "Active Directory" 클레임 공급자 트러스트이므로 이것으로 클레임 공급자 트러스트를 무시할 수 있습니다.  그러나 마이그레이션 전에 Active Directory 트러스트에 추가했을 수 있는 모든 사용자 지정 클레임 규칙을 확인해야 합니다. 클레임 공급자 트러스트를 만드는 방법에 대한 자세한 내용은 [페더레이션 메타데이터를 사용하여 클레임 공급자 트러스트 만들기](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-using-federation-metadata) 또는 [수동으로 클레임 공급자 트러스트 만들기](../operations/create-a-claims-provider-trust.md#to-create-a-claims-provider-trust-manually)를 참조하세요.  
  
-   AD FS 관리 콘솔에서 **신뢰 당사자 트러스트**를 선택합니다. **신뢰 당사자 트러스트 추가 마법사**를 사용하여 각 신뢰 당사자 트러스트를 수동으로 다시 만들어야 합니다. AD FS 마이그레이션을 준비하는 동안 내보내고 기록한 신뢰 당사자 트러스트 목록을 사용합니다. 신뢰 당사자 트러스트를 만드는 방법에 대한 자세한 내용은 [페더레이션 메타데이터를 사용하여 신뢰 당사자 트러스트 만들기](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata) 또는 [수동으로 신뢰 당사자 트러스트 만들기](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)를 참조하세요. 

## <a name="next-steps"></a>다음 단계
 [AD FS 2.0 페더레이션 서버 마이그레이션 준비](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시  마이그레이션 준비](prepare-to-migrate-ad-fs-fed-proxy.md)  
 [AD FS 2.0 페더레이션 서버 마이그레이션](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 페더레이션 서버 프록시  마이그레이션](migrate-the-ad-fs-2-fed-server-proxy.md)  
 [AD FS 1.1 웹 에이전트 마이그레이션](migrate-the-ad-fs-web-agent.md)




-   
-    