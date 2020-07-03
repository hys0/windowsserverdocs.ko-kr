---
title: 장치 추가
description: Active directory 도메인 서비스에서 컴퓨터를 사전 준비 하는 추가 장치에 대 한 참조 문서입니다. 사전 준비 된 컴퓨터에는 알려진된 컴퓨터 라고도 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e599cc4-464a-421b-b6bb-c101af154131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e410132ea3d7ce151c47d4708f284a8e44448aaf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937239"
---
# <a name="add-device"></a>장치 추가

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active directory 도메인 서비스에서 컴퓨터를 사전 준비 합니다. 사전 준비 된 컴퓨터에는 알려진된 컴퓨터 라고도 합니다. 이 클라이언트의 설치를 제어 하는 속성을 구성할 수 있습니다. 예를 들어 클라이언트가 네트워크 부팅 프로그램을 다운로드 해야 하는 서버 뿐만 아니라 네트워크 부팅 프로그램 및 클라이언트가 수신 해야 하는 무인 파일을 구성할 수 있습니다.

## <a name="syntax"></a>구문
```
wdsutil /add-Device /Device:<Device name> /ID:<UUID | MAC address> [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>]
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/OU:<DN of OU>] [/Domain:<Domain>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|장치<computer name>|추가할 컴퓨터의 이름을 지정 합니다.|
|/ID: <UUID &#124; MAC 주소>|GUID/UUID 또는 컴퓨터의 MAC 주소를 지정합니다. GUID/UUID는 두 형식 이진 문자열 또는 GUID 문자열 중 하나 여야 합니다. 예를 들어:<p>이진 문자열: **/id: ACEFA3E81F20694E953EB2DAA1E8B1B6**<p>GUID 문자열: **/ID:E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<p>MAC 주소를 다음 형식 이어야 합니다: **00B056882FDC** (대시가 없는) 또는 **00-B0-56-88-2F-DC** (대시로)|
|[/ ReferralServer:<Server name>]|Tftp (Trivial 파일 전송 프로토콜)를 사용 하 여 네트워크 부팅 프로그램 및 부팅 이미지를 다운로드 하기 위해 연결할 서버의 이름을 지정 합니다.|
|[/ BootProgram:<Relative path>]|이 컴퓨터에서 수신 해야 하는 네트워크 부팅 프로그램에 대 한 remoteInstall 폴더의 상대 경로를 지정 합니다. 예를 들어: boot\x86\pxeboot.com|
|[/ WdsClientUnattend:<Relative path>]|Windows 배포 서비스 클라이언트의 설치 화면을 자동화 하는 무인 설치 파일에 대 한 remoteInstall 폴더의 상대 경로를 지정 합니다.|
|[/User: <Domain\User &#124; User@Domain>]|컴퓨터를 도메인에 가입 하는 데 필요한 권한이 지정된 된 사용자에 게 컴퓨터 계정 개체에 사용 권한을 설정 합니다.|
|[/ JoinRights: {JoinOnly & #124; 전체}]|사용자에 게 할당할 권한의 유형을 지정 합니다.<p>-   **Joinonly** 를 사용 하려면 관리자가 컴퓨터 계정을 다시 설정 해야 사용자가 컴퓨터를 도메인에 가입할 수 있습니다.<br />-   **Full** 은 컴퓨터를 도메인에 가입 시킬 수 있는 권한을 포함 하는 사용자에 게 모든 권한을 부여 합니다.|
|[/ JoinDomain: {예 & #124; No}]|컴퓨터가 운영 체제를 설치 하는 동안이 컴퓨터 계정으로 도메인에 가입 되어야 해야 여부를 지정 합니다. 기본값은 **예**입니다.|
|[/BootImagepath: <Relative path> ]|이 컴퓨터에서 사용 해야 하는 부팅 이미지에 대 한 remoteInstall 폴더의 상대 경로를 지정 합니다.|
|[/OU:<DN of OU>]|컴퓨터 계정 개체 만들어야 하는 조직 구성 단위의 고유 이름입니다. 예를 들어: **OU = MyOU, CN = 테스트, DC = Domain, DC = com**합니다. 기본 위치는 기본 컴퓨터의 컨테이너입니다.|
|[/ 도메인:<Domain>]|도메인 컴퓨터 계정 개체 만들어야 합니다. 기본 위치는 로컬 도메인입니다.|
## <a name="examples"></a>예
MAC 주소를 사용 하 여 컴퓨터를 추가 하려면 다음을 입력 합니다.
```
wdsutil /add-Device /Device:computer1 /ID:00-B0-56-88-2F-DC
```
GUID 문자열을 사용 하 여 컴퓨터를 추가 하려면 다음을 입력 합니다.
```
wdsutil /add-Device /Device:computer1 /ID:{E8A3EFAC-201F-4E69-953F-B2DAA1E8B1B6} /ReferralServer:WDSServer1 /BootProgram:boot\x86\pxeboot.com
/WDSClientUnattend:WDSClientUnattend\unattend.xml /User:Domain\MyUser/JoinRights:Full /BootImagepath:boot\x86\images\boot.wim /OU:OU=MyOU,CN=Test,DC=Domain,DC=com
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [Get AllDevices 명령을](using-the-get-alldevices-command.md) 
 사용 하 여 [Get 장치 명령을](using-the-get-device-command.md) 
 사용 하 여 [하위 명령: 설정-장치](subcommand-set-device.md) 
 [새로 만들기-WdsClient](https://technet.microsoft.com/library/dn283430.aspx)
