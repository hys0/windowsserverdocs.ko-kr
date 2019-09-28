---
title: 서버 인증서 배포 계획
description: 이 항목은 서버 배포 인증서 802.1 X 유선 및 무선 배포 가이드의 일부
manager: brianlic
ms.topic: article
ms.assetid: 7eb746e0-1046-4123-b532-77d5683ded44
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ec5bc315381f85434753f9becc94409a74271b7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356112"
---
# <a name="server-certificate-deployment-planning"></a>서버 인증서 배포 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

서버 인증서를 배포 하기 전에 다음 항목을 계획 해야 합니다.  
  
-   [기본 서버 구성 계획](#bkmk_basic)  
  
-   [도메인 액세스 계획](#bkmk_domain)  
  
-   [웹 서버에서 가상 디렉터리의 위치와 이름을 계획 합니다.](#bkmk_virtual)  
  
-   [웹 서버에 대 한 DNS 별칭 (CNAME) 레코드 계획](#bkmk_cname)  
  
-   [Capolicy.inf의 구성 계획](#bkmk_capolicy)  
  
-   [C A 1에서 CDP 및 AIA 확장의 구성 계획](#bkmk_cdp)  
  
-   [CA와 웹 서버 간의 복사 작업 계획](#bkmk_copy)  
  
-   [CA에서 서버 인증서 템플릿의 구성 계획](#bkmk_template)  
  
## <a name="bkmk_basic"></a>기본 서버 구성 계획  
인증 기관 및 웹 서버를 사용 하도록 계획 하는 컴퓨터에서 Windows Server 2016를 설치한 후 컴퓨터 이름을 바꾸고 및 할당 하 고 구성 해야 로컬 컴퓨터에 대 한 고정 IP 주소입니다.  
  
자세한 내용은 Windows Server 2016을 참조 하십시오. [핵심 네트워크 가이드](../../../core-network-guide/Core-Network-Guide.md)합니다.  
  
## <a name="bkmk_domain"></a>도메인 액세스 계획  
하려면 도메인에 로그온 컴퓨터는 도메인 구성원 컴퓨터 및 사용자 계정에 로그온 하기 전에 AD DS에 만들어야 합니다. 또한이 가이드의 대부분 절차를 사용 하려면 사용자 계정 Active Directory 사용자 및 컴퓨터에서 Domain Admins 또는 Enterprise Admins 그룹의 구성원 ca에 적절 한 그룹 멤버 자격을 가진 계정에 로그온 해야 합니다.  
  
자세한 내용은 Windows Server 2016을 참조 하십시오. [핵심 네트워크 가이드](../../../core-network-guide/Core-Network-Guide.md)합니다.  
  
## <a name="bkmk_virtual"></a>웹 서버에서 가상 디렉터리의 위치와 이름을 계획 합니다.  
다른 컴퓨터에 CA 인증서와 CRL에 대 한 액세스를 제공 하려면 웹 서버에 가상 디렉터리에 이러한 항목을 저장할 해야 있습니다. 이 가이드에서는 가상 디렉터리는 웹 서버 w e b 1에 있습니다. 이 폴더는 "c:" 드라이브 및 "pki." 라고 합니다. 배포에 적합 한 모든 폴더 위치에서 웹 서버의 가상 디렉터리를 찾을 수 있습니다.  
  
## <a name="bkmk_cname"></a>웹 서버에 대 한 DNS 별칭 (CNAME) 레코드 계획  
별칭 (CNAME) 리소스 레코드를 정식 이름 리소스 레코드 라고도 합니다. 이러한 레코드를 통해 쉽게 프로토콜 FTP (파일 전송) 서버와 동일한 컴퓨터에 웹 서버 호스트와 같은 작업을 수행할 수 있도록 단일 호스트를 가리키도록 이름을 여러 개 사용할 수 있습니다. 예를 들어, 잘 알려진 서버 이름 (ftp, www)는 이러한 서비스를 호스팅하는 도메인 이름 시스템 (DNS) 호스트 이름, 예: WEB1 서버 컴퓨터에 매핑되는 별칭 (CNAME) 리소스 레코드를 사용 하 여 등록 됩니다.  
  
이 가이드는 인증 기관 (CA)에 대해 인증서 해지 목록 (CRL)를 호스트 하 여 웹 서버를 구성 하기 위한 지침을 제공 합니다. 호스팅하는 FTP 또는 웹 사이트와 같은 다른 용도로 웹 서버를 사용할 수도 있습니다, 되므로 웹 서버에 대 한 dns에서 별칭 리소스 레코드를 만드는 것이 좋습니다. 이 가이드에서는 CNAME 레코드는 "pki" 이라고 하지만 배포에 적합 한 이름을 선택할 수 있습니다.  
  
## <a name="bkmk_capolicy"></a>Capolicy.inf의 구성 계획  
AD CS를 설치 하기 전에 배포에 대 한 올바른 정보를 사용 하는 CA에서 CAPolicy.inf를 구성 해야 합니다. CAPolicy.inf 파일에는 다음과 같은 정보가 포함 되어 있습니다.  
  
```  
[Version]  
Signature="$Windows NT$"  
[PolicyStatementExtension]  
Policies=InternalPolicy  
[InternalPolicy]  
OID=1.2.3.4.1455.67.89.5  
Notice="Legal Policy Statement"  
URL=https://pki.corp.contoso.com/pki/cps.txt  
[Certsrv_Server]  
RenewalKeyLength=2048  
RenewalValidityPeriod=Years  
RenewalValidityPeriodUnits=5  
CRLPeriod=weeks  
CRLPeriodUnits=1  
LoadDefaultTemplates=0  
AlternateSignatureAlgorithm=1  
```  
이 파일에 대 한 다음 항목을 계획 해야 합니다.  
  
-   **URL**합니다. 예제 Capolicy.inf 파일은 URL 값 **https://pki.corp.contoso.com/pki/cps.txt** 입니다. 이 가이드의 웹 서버 이름이 w e b 1 및 pki DNS CNAME 리소스 레코드를가지고 때문입니다. 웹 서버는 또한 corp.contoso.com 도메인에 가입 됩니다. 또한 인증서 해지 목록을 저장 된 "pki" 라는 웹 서버의 가상 디렉터리가입니다. 값에에서 입력 한 URL에 대 한 가상 디렉터리에 사용자 CAPolicy.inf 파일 지점을 도메인에서 웹 서버에 있는지 확인 합니다.  
  
-   **RenewalKeyLength**합니다. Windows Server 2012의 AD CS에 대 한 기본 갱신 키 길이 2048입니다. 선택 하는 키 길이 사용 하려는 응용 프로그램 호환성을 제공 하면서 최대한 오랫동안 이어야 합니다.  
  
-   **RenewalValidityPeriodUnits**합니다. 예제 CAPolicy.inf 파일에는 5 년 RenewalValidityPeriodUnits 값을 있습니다. CA의 수명이 예상된은 약 10 년 동안 때문입니다. RenewalValidityPeriodUnits 값 CA 또는 등록을 제공 하려면 년의 가장 높은 숫자의 전체 유효 기간을 반영 해야 합니다.  
  
-   **CRLPeriodUnits**합니다. 예제 CAPolicy.inf 파일은 CRLPeriodUnits 값이 1에 있습니다. 이 가이드의 인증서 해지 목록에 대 한 예제에서는 새로 고침 간격은 1 주 때문입니다. 이 설정을 지정 하는 간격 값에서 CRL을 저장 하 여 웹 서버 가상 디렉터리에 CA에 CRL을 게시 하 고 인증 프로세스에 있는 컴퓨터에 대 한에 대 한 액세스를 제공 해야 합니다.  
  
-   **AlternateSignatureAlgorithm**합니다. 이 CAPolicy.inf 대체 서명 형식 구현 하 여 향상 된 보안 메커니즘을 구현 합니다. 이 CA의에서 인증서를 필요로 하는 Windows XP 클라이언트를 여전히 있으면이 설정은 구현 하지 않아야 합니다.  
  
공개 키 인프라에는 나중에 모든 하위 Ca를 추가 하지 않으려는 경우와 모든 하위 Ca 추가 하지 못하게 하려면 있으면 값이 0 인 CAPolicy.inf 파일에 PathLength 키를 추가할 수 있습니다. 이 키를 추가 하려면 복사 하 여 파일에 다음 코드를 붙여 넣습니다.  
  
```  
[BasicConstraintsExtension]  
PathLength=0  
Critical=Yes  
```  
  
> [!IMPORTANT]  
> 하지 않는 한 특정 이유가 없다면 CAPolicy.inf 파일에 설정을 변경 하는 것이 좋습니다.  
  
## <a name="bkmk_cdp"></a>C A 1에서 CDP 및 AIA 확장의 구성 계획  
C a 1에서 액세스 AIA (기관 정보) 설정과 (CDP (인증서 해지 목록 (CRL) 배포 지점)를 구성할 때 웹 서버와 도메인 이름을의 이름이 필요 합니다. 웹 서버 인증서 해지 목록 (CRL) 및 인증 기관 인증서 저장 된 위치에 만든 가상 디렉터리의 이름을 알아야 합니다.  
  
이 배포 단계를 입력 해야 하는 CDP 위치 형식은 같습니다.  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl.`  
      
예를 들어 웹 서버 이름이 w e b 1이 고 DNS 별칭 웹 서버에 대 한 CNAME 레코드는 "pki", 도메인 corp.contoso.com에 및 가상 디렉터리의 이름이 pki가 CDP 위치는:  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`  
      
AIA 위치를 입력 해야 하는 형식은 같습니다.  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<ServerDNSName>\_<CaName><CertificateName>.crt.`  
      
예를 들어 웹 서버 이름이 w e b 1이 고 DNS 별칭 웹 서버에 대 한 CNAME 레코드는 "pki", 도메인 corp.contoso.com에 및 가상 디렉터리의 이름이 pki가 AIA 위치는:  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`  
      
## <a name="bkmk_copy"></a>CA와 웹 서버 간의 복사 작업 계획  
웹 서버 가상 디렉터리에 CA의 CRL 및 CA 인증서를 게시 하려면 CA의 CDP 및 AIA 위치를 구성한 후 certutil-crl 명령을 실행할 수 있습니다. CA 속성에 올바른 경로 구성 해야 **확장** 이 가이드의 지침을 사용 하 여이 명령을 실행 하기 전에 탭 합니다. 또한 엔터프라이즈 CA 인증서를 웹 서버에 복사 하려면 해야 이미 웹 서버의 가상 디렉터리를 만들 있고 구성 폴더를 공유 폴더로 합니다.  
  
## <a name="bkmk_template"></a>CA에서 서버 인증서 템플릿의 구성 계획  
자동 등록 된 서버 인증서를 배포 하려면 인증서 템플릿을 복사 해야 **RAS 및 IAS 서버**합니다. 기본적으로이 복사본 이름은 **복사본의 RAS 및 IAS 서버**합니다. 이 서식 파일 복사본의 이름을 변경 하려는 경우이 배포 단계를 사용 하 여 원하는 이름을 계획 합니다.  
  
> [!NOTE]  
> -는 서버 인증서 자동 등록을 구성, 서버에서 그룹 정책을 새로 고칠 수 및 서버 CA에서 유효한 서버 인증서를 받은 있는지 확인-이 가이드의 마지막 세 가지 배포 섹션에는 추가 계획 단계가 필요 하지 않습니다.  
  


