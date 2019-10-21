---
title: rdpsign
description: RDP 파일에 디지털 서명 하는 방법에 대해 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a6fa8ce-3d32-49a5-b056-bcc1a23391f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 406563a07d3760c2846c201410f3a7b8f1c2829b
ms.sourcegitcommit: b7f55949f166554614f581c9ddcef5a82fa00625
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72588053"
---
# <a name="rdpsign"></a>rdpsign

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디지털 방식으로 원격 데스크톱 프로토콜 (.rdp) 파일에 서명할 수 있습니다.
이 명령을 사용 하는 방법에 대 한 예는 [예제](#BKMK_examples)를 참조 하세요.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능에 대 한 자세한 내용은 Windows Server TechNet 라이브러리의 [Windows server 2012에 있는 원격 데스크톱 서비스의 새로운 기능](https://technet.microsoft.com/library/hh831527) 을 참조 하십시오.

## <a name="syntax"></a>구문
```
rdpsign /sha1 <hash> [/q | /v |] [/l] <file_name.rdp>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|/sha1 \<hash >|한 Secure Hash Algorithm 1 (SHA1) 해시는 인증서 저장소에 포함 된 서명 인증서의 지문을 지정 합니다. Windows Server 2012 R2 이상에서 사용 됩니다.|
|/sha256 \<hash >|인증서 저장소에 포함 되는 서명 인증서의 SHA256 (Secure Hash Algorithm 256) 해시 인 지문을 지정 합니다. Windows Server 2016 이상에서/ss를 대체 합니다.|
|/q|자동 모드입니다. 명령이 성공 하는 경우의 출력 및 명령이 실패 하는 경우 최소 출력 합니다.|
|/v|자세한 정보 표시 모드입니다. 모든 경고, 메시지 및 상태를 표시합니다.|
|/l|실제로 입력된 파일 중 하나를 바꾸지 않고 서명 및 출력 결과 테스트 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   SHA1 또는 SHA256 인증서 지 문은 신뢰할 수 있는 .rdp 파일 게시자를 나타내야 합니다. 인증서 지문을 얻으려면 인증서 스냅인을 열고 사용할 인증서 (로컬 컴퓨터의 인증서 저장소 또는 개인 인증서 저장소)를 두 번 클릭 한 다음 **세부 정보 탭을 클릭 하 고 필드** 목록에서 **손 도장 (Thumbprint**)을 클릭 합니다.

    > [!NOTE]
    > Rdpsign 도구와 함께 사용 하기 위해 지문을 복사할 때 공백을 모두 제거 해야 합니다.

-   전체 파일 이름을 사용 하 여 서명 하는.rdp 파일 (또는 파일)를 지정 해야 합니다. 와일드 카드 문자 허용 되지 않습니다.
-   서명 된 출력 파일은 입력된 파일을 덮어쓰게 됩니다.
-   .rdp 파일 중 하나를 읽거나 쓸 수 없는 경우 여러 파일을 지정 하면 도구는 다음 파일로 계속 됩니다.

## <a name="BKMK_examples"></a>예와
- File1.rdp 라는.rdp 파일을 서명 하려면.rdp 파일을 저장 한 폴더를 찾아 다음 코드를 입력 합니다.
  ```
  rdpsign /sha1 hash file1.rdp
  ```
  > [!NOTE]
  > *해시* SHA1 인증서 지 문은 공백 없이 값을 나타냅니다.
- 실제로 파일을 서명 하지 않고.rdp 파일에 대 한 성공할 디지털 서명을 지 여부를 테스트 하려면 다음을 입력 합니다.
  ```
  rdpsign /sha1 hash /l file1.rdp
  ```
- 여러.rdp 파일을 서명 하려면 공백을 사용 하 여 파일 이름을 구분 합니다. 예를 들어 File1.rdp, File2.rdp, 및 File3.rdp 여러.rdp 파일을 서명 하려면 다음을 입력 합니다.
  ```
  rdpsign /sha1 hash file1.rdp file2.rdp file3.rdp
  ```
  ## <a name="see-also"></a>참고 항목
  [명령줄 구문 키](command-line-syntax-key.md)
  [원격 데스크톱 서비스 & #40; 터미널 서비스 및 #41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
