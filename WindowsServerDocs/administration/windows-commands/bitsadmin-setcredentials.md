---
title: bitsadmin setcredentials
description: 작업에 자격 증명을 추가 하는 bitsadmin setcredentials 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e28bf17812335e55db0ae8c5ddd54c418dcb2d66
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927862"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

작업에 자격 증명을 추가 합니다.

> [!NOTE]
> 이 명령은 BITS 1.2 이전 버전에서는 지원 되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /setcredentials <job> <target> <scheme> <username> <password>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| 대상 | **서버** 또는 **프록시**를 사용 합니다. |
| scheme | 다음 중 하나를 사용합니다.<ul><li>**기본.** 사용자 이름 및 암호가 일반 텍스트로 서버나 프록시로 전송 되는 인증 체계입니다.</li><li>**이해할.** 챌린지에 대해 서버 지정 데이터 문자열을 사용 하는 챌린지-응답 인증 체계입니다.</li><li>**N.** Windows 네트워크 환경에서 인증을 위해 사용자의 자격 증명을 사용 하는 챌린지-응답 인증 체계입니다.</li><li>**NEGOTIATE (단순 및 보호 된 협상 프로토콜이 라고도 함)** 인증에 사용할 체계를 결정 하기 위해 서버 또는 프록시와 협상 하는 챌린지-응답 인증 체계입니다. 이러한 예로는 Kerberos 프로토콜 및 NTLM이 있습니다.</li><li>**PASSPORT.** Microsoft에서 제공 하는 중앙 집중식 인증 서비스로, 구성원 사이트에 대해 단일 로그온을 제공 합니다.</li></ul> |
| 사용자_이름 | 사용자의 이름입니다. |
| password | 제공 된 *사용자 이름과*연결 된 암호입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 작업에 자격 증명을 추가 하려면 다음을 수행 합니다.

```
bitsadmin /setcredentials myDownloadJob SERVER BASIC Edward password20
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
