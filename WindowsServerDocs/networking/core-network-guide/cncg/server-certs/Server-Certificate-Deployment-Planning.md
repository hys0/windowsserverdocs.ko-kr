---
title: 서버 인증서를 배포 계획
description: 이 항목은 802.1 X 유선 및 무선 배포에 대 한 배포 서버 인증서 가이드
manager: brianlic
ms.topic: article
ms.assetid: 7eb746e0-1046-4123-b532-77d5683ded44
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: eacfa404da91d14a7a7328646c2320be8220000c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="server-certificate-deployment-planning"></a>서버 인증서를 배포 계획

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

서버 인증서를 배포 하기 전에 다음과 같은 항목을 계획 해야 합니다.  
  
-   [기본 서버 구성 계획](#bkmk_basic)  
  
-   [요금제 도메인 액세스](#bkmk_domain)  
  
-   [웹 서버에 위치 및 가상 디렉터리의 이름을 계획합니다](#bkmk_virtual)  
  
-   [DNS (CNAME) 별칭 기록 웹 서버에 대 한 계획](#bkmk_cname)  
  
-   [CAPolicy.inf 계획 구성](#bkmk_capolicy)  
  
-   [요금제 구성 CA1에서 CDP 및 AIA 확장](#bkmk_cdp)  
  
-   [캐나다의 웹 서버 사이의 복사 작업 계획](#bkmk_copy)  
  
-   [캐나다의 서버 인증서 템플릿의 구성을 계획합니다](#bkmk_template)  
  
## <a name="bkmk_basic"></a>기본 서버 구성 계획  
Windows Server 2016 하려고 인증 기관 및 웹 서버를 사용 하는 컴퓨터에 설치 하면 컴퓨터의 이름을 바꿉니다 및 지정 하 고 구성 해야 로컬 컴퓨터에서 고정 IP 주소를 합니다.  
  
자세한 내용은 참조 Windows Server 2016 [Core 네트워크 가이드](../../../core-network-guide/Core-Network-Guide.md)합니다.  
  
## <a name="bkmk_domain"></a>요금제 도메인 액세스  
도메인에 로그온 할 때 켜져 있어야 하는 도메인 회원 컴퓨터와 사용자 계정에에서 만들어야 AD DS 로그온 시도가 하기 전에 합니다. 또한,이 가이드 대부분 절차에 필요 사용자 계정 인지 Active Directory 사용자 및 컴퓨터 도메인 관리자 Enterprise 관리자 또는 그룹의 회원 하므로 캘리포니아 적절 한 그룹 구성원에는 계정에 로그인 해야 합니다.  
  
자세한 내용은 참조 Windows Server 2016 [Core 네트워크 가이드](../../../core-network-guide/Core-Network-Guide.md)합니다.  
  
## <a name="bkmk_virtual"></a>웹 서버에 위치 및 가상 디렉터리의 이름을 계획합니다  
CRL 및 다른 컴퓨터에는 선택 된 인증서를 액세스를 제공 하 웹 서버에서 이러한 항목 가상 디렉터리에 저장 해야 있습니다. 이 가이드에서는 가상 디렉터리 WEB1 웹 서버에 있습니다. 이 폴더가 "c:" 드라이브 켜져 있고 "pki." 라는 가상 디렉터리의 웹 서버에서 여 배포를 위해 적합 한 모든 폴더 위치를 찾을 수 있습니다.  
  
## <a name="bkmk_cname"></a>DNS (CNAME) 별칭 기록 웹 서버에 대 한 계획  
(CNAME) 별칭 리소스 레코드를 리소스 정식 이름 레코드 라고도 합니다. 이러한 레코드를 통해 쉽게 한 파일을 전송 프로토콜 ()으 동일한 컴퓨터에는 웹 서버 호스트 하는 등의 작업을 수행할 수 있도록 단일 호스트 가리키도록 개 이상의 이름을 사용할 수 있습니다. 예를 들어, 이러한 서비스 호스트 하는 시스템 DNS (도메인 이름) 호스트 이름을 WEB1와 같은 서버 컴퓨터에 대 한에 매핑하는 (CNAME) 별칭 리소스 레코드를 사용 하 여 유명 서버 이름 (ftp, www) 등록 되어 있습니다.  
  
이 가이드를 개최 된 인증서 해지 목록 (CRL) 인증 기관 (캐나다)에 대 한 구성 웹 서버에 대 한 지침을 제공 합니다. 호스트 FTP 또는 웹 사이트를와 같이 웹 서버를 다른 용도로 사용 하려는 수, 것이 좋습니다 웹 서버에 대 한 별칭 리소스 레코드 DNS에 만들 수 있습니다. 이 가이드에서는 CNAME 기록 "pki" 라는 하지만 여 배포를 위해 적합 한 이름 선택할 수 있습니다.  
  
## <a name="bkmk_capolicy"></a>CAPolicy.inf 계획 구성  
AD CS 설치 하기 전에 CAPolicy.inf 올바른 배포에 대 한 정보를와 캐나다의 구성 해야 합니다. CAPolicy.inf 파일에는 다음과 같은 정보가 포함 되어 있습니다.  
  
```  
[Version]  
Signature="$Windows NT$"  
[PolicyStatementExtension]  
Policies=InternalPolicy  
[InternalPolicy]  
OID=1.2.3.4.1455.67.89.5  
Notice="Legal Policy Statement"  
URL=http://pki.corp.contoso.com/pki/cps.txt  
[Certsrv_Server]  
RenewalKeyLength=2048  
RenewalValidityPeriod=Years  
RenewalValidityPeriodUnits=5  
CRLPeriod=weeks  
CRLPeriodUnits=1  
LoadDefaultTemplates=0  
AlternateSignatureAlgorithm=1  
```  
이 파일에는 다음과 같은 항목이 계획 해야 합니다.  
  
-   **URL**합니다. 예제 CAPolicy.inf 파일은 URL 값은 **http://pki.corp.contoso.com/pki/cps.txt**합니다. 이 가이드의 웹 서버 WEB1 라는 pki 리소스 CNAME DNS 레코드를가지고 하기 때문입니다. 웹 서버 corp.contoso.com 도메인에 가입도 되어 있습니다. 또한 웹 서버의 인증서 해지 목록을 저장 된 "pki" 라는 가상 디렉터리가입니다. 에 입력 한 URL에 대 한 가상 디렉터리 CAPolicy.inf 파일 포인트 도메인의 웹 서버에 값을 확인 합니다.  
  
-   **RenewalKeyLength**합니다. Windows Server 2012에서 AD CS 대 한 기본 갱신 키 길이 2048입니다. 선택 하는 주요 길이 사용 하는 응용 프로그램 호환성을 제공 하면서 가능한 한 오래 여야 합니다.  
  
-   **RenewalValidityPeriodUnits**합니다. CAPolicy.inf 파일의 예는 5 년 RenewalValidityPeriodUnits 값을 갖습니다. 예상 되 고 캐나다 수명을 약 10 년 때문입니다. RenewalValidityPeriodUnits 값은 캘리포니아 또는 등록을 제공 하려는 년 수가 가장 전체 유효 기간의 반영 해야 합니다.  
  
-   **CRLPeriodUnits**합니다. 예제 CAPolicy.inf 파일은 1 CRLPeriodUnits 값은 합니다. 이 가이드 인증서 해지 목록에 대 한 예제 새로 고침 간격은 1 주 하기 때문입니다. 이 설정을 지정 하는 간격 값을 캐나다에 CRL CRL 저장 하는 웹 서버 가상 디렉터리에 게시 하 고 인증 프로세스에서를 컴퓨터에 대 한 액세스를 제공 합니다.  
  
-   **AlternateSignatureAlgorithm**합니다. 이 CAPolicy.inf 대체 서명 형식 구현 하 여 강화 된 보안 메커니즘을 구현 합니다. 이 캐나다의 인증서를 필요로 하는 Windows XP 클라이언트 아직 있는 경우이 설정을 구현 해서는 안 됩니다.  
  
나중에 하위 Ca 모든 공개 키 인프라를 추가 하지 않으려는 경우 하 고 모든 하위 Ca 추가 되지 않도록 하려면 PathLength 키 0와 CAPolicy.inf 파일을 추가할 수 있습니다. 이 키를 추가 하려면 복사한 다음 코드를 파일에 붙여 넣습니다.  
  
```  
[BasicConstraintsExtension]  
PathLength=0  
Critical=Yes  
```  
  
> [!IMPORTANT]  
> 하지 한 특정 이유가 않은 경우 CAPolicy.inf 파일의 다른 설정을 변경 하는 것이 좋습니다.  
  
## <a name="bkmk_cdp"></a>요금제 구성 CA1에서 CDP 및 AIA 확장  
CA1에는 인증서 목록 CRL (해지) 지점 CDP (배포) 및 정보 AIA 기관 액세스 () 설정을 구성한 경우 웹 서버와 도메인 이름 이름이 필요 합니다. 사용자가 만든 웹 서버의 인증서 해지 목록 (CRL) 및 인증 기관 인증서 저장 된 위치 가상 디렉터리의 이름을 해야 합니다.  
  
이 배포 단계를 입력 해야 하는 CDP 위치 형식을 사항은 다음과 같습니다.  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl.`  
      
예를 들어, 웹 서버 WEB1 라고 하는 경우 사용자 DNS 웹 서버에 대 한 CNAME 기록 별칭은 "pki" 도메인 corp.contoso.com, 하며 pki 이라는 가상 디렉터리, CDP 위치는 다음과 같습니다.  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`  
      
입력 해야 하는 AIA 위치 형식을 사항은 다음과 같습니다.  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<ServerDNSName>\_<CaName><CertificateName>.crt.`  
      
예를 들어, 웹 서버 WEB1 라고 하는 경우 사용자 DNS 웹 서버에 대 한 CNAME 기록 별칭은 "pki" 도메인 corp.contoso.com, 하며 pki 이라는 가상 디렉터리, AIA 위치는 다음과 같습니다.  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`  
      
## <a name="bkmk_copy"></a>캐나다의 웹 서버 사이의 복사 작업 계획  
웹 서버 가상 디렉터리 하 고 캐나다에서는 CRL 및 캐나다 인증서를 게시 하 고 캐나다의 CDP 및 AIA 위치를 구성 하 고 나면 certutil crl 명령의 실행할 수 있습니다. 캘리포니아 속성에서 올바른 경로 구성할 수 있도록 **확장** 이 가이드의 지침을 사용 하 여이 명령을 실행 하기 전에 탭 합니다. 또한 엔터프라이즈 인증서는 웹 서버를 복사 하려면 해야 이미 가상 디렉터리 웹 서버에서 만든을 폴더 공유 폴더를 구성할 합니다.  
  
## <a name="bkmk_template"></a>캐나다의 서버 인증서 템플릿의 구성을 계획합니다  
자동 서버 인증서를 배포 하 라는 인증서 템플릿을 복사 해야 **RAS와 IAS 서버**합니다. 이 기본적으로 라고 **RAS 복사 및 IAS 서버**합니다. 이 서식 복사본 이름을 변경 하려는 경우이 배포 단계 사용 하 여 원하는 이름을 계획입니다.  
  
> [!NOTE]  
> 이 가이드-는 인증서 자동 등록 서버 구성, 그룹 정책, 서버에 새로 고침 수 있도록 하 고 서버는 받았는지 확인 유효한 서버 인증서의 캐나다에서-의 마지막 사진 3 배포 섹션 계획 추가 단계를 수행 하지 않아도 됩니다.  
  


