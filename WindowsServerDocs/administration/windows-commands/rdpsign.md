---
title: rdpsign
description: RDP 파일에 디지털 서명 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9e35d3a3e85ed046fb658bbf5a97ab5fc5eec6d3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442017"
---
# <a name="rdpsign"></a>rdpsign

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디지털 방식으로 원격 데스크톱 프로토콜 (.rdp) 파일에 서명할 수 있습니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.

> [!NOTE]
> Windows Server 2008 R2에서는 터미널 서비스의 이름이 원격 데스크톱 서비스로 바뀌었습니다. 최신 버전의 새로운 기능을 참조 하세요 [어떤 새로운 Windows Server 2012의 원격 데스크톱 서비스](https://technet.microsoft.com/library/hh831527) 는 Windows Server TechNet 라이브러리에서.

## <a name="syntax"></a>구문
```
rdpsign /sha1 <hash> [/q | /v |] [/l] <file_name.rdp>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|/sha1 \<hash>|한 Secure Hash Algorithm 1 (SHA1) 해시는 인증서 저장소에 포함 된 서명 인증서의 지문을 지정 합니다.|
|/q|자동 모드입니다. 명령이 성공 하는 경우의 출력 및 명령이 실패 하는 경우 최소 출력 합니다.|
|/v|자세한 정보 표시 모드입니다. 모든 경고, 메시지 및 상태를 표시합니다.|
|/l|실제로 입력된 파일 중 하나를 바꾸지 않고 서명 및 출력 결과 테스트 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   SHA1 인증서 지문 신뢰할 수 있는.rdp 파일 게시자를 나타내야 합니다. 인증서 지문을 얻으려면 인증서 스냅인을 열고, 클릭 (로컬 컴퓨터의 인증서 저장소에 또는 개인 인증서 저장소에)를 사용 하려는 인증서를 두 번 클릭 합니다 **세부 정보** 탭 한 다음 합니다 **필드** 목록에서 클릭 **지문**합니다.

    > [!NOTE]
    > Rdpsign.exe 도구 사용에 대 한 지문을 복사할 때 공백을 제거 해야 합니다.

-   전체 파일 이름을 사용 하 여 서명 하는.rdp 파일 (또는 파일)를 지정 해야 합니다. 와일드 카드 문자 허용 되지 않습니다.
-   서명 된 출력 파일은 입력된 파일을 덮어쓰게 됩니다.
-   .rdp 파일의 없습니다 수 읽기 또는 쓰기, 경우 여러 파일이 지정 된 경우 도구는 다음 파일에 계속 됩니다.

## <a name="BKMK_examples"></a>예제
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
  ## <a name="see-also"></a>관련 항목
  [명령줄 구문 키](command-line-syntax-key.md)
  [원격 데스크톱 서비스&#40; 터미널 서비스 및&#41; 명령 참조](remote-desktop-services-terminal-services-command-reference.md)
