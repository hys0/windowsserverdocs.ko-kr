---
title: 승인-AutoaddDevices
description: 승인-AutoaddDevices에 대 한 Windows 명령 항목. 관리 승인이 보류 중인 컴퓨터를 승인 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8d76e8d3-ab35-429c-be7b-904f95d0782d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7f63faabf37337136cad186fd252915adf1a743
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831836"
---
# <a name="approve-autoadddevices"></a>승인-AutoaddDevices

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

관리자의 승인이 보류 중인 컴퓨터를 승인 합니다. 자동 추가 정책을 사용 하는 경우 알 수 없는 컴퓨터 (사전 준비 되지 않은 컴퓨터)에서 이미지를 설치할 수 있으려면 관리자 승인이 필요 합니다. 서버 속성 페이지의 **PXE 응답** 탭을 사용 하 여이 정책을 사용 하도록 설정할 수 있습니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>] 
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지 않으면 로컬 서버가 사용 됩니다.|
|/ 요청 Id: {요청 ID &#124; 모든}|보류 중인 컴퓨터에 할당 된 요청 ID를 지정 합니다. 지정 **모든** 모든 보류 중인 컴퓨터를 승인 합니다.|
|[/ MachineName:<Device name>]|추가할 컴퓨터의 이름을 지정 합니다. 모든 컴퓨터를 승인 하는 경우이 옵션을 사용할 수 없습니다.|
|[/OU:<DN of OU>]|컴퓨터 계정 개체를 만들 수는 조직 구성 단위 (OU)의 고유 이름을 지정 합니다. 예를 들어: **OU = MyOU, CN = 테스트, DC = Domain, DC = com**합니다. 기본 위치는 기본 컴퓨터의 컨테이너입니다.|
|[/User: < Domain\User &#124; User@Domain>]|필요한 권한이 지정된 된 사용자를 할당 하려면 컴퓨터 계정 개체에 사용 권한을 설정 합니다.|
|[/ JoinRights: {JoinOnly &#124; 전체}]|지정된 된 사용자에 할당할 권한의 유형을 지정 합니다.<p>-   **Joinonly** 를 사용 하려면 관리자가 컴퓨터 계정을 다시 설정 해야 사용자가 컴퓨터를 도메인에 연결할 수 있습니다.<br />-   **full** 은 컴퓨터를 도메인에 가입 시킬 수 있는 권한을 포함 하는 사용자에 게 모든 권한을 부여 합니다.|
|[/ JoinDomain: {예 &#124; No}]|컴퓨터가 운영 체제를 설치 하는 동안이 컴퓨터 계정으로 도메인에 가입 되어야 해야 여부를 지정 합니다. 기본값은 **예**합니다.|
|[/ ReferralServer:<Server name>]|Tftp (Trivial 파일 전송 프로토콜)를 사용 하 여 네트워크 부팅 프로그램 및 부팅 이미지를 다운로드 하기 위해 연결할 서버의 이름을 지정 합니다.|
|[/ BootProgram:<Relative path>]|이 컴퓨터에서 수신 해야 하는 네트워크 부팅 프로그램에 대 한 remoteInstall 폴더의 상대 경로를 지정 합니다. 예를 들어: **boot\x86\pxeboot.com**합니다.|
|[/ WdsClientUnattend:<Relative path>]|Windows 배포 서비스 클라이언트를 자동화 하는 무인 파일에 대 한 remoteInstall 폴더의 상대 경로를 지정 합니다.|
|[/BootImagepath:<Relative path>]|이 컴퓨터가 수신할 부팅 이미지에 대 한 remoteInstall 폴더의 상대 경로를 지정 합니다.|
## <a name="examples"></a><a name=BKMK_examples></a>예와
12 RequestId 사용 하 여 컴퓨터를 승인 하는 경우, 다음을 입력 합니다.
```
wdsutil /Approve-AutoaddDevices /RequestId:12
```
20 대 한 요청 Id 사용 하 여 컴퓨터를 승인 하 고 지정 된 설정 사용 하 여 이미지를 배포 하려면 다음을 입력 합니다.
```
wdsutil /Approve-AutoaddDevices /RequestId:20 /MachineName:computer1 /OU:OU=Test,CN=company,DC=Domain,DC=Com /User:Domain\User1 
/JoinRights:Full /ReferralServer:MyWDSServer /BootProgram:boot\x86\pxeboot.n12 /WdsClientUnattend:WDSClientUnattend\Unattend.xml /BootImagepath:boot\x86\images\boot.wim
```
모든 보류 중인 컴퓨터를 승인 하려면 다음을 입력 합니다.
```
wdsutil /verbose /Approve-AutoaddDevices /RequestId:ALL
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) [삭제](using-the-delete-autoadddevices-command.md) -autoadddevices 명령을 사용 하 여
는 [get](using-the-get-autoadddevices-command.md) autoadddevices 명령을 사용 하 여
[거부 autoadddevices](using-the-reject-autoadddevices-command.md) 명령을 사용 하 여

