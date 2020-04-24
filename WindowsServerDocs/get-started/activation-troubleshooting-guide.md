---
title: Windows 볼륨 정품 인증 문제 해결
description: 볼륨 정품 인증에 대한 모범 사례 및 정품 인증 문제 해결에 대한 정보를 제공하는 리소스를 나열합니다.
ms.topic: troubleshooting
ms.date: 09/24/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 09206b90dc8b829aaa70d0cca34bd05a9e0eb693
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "71963049"
---
# <a name="troubleshooting-windows-volume-activation"></a>Windows 볼륨 정품 인증 문제 해결

제품 정품 인증은 특정 컴퓨터에 소프트웨어를 설치한 후 소프트웨어의 유효성을 검사하는 프로세스입니다. 정품 인증에서는 제품이 정품인지(불법 복사본이 아닌지) 확인하고 제품 키 또는 일련 번호가 유효하며 손상되었거나 해지되지 않았는지 확인합니다. 정품 인증에서는 제품 키와 설치 간 링크 또는 관계도 설정합니다.

볼륨 정품 인증은 볼륨 사용이 허가된 제품을 활성화하는 프로세스입니다. 볼륨 라이선스 고객이 되려면 조직이 Microsoft와 볼륨 라이선싱 계약을 맺어야 합니다. Microsoft는 조직의 크기 및 구매 기본 설정을 수용할 수 있게 사용자 지정된 볼륨 라이선싱 프로그램을 제공합니다. 자세한 내용은 [Microsoft 볼륨 라이선싱 서비스 센터](https://www.microsoft.com/Licensing/servicecenter/default.aspx)를 참조하세요.

[Windows Server 2016 정품 인증 가이드](server-2016-activation.md)는 KMS(키 관리 서비스) 정품 인증 기술에 중점을 둡니다. 이 섹션에서는 일반적인 문제를 해결하고 KMS 및 기타 여러 볼륨 정품 인증 기술에 대한 문제 해결 지침을 제공합니다.

## <a name="best-practices-for-volume-activation"></a>볼륨 정품 인증에 대한 모범 사례

다음 문서에서는 Microsoft의 볼륨 정품 인증 기술에 대한 기술 정보와 모범 사례를 제공합니다.

### <a name="key-management-service-kms"></a>KMS(키 관리 서비스)

- [볼륨 정품 인증 계획](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)
- [KMS 이해](https://docs.microsoft.com/previous-versions/tn-archive/ff793434(v=technet.10))
- [KMS 정품 인증 배포](https://docs.microsoft.com/previous-versions/tn-archive/ff793409%28v=technet.10%29)
- [KMS 호스트 구성](https://docs.microsoft.com/previous-versions/tn-archive/ff793407%28v%3dtechnet.10%29)
- [DNS 구성](https://docs.microsoft.com/previous-versions/tn-archive/ff793405%28v%3dtechnet.10%29)
- [키 관리 서비스를 사용하여 정품 인증](https://docs.microsoft.com/windows/deployment/volume-activation/activate-using-key-management-service-vamt)

### <a name="active-directory-based-activation-adba"></a>ADBA(Active Directory 기반 정품 인증)

- [Active Directory 기반 정품 인증 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn502534%28v%3Dws.11%29)
- [Active Directory 기반 정품 인증을 사용하여 정품 인증](https://docs.microsoft.com/windows/deployment/volume-activation/activate-using-active-directory-based-activation-client)
- [Active Directory 기반 정품 인증 개요](https://docs.microsoft.com/windows/deployment/volume-activation/active-directory-based-activation-overview)

### <a name="multiple-activation-key-mak-activation"></a>MAK(복수 정품 인증 키) 정품 인증

- [MAK 정품 인증 사용](https://docs.microsoft.com/previous-versions/tn-archive/ff793438%28v=technet.10%29)
- [MAK 정품 인증 이해](https://docs.microsoft.com/previous-versions/tn-archive/ff793435%28v%3dtechnet.10%29)
- [MAK 클라이언트 활성화](https://docs.microsoft.com/previous-versions/tn-archive/ff793398%28v%3dtechnet.10%29)

### <a name="subscription-activation"></a>구독 정품 인증

- [Windows 10 구독 정품 인증](https://docs.microsoft.com/windows/deployment/windows-10-subscription-activation)
- [Windows 10 Enterprise 라이선스 배포](https://docs.microsoft.com/windows/deployment/deploy-enterprise-licenses)
- [CSP의 Windows 10 Enterprise E3](https://docs.microsoft.com/windows/deployment/windows-10-enterprise-e3-overview)

## <a name="resources-for-troubleshooting-activation-issues"></a>정품 인증 문제 해결을 위한 리소스

다음 문서에서는 볼륨 정품 인증 문제 해결을 위한 도구에 대한 지침 및 정보를 제공합니다.

- [KMS(키 관리 서비스) 문제 해결에 대한 지침](activation-troubleshoot-kms-general.md)
- [볼륨 정품 인증 정보를 얻기 위한 Slmgr.vbs 옵션](activation-slmgr-vbs-options.md)
- [예제: 활성화되지 않은 ADBA 클라이언트 문제 해결](activation-troubleshoot-adba-clients.md)

다음 문서에서는 보다 구체적인 정품 인증 문제를 해결하기 위한 지침을 제공합니다.

- [일반 정품 인증 오류 코드 해결](activation-error-codes.md)
- [KMS 정품 인증: 알려진 문제](activation-troubleshoot-KMS-issues.md)
- [MAK 정품 인증: 알려진 문제](activation-troubleshoot-MAK-issues.md)
- [DNS 관련 정품 인증 문제 해결을 위한 지침](common-troubleshooting-procedures-kms-dns.md)
- [Tokens.dat 파일을 다시 빌드하는 방법](activation-rebuild-tokens-dat-file.md)
