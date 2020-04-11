---
title: MAK 정품 인증 알려진 문제
description: MAK 정품 인증 프로세스 중에 발생할 수 있는 일반적인 문제를 설명하고 해결 방법 및 지침을 제공합니다.
ms.topic: article
ms.date: 10/3/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 0f4153387d740379e66eca9e8069b7a446a1ec71
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826236"
---
# <a name="mak-activation-known-issues"></a>MAK 정품 인증: 알려진 문제

이 문서에서는 MAK(복수 정품 인증 키) 정품 인증 중에 발생할 수 있는 일반적인 문제를 설명하고 이러한 문제를 해결하기 위한 지침을 제공합니다.

## <a name="how-can-i-tell-whether-my-computer-is-activated"></a>내 컴퓨터가 활성화되었는지 어떻게 알 수 있나요?

컴퓨터에서 **System** 제어판을 열고 **Windows가 활성화됨**을 찾습니다. 또는 Slmgr.vbs를 실행하고 **/dli** 명령줄 옵션을 사용합니다.

## <a name="the-computer-does-not-activate-over-the-internet"></a>컴퓨터가 인터넷을 통해 활성화되지 않습니다.

필요한 포트가 방화벽에 열려 있는지 확인합니다. 포트 목록은 [볼륨 정품 인증 배포 가이드](https://go.microsoft.com/fwlink/?linkid=150083)를 참조하세요.

## <a name="internet-and-telephone-activation-fail"></a>인터넷 및 전화 정품 인증 실패

Microsoft 정품 인증 센터에 문의하세요. 전 세계 Microsoft 정품 인증 센터 전화 번호는 [Microsoft 라이선스 정품 인증 센터 전 세계 전화 번호](https://www.microsoft.com/Licensing/existing-customer/activation-centers)로 이동하세요. 호출할 때 볼륨 라이선스 계약 정보와 구매 증명서를 제공해야 합니다.

## <a name="slmgrvbs-ato-returns-an-error-code"></a>Slmgr.vbs /ato가 오류 코드를 반환합니다.

Slmgr.vbs가 16진수 오류 코드를 반환하면 다음 스크립트를 실행하여 해당 오류 메시지를 확인합니다.

```cmd
slui.exe 0x2a 0x <ErrorCode>
```

특정 오류 코드 및 이를 해결하는 방법에 대한 자세한 내용은 [일반 정품 인증 오류 코드 해결](activation-error-codes.md)을 참조하세요.
