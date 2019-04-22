---
title: 관리 bde 잠금 해제
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a86267890449be2048221940e5955e49f30f99f3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814604"
---
# <a name="manage-bde-unlock"></a>관리 bde: 잠금 해제



복구 암호 또는 복구 키를 사용 하 여 BitLocker 보호 드라이브를 잠금 해제 합니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
manage-bde -unlock {-recoverypassword <Password>|-recoverykey <PathToExternalKeyFile>} <Drive> [-certificate {-cf PathToCertificateFile | -ct CertificateThumbprint} {-pin}] [-password] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

|매개 변수|값|설명|
|---------|-----|-----------|
|-recoverypassword||복구 암호를 드라이브의 잠금을 해제 하는 것을 지정 합니다. Rp 약어:|
||\<Password>|드라이브를 잠금 해제를 사용할 수 있는 복구 암호를 나타냅니다.|
|-recoverykey||외부 복구 키 파일의 드라이브 잠금을 해제 하는 것을 지정 합니다. 약어: 날짜별|
||\<PathToExternalKeyFile>|드라이브를 잠금 해제를 사용할 수 있는 외부 복구 키 파일을 나타냅니다.|
||\<Drive>|드라이브 문자를 뒤에 콜론을 나타냅니다.|
|-인증서||Unclock 볼륨에 BitLocker 인증서에 대 한 로컬 사용자 인증서는 locat 사용자 인증서 저장소에 있습니다. 약어:-인증서|
||<-cf PathToCertificateFile >|Cerficate 파일 경로|
||<-ct CertificateThumbprint >|PIN을 선택적으로 포함할 수 있는 인증서 지문 (-핀).|
|-암호||볼륨의 잠금을 해제 하려면 암호에 대 한 프롬프트를 표시 합니다. Pw 약어:|
|-computername||다른 컴퓨터에서 BitLocker 보호를 수정 하려면 bde.exe 사용될지를 지정 합니다. 약어:-cn|
||\<이름 >|BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.|
|-? 또는 /?||도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h||명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="BKMK_Examples"></a>예제

다음 예제를 사용 하는 **-잠금 해제** 다른 드라이브에 백업 폴더에 저장 된 복구 키 파일과 함께 E 드라이브를 잠금 해제 하는 명령입니다.
```
manage-bde –unlock E: -recoverykey "F:\Backupkeys\recoverykey.bek"
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)