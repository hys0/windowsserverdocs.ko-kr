---
title: KMS 정품 인증의 알려진 문제
description: KMS 정품 인증 프로세스 중에 발생할 수 있는 일반적인 문제를 설명하고 해결 방법과 지침을 제공합니다.
ms.topic: article
ms.date: 10/3/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 3446ad0954510d8c96e9a2d361f24c90d325b782
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826256"
---
# <a name="kms-activation-known-issues"></a>KMS 정품 인증: 알려진 문제

이 문서에서는 KMS(키 관리 서비스) 정품 인증 중에 발생할 수 있는 일반적인 질문과 문제에 대해 설명하고, 문제 해결을 위한 지침을 제공합니다.

> [!NOTE]
> DNS와 관련된 문제로 의심되는 경우 [KMS 및 DNS 문제에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.

## <a name="should-i-back-up-kms-host-information"></a>KMS 호스트 정보를 백업해야 하나요?

KMS 호스트에는 백업이 필요하지 않습니다. 그러나 도구를 사용하여 이벤트 로그를 정기적으로 정리하는 경우 로그에 저장된 정품 인증 기록이 손실될 수 있습니다. 이벤트 로그를 사용하여 KMS 정품 인증을 추적하거나 문서화하는 경우 이벤트 뷰어의 [애플리케이션 및 서비스 로그] 폴더에서 키 관리 서비스 이벤트 로그를 정기적으로 내보냅니다.

System Center Operations Manager를 사용하는 경우 System Center Data Warehouse 데이터베이스는 보고를 위해 이벤트 로그 데이터를 저장하므로 이벤트 로그를 별도로 백업할 필요가 없습니다.

## <a name="is-the-kms-client-computer-activated"></a>KMS 클라이언트 컴퓨터가 정품 인증되었나요?

KMS 클라이언트 컴퓨터에서 **시스템** 제어판을 열고, **Windows 정품 인증을 받았습니다.** 라는 메시지를 찾습니다. 또는 Slmgr.vbs를 실행하고, **/dli** 명령줄 옵션을 사용합니다.

## <a name="the-kms-client-computer-does-not-activate"></a>KMS 클라이언트 컴퓨터가 정품 인증되지 않음

KMS 정품 인증 임계값이 충족되었는지 확인합니다. KMS 호스트 컴퓨터에서 Slmgr.vbs를 실행하고, **/dli** 명령줄 옵션을 사용하여 호스트의 현재 개수를 확인합니다. KMS 호스트의 개수가 25개일 때까지 Windows 7 클라이언트 컴퓨터를 정품 인증할 수 없습니다. Windows Server 2008 R2 KMS 클라이언트를 정품 인증하려면 KMS 수가 5여야 합니다. KMS 요구 사항에 대한 자세한 내용은 [볼륨 정품 인증 계획 가이드](https://go.microsoft.com/fwlink/?linkid=155926)를 참조하세요. 

KMS 클라이언트 컴퓨터의 애플리케이션 이벤트 로그에서 12289 이벤트 ID를 확인합니다. 이 이벤트에서 다음 정보를 확인합니다.

- 결과 코드가 **0**인지 여부. 다른 모든 코드는 오류입니다.
- 이벤트의 KMS 호스트 이름이 올바른지 여부
- KMS 포트가 올바른지 여부
- KMS 호스트에 액세스할 수 있는지 여부
- 클라이언트에서 Microsoft 이외의 방화벽을 실행하는 경우 아웃바운드 포트를 구성해야 하는지 여부

KMS 호스트 컴퓨터의 KMS 이벤트 로그에서 12290 이벤트 ID를 확인합니다. 이 이벤트에서 다음 정보를 확인합니다.

- KMS 호스트에서 클라이언트 컴퓨터의 요청을 기록했는지 여부. KMS 클라이언트 컴퓨터의 이름이 나열되어 있는지 확인합니다. 클라이언트와 KMS 호스트에서 통신할 수 있는지 확인합니다. 클라이언트에서 응답을 받았는지 여부.
- 이벤트가 KMS 클라이언트에서 기록되지 않은 경우 요청이 KMS 호스트에 도달하지 않았거나 KMS 호스트에서 이벤트를 처리할 수 없습니다. 라우터에서 1688 TCP 포트를 사용하여(기본 포트를 사용하는 경우) 트래픽을 차단하지 않고 KMS 클라이언트에 대한 상태 저장 트래픽이 허용되어야 합니다.

## <a name="what-does-this-error-code-mean"></a>이 오류 코드의 의미는 무엇인가요?

Windows는 12290 이벤트 ID의 KMS 이벤트를 제외하고 모든 정품 인증 이벤트를 애플리케이션 이벤트 로그의 Microsoft-Windows-Security-SPP 이벤트 공급자 이름 아래에 기록합니다. Windows는 KMS 이벤트를 [애플리케이션 및 서비스] 폴더의 키 관리 서비스 로그에 기록합니다. IT 전문가는 Slui.exe를 실행하여 대부분의 정품 인증 관련 오류 코드에 대한 설명을 표시할 수 있습니다. 이 명령의 일반 구문은 다음과 같습니다.

```cmd
slui.exe 0x2a ErrorCode
```

예를 들어 0x8007267C 오류 코드가 12293 이벤트 ID에 포함되어 있으면 다음 명령을 실행하여 해당 오류에 대한 설명을 표시할 수 있습니다.

```cmd
slui.exe 0x2a 0x8007267C
```

특정 오류 코드 및 이를 해결하는 방법에 대한 자세한 내용은 [일반적인 정품 인증 오류 코드 해결](activation-error-codes.md)을 참조하세요.

## <a name="clients-are-not-adding-to-the-kms-count"></a>클라이언트가 KMS 개수에 추가되지 않음

CMID(클라이언트 컴퓨터 ID) 및 기타 제품 정품 인증 정보를 다시 설정하려면 **sysprep /generalize** 또는 **slmgr /rearm**을 실행합니다. 그렇지 않으면 각 클라이언트 컴퓨터가 동일하게 표시되고, KMS 호스트에서 이를 별도의 KMS 클라이언트로 계산하지 않습니다.

## <a name="kms-hosts-are-unable-to-create-srv-records"></a>KMS 호스트에서 SRV 레코드를 만들 수 없음

DNS(Domain Name System)에서 쓰기 액세스 권한을 제한하거나 DDNS(동적 DNS)를 지원하지 않을 수 있습니다. 이 경우 DNS 데이터베이스에 대한 쓰기 액세스 권한을 KMS 호스트에 부여하거나 서비스(SRV) RR(리소스 레코드)을 수동으로 만듭니다. KMS 및 DNS 문제에 대한 자세한 내용은 [KMS 및 DNS 문제에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.

## <a name="only-the-first-kms-host-is-able-to-create-srv-records"></a>첫 번째 KMS 호스트만 SRV 레코드를 만들 수 있음

조직에 둘 이상의 KMS 호스트가 있는 경우 SRV 기본 권한이 변경되지 않는 한 다른 호스트에서 SRV RR을 업데이트하지 못할 수 있습니다. KMS 및 DNS 문제에 대한 자세한 내용은 [KMS 및 DNS 문제에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.

## <a name="i-installed-a-kms-key-on-the-kms-client"></a>KMS 클라이언트에 KMS 키를 설치했습니다.

KMS 키는 KMS 클라이언트가 아니라 KMS 호스트에만 설치해야 합니다. **slmgr.vbs -ipk &lt;SetupKey&gt;** 를 실행합니다. 컴퓨터를 KMS 클라이언트로 구성하는 데 사용할 수 있는 키 테이블은 [KMS 클라이언트 설정 키](KMSclientkeys.md)를 참조하세요. 이러한 키는 공개적으로 알려져 있으며 버전별로 다릅니다. DNS에서 불필요한 SRV RR을 삭제한 다음, 컴퓨터를 다시 시작해야 합니다.

## <a name="a-kms-host-failed"></a>KMS 호스트에서 오류가 발생함

KMS 호스트에서 오류가 발생하면 KMS 호스트 키를 새 호스트에 설치한 다음, 해당 호스트를 정품 인증해야 합니다. 새 KMS 호스트의 DNS 데이터베이스에 SRV RR이 있는지 확인합니다. 오류가 발생한 KMS 호스트와 동일한 컴퓨터 이름과 IP 주소를 사용하여 새 KMS 호스트를 설치하는 경우 새 KMS 호스트에서 오류가 발생한 호스트의 DNS SRV 레코드를 사용할 수 있습니다. 새 호스트의 컴퓨터 이름이 다른 경우 오류가 발생한 호스트의 DNS SRV RR을 수동으로 제거하거나, DNS에서 자동으로 제거하도록 할 수 있습니다(DNS에서 청소 기능을 사용하도록 설정한 경우). 네트워크에서 DDNS를 사용하는 경우 새 KMS 호스트에서 새 SRV RR을 DNS 서버에 자동으로 만듭니다. 그러면 새 KMS 호스트에서 클라이언트 갱신 요청 수집을 시작하고, KMS 정품 인증 임계값이 충족되는 즉시 클라이언트 정품 인증을 시작합니다.

KMS 클라이언트에서 자동 검색을 사용하는 경우 원래 KMS 호스트에서 갱신 요청에 응답하지 않으면 다른 KMS 호스트를 자동으로 선택합니다. 클라이언트에서 자동 검색을 사용하지 않는 경우 **slmgr.vbs /skms**를 실행하여 오류가 발생한 KMS 호스트에 할당된 KMS 클라이언트 컴퓨터를 수동으로 업데이트해야 합니다. 이 시나리오를 방지하려면 자동 검색을 사용하도록 KMS 클라이언트를 구성합니다. 자세한 내용은 [볼륨 정품 인증 배포 가이드](https://go.microsoft.com/fwlink/?linkid=150083)를 참조하세요.
