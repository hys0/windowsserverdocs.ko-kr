---
title: ktpass
description: Ktpass 명령에 대 한 참조 항목으로, AD DS에서 호스트 또는 서비스에 대 한 서버 보안 주체 이름을 구성 하 고 서비스의 공유 비밀 키를 포함 하는 keytab 파일을 생성 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47087676-311e-41f1-8414-199740d01444
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 432918343ccee70f0c30d294a349fb721f18f705
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817233"
---
# <a name="ktpass"></a>ktpass

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory 도메인 서비스 (AD DS)에서 호스트 또는 서비스에 대 한 서버 보안 주체 이름 구성 하 고 서비스의 공유 암호 키를 포함 하는.keytab 파일을 생성 합니다. .keytab 파일은 MIT(매사추세츠 공과대학교)의 Kerberos 인증 프로토콜 구현을 기반으로 합니다. Ktpass 명령줄 도구를 사용 하면 kerberos 인증을 지 원하는 비 Windows 서비스가 Kerberos 키 배포 센터 (KDC) 서비스에서 제공 하는 상호 운용성 기능을 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
ktpass
[/out <filename>]
[/princ <principalname>]
[/mapuser <useraccount>]
[/mapop {add|set}] [{-|+}desonly] [/in <filename>]
[/pass {password|*|{-|+}rndpass}]
[/minpass]
[/maxpass]
[/crypto {DES-CBC-CRC|DES-CBC-MD5|RC4-HMAC-NT|AES256-SHA1|AES128-SHA1|All}]
[/itercount]
[/ptype {KRB5_NT_PRINCIPAL|KRB5_NT_SRV_INST|KRB5_NT_SRV_HST}]
[/kvno <keyversionnum>]
[/answer {-|+}]
[/target]
[/rawsalt] [{-|+}dumpsalt] [{-|+}setupn] [{-|+}setpass <password>]  [/?|/h|/help]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ------------|
| /out`<filename>` | 생성할 Kerberos 버전 5.keytab 파일의 이름을 지정 합니다. **참고:** 이 파일은 Windows 운영 체제를 실행 하지 않는 컴퓨터에 전송 하는 keytab 파일입니다 .이 파일을 기존. keytab 파일인 */Etc/Krb5.keytab*로 바꾸거나 병합 합니다. |
| /princ`<principalname>` | 형식으로 보안 주체 이름을 지정 합니다 host/computer.contoso.com@CONTOSO.COM . **경고:** 이 매개 변수는 대/소문자를 구분 합니다. |
| /mapuser`<useraccount>` | 지정 된 Kerberos 사용자 이름을 매핑하는 **princ** 매개 변수를 지정 된 도메인 계정. |
| /mapop`{add|set}` | 매핑 특성을 설정 하는 방법을 지정 합니다.<ul><li>**추가** -지정 된 로컬 사용자 이름의 값을 추가 합니다. 이것이 기본값입니다.</li><li>**설정** -지정 된 로컬 사용자 이름에 대 한 DES (Data encryption Standard) 전용 암호화 값을 설정 합니다.</li></ul> |
| `{-|+}`desonly | DES 전용 암호화는 기본적으로 설정 됩니다.<ul><li>**+** DES 전용 암호화에 대 한 계정을 설정 합니다.</li><li>**-** DES 전용 암호화에 대 한 계정에 대 한 제한을 해제 합니다. **중요:** Windows에서는 기본적으로 DES를 지원 하지 않습니다.</li></ul> |
| /in`<filename>` | Windows 운영 체제를 실행 하지 않는 호스트 컴퓨터에서 읽을.keytab 파일을 지정 합니다. |
| /pass`{password|*|{-|+}rndpass}` | 로 지정 된 주 사용자 이름에 대 한 암호를 지정 된 **princ** 매개 변수입니다. `*`를 사용 하 여 암호를 묻는 메시지를 표시 합니다. |
| /minpass | 15 자로 임의의 암호의 최소 길이 설정합니다. |
| /maxpass | 임의의 암호의 최대 길이 256 자로 설정합니다. |
| /crypto`{DES-CBC-CRC|DES-CBC-MD5|RC4-HMAC-NT|AES256-SHA1|AES128-SHA1|All}` | 키 파일에서 생성 되는 키를 지정 합니다.<ul><li>**DES-cbc-mac** -호환성을 위해 사용 됩니다.</li><li>**DES-MD5** -MIT 구현에 보다 긴밀 하 게 준수 하 고 호환성을 위해 사용 됩니다.</li><li>**RC4-HMAC-NT** -128 비트 암호화를 활용 합니다.</li><li>**AES256** -AES256 암호화를 활용 합니다.</li><li>   **AES128** -AES128 암호화를 활용 합니다.</li><li>**모든** -지원 되는 모든 암호화 형식을 사용할 수 있음을 명시 합니다.</li></ul><p>**참고:** 기본 설정은 이전 MIT 버전을 기반으로 하므로 항상 매개 변수를 사용 해야 합니다 `/crypto` . |
| /itercount | AES 암호화에 사용 되는 반복 횟수를 지정 합니다. 기본값은 비 AES 암호화에 대 한 **itercount** 을 무시 하 고 aes 암호화를 4096으로 설정 합니다. |
| /ptype`{KRB5_NT_PRINCIPAL|KRB5_NT_SRV_INST|KRB5_NT_SRV_HST}` | 보안 주체 유형을 지정합니다.<ul><li>**KRB5_NT_PRINCIPAL** -일반 보안 주체 유형 (권장)</li><li>**KRB5_NT_SRV_INST** -사용자 서비스 인스턴스</li><li>  **KRB5_NT_SRV_HST** -호스트 서비스 인스턴스</li></ul> |
| /kvno`<keyversionnum>` | 키 버전 번호를 지정합니다. 기본값은 1입니다. |
| /answer`{-|+}` | 배경 응답 모드를 설정합니다.<ul><li>**-** 대답은 **아니요**를 사용 하 여 암호 프롬프트를 자동으로 다시 설정 합니다.</li><li>**+** 대답 암호 프롬프트를 자동으로 다시 설정 **예**를 표시 합니다.</li></ul> |
| /target | 도메인 컨트롤러를 사용 하도록 설정 합니다. 기본값은 검색, 보안 주체 이름을 기반으로 하는 도메인 컨트롤러입니다. 도메인 컨트롤러 이름이 확인 되지 않으면 올바른 도메인 컨트롤러에 대 한 대화 상자가 표시 됩니다. |
| /rawsalt | 키를 생성할 때 ktpass에서 rawsalt 알고리즘을 강제로 사용 하도록 합니다. 이 매개 변수는 선택 사항입니다. |
| `{-|+}dumpsalt` | 이 매개 변수는 출력 키를 생성 하는 데 사용 되는 MIT salt 알고리즘을 보여 줍니다. |
| `{-|+}setupn` | 서비스 사용자 이름 (SPN) 외에도 사용자 보안 주체 이름 (UPN)을 설정합니다. 기본값은.keytab 파일에서 모두 설정 하는 것입니다. |
| `{-|+}setpass <password>` | 제공 되는 경우 사용자의 암호를 설정 합니다. Rndpass 사용 되는 경우에 임의의 암호를 대신 생성 됩니다. |
| /? | 이 명령에 대 한 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- Windows 운영 체제를 실행 하지 않는 시스템에서 실행 되는 서비스는 AD DS의 서비스 인스턴스 계정으로 구성할 수 있습니다. 따라서 모든 Kerberos 클라이언트 Windows Kdc를 사용 하 여 Windows 운영 체제를 실행 하지 않는 서비스에 인증할 수 있습니다.

- **/Princ** 매개 변수는 ktpass에서 평가 되지 않으며 제공 된 대로 사용 됩니다. Keytab 파일을 생성할 때 매개 변수가 **userPrincipalName** 특성 값의 정확한 대/소문자와 일치 하는지 여부는 확인할 수 없습니다. 이 Keytab 파일을 사용 하는 대/소문자를 구분 하는 Kerberos 배포판에 정확한 대/소문자 일치가 없는 경우 문제가 발생 하 고 사전 인증 중에도 실패할 수 있습니다. LDifDE 내보내기 파일에서 올바른 **userPrincipalName** 특성 값을 확인 하 고 검색 하려면입니다. 다음은 그 예입니다.

    ```
    ldifde /f keytab_user.ldf /d CN=Keytab User,OU=UserAccounts,DC=contoso,DC=corp,DC=microsoft,DC=com /p base /l samaccountname,userprincipalname
    ````

### <a name="examples"></a>예

Windows 운영 체제를 실행 하지 않는 호스트 컴퓨터에 대 한 keytab 파일을 만들려면 보안 주체를 계정에 매핑하고 호스트 주체 암호를 설정 해야 합니다.

1. Active directory **사용자 및 컴퓨터** 스냅인을 사용 하 여 Windows 운영 체제를 실행 하지 않는 컴퓨터에서 서비스에 대 한 사용자 계정을 만듭니다. 예를 들어 *User1*이름으로 계정을 만듭니다.

2. **Ktpass** 명령을 사용 하 여 다음을 입력 하 여 사용자 계정에 대 한 id 매핑을 설정 합니다.

    ```
    ktpass /princ host/User1.contoso.com@CONTOSO.COM /mapuser User1 /pass MyPas$w0rd /out machine.keytab /crypto all /ptype KRB5_NT_PRINCIPAL /mapop set
    ```

    > [!NOTE]
    > 동일한 사용자 계정에 여러 서비스 인스턴스를 매핑할 수 없습니다.

3. Windows 운영 체제를 실행 하지 않는 호스트 컴퓨터의 */Etc/Krb5.keytab* 파일을 사용 하 여 keytab 파일을 병합 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
