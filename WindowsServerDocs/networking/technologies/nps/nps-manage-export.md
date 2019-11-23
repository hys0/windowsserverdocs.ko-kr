---
title: 다른 서버에서 가져오기 위한 NPS 구성 내보내기
description: 이 항목을 사용 하 여 Windows Server 2016에서 네트워크 정책 서버 구성을 내보내는 방법을 알아볼 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d268dc57-78f8-47ba-9a7a-a607e8b9225c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cbebd0388ccd5dd2540a20f5d325d7f97c7e2bb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405437"
---
# <a name="export-an-nps-configuration-for-import-on-another-server"></a>다른 서버에서 가져오기 위한 NPS 구성 내보내기

적용 대상: Windows Server 2016

다른 nps에서 가져오기 위해 한 NPS에서 RADIUS 클라이언트 및 서버, 네트워크 정책, 연결 요청 정책, 레지스트리 및 로깅 구성을 비롯 한 전체 NPS 구성을 내보낼 수 있습니다. 

다음 도구 중 하나를 사용 하 여 NPS 구성을 내보냅니다.

- Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서는 Netsh를 사용 하거나 Windows PowerShell을 사용할 수 있습니다.
- Windows Server 2008 R2 및 Windows Server 2008에서는 Netsh를 사용 합니다.

> [!IMPORTANT]
> 원본 NPS 데이터베이스가 대상 NPS 데이터베이스의 버전 번호 보다 높은 버전 번호를 사용 하는 경우에는이 절차를 사용 하지 마십시오. **Netsh nps show config** 명령의 표시에서 NPS 데이터베이스의 버전 번호를 볼 수 있습니다.

NPS 구성은 내보낸 XML 파일에서 암호화 되지 않으므로 네트워크를 통해 전송 하면 보안 위험이 발생할 수 있으므로 원본 서버에서 대상 서버로 XML 파일을 이동할 때 예방 조치를 취해야 합니다. 예를 들어 파일을 이동 하기 전에 암호화 된 암호로 보호 된 보관 파일에 파일을 추가 합니다. 또한 악의적인 사용자가 액세스 하지 못하도록 파일을 안전한 위치에 저장 합니다.

> [!NOTE]
> 원본 NPS에 SQL Server 로깅이 구성 된 경우 SQL Server 로깅 설정은 XML 파일로 내보내지 않습니다. 다른 NPS에서 파일을 가져온 후에 SQL Server 로깅을 수동으로 구성 해야 합니다.

## <a name="export-and-import-the-nps-configuration-by-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 NPS 구성 내보내기 및 가져오기

Windows Server 2012 이상 운영 체제 버전의 경우 Windows PowerShell을 사용 하 여 NPS 구성을 내보낼 수 있습니다.

NPS 구성을 내보내기 위한 명령 구문은 다음과 같습니다. 

    Export-NpsConfiguration -Path <filename>

다음 표에서는 Windows PowerShell의 **Export-NpsConfiguration** cmdlet에 대 한 매개 변수를 나열 합니다. 굵게 표시 된 매개 변수는 필수입니다.

|매개 변수|설명|
|---------|-----------|
|경로|NPS 구성을 내보낼 XML 파일의 이름과 위치를 지정 합니다.|

**관리 자격 증명**

이 절차를 완료 하려면 Administrators 그룹의 멤버 여야 합니다.

### <a name="export-example"></a>내보내기 예 

다음 예에서는 로컬 드라이브에 있는 XML 파일로 NPS 구성을 내보냅니다. 이 명령을 실행 하려면 NPS 원본에서 관리자 권한으로 Windows PowerShell을 실행 하 고 다음 명령을 입력 한 다음 Enter 키를 누릅니다.

`Export-NpsConfiguration –Path c:\config.xml` 

자세한 내용은 [Export-NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx)을 참조 하세요.

NPS 구성을 내보낸 후 대상 서버에 XML 파일을 복사 합니다.

대상 서버에서 NPS 구성을 가져오기 위한 명령 구문은 다음과 같습니다.

    Import-NpsConfiguration [-Path] <String> [ <CommonParameters>]

### <a name="import-example"></a>가져오기 예제

다음 명령은 C:\Npsconfig.xml 이라는 파일에서 NPS로 설정을 가져옵니다. 이 명령을 실행 하려면 대상 NPS에서 관리자 권한으로 Windows PowerShell을 실행 하 고 다음 명령을 입력 한 다음 Enter 키를 누릅니다.

    PS C:\> Import-NpsConfiguration -Path "C:\Npsconfig.xml"

자세한 내용은 [가져오기-NpsConfiguration](https://technet.microsoft.com/library/jj872750.aspx)을 참조 하세요.

## <a name="export-and-import-the-nps-configuration-by-using-netsh"></a>Netsh를 사용 하 여 NPS 구성 내보내기 및 가져오기

Network Shell \(Netsh\)를 사용 하 여 **netsh nps 내보내기** 명령을 사용 하 여 NPS 구성을 내보낼 수 있습니다.

**Netsh nps import** 명령이 실행 될 때 nps는 업데이트 된 구성 설정을 사용 하 여 자동으로 새로 고쳐집니다. **Netsh nps 가져오기** 명령을 실행 하기 위해 대상 컴퓨터에서 nps를 중지할 필요는 없지만 구성 가져오기 중에 nps 콘솔 또는 nps MMC 스냅인이 열려 있으면 보기를 새로 고칠 때까지 서버 구성에 대 한 변경 내용이 표시 되지 않습니다. 

> [!NOTE]
> **Netsh nps export** 명령을 사용 하는 경우 명령 매개 변수 **exportPSK** 을 **예**값으로 제공 해야 합니다. 이 매개 변수 및 값은 NPS 구성을 내보내는 것을 이해 하 고, 내보낸 XML 파일에 RADIUS 클라이언트 및 원격 RADIUS 서버 그룹의 구성원에 대 한 암호화 되지 않은 공유 암호를 포함 한다는 것을 명시적으로 표시 합니다.

**관리 자격 증명**

이 절차를 완료 하려면 Administrators 그룹의 멤버 여야 합니다.

### <a name="to-copy-an-nps-configuration-to-another-nps-using-netsh-commands"></a>Netsh 명령을 사용 하 여 NPS 구성을 다른 NPS에 복사 하려면

1. 원본 NPS에서 **명령 프롬프트**를 열고 **netsh**를 입력 한 다음 enter 키를 누릅니다.

2. **Netsh** 프롬프트에서 **nps**를 입력 한 다음 enter 키를 누릅니다. 

3. **Netsh nps** 프롬프트에서 **export filename =** "*path\file.xml*" **exportPSK = YES**를 입력 합니다. 여기서 *path* 는 nps 구성 파일을 저장 하려는 폴더 위치이 고 *file* 은 저장 하려는 xml 파일의 이름입니다. Enter 키를 누릅니다. 

이렇게 하면 XML 파일에\) 레지스트리 설정을 포함 하 \(구성 설정이 저장 됩니다. 경로는 상대 또는 절대 경로일 수 있으며 UNC\) 경로 \(범용 명명 규칙 일 수 있습니다. Enter 키를 누르면 파일로 내보내기의 성공 여부를 나타내는 메시지가 표시 됩니다.

4. 만든 파일을 대상 NPS에 복사 합니다.

5. 대상 NPS의 명령 프롬프트에서 **netsh NPS import filename =** "*path\file.xml*"를 입력 한 다음 enter 키를 누릅니다. XML 파일에서 가져오기가 성공 했는지 여부를 나타내는 메시지가 표시 됩니다.

Netsh에 대 한 자세한 내용은 [netsh (네트워크 셸)](../netsh/netsh.md)를 참조 하세요.

