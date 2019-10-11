---
title: Windows 정품 인증 오류 코드 해결
description: 정품 인증 오류 코드 문제를 해결하는 방법 알아보기
ms.topic: article
ms.date: 9/18/2019
ms.technology: server-general
ms.assetid: ''
author: kaushika-msft
ms.author: kaushika-msft; v-tea
ms.localizationpriority: medium
ms.openlocfilehash: 26b107264c9dfaca16ef445760089b8ac0ae8e22
ms.sourcegitcommit: 9855d6b59b1f8722f39ae74ad373ce1530da0ccf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71960967"
---
# <a name="resolve-windows-activation-error-codes"></a>Windows 정품 인증 오류 코드 해결

> **홈 사용자**  
> 이 문서는 지원 담당자 및 IT 전문가용으로 제작되었습니다. Windows 정품 인증 오류 메시지에 대한 자세한 정보를 찾고 있다면 [Windows 정품 인증 오류에 대한 도움말 보기](https://support.microsoft.com/help/10738/windows-10-get-help-with-activation-errors)를 참조하세요.  

이 문서에서는 MAK(복수 정품 인증 키) 또는 KMS(키 관리 서비스)를 사용하여 하나 이상의 Windows 기반 컴퓨터에서 볼륨 정품 인증을 수행할 때 발생할 수 있는 오류 메시지에 대처할 수 있도록 문제 해결 정보를 제공합니다. 다음 표에서 오류 코드를 찾은 다음, 링크를 선택하여 해당 오류 코드에 대한 자세한 내용과 오류 해결 방법을 확인하세요.

볼륨 정품 인증에 대한 자세한 내용은 [볼륨 정품 인증 계획](https://docs.microsoft.com/en-us/windows/deployment/volume-activation/plan-for-volume-activation-client)을 참조하세요.

현재 및 최신 버전 Windows의 볼륨 정품 인증에 대한 자세한 내용은 [볼륨 정품 인증[클라이언트]](https://docs.microsoft.com/windows/deployment/volume-activation/volume-activation-windows-10)을 참조하세요.

이전 버전 Windows의 볼륨 정품 인증에 대한 자세한 내용은 KB 929712  [Windows Vista, Windows Server 2008, Windows Server 2008 R2 및 Windows 7의 볼륨 정품 인증 정보](https://support.microsoft.com/en-us/help/929712/volume-activation-information-for-windows-vista-windows-server-2008-wi)를 참조하세요.

## <a name="summary-of-error-codes"></a>오류 코드 요약

|오류 코드 |오류 메시지 |Activation&nbsp;type|
|-----------|--------------|----------------|
|[0x8004FE21](#0x8004fe21-this-computer-is-not-running-genuine-windows) |이 컴퓨터가 정품 Windows를 실행하고 있지 않습니다.  |MAK<br />KMS 클라이언트 |
|[0x80070005](#0x80070005-access-denied) |액세스가 거부되었습니다. 요청한 작업에는 상승된 권한이 필요합니다. |MAK<br />KMS 클라이언트<br />KMS 호스트 |
|[0x8007007b](#0x8007007b-dns-name-does-not-exist) |0x8007007b DNS 이름이 없습니다. |KMS 클라이언트 |
|[0x80070490](#0x80070490-the-product-key-you-entered-didnt-work) |입력한 제품 키가 작동되지 않았습니다. 제품 키를 확인하고 다시 시도하거나 다른 제품 키를 입력하세요. |MAK |
|[0x800706BA](#0x800706ba-the-rpc-server-is-unavailable) |RPC 서버를 사용할 수 없습니다. |KMS 클라이언트 |
|[0x8007232A](#0x8007232a-dns-server-failure) |DNS 서버 오류  |KMS 호스트  |
|[0x8007232B](#0x8007232b-dns-name-does-not-exist) |DNS 이름이 없습니다. |KMS 클라이언트 |
|[0x8007251D](#0x8007251d-no-records-found-for-dns-query) |DNS 쿼리에 대한 레코드가 없습니다. |KMS 클라이언트 |
|[0x80092328](#0x80092328-dns-name-does-not-exist) |DNS 이름이 없습니다.  |KMS 클라이언트 |
|[0xC004B100](#0xc004b100-the-activation-server-determined-that-the-computer-could-not-be-activated) |정품 인증 서버에서 컴퓨터의 정품을 인증할 수 없는 것으로 확인되었습니다. |MAK |
|[0xC004C001](#0xc004c001-the-activation-server-determined-the-specified-product-key-is-invalid) |정품 인증 서버에서 지정한 제품 키가 잘못된 것으로 확인되었습니다. |MAK|
|[0xC004C003](#0xc004c003-the-activation-server-determined-the-specified-product-key-is-blocked) |정품 인증 서버에서 지정한 제품 키가 차단된 것으로 확인되었습니다. |MAK |
|[0xC004C008](#0xc004c008-the-activation-server-determined-that-the-specified-product-key-could-not-be-used) |정품 인증 서버에서 지정한 제품 키가 사용된 것으로 확인되었습니다. |KMS |
|[0xC004C020](#0xc004c020-the-activation-server-reported-that-the-multiple-activation-key-has-exceeded-its-limit) |정품 인증 서버에서 복수 정품 인증 키가 잠금 해제 제한을 초과한 것이 확인되었습니다. |MAK |
|[0xC004C021](#0xc004c021-the-activation-server-reported-that-the-multiple-activation-key-extension-limit-has-been-exceeded) |정품 인증 서버에서 MAK(복수 정품 인증 키) 연장 제한이 초과되었다고 보고했습니다. |MAK |
|[0xC004F009](#0xc004f009-the-software-protection-service-reported-that-the-grace-period-expired) |소프트웨어 보호 서비스에서 유예 기간이 만료되었다고 보고했습니다. |MAK |
|[0xC004F00F](#0xc004f00f-the-software-licensing-server-reported-that-the-hardware-id-binding-is-beyond-level-of-tolerance) |소프트웨어 라이선스 서버에서 하드웨어 ID 바인딩이 오차 허용 수준을 벗어났다고 보고했습니다. |MAK<br />KMS 클라이언트<br />KMS 호스트 |
|[0xC004F014](#0xc004f014-the-software-protection-service-reported-that-the-product-key-is-not-available) |소프트웨어 보호 서비스에서 제품 키를 사용할 수 없다고 보고했습니다. |MAK<br />KMS 클라이언트 |
|[0xC004F02C](#0xc004f02c-the-software-protection-service-reported-that-the-format-for-the-offline-activation-data-is-incorrect) |소프트웨어 보호 서비스에서 오프라인 정품 인증 데이터 형식이 잘못되었다고 보고했습니다. |MAK<br />KMS 클라이언트 |
|[0xC004F035](#0xc004f035-invalid-volume-license-key) |소프트웨어 보호 서비스에서 볼륨 라이선스 제품 키를 사용하여 컴퓨터의 정품을 인증할 수 없다고 보고했습니다. |KMS 클라이언트<br />KMS 호스트 |
|[0xC004F038](#0xc004f038-the-count-reported-by-your-key-management-service-kms-is-insufficient) |소프트웨어 보호 서비스에서 해당 컴퓨터를 정품 인증할 수 없다고 보고했습니다. KMS(키 관리 서비스)에서 반환한 수가 부족합니다. 시스템 관리자에게 문의하세요. |KMS 클라이언트 |
|[0xC004F039](#0xc004f039-the-key-management-service-kms-is-not-enabled) |소프트웨어 보호 서비스에서 해당 컴퓨터를 정품 인증할 수 없다고 보고했습니다. KMS(키 관리 서비스)를 사용하고 있지 않습니다. |KMS 클라이언트 |
|[0xC004F041](#0xc004f041-the-software-protection-service-determined-that-the-key-management-server-kms-is-not-activated) |소프트웨어 보호 서비스에서 KMS(키 관리 서비스)가 정품 인증되지 않은 것이 확인되었습니다. KMS를 활성화해야 합니다.  |KMS 클라이언트 |
|[0xC004F042](#0xc004f042-the-software-protection-service-determined-that-the-specified-key-management-service-kms-cannot-be-used) |소프트웨어 보호 서비스에서 지정된 KMS(키 관리 서비스)를 사용할 수 없음이 확인되었습니다. |KMS 클라이언트 |
|[0xC004F050](#0xc004f050-the-software-protection-service-reported-that-the-product-key-is-invalid) |소프트웨어 보호 서비스에서 제품 키가 잘못되었다고 보고했습니다. |MAK<br />KMS<br />KMS 클라이언트 |
|[0xC004F051](#0xc004f051-the-software-protection-service-reported-that-the-product-key-is-blocked) |소프트웨어 보호 서비스에서 제품 키가 차단되었다고 보고했습니다. |MAK<br />KMS |
|[0xC004F064](#0xc004f064-the-software-protection-service-reported-that-the-non-genuine-grace-period-expired) |소프트웨어 보호 서비스에서 비정품 유예 기간이 만료되었다고 보고했습니다. |MAK |
|[0xC004F065](#0xc004f065-the-software-protection-service-reported-that-the-application-is-running-within-the-valid-non-genuine-period) |소프트웨어 보호 서비스에서 애플리케이션이 비정품 유효 기간 내에서 실행되고 있다고 보고했습니다. |MAK<br />KMS 클라이언트 |
|[0xC004F06C](#0xc004f06c-the-request-timestamp-is-invalid) |소프트웨어 보호 서비스에서 해당 컴퓨터를 정품 인증할 수 없다고 보고했습니다. KMS(키 관리 서비스)에서 요청 타임스탬프가 잘못된 것으로 확인되었습니다.  |KMS 클라이언트 |
|[0xC004F074](#0xc004f074-no-key-management-service-kms-could-be-contacted) |소프트웨어 보호 서비스에서 해당 컴퓨터를 정품 인증할 수 없다고 보고했습니다. 연결할 수 있는 KMS(키 관리 서비스)가 없습니다. 자세한 내용은 응용 프로그램 이벤트 로그를 참조하세요.  |KMS 클라이언트 |

## <a name="causes-and-resolutions"></a>원인 및 해결 방법

### <a name="0x8004fe21-this-computer-is-not-running-genuine-windows"></a>0x8004FE21 이 컴퓨터가 정품 Windows를 실행하고 있지 않습니다.  

#### <a name="possible-cause"></a>가능한 원인

이 이슈는 여러 가지 이유로 발생할 수 있습니다. 가장 가능성이 높은 이유는 추가 언어 팩에 대한 라이선스가 부여되지 않은 Windows 버전을 실행 중인 컴퓨터에 언어 팩(MUI)이 설치된 것입니다.  

> [!NOTE]
> 이 이슈가 반드시 변조를 나타내는 것은 아닙니다. 일부 애플리케이션은 해당 Windows 버전에 이러한 언어 팩에 대한 라이선스가 부여되지 않은 경우에도 다국어 지원을 설치할 수 있습니다.  

Windows가 맬웨어에 의해 추가 기능 설치를 허용하도록 수정된 경우에도 이 이슈가 발생할 수 있습니다. 특정 시스템 파일이 손상된 경우에도 이 문제가 발생할 수 있습니다.  

#### <a name="resolution"></a>해상도

이 이슈를 해결하려면 운영 체제를 다시 설치해야 합니다.  

### <a name="0x80070005-access-denied"></a>0x80070005 액세스 거부됨

이 오류 메시지의 전체 텍스트는 다음과 비슷합니다.

> 액세스가 거부되었습니다. 요청한 작업에는 상승된 권한이 필요합니다.

#### <a name="possible-cause"></a>가능한 원인

UAC(사용자 계정 컨트롤)에 의해 낮은 권한의 명령 프롬프트 창에서 정품 인증 프로세스를 실행하는 것이 금지되었습니다.  

#### <a name="resolution"></a>해상도

관리자 권한 명령 프롬프트에서 **slmgr.vbs** 명령을 실행하세요. 이렇게 하려면 **시작 메뉴**에서 **cmd.exe**를 마우스 오른쪽 단추로 클릭한 다음, **관리자 권한으로 실행**을 선택합니다.  

### <a name="0x8007007b-dns-name-does-not-exist"></a>0x8007007b DNS 이름이 없습니다.

#### <a name="possible-cause"></a>가능한 원인

KMS 클라이언트가 DNS에서 KMS SRV 리소스 레코드를 찾을 수 없으면 이 이슈가 발생할 수 있습니다.  

#### <a name="resolution"></a>해상도

DNS 관련 이슈 같은 문제 해결 방법에 대한 자세한 내용은 [KMS 및 DNS 이슈에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.  

### <a name="0x80070490-the-product-key-you-entered-didnt-work"></a>0x80070490 입력한 제품 키가 작동하지 않습니다.

이 오류의 전체 텍스트는 다음과 비슷합니다.
> 입력한 제품 키가 작동하지 않습니다. 제품 키를 확인하고 다시 시도하거나 다른 제품 키를 입력하세요.  

#### <a name="possible-cause"></a>가능한 원인

이 이슈는 잘못된 MAK를 입력한 경우 또는 Windows Server 2019의 알려진 이슈로 인해 발생합니다.  

#### <a name="resolution"></a>해상도

이 이슈를 해결하고 컴퓨터를 정품 등록하려면 관리자 권한 명령 프롬프트에서 **slmgr -ipk <5x5 key>** 를 실행합니다.

### <a name="0x800706ba-the-rpc-server-is-unavailable"></a>0x800706BA RPC 서버를 사용할 수 없음

#### <a name="possible-cause"></a>가능한 원인

방화벽 설정이 KMS 호스트에 구성되어 있지 않거나 DNS SRV 레코드가 부실합니다.  

#### <a name="resolution"></a>해상도

KMS 호스트에서 키 관리 서비스에 방화벽 예외가 적용되었는지 확인하세요(TCP 포트 1688).

DNS SRV 레코드가 유효한 KMS 호스트를 가리키는지 확인하세요. 

네트워크 연결 문제를 해결하십시오.  

DNS 관련 이슈 같은 문제 해결 방법에 대한 자세한 내용은 [KMS 및 DNS 이슈에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.  

### <a name="0x8007232a-dns-server-failure"></a>0x8007232A DNS 서버 오류

#### <a name="possible-cause"></a>가능한 원인

시스템에 네트워크 또는 DNS 문제가 있습니다.

#### <a name="resolution"></a>해상도

네트워크 및 DNS 문제를 해결하세요.  

### <a name="0x8007232b-dns-name-does-not-exist"></a>0x8007232B DNS 이름이 없음

#### <a name="possible-cause"></a>가능한 원인

KMS 클라이언트가 DNS에서 KMS 서버 리소스 레코드(SRV RR)를 찾을 수 없습니다.  

#### <a name="resolution"></a>해상도

KMS 호스트가 설치되어 있고 DNS 게시가 사용되는지(기본값) 확인하세요. DNS를 사용할 수 없는 경우 **slmgr.vbs /skms <*kms_host_name*>** 명령을 사용하여 KMS 호스트를 가리키도록 KMS 클라이언트를 설정하세요.  

KMS 호스트가 없으면 MAK를 다운로드하여 설치합니다. 그런 다음, 시스템을 활성화합니다.

DNS 관련 이슈 같은 문제 해결 방법에 대한 자세한 내용은 [KMS 및 DNS 이슈에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.  

### <a name="0x8007251d-no-records-found-for-dns-query"></a>0x8007251D DNS 쿼리에 대한 레코드가 없음

#### <a name="possible-cause"></a>가능한 원인

KMS 클라이언트가 DNS에서 KMS SRV 레코드를 찾을 수 없습니다.

#### <a name="resolution"></a>해상도

네트워크 연결 및 DNS 문제를 해결하세요. DNS 관련 이슈 해결 방법에 대한 자세한 내용은 [KMS 및 DNS 이슈에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.  

### <a name="0x80092328-dns-name-does-not-exist"></a>0x80092328 DNS 이름이 없습니다.

#### <a name="possible-cause"></a>가능한 원인

KMS 클라이언트가 DNS에서 KMS SRV 리소스 레코드를 찾을 수 없으면 이 이슈가 발생할 수 있습니다.

#### <a name="resolution"></a>해상도

DNS 관련 이슈 같은 문제 해결 방법에 대한 자세한 내용은 [KMS 및 DNS 이슈에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.  

### <a name="0xc004b100-the-activation-server-determined-that-the-computer-could-not-be-activated"></a>0xC004B100 정품 인증 서버에서 컴퓨터의 정품을 인증할 수 없는 것으로 확인되었습니다.

#### <a name="possible-cause"></a>가능한 원인

MAK가 지원되지 않습니다.  

#### <a name="resolution"></a>해상도

이 이슈를 해결하려면 사용하는 MAK가 Microsoft에서 제공한 것인지 확인하세요. MAK가 유효한지 확인하려면 [Microsoft 라이선싱 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하세요.

### <a name="0xc004c001-the-activation-server-determined-the-specified-product-key-is-invalid"></a>0xC004C001 정품 인증 서버에서 지정한 제품 키가 잘못된 것으로 확인되었습니다.

#### <a name="possible-cause"></a>가능한 원인

입력한 MAK가 유효하지 않습니다.

#### <a name="resolution"></a>해상도

키가 Microsoft에서 제공한 MAK인지 확인하세요. 추가 도움이 필요하면 [Microsoft 라이선싱 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하세요.

### <a name="0xc004c003-the-activation-server-determined-the-specified-product-key-is-blocked"></a>0xC004C003 정품 인증 서버에서 지정한 제품 키가 차단된 것으로 확인되었습니다.

#### <a name="possible-cause"></a>가능한 원인

MAK가 정품 인증 서버에서 차단되었습니다.

#### <a name="resolution"></a>해상도

새 MAK를 얻으려면 [Microsoft 라이선싱 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하세요. 새 MAK를 얻은 후 Windows를 다시 설치하고 정품 인증을 시도하세요.  

### <a name="0xc004c008-the-activation-server-determined-that-the-specified-product-key-could-not-be-used"></a>0xC004C008 정품 인증 서버에서 지정한 제품 키가 사용된 것으로 확인되었습니다.

#### <a name="possible-cause"></a>가능한 원인

KMS 키가 정품 인증 제한을 초과했습니다. KMS 호스트 키는 최대 6대의 컴퓨터에서 최대 10번까지 정품 인증할 수 있습니다.  

#### <a name="resolution"></a>해상도

추가 정품 인증이 필요하면 [Microsoft 라이선싱 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하세요.  

### <a name="0xc004c020-the-activation-server-reported-that-the-multiple-activation-key-has-exceeded-its-limit"></a>0xC004C020 정품 인증 서버에서 복수 정품 인증 키가 잠금 해제 제한을 초과한 것이 확인되었습니다.

#### <a name="possible-cause"></a>가능한 원인

MAK가 정품 인증 제한을 초과했습니다. 기본적으로 MAK는 정품 인증 횟수가 제한되어 있습니다.

#### <a name="resolution"></a>해상도

추가 정품 인증이 필요하면 [Microsoft 라이선싱 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하세요.

### <a name="0xc004c021-the-activation-server-reported-that-the-multiple-activation-key-extension-limit-has-been-exceeded"></a>0xC004C021 정품 인증 서버에서 복수 정품 인증 키 연장 제한이 초과되었다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

MAK가 정품 인증 제한을 초과했습니다. 기본적으로 MAK는 제한된 횟수만큼 정품 인증할 수 있습니다.

#### <a name="resolution"></a>해상도

추가 정품 인증이 필요하면 [Microsoft 라이선싱 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하세요.

### <a name="0xc004f009-the-software-protection-service-reported-that-the-grace-period-expired"></a>0xC004F009 소프트웨어 보호 서비스에서 유예 기간이 만료되었다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

소프트웨어가 정품 인증되기 전에 유예 기간이 만료되었습니다. 이제 시스템이 알림 상태입니다.  

#### <a name="resolution"></a>해상도

도움이 필요하면 [Microsoft 라이선스 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하세요.

### <a name="0xc004f00f-the-software-licensing-server-reported-that-the-hardware-id-binding-is-beyond-level-of-tolerance"></a>0xC004F00F 소프트웨어 라이선스 서버에서 하드웨어 ID 바인딩이 오차 허용 수준을 벗어났다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

하드웨어가 변경되거나 드라이버가 시스템에서 업데이트되었습니다.  

#### <a name="resolution"></a>해상도

MAK 정품 인증을 사용하는 경우 온라인 또는 전화 정품 인증을 사용하여 OOT 유예 기간 동안 시스템을 다시 정품 인증합니다.  

KMS 정품 인증을 사용하는 경우 Windows를 다시 시작하거나 **slmgr.vbs /ato** 명령을 실행합니다.

### <a name="0xc004f014-the-software-protection-service-reported-that-the-product-key-is-not-available"></a>0xC004F014 소프트웨어 보호 서비스에서 제품 키를 사용할 수 없다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

시스템에 설치된 제품 키가 없습니다.  

#### <a name="resolution"></a>해상도

MAK 정품 인증을 사용하는 경우 MAK 제품 키를 설치합니다. 

KMS 정품 인증을 사용하는 경우 KMS 설치 키의 Pid.txt 파일(\sources 폴더의 설치 미디어에 있음)을 확인합니다. 키를 설치합니다.

### <a name="0xc004f02c-the-software-protection-service-reported-that-the-format-for-the-offline-activation-data-is-incorrect"></a>0xC004F02C 소프트웨어 보호 서비스에서 오프라인 정품 인증 데이터 형식이 잘못되었다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

시스템에서 전화 정품 인증 중에 입력된 데이터가 유효하지 않은 것을 감지했습니다.  

#### <a name="resolution"></a>해상도

CID를 올바르게 입력했는지 확인하세요.  

### <a name="0xc004f035-invalid-volume-license-key"></a>0xC004F035 잘못된 볼륨 라이선스 키

이 오류 메시지의 전체 텍스트는 다음과 비슷합니다.

> 오류: 볼륨 라이선스 키가 유효하지 않습니다. 정품을 인증하려면 제품 키를 유효한 MAK(복수 정품 인증 키) 또는 정품 키로 변경해야 합니다. 적격 운영 체제 라이선스와 볼륨 라이선스 Windows 7 업그레이드 라이선스 또는 소매점의 Windows 7 정품 라이선스가 있어야 합니다. 이 소프트웨어의 다른 모든 설치는 계약 및 관련 저작권 법에 위배됩니다.  

오류 텍스트가 올바르지만 모호합니다. 이 오류는 컴퓨터에 Windows의 정식 버전을 실행 중인 OEM 시스템으로 식별되는 Windows 마커가 BIOS에 누락되었음을 나타냅니다. 이 정보는 KMS 클라이언트 정품 인증에 필요합니다. 이 코드의 보다 구체적인 의미는 "오류: 잘못된 볼륨 라이선스 키"입니다.

#### <a name="possible-cause"></a>가능한 원인

Windows 7 볼륨 버전은 업그레이드용으로만 라이선스가 부여됩니다. 적격 운영 체제가 설치되지 않은 컴퓨터에는 볼륨 운영 체제를 설치할 수 없습니다.  

#### <a name="resolution"></a>해상도

활성화하려면 다음 중 하나를 수행해야 합니다.

- 제품 키를 유효한 MAK(복수 정품 인증 키) 또는 정품 키로 변경해야 합니다. 적격 운영 체제 라이선스와 볼륨 라이선스 Windows 7 업그레이드 라이선스 또는 소매점의 Windows 7 정품 라이선스가 있어야 합니다.
  > [!NOTE]
  > 활성화하려고 할 때 0x80072ee2 오류 메시지가 표시되면 뒤에 나오는 전화 정품 인증 방법을 사용합니다.
- 다음 단계를 수행하여 전화로 활성화합니다.
   1. **slmgr /dti**를 실행한 다음, 설치 ID의 값을 기록합니다. </li>
   1. 확인 ID를 받으려면 [Microsoft 라이선싱 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하여 설치 ID를 제공합니다.</li>
   1. 확인 ID를 사용하여 활성화하려면 **slmgr/atp &lt;확인 ID&gt;** 를 실행합니다.

### <a name="0xc004f038-the-count-reported-by-your-key-management-service-kms-is-insufficient"></a>0xC004F038 KMS(키 관리 서비스)에서 반환한 수가 부족합니다.

이 오류 메시지의 전체 텍스트는 다음과 비슷합니다.

> 소프트웨어 보호 서비스에서 해당 컴퓨터를 정품 인증할 수 없다고 보고했습니다. KMS(키 관리 서비스)에서 반환한 수가 부족합니다. 시스템 관리자에게 문의하세요.  

#### <a name="possible-cause"></a>가능한 원인

KMS 호스트의 수가 적습니다. Windows Server의 경우 KMS 수가 5보다 크거나 같아야 합니다. Windows(클라이언트)의 경우 KMS 수가 25보다 크거나 같아야 합니다.  

#### <a name="resolution"></a>해상도
KMS를 사용하여 Windows를 정품 인증하려면 KMS 풀에 더 많은 컴퓨터가 있어야 합니다. KMS 호스트의 현재 수를 확인하려면 **Slmgr.vbs /dli** 명령을 실행합니다.  

### <a name="0xc004f039-the-key-management-service-kms-is-not-enabled"></a>0xC004F039 KMS(키 관리 서비스)를 사용하고 있지 않습니다.

이 오류 메시지의 전체 텍스트는 다음과 비슷합니다.

> 소프트웨어 보호 서비스에서 해당 컴퓨터를 정품 인증할 수 없다고 보고했습니다. KMS(키 관리 서비스)를 사용하고 있지 않습니다.  

#### <a name="possible-cause"></a>가능한 원인

KMS가 KMS 요청에 응답하지 않았습니다.

#### <a name="resolution"></a>해상도

KMS 호스트와 클라이언트 간의 네트워크 연결 문제를 해결하세요. TCP 포트 1688(기본값)이 방화벽으로 차단되거나 다른 방식으로 필터링되지 않는지 확인하세요.

### <a name="0xc004f041-the-software-protection-service-determined-that-the-key-management-server-kms-is-not-activated"></a>0xC004F041 소프트웨어 보호 서비스에서 KMS(키 관리 서비스)가 활성화되지 않은 것이 확인되었습니다.

이 오류 메시지의 전체 텍스트는 다음과 비슷합니다.

> 소프트웨어 보호 서비스에서 KMS(키 관리 서비스)가 정품 인증되지 않은 것이 확인되었습니다. KMS를 활성화해야 합니다.  

#### <a name="possible-cause"></a>가능한 원인

KMS 호스트가 정품 인증되지 않았습니다.  

#### <a name="resolution"></a>해상도

온라인 또는 전화 정품 인증을 통해 KMS 호스트를 정품 인증하세요.  

### <a name="0xc004f042-the-software-protection-service-determined-that-the-specified-key-management-service-kms-cannot-be-used"></a>0xC004F042 소프트웨어 보호 서비스에서 지정된 KMS(키 관리 서비스)를 사용할 수 없는 것으로 확인되었습니다.

#### <a name="possible-cause"></a>가능한 원인

KMS 클라이언트가 클라이언트 소프트웨어를 정품 인증할 수 없는 KMS 호스트에 연결하면 이 오류가 발생합니다. 예를 들어 애플리케이션 및 운영 체제별 KMS 호스트를 포함하는 혼합 환경에서 이 오류가 주로 발생할 수 있습니다.  

#### <a name="resolution"></a>해상도

특정 KMS 호스트를 사용하여 특정 애플리케이션 또는 운영 체제를 정품 인증하는 경우 KMS 클라이언트가 올바른 호스트에 연결하도록 주의해야 합니다.

### <a name="0xc004f050-the-software-protection-service-reported-that-the-product-key-is-invalid"></a>0xC004F050 소프트웨어 보호 서비스에서 제품 키가 잘못되었다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

KMS 키를 잘못 입력하거나 정식 버전의 운영 체제에서 베타 키를 입력한 경우에 발생할 수 있습니다.  

#### <a name="resolution"></a>해상도

해당 Windows 버전에 적절한 KMS 키를 설치하세요. 맞춤법을 검사하세요. 키를 복사하여 붙여넣는 경우 키의 하이픈이 em 대시로 대체되지 않았는지 확인하세요.  

### <a name="0xc004f051-the-software-protection-service-reported-that-the-product-key-is-blocked"></a>0xC004F051 소프트웨어 보호 서비스에서 제품 키가 차단되었다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

정품 인증 서버의 확인 결과, Microsoft에서 제품 키를 차단한 것으로 확인되었습니다.  

#### <a name="resolution"></a>해상도

새 MAK 또는 KMS 키를 받아서 시스템에 설치하고 정품 인증하세요.

### <a name="0xc004f064-the-software-protection-service-reported-that-the-non-genuine-grace-period-expired"></a>0xC004F064 소프트웨어 보호 서비스에서 비정품 유예 기간이 만료되었다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

WAT(Windows 정품 인증 도구)에서 시스템이 정품이 아님을 확인했습니다.  

#### <a name="resolution"></a>해상도

도움이 필요하면 [Microsoft 라이선스 정품 인증 센터](https://www.microsoft.com/en-us/Licensing/existing-customer/activation-centers)에 문의하세요.

### <a name="0xc004f065-the-software-protection-service-reported-that-the-application-is-running-within-the-valid-non-genuine-period"></a>0xC004F065 소프트웨어 보호 서비스에서 애플리케이션이 비정품 유효 기간 내에서 실행되고 있다고 보고했습니다.

#### <a name="possible-cause"></a>가능한 원인

Windows 정품 인증 도구에서 시스템이 정품이 아님을 확인했습니다. 비정품 유예 기간 동안 시스템이 계속 실행됩니다.  

#### <a name="resolution"></a>해상도

유예 기간 동안 정품 제품 키를 받아서 설치하고 시스템을 정품 인증하세요. 그렇지 않으면 시스템이 유예 기간 종료 후 알림 상태로 전환됩니다.

### <a name="0xc004f06c-the-request-timestamp-is-invalid"></a>0xC004F06C 요청 타임스탬프가 잘못되었습니다.

이 오류 메시지의 전체 텍스트는 다음과 비슷합니다.

> 소프트웨어 보호 서비스에서 해당 컴퓨터를 정품 인증할 수 없다고 보고했습니다. KMS(키 관리 서비스)에서 요청 타임스탬프가 잘못된 것으로 확인되었습니다.  

#### <a name="possible-cause"></a>가능한 원인

클라이언트 컴퓨터의 시스템 시간이 KMS 호스트의 시간과 너무 다릅니다. 시간 동기화는 여러 가지 이유로 시스템 및 네트워크 보안에 중요합니다.  

#### <a name="resolution"></a>해상도

KMS 호스트와 동기화되도록 클라이언트의 시스템 시간을 변경하여 이 이슈를 해결하세요. NTP(네트워크 시간 프로토콜) 시간 원본 또는 Active Directory Domain Services를 사용하여 시간을 동기화하는 것이 좋습니다. 이 이슈는 UTP 시간을 사용하며 선택한 표준 시간대와 무관합니다.  

### <a name="0xc004f074-no-key-management-service-kms-could-be-contacted"></a>0xC004F074 연결할 수 있는 KMS(키 관리 서비스)가 없음

이 오류 메시지의 전체 텍스트는 다음과 비슷합니다.

> 소프트웨어 보호 서비스에서 해당 컴퓨터를 정품 인증할 수 없다고 보고했습니다. 연결할 수 있는 KMS(키 관리 서비스)가 없습니다. 자세한 내용은 응용 프로그램 이벤트 로그를 참조하세요.  

#### <a name="possible-cause"></a>가능한 원인

모든 KMS 호스트 시스템에서 오류를 반환했습니다.  

#### <a name="resolution"></a>해상도

애플리케이션 이벤트 로그에서, 이벤트 ID가 12288이고 정품 등록 시도와 연결된 각 이벤트를 확인합니다. 이러한 이벤트의 오류를 해결합니다.

DNS 관련 이슈 해결 방법에 대한 자세한 내용은 [KMS 및 DNS 이슈에 대한 일반적인 문제 해결 절차](common-troubleshooting-procedures-kms-dns.md)를 참조하세요.  
