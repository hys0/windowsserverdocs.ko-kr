---
title: tpmtool
description: Tpmtool에 대 한 Windows 명령 항목-신뢰할 수 있는 플랫폼 모듈에 대 한 정보를 가져옵니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: 3967136bc64d1e06425a019466dea15ddce3a563
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385722"
---
# <a name="tpmtool"></a>tpmtool

이 유틸리티는 [TPM (신뢰할 수 있는 플랫폼 모듈)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview)에 대 한 정보를 가져오는 데 사용할 수 있습니다.

>[!IMPORTANT]
>일부 정보는 상업용으로 출시되기 전에 상당 부분 수정될 수 있는 시험판 제품과 관련이 있습니다. Microsoft는 여기에 제공된 정보에 대해 명시적 또는 묵시적 보증을 하지 않습니다.

이 명령을 사용하는 방법의 예는 [예](#tpmtool_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
tpmtool /parameter [<arguments>]
```
## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|getdeviceinformation|TPM의 기본 정보를 표시 합니다. 정보 플래그 값의 의미는 [여기](https://docs.microsoft.com/windows/desktop/SecProv/win32-tpm-isreadyinformation#parameters)에서 찾을 수 있습니다.|
|gatherlogs [출력 디렉터리 경로]|TPM 로그를 수집 하 여 지정 된 디렉터리에 저장 합니다. 해당 디렉터리가 없으면 만들어집니다. 기본적으로 현재 디렉터리에 배치 됩니다. 생성 될 수 있는 파일은 다음과 같습니다. </br>-TpmEvents. .evtx</br>-TpmInformation .txt</br>-SRTMBoot .dat</br>-SRTMResume. .dat</br>-DRTMBoot .dat</br>-DRTMResume. .dat</br>|
|drivertracing [start/stop]|TPM 드라이버 추적 수집을 시작/중지 합니다. 추적 로그 인 TPMTRACE .etl이 생성 되 고 현재 디렉터리에 배치 됩니다.|
|parsetcglogs [-validate (-v)]|분석 된 TCG 로그 (Windows 부팅 구성 로그 (WBCL) 라고도 함)를 표시 합니다. 최신 이벤트 설명은 [TCG 웹 사이트](https://trustedcomputinggroup.org/resource/pc-client-specific-platform-firmware-profile-specification/)의 **이벤트 설명**에서 확인할 수 있습니다. @No__t-0 플래그가 설정 된 경우 TPM의 PCR (Platform Configuration Register) 값이 로그의 값과 일치 하는지 확인 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="tpmtool_examples"></a>예와

TPM의 기본 정보를 표시 하려면 다음을 입력 합니다.
```
tpmtool getdeviceinformation
```
TPM 로그를 수집 하 고 현재 디렉터리에 저장 하려면 다음을 입력 합니다.
```
tpmtool gatherlogs
```
TPM 로그를 수집 하 고 `C:\Users\Public`에 저장 하려면 다음을 입력 합니다.
```
tpmtool gatherlogs C:\Users\Public
```
TPM 드라이버 추적을 수집 하려면 다음을 입력 합니다.
```
tpmtool drivertracing start
# Run scenario
tpmtool drivertracing stop
```
TCG 로그를 구문 분석 하려면:
```
tpmtool parsetcglogs
```
TCG 로그를 구문 분석 하 고 PCRs의 유효성을 검사 하려면:
```
tpmtool parsetcglogs -validate
```

## <a name="decoding-error-codes"></a>오류 코드 디코딩

TPM 관련 오류 코드는 [여기](https://docs.microsoft.com/windows/desktop/com/com-error-codes-6)에 설명 되어 있습니다.
