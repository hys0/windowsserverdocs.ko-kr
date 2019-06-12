---
title: 다른 서버에서 가져오기에는 NPS 구성 내보내기
description: Windows Server 2016에서 네트워크 정책 서버 구성 내보내기 하는 방법을 알아보려면이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b95e39af63e284d0147335faabfb740c0dd175bc
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812296"
---
# <a name="export-an-nps-configuration-for-import-on-another-server"></a>다른 서버에서 가져오기에는 NPS 구성 내보내기

적용 대상: Windows Server 2016

전체 NPS 구성을 내보낼 수 있습니다-RADIUS 클라이언트 및 서버, 네트워크 정책, 연결 요청 정책, 레지스트리 및 로깅 구성을 포함 하 여-다른 NPS에서 가져오기에 대 한 NPS에서. 

NPS 구성을 내보내려면 다음 도구 중 하나를 사용 합니다.

- Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 Netsh를 사용할 수 있습니다 또는 Windows PowerShell을 사용할 수 있습니다.
- Windows Server 2008 R2 및 Windows Server 2008에서 Netsh를 사용 합니다.

> [!IMPORTANT]
> 원본 NPS 데이터베이스에는 대상 NPS 데이터베이스의 버전 번호 보다 높은 버전 번호를 하는 경우에이 절차를 사용 하지 마십시오. 표시에서 NPS 데이터베이스의 버전 번호를 볼 수 있습니다 합니다 **netsh nps 구성 표시** 명령입니다.

NPS 구성으로에서 암호화 되지 않은 내보낸된 XML 파일을 네트워크를 통해 전송 하기 때문에 보안 위험을 내포할 따라서 XML 파일을 원본 서버에서 대상 서버로 이동 하는 경우 예방 조치를 취할 수도 있습니다. 예를 들어 파일을 이동 하기 전에 파일을 암호화 된 암호 보호 된 보관 파일에 추가 합니다. 또한 악의적인 사용자가 액세스 하지 못하도록 안전한 위치에 파일을 저장 합니다.

> [!NOTE]
> SQL Server 로깅 원본 NPS에 구성 된 경우 SQL Server 로깅 설정 XML 파일을 내보내지 않습니다. 다른 NPS에서 파일을 가져온 후 SQL Server 로깅 수동으로 구성 해야 합니다.

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 NPS 구성을 내보내고

Windows Server 2012 및 이후 운영 체제 버전에 대 한 Windows PowerShell을 사용 하 여 NPS 구성을 내보낼 수 있습니다.

NPS 구성을 내보내는 위한 명령 구문은 다음과 같습니다. 

    Export-NpsConfiguration -Path <filename>

다음 표에 대 한 매개 변수를 **내보내기 NpsConfiguration** Windows PowerShell cmdlet. 굵게 표시 된 매개 변수는 필수입니다.

|매개 변수|설명|
|---------|-----------|
|Path|NPS 구성을 내보내는 하려는 XML 파일의 위치와 이름을 지정 합니다.|

**관리자 자격 증명**

이 절차를 완료 하려면 Administrators 그룹의 멤버 여야 합니다.

### <a name="export-example"></a>내보내기 예 

다음 예제에서는 NPS 구성은 로컬 드라이브에 있는 XML 파일로 내보내집니다. 이 명령을 실행 하려면 원본 NPS에서 관리자 권한으로 Windows PowerShell을 실행, 다음 명령을 입력 하 고 Enter 키를 누릅니다.

`Export-NpsConfiguration –Path c:\config.xml` 

자세한 내용은 [내보내기 NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx)합니다.

NPS 구성의 내보낸 후 대상 서버에 XML 파일을 복사 합니다.

대상 서버의 NPS 구성을 가져오기 위한 명령 구문은 다음과 같습니다.

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>가져오기 예제

다음 명령을 C:\Npsconfig.xml NPS로 라는 파일에서 설정을 가져옵니다. 이 명령을 실행 하려면 대상 NPS에 관리자 권한으로 Windows PowerShell을 실행, 다음 명령을 입력 하 고 Enter 키를 누릅니다.

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

자세한 내용은 [가져오기-NpsConfiguration](https://technet.microsoft.com/library/jj872750.aspx)합니다.

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>Netsh를 사용 하 여 NPS 구성을 내보내고

네트워크 셸을 사용할 수 있습니다 \(Netsh\) 사용 하 여 NPS 구성을 내보내려면 합니다 **netsh nps 내보내기** 명령입니다.

경우는 **netsh nps 가져오기** 명령을 실행, NPS는 자동 업데이트 구성 설정으로 새로 고쳐집니다. 그러나 NPS를 실행 하려면 대상 컴퓨터에서 중지 해야 합니다 **netsh nps 가져오기** NPS 콘솔 또는 NPS MMC 스냅인가 열려 있으면 구성 가져오는 동안 서버 구성 변경 내용을 표시 되지 않습니다 될 때까지 명령 보기를 새로 고칩니다. 

> [!NOTE]
> 사용 하는 경우는 **netsh nps 내보내기** 명령, 명령 매개 변수를 제공 해야 **exportPSK** 값을 가진 **예**합니다. 이 매개 변수 및 값을 명시적으로 지정할 NPS 구성을 내보내는 및 공유 암호를 암호화 되지 않은 RADIUS 클라이언트 및 원격 RADIUS 서버 그룹의 멤버에 대해 내보낸된 XML 파일에 포함 되어 있는지를 이해 합니다.

**관리자 자격 증명**

이 절차를 완료 하려면 Administrators 그룹의 멤버 여야 합니다.

### <a name="to-copy-an-nps-configuration-to-another-nps-using-netsh-commands"></a>Netsh 명령을 사용 하 여 다른 NPS에는 NPS 구성을 복사

1. 원본 NPS에서 엽니다 **명령 프롬프트**, 형식 **netsh**, 한 다음 Enter를 누릅니다.

2. 에 **netsh** 프롬프트에 입력 **nps**, 한 다음 Enter를 누릅니다. 

3. 에 **netsh nps** 프롬프트에 입력 **파일 이름 내보내기 =** "*path\file.xml*" **exportPSK = YES**여기서 *경로* NPS 구성 파일을 저장 하려는 폴더 위치 및 *파일* 저장 하려는 XML 파일의 이름입니다. Enter 키를 누릅니다. 

이렇게 구성 설정이 저장 \(레지스트리 설정을 비롯 한\) XML 파일에 있습니다. 상대 또는 절대 경로일 수 있습니다 또는 수는 Universal Naming Convention \(UNC\) 경로입니다. Enter를 누르면 파일로 내보내기의 성공 여부를 나타내는 메시지가 나타납니다.

4. 대상 NPS 만든 파일을 복사 합니다.

5. 대상 NPS에서 명령 프롬프트에서 입력 **netsh nps 가져오기 filename =** "*path\file.xml*", 한 다음 Enter를 누릅니다. XML 파일에서 가져오기 성공 여부를 알리는 메시지가 나타납니다.

Netsh에 대 한 자세한 내용은 참조 하세요. [네트워크 셸 (Netsh)](../netsh/netsh.md)합니다.

