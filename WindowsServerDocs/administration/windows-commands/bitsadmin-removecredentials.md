---
title: bitsadmin removecredentials
description: 작업에서 자격 증명을 제거 하는 bitsadmin **removecredentials**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4a78ce9a-1feb-4811-a000-cce81287b22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55ff7e2a813c7cc6b60e04d55ef63804a2aed796
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849846"
---
# <a name="bitsadmin-removecredentials"></a>bitsadmin removecredentials

작업에서 자격 증명을 제거 합니다.

> [!NOTE]
> 이 명령은 BITS 1.2 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /removecredentials <job> <target> <scheme>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| target | **서버** 또는 **프록시**를 사용 합니다. |
| scheme | 다음 중 하나를 사용 합니다.<ul><li>**기본.** 사용자 이름 및 암호가 일반 텍스트로 서버나 프록시로 전송 되는 인증 체계입니다.</li><li>**이해할.** 챌린지에 대해 서버 지정 데이터 문자열을 사용 하는 챌린지-응답 인증 체계입니다.</li><li>**N.** Windows 네트워크 환경에서 인증을 위해 사용자의 자격 증명을 사용 하는 챌린지-응답 인증 체계입니다.</li><li>**negotiate (단순 및 보호 된 협상 프로토콜이 라고도 함)** 인증에 사용할 체계를 결정 하기 위해 서버 또는 프록시와 협상 하는 챌린지-응답 인증 체계입니다. 이러한 예로는 Kerberos 프로토콜 및 NTLM이 있습니다.</li><li>**passport.** Microsoft에서 제공 하는 중앙 집중식 인증 서비스로, 구성원 사이트에 대해 단일 로그온을 제공 합니다.</li></ul> |

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예에서는 *Mydownloadjob*이라는 작업에서 자격 증명을 제거 합니다.

```
C:\>bitsadmin /removecredentials myDownloadJob server basic
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)