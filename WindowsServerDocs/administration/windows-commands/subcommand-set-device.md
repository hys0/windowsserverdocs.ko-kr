---
title: 하위 명령 집합-장치
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 401567f8-eaeb-4a2d-b811-140bb007028d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 92e319e7c6671e9117e33f13ee8fb40a19df93bd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383897"
---
# <a name="subcommand-set-device"></a>하위 명령: 집합 장치

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사전 준비 된 컴퓨터의 특성을 변경 합니다. 사전 준비 된 컴퓨터는 AD DS (active directory 도메인 서버)의 컴퓨터 계정 개체에 연결 된 컴퓨터입니다. 사전 준비 된 클라이언트는 알려진된 컴퓨터 라고도 합니다. 클라이언트 설치를 제어할 컴퓨터 계정의 속성을 구성할 수 있습니다. 예를 들어 클라이언트가 네트워크 부팅 프로그램을 다운로드 해야 하는 서버 뿐만 아니라 네트워크 부팅 프로그램 및 클라이언트가 수신 해야 하는 무인 파일을 구성할 수 있습니다.
## <a name="syntax"></a>구문
```
wdsutil [Options] /Set-Device /Device:<Device name> [/ID:<UUID | MAC address>] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] 
[/WdsClientUnattend:<Relative path>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/Domain:<Domain>] [/resetAccount]
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/Device: <computer name>|컴퓨터 (SAM 계정 이름)의 이름을 지정합니다.|
|[/ ID: < UUID &#124; MAC 주소 >]|GUID/UUID 또는 컴퓨터의 MAC 주소를 지정합니다. 이 값은 다음 세 가지 형식 중 하나 여야 합니다.<br /><br />-이진 문자열: **/ID:ACEFA3E81F20694E953EB2DAA1E8B1B6**<br />-GUID/UUID 문자열: / ID:**E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<br />-MAC 주소: **00B056882FDC** (대시 없음) 또는 **00-B0-56-88-2f-DC** (대시 포함)|
|[/ ReferralServer:<Server name>]|Tftp (Trivial 파일 전송 프로토콜)를 사용 하 여 네트워크 부팅 프로그램 및 부팅 이미지를 다운로드 하기 위해 연결할 서버의 이름을 지정 합니다.|
|[/ BootProgram:<Relative path>]|RemoteInstall 폴더에서 지정 된 컴퓨터에 수신 되는 네트워크 부팅 프로그램에 대 한 상대 경로를 지정 합니다. 예를 들어: **boot\x86\pxeboot.com**|
|[/ WdsClientUnattend:<Relative path>]|Windows 배포 서비스 클라이언트의 설치 화면을 자동화 하는 무인 파일에 대 한 remoteInstall 폴더의 상대 경로를 지정 합니다.|
|[/User: < Domain\User &#124; User@Domain >]|컴퓨터를 도메인에 가입 하는 데 필요한 권한이 지정된 된 사용자에 게 컴퓨터 계정 개체에 사용 권한을 설정 합니다.|
|[/ JoinRights: {JoinOnly & #124; 전체}]|사용자에 게 할당할 권한의 유형을 지정 합니다.<br /><br />-   **Joinonly** 를 사용 하려면 관리자가 컴퓨터 계정을 다시 설정 해야 사용자가 컴퓨터를 도메인에 연결할 수 있습니다.<br />0 @no__t**full** 은 컴퓨터를 도메인에 가입 시킬 수 있는 권한을 포함 하 여 사용자에 게 모든 권한을 부여 합니다.|
|[/ JoinDomain: {예 & #124; No}]|컴퓨터가 Windows 배포 서비스를 설치 하는 동안이 컴퓨터 계정으로 도메인에 가입 되어야 해야 여부를 지정 합니다. 기본 설정은 **예**합니다.|
|[/BootImagepath: <Relative path>]|컴퓨터에서 사용 하는 부팅 이미지에 대 한 remoteInstall 폴더의 상대 경로를 지정 합니다.|
|[/ 도메인:<Domain>]|사전 준비 된 컴퓨터에 대 한 검색할 도메인을 지정 합니다. 기본값은 로컬 도메인입니다.|
|[/resetAccount]|적절 한 사용 권한이 있는 모든 사용자가이 계정을 사용 하 여 도메인에 가입할 수 있도록 지정 된 컴퓨터에 대 한 사용 권한을 다시 설정 합니다.|
## <a name="BKMK_examples"></a>예와
컴퓨터에 대 한 네트워크 부팅 프로그램 및 조회 서버를 설정 하려면 다음을 입력 합니다.
```
wdsutil /Set-Device /Device:computer1 /ReferralServer:MyWDSServer
/BootProgram:boot\x86\pxeboot.n12
```
컴퓨터에 대 한 다양 한 설정을 지정 하려면 다음을 입력 합니다.
```
wdsutil /verbose /Set-Device /Device:computer2 /ID:00-B0-56-88-2F-DC /WdsClientUnattend:WDSClientUnattend\unattend.xml 
/User:Domain\user /JoinRights:JoinOnly /JoinDomain:No /BootImagepath:boot\x86\images\boot.wim /Domain:NorthAmerica /resetAccount
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[장치 추가 명령을 사용 하 여](using-the-add-device-command.md)
[get AllDevices 명령을 사용 하 여](using-the-get-alldevices-command.md)
[get 장치 명령을 사용 하 여](using-the-get-device-command.md)
