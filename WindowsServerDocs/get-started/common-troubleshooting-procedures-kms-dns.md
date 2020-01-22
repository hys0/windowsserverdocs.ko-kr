---
title: DNS 관련 정품 인증 문제 해결을 위한 지침
description: ''
ms.topic: article
ms.date: 09/10/2019
ms.technology: server-general
ms.assetid: ''
author: Teresa-Motiv
ms.author: v-tea
ms.localizationpriority: medium
ms.openlocfilehash: 17d4dc0ce531327db21d660481386fcc56498ae3
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75948279"
---
# <a name="guidelines-for-troubleshooting-dns-related-activation-issues"></a>DNS 관련 정품 인증 문제 해결을 위한 지침

다음 조건 중 하나 이상을 충족하는 경우 다음 방법을 사용해야 할 수도 있습니다.

- 볼륨 라이선스 미디어와&nbsp;볼륨 라이선스 일반 제품 키를 사용하여 다음 운영 체제 중 하나를 설치합니다.
   - 시작
   - Windows Server 2016
   - Windows Server 2012 R2
   - Windows Server 2012
   - Windows Server 2008 R2
   - Windows Server 2008
   - Windows 10
   - Windows 8.1
   - Windows 8
- 정품 인증 마법사는 KMS 호스트 컴퓨터에 연결할 수 없습니다.

클라이언트 시스템을 정품 인증하려고 시도하면 정품 인증 마법사가 DNS를 사용하여 KMS 소프트웨어를 실행하는 해당 컴퓨터를 찾습니다. 마법사가 DNS를 쿼리하고 KMS 호스트 컴퓨터의 DNS 항목을 찾지 못하는 경우 마법사가 오류를 보고합니다.   

<a id="list"></a>다음 목록을 검토하여 상황에 맞는 접근 방식을 찾아보세요.

- KMS 호스트를 설치할 수 없거나 KMS 정품 인증을 사용할 수 없는 경우 [제품 키를 MAK로 변경](#change-the-product-key-to-an-mak) 절차를 따릅니다.
- KMS 호스트를 설치하고 구성해야 하는 경우 [정품 인증할 클라이언트의 KMS 호스트 구성](#configure-a-kms-host-for-the-clients-to-activate-against) 절차를 따릅니다.
- 클라이언트가 기존 KMS 호스트를 찾을 수 없는 경우 다음 절차에 따라 라우팅 구성 문제를 해결합니다. 다음 절차는 가장 간단한 것부터 가장 복잡한 순서대로 정렬되어 있습니다.
  - [DNS 서버에 대한 기본 IP 연결 확인](#verify-basic-ip-connectivity-to-the-dns-server)
  - [KMS 호스트 구성 확인](#verify-the-configuration-of-the-kms-host)  
  - [라우팅 이슈의 유형 확인](#determine-the-type-of-routing-issue)
  - [DNS 구성 확인](#verify-the-dns-configuration)
  - [수동으로 KMS SRV 레코드 만들기](#manually-create-a-kms-srv-record)
  - [수동으로 KMS 클라이언트에 KMS 호스트 할당](#manually-assign-a-kms-host-to-a-kms-client)
  - [여러 DNS 도메인에 게시하도록 KMS 호스트 구성](#configure-the-kms-host-to-publish-in-multiple-dns-domains)

## <a name="change-the-product-key-to-an-mak"></a>제품 키를 MAK로 변경

KMS 호스트를 설치할 수 없거나 어떤 이유로 KMS 정품 인증을 사용할 수 없는 경우 제품 키를 MAK로 변경합니다. MSDN(Microsoft Developer Network) 또는 TechNet에서 Windows 이미지를 다운로드한 경우 미디어 아래에 나열되는 SKU(재고 유지 단위)는 일반적으로 볼륨 라이선스 미디어이고, 제공되는 제품 키는 MAK 키입니다.

제품 키를 MAK로 변경하려면 다음 단계를 수행합니다.

1. 관리자 권한 명령 프롬프트 창을 엽니다. 이렇게 하려면 Windows 로고 키+X를 누르고, **명령 프롬프트**를 마우스 오른쪽 단추로 클릭한 다음, **관리자 권한으로 실행**을 선택합니다. 관리자 암호 또는 확인을 요구하는 메시지가 표시되면 암호를 입력하거나 확인 작업을 수행합니다.
2. 명령 프롬프트에서 다음 명령을 실행합니다.
   ```cmd
    slmgr -ipk xxxxx-xxxxx-xxxxx-xxxxx-xxxxx
   ```
   > [!NOTE]
   > **xxxxx-xxxxx-xxxxx-xxxxx-xxxxx** 자리 표시자는 MAK 제품 키를 나타냅니다.  

[절차 목록으로 돌아갑니다.](#list)

## <a name="configure-a-kms-host-for-the-clients-to-activate-against"></a>정품 인증할 클라이언트의 KMS 호스트 구성

KMS를 정품 인증하려면 정품 인증할 클라이언트에 대해 KMS 호스트를 구성해야 합니다. 현재 환경에 KMS 호스트가 구성되어 있지 않으면 적절한 KMS 호스트 키를 사용하여 KMS 호스트를 설치하고 정품 인증합니다. KMS 소프트웨어를 호스트하도록 네트워크에서 컴퓨터를 구성한 후에는 DNS(Domain Name System) 설정을 게시합니다.

KMS 호스트 구성 프로세스에 대한 자세한 내용은 [키 관리 서비스를 사용하여 정품 인증](https://docs.microsoft.com/windows/deployment/volume-activation/activate-using-key-management-service-vamt) 및 [VAMT 설치 및 구성](https://docs.microsoft.com/windows/deployment/volume-activation/install-configure-vamt)을 참조하세요.

[절차 목록으로 돌아갑니다.](#list)

## <a name="verify-basic-ip-connectivity-to-the-dns-server"></a>DNS 서버에 대한 기본 IP 연결 확인

ping 명령을 사용하여 DNS 서버에 대한 기본 IP 연결을 확인합니다. 이렇게 하려면 오류가 발생하는 KMS 클라이언트와 KMS 호스트 컴퓨터에서 다음 단계를 수행합니다.

1. 관리자 권한 명령 프롬프트 창을 엽니다.
1. 명령 프롬프트에서 다음 명령을 실행합니다.
   ```cmd
   ping <DNS_Server_IP_address>
   ```
   > [!NOTE]
   > 이 명령의 출력에 "의 응답"이라는 문구가 없으면 네트워크 문제 또는 DNS 이슈가 있는 것입니다. 이 문서의 다른 절차를 사용하려면 이 문제를 먼저 해결해야 합니다. DNS 서버를 ping 할 수 없는 경우 TCP/IP 이슈를 해결하는 방법에 대한 자세한 내용은 [TCP/IP의 고급 이슈 해결](https://docs.microsoft.com/windows/client-management/troubleshoot-tcpip)을 참조하세요.

[절차 목록으로 돌아갑니다.](#list)

## <a name="verify-the-configuration-of-the-kms-host"></a>KMS 호스트 구성 확인

KMS 호스트 서버의 레지스트리를 검사하여 DNS에 등록하는지 확인합니다. 기본적으로 KMS 호스트 서버는 24시간마다 한 번씩 DNS SRV 레코드를 동적으로 등록합니다. 
> [!IMPORTANT]
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/help/322756)해 두세요.  

이 설정을 확인하려면 다음 단계를 수행합니다.
1. 레지스트리 편집기를 시작합니다. 이렇게 하려면 **시작**을 마우스 오른쪽 단추로 클릭하고, **실행**을 선택하고, **regedit**를 입력한 다음, Enter 키를 누릅니다.
1. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SL** 하위 키를 찾아서 **DisableDnsPublishing** 항목의 값을 확인합니다. 이 항목의 가능한 값은 다음과 같습니다.
   - **0** 또는 정의되지 않음(기본값): KMS 호스트 서버는 24시간마다 한 번씩 SRV 레코드를 등록합니다.
   - **1**: KMS 호스트 서버는 SRV 레코드를 자동으로 등록하지 않습니다. 현재 구현된 시스템에서 동적 업데이트를 지원하지 않는 경우 [수동으로 KMS SRV 레코드 만들기](#manually-create-a-kms-srv-record)를 참조하세요.  
1. **DisableDnsPublishing** 항목이 없는 경우 새로 만듭니다(형식은 DWORD). 동적 등록을 사용할 수 있는 경우 값을 정의되지 않은 상태로 두거나 **0**으로 설정합니다.

[절차 목록으로 돌아갑니다.](#list)

## <a name="determine-the-type-of-routing-issue"></a>라우팅 이슈의 유형 확인

다음 명령을 사용하여 이름 확인 이슈인지 아니면 SRV 레코드 이슈인지 확인할 수 있습니다.  

1. KMS 클라이언트에서 관리자 권한으로 명령 프롬프트 창을 엽니다.  
1. 명령 프롬프트에서 다음 명령을 실행합니다.
   ```cmd
   cscript \windows\system32\slmgr.vbs -skms <KMS_FQDN>:<port>
   cscript \windows\system32\slmgr.vbs -ato
   ```
   > [!NOTE]
   > 이 명령에서 <KMS_FQDN>은 KMS 호스트 컴퓨터의 FQDN(정규화된 도메인 이름)을 나타내고, \<port\>는 KMS에서 사용하는 TCP 포트를 나타냅니다.  

   이러한 명령으로 문제가 해결되면 SRV 레코드 이슈인 것입니다. [수동으로 KMS 클라이언트에 KMS 호스트 할당](#manually-assign-a-kms-host-to-a-kms-client) 절차에 설명된 명령 중 하나를 사용하여 문제를 해결할 수 있습니다.  

1. 문제가 지속되면 다음 명령을 실행합니다.
   ```cmd
   cscript \windows\system32\slmgr.vbs -skms <IP Address>:<port>
   cscript \windows\system32\slmgr.vbs -ato
   ```
   > [!NOTE]
   > 이 명령에서 \<IP Address\>는 KMS 호스트 컴퓨터의 IP 주소를 나타내고, \<port\>는 KMS에서 사용하는 TCP 포트를 나타냅니다.  

   이러한 명령으로 문제가 해결되면 이름 확인 이슈일 가능성이 높습니다. 추가 문제 해결 정보는 [DNS 구성 확인](#verify-the-dns-configuration) 절차를 참조하세요.

1. 이러한 명령으로 문제가 해결되지 않으면 컴퓨터의 방화벽 구성을 확인합니다. KMS 클라이언트와 KMS 호스트 간에 발생하는 모든 정품 인증 통신에는 1688 TCP 포트가 사용됩니다. KMS 클라이언트와 KMS 호스트의 방화벽이 포트 1688을 통한 통신을 허용해야 합니다.

[절차 목록으로 돌아갑니다.](#list)

## <a name="verify-the-dns-configuration"></a>DNS 구성 확인

>[!NOTE]
> 달리 명시되지 않는 한, 해당 오류가 발생한 KMS 클라이언트에서 다음 단계를 수행합니다.

1. 관리자 권한으로 명령 프롬프트 창을 엽니다.
1. 명령 프롬프트에서 다음 명령을 실행합니다.
   ```cmd
   IPCONFIG /all
   ```
1. 명령 결과에서 다음 정보를 기록해 둡니다.
   - KMS 클라이언트 컴퓨터에 할당된 IP 주소
   - KMS 클라이언트 컴퓨터에서 사용하는 기본 DNS 서버의 IP 주소
   - KMS 클라이언트 컴퓨터에서 사용하는 기본 게이트웨이의 IP 주소
   - KMS 클라이언트 컴퓨터에서 사용하는 DNS 접미사 검색 목록
1. KMS 호스트 SRV 레코드가 DNS에 등록되었는지 확인합니다. 이렇게 하려면 다음 단계를 따르십시오.  
   1. 관리자 권한 명령 프롬프트 창을 엽니다.
   1. 명령 프롬프트에서 다음 명령을 실행합니다.
      ```cmd
      nslookup -type=all _vlmcs._tcp>kms.txt
      ```
   1. 명령을 통해 생성되는 KMS.txt 파일을 엽니다. 이 파일에는 다음 항목과 유사한 항목이 하나 이상 포함되어 있습니다.
       ```
       _vlmcs._tcp.contoso.com SRV service location:
       priority = 0
       weight = 0
       port = 1688 svr hostname = kms-server.contoso.com
       ```
       > [!NOTE]
       > 이 항목에서 contoso.com은 KMS 호스트의 도메인을 나타냅니다.
      1. KMS 호스트의의 IP 주소, 호스트 이름, 포트 및 도메인을 확인합니다.
      1. **_vlmcs** 항목이 있고 이 항목에 예상 KMS 호스트 이름이 들어 있는 경우 [수동으로 KMS 클라이언트에 KMS 호스트 할당](#manually-assign-a-kms-host-to-a-kms-client)으로 이동합니다.  
      > [!NOTE]
      > [**nslookup**](https://docs.microsoft.com/windows-server/administration/windows-commands/nslookup) 명령이 KMS 호스트를 발견하더라도 DNS 클라이언트가 KMS 호스트를 찾을 수 있다는 의미는 아닙니다. **nslookup** 명령이 KMS 호스트를 찾았지만 여전히 KMS 호스트를 사용하여 정품 인증할 수 없는 경우 기본 DNS 접미사나 DNS 접미사의 검색 목록 같은 다른 DNS 설정을 확인합니다.
1. 기본 DNS 접미사의 검색 목록에 KMS 호스트와 연결된 DNS 도메인 접미사가 포함되어 있는지 확인합니다. 검색 목록에 이 정보가 포함되어 있지 않으면 [여러 DNS 도메인에 게시하도록 KMS 호스트 구성](#configure-the-kms-host-to-publish-in-multiple-dns-domains) 절차로 이동합니다.

[절차 목록으로 돌아갑니다.](#list)

## <a name="manually-create-a-kms-srv-record"></a>수동으로 KMS SRV 레코드 만들기

Microsoft DNS 서버를 사용하는 KMS 호스트에 대한 SRV 레코드를 수동으로 만들려면 다음 단계를 수행합니다.

1. DNS 서버에서 DNS 관리자를 엽니다. DNS 관리자를 열려면 **시작**, **관리 도구**, **DNS**를 차례로 선택합니다.
1. SRV 리소스 레코드를 만들어야 하는 DNS 서버를 선택합니다.
1. 콘솔 트리에서 **전방 조회 영역**을 확장하고 도메인을 마우스 오른쪽 단추로 클릭한 다음, **다른 새 레코드**를 선택합니다.
1. 목록을 아래로 스크롤하여 **서비스 위치(SRV)** 를 선택한 다음, **레코드 만들기**를 선택합니다.
1. 다음 정보를 입력합니다.
   - 서비스: **_VLMCS**
   - 프로토콜: **_TCP**
   - 포트 번호: **1688**
   - 서비스를 제공하는 호스트: **&lt;*KMS 호스트의 FQDN*&gt;**
1. 모두 마쳤으면 **확인**을 선택한 다음, **완료**를 선택합니다.

BIND 9.x 호환 DNS 서버를 사용하는 KMS 호스트에 대한 SRV 레코드를 수동으로 만들려면 해당 DNS 서버에 대한 지침을 따르고 SRV 레코드에 대한 다음 정보를 입력합니다.

- 이름:&nbsp; **_vlmcs._TCP**
- 유형:&nbsp;**SRV**
- 우선 순위: **0**
- 가중치: **0**
- 포트: **1688**
- 호스트 이름: **&lt;*KMS 호스트의 FQDN 또는 A 이름*&gt;**

> [!NOTE]
> KMS는 **우선 순위** 또는 **가중치** 값을 사용하지 않습니다. 그러나 레코드에는 이러한 값이 포함되어야 합니다.

KMS 자동 게시를 지원하도록 BIND 9.x 호환 DNS 서버를 구성하려면 KMS 호스트에서 리소스 레코드 업데이트를 사용하도록 DNS 서버를 구성합니다. 예를 들어 Named.conf 또는 Named.conf.local의 영역 정의에 다음 줄을 추가합니다.

```cmd
allow-update { any; };
```
## <a name="manually-assign-a-kms-host-to-a-kms-client"></a>수동으로 KMS 클라이언트에 KMS 호스트 할당

기본적으로 KMS 클라이언트는 자동 검색 프로세스를 사용합니다. 이 프로세스에 따라 KMS 클라이언트는 DNS를 쿼리하여 클라이언트의 구성원 영역 내부에 _vlmcs SRV 레코드를 게시한 서버 목록을 찾습니다. DNS는 임의의 순서로 KMS 호스트 목록을 반환합니다. 클라이언트는 KMS 호스트를 선택하고 해당 호스트에 대한 세션을 설정하려고 시도합니다. 이 시도가 정상적으로 작동하면 클라이언트는 KMS 호스트 이름을 캐시하고 다음 갱신 때 사용합니다. 세션 설정이 실패하면 클라이언트는 다른 KMS 호스트를 임의로 선택합니다. 자동 검색 프로세스를 사용할 것을 강력하게 권장합니다.  

하지만 KMS 호스트를 특정 KMS 클라이언트에 수동으로 할당할 수 있습니다. 이를 위해 다음 단계를 수행합니다.

1. KMS 클라이언트에서 관리자 권한으로 명령 프롬프트 창을 엽니다.
1. 구현에 따라 다음 단계 중 하나를 수행합니다.
   - 호스트의 FQDN을 사용하여 KMS 호스트를 할당하려면 다음 명령을 실행합니다.
     ```cmd
     cscript \windows\system32\slmgr.vbs -skms <KMS_FQDN>:<port>
     ```
   - 호스트의 버전 4 IP 주소를 사용하여 KMS 호스트를 할당하려면 다음 명령을 실행합니다.
     ```cmd
     cscript \windows\system32\slmgr.vbs -skms <IPv4Address>:<port>
     ```
    - 호스트의 버전 6 IP 주소를 사용하여 KMS 호스트를 할당하려면 다음 명령을 실행합니다.
      ```cmd
      cscript \windows\system32\slmgr.vbs -skms <IPv6Address>:<port>
      ```
    - 호스트의 NETBIOS 이름을 사용하여 KMS 호스트를 할당하려면 다음 명령을 실행합니다.
      ```cmd
      cscript \windows\system32\slmgr.vbs -skms <NETBIOSName>:<port>
      ```
   - KMS 클라이언트에서 자동 검색으로 되돌리려면 다음 명령을 실행합니다.
     ```cmd
     cscript \windows\system32\slmgr.vbs -ckms
     ```
     > [!NOTE]
     > 이러한 명령은 다음 자리 표시자를 사용합니다.
     >- **<KMS_FQDN>** 은 KMS 호스트 컴퓨터의 FQDN(정규화된 도메인 이름)을 나타냅니다.
     >- **\<IPv4Address\>** 는 KMS 호스트 컴퓨터의 IP 버전 4 주소를 나타냅니다.
     >- **\<IPv6Address\>** 는 KMS 호스트 컴퓨터의 IP 버전 6 주소를 나타냅니다.
     >- **\<NETBIOSName\>** 은 KMS 호스트 컴퓨터의 NETBIOS 이름을 나타냅니다.
     >- **\<port\>** 는 KMS에서 사용하는 TCP 포트를 나타냅니다.  

## <a name="configure-the-kms-host-to-publish-in-multiple-dns-domains"></a>여러 DNS 도메인에 게시하도록 KMS 호스트 구성

> [!IMPORTANT]
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/help/322756)해 두세요.

[수동으로 KMS 클라이언트에 KMS 호스트 할당](#manually-assign-a-kms-host-to-a-kms-client)에 설명된 대로, KMS 클라이언트는 일반적으로 자동 검색 프로세스를 사용하여 KMS 호스트를 식별합니다. 이 프로세스를 수행하려면 KMS 클라이언트 컴퓨터의 DNS 영역에서 _vlmcs SRV 레코드를 사용할 수 있어야 합니다. DNS 영역은 컴퓨터의 기본 DNS 접미사 또는 다음 중 하나에 해당합니다.
- 도메인에 가입된 컴퓨터의 경우 DNS 시스템에서 할당한 컴퓨터의 도메인(예: AD DS(Active Directory Domain Services) DNS).
- 작업 그룹 컴퓨터의 경우 DHCP(Dynamic Host Configuration Protocol)에서 할당한 컴퓨터의 도메인. 이 도메인 이름은 RFC(Request for Comments) 2132에 정의된 대로 코드 값이 15인 옵션을 통해 정의됩니다.

기본적으로 KMS 호스트는 KMS 호스트 컴퓨터의 도메인과 일치하는 DNS 영역에 SRV 레코드를 등록합니다. 예를 들어 KMS 호스트가 contoso.com 도메인에 가입한다고 가정해 봅시다. 이 시나리오에서 KMS 호스트는 _vmlcs SRV 레코드를 contoso.com DNS 영역 아래에 등록합니다. 따라서 레코드는 서비스를 VLMCS._TCP.CONTOSO.COM으로 식별합니다.

KMS 호스트와 KMS 클라이언트가 서로 다른 DNS 영역을 사용하는 경우 SRV 레코드를 여러 DNS 도메인에 자동으로 게시하도록 KMS 호스트를 구성해야 합니다. 이렇게 하려면 다음 단계를 따르십시오.

1. KMS 호스트에서 레지스트리 편집기를 시작합니다. 
1. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SL** 하위 키를 찾아서 선택합니다.
1. **세부 정보** 창에서 빈 영역을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택한 다음, **다중 문자열 값**을 선택합니다.
1. 새 항목의 이름으로 **DnsDomainPublishList**를 입력합니다.
1. 새 **DnsDomainPublishList** 항목을 마우스 오른쪽 단추로 클릭한 다음, **수정**을 선택합니다.
1. **다중 문자열 편집** 대화 상자에서 KMS가 별도의 줄에 게시하는 각 DNS 도메인 접미사를 입력한 다음, **확인**을 선택합니다.
   > [!NOTE]
   > Windows Server 2008 R2의 경우 **DnsDomainPublishList**의 형식이 다릅니다. 자세한 내용은 볼륨 정품 인증 기술 참조 가이드를 확인하세요.
1. 서비스 관리 도구를 사용하여 소프트웨어 라이선스 서비스를 다시 시작합니다. 이 작업은 SRV 레코드를 만듭니다.
1. 구성된 KMS 호스트에 KMS 클라이언트가 연결할 수 있는지 일반적인 방법을 사용하여 확인합니다. KMS 클라이언트가 이름 및 IP 주소를 기준으로 KMS 호스트를 올바르게 식별하는지 확인합니다. 두 확인 중 하나라도 실패하면 이 DNS 클라이언트 확인자 이슈를 조사합니다.
1. KMS 클라이언트에서 이전에 캐시된 KMS 호스트 이름을 지우려면 KMS 클라이언트에서 관리자 권한으로 명령 프롬프트 창을 열고 다음 명령을 실행합니다.
   ```cmd
   cscript C:\Windows\System32\slmgr.vbs -ckms
   ```
