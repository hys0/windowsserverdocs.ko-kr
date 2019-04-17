---
title: 다른 서버의 가져오기 NPS 서버 구성 내보내기
description: Windows Server 2016에는 네트워크 정책 서버 구성 내보낼 방법을이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 141a99e930672d8403315cb6804290d184ef3007
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="export-an-nps-server-configuration-for-import-on-another-server"></a>다른 서버의 가져오기 NPS 서버 구성 내보내기

Windows Server 2016 적용 됩니다.

전체 NPS 구성 내보낼 수 있는-RADIUS 클라이언트 및 서버, 네트워크 정책, 연결 요청 정책, 레지스트리 로깅 구성 등-NPS 서버를 다른 NPS 서버의 가져오기에서 합니다. 

다음 도구 중 하나를 사용 하 여 NPS 구성 내보내기:

- Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 Netsh, 사용 하거나 Windows PowerShell 사용할 수 있습니다.
- Windows Server 2008 R2 및 Windows Server 2008 Netsh 사용 합니다.

>[!IMPORTANT]
>원본 NPS 데이터베이스에는 대상 NPS 데이터베이스의 버전 번호가 보다 높은 버전 번호를 하는 경우이 절차를 사용 하지 마십시오. NPS 데이터베이스의 디스플레이를 버전 번호를 볼 수는 **netsh nps 표시 구성** 명령을 합니다.

서버 구성 NPS 암호화 되지 않은 내보낸된 XML 파일에는 보안 위험이 발생할 수 있으므로 네트워크로 전송 되므로 지금 주의 대상 서버 원본 서버에서 XML 파일을 이동할 때 합니다. 예를 들어, 파일을 이동 하기 전에 파일 암호화를 암호 보관 보호 된 파일에 추가 합니다. 또한 파일이 악의적인 사용자가 액세스 하지 못하도록 하려면 안전한 장소에 저장 합니다.

>[!NOTE]
>원본 NPS 서버의 SQL Server 로깅 구성 되어는 SQL Server 로깅 설정은 XML 파일 내보낼 수 없습니다. 다른 NPS 서버에서 파일을 가져온 후에 수동으로 SQL Server 로깅을 구성 해야 합니다.

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>Windows PowerShell를 사용 하 여 NPS 구성 내보내고

Windows Server 2012 및 이후 운영 체제 버전을 사용 하 여 Windows PowerShell NPS 구성을 내보낼 수 있습니다.

내보내기 NPS 구성에 대 한 명령 구문을 다음과 같습니다. 

    Export-NpsConfiguration -Path <filename>

다음 표에서에 대 한 매개는 **내보내기 NpsConfiguration** 에서 Windows PowerShell cmdlet 합니다. 굵게 매개는 필요 합니다.

|매개|설명|
|---------|-----------|
|경로|이름 및 내보낼 NPS 서버 구성 하려면 XML 파일의 위치를 지정 합니다.|

**관리자 자격 증명**

이 절차를 수행 하려면 관리자가 그룹의 회원 이어야 합니다.

### <a name="export-example"></a>예를 내보내려면 

다음 예제에서 NPS 구성 로컬 드라이브에 파일로 XML 내보낼 합니다. 이 명령을 실행 하려면 소스 NPS 서버에서 Windows PowerShell 관리자 권한으로 실행 다음 명령을 입력 하 고 Enter 키를 누릅니다.

`Export-NpsConfiguration –Path c:\config.xml` 

자세한 내용은 참조 [내보내기 NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx)합니다.

NPS 구성 내보낸 후 대상 서버로 XML 파일을 복사 합니다.

가져올 대상 서버의 NPS 구성에 대 한 명령 구문을 다음과 같습니다.

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>예제 가져오기

다음 명령을 C:\Npsconfig.xml NPS 하 라는 파일에서 설정을 가져옵니다. 이 명령을 실행 하려면 대상 NPS 서버에서 Windows PowerShell 관리자 권한으로 실행 다음 명령을 입력 하 고 Enter 키를 누릅니다.

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

자세한 내용은 참조 [가져오기 NpsConfiguration](https://technet.microsoft.com/library/jj872750.aspx)합니다.

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>Netsh을 사용 하 여 NPS 구성 내보내고

네트워크 셸 \(Netsh\)를 사용 하 여 사용 하 여 NPS 서버 구성 내보낼는 **netsh nps 내보내기** 명령을 합니다.

때는 **netsh nps 가져오기** 명령을 실행, NPS 구성 업데이트 설정을 사용 하 여 자동으로 새로 고쳐집니다. 그러나 대상 실행 하려면 컴퓨터에서 NPS 중지 필요가 없습니다는 **netsh nps 가져오기** 명령 NPS 콘솔 또는 NPS mmc 열려 있으면 구성 가져오는 동안 서버 구성 변경 내용이 표시 되지 않습니다 보기를 새로 고칩니다 될 때까지 합니다. 

>[!NOTE]
>사용 하는 **netsh nps 내보내기** 명령 명령 매개 변수를 제공 해야 하는 **exportPSK** 값으로 **예**합니다. 매개 변수와 값이 명시적으로 NPS 서버 구성 내보내는 공유 암호 내보낸된 XML 파일 포함 암호화 되지 않은 RADIUS 클라이언트 및 원격 RADIUS 서버 그룹의 회원에 대해 이해 하는 주입니다.

**관리자 자격 증명**

이 절차를 수행 하려면 관리자가 그룹의 회원 이어야 합니다.

### <a name="to-copy-an-nps-server-configuration-to-another-nps-server-using-netsh-commands"></a>Netsh 명령을 사용 하 여 다른 NPS 서버로 NPS 서버 구성 복사

1. 원본 NPS 서버에서 엽니다 **명령 프롬프트**, 입력 **netsh**, Enter 키를 누릅니다.

2. 에 **netsh** 입력 합니다 **nps**, Enter 키를 누릅니다. 

3. 에 **netsh nps** 입력 합니다 **파일 이름을 내보내기 =**"*path\file.xml*" **exportPSK = 예**, 여기서 *경로* 저장 NPS 서버 구성 파일을 저장할 폴더 위치가 및 *파일* 저장 하려는 XML 파일 이름입니다. Enter 키를 누릅니다. 

구성 설정 저장 \(including registry settings\) XML 파일에 있습니다. 경로 상대 또는 절대, 이거나 범용 명명 규칙 \(UNC\) 경로 될 수 있습니다. Enter 키를 파일에 내보내기의 성공 여부를 알리는 메시지가 나타납니다.

4. 대상 NPS 서버로 생성 된 파일을 복사 합니다.

5. 대상 NPS 서버에서 명령 프롬프트에 입력 **netsh nps 가져오기 파일 이름 =**"*path\file.xml*"를 누른 다음 Enter 키를 누릅니다. XML 파일에서 가져오기에 성공 여부를 알리는 메시지가 나타납니다.

Netsh에 대 한 자세한 내용은 참조 [네트워크 (Netsh) 셸](../netsh/netsh.md)합니다.

