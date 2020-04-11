---
title: Windows Server 2012를 Windows Server 2016으로 업그레이드 | Microsoft Docs
description: 현재 위치 업그레이드를 수행하여 Windows Server 2012에서 Windows Server 2016으로 이동하는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: c6cc52e24b7ba66b349b3715bacf3a0f671ff0d0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854276"
---
# <a name="upgrade-windows-server-2012-to-windows-server-2016"></a>Windows Server 2012를 Windows Server 2016으로 업그레이드

서버를 평면화하지 않고 동일한 하드웨어와 이미 설정한 모든 서버 역할을 유지하려면 현재 위치 업그레이드를 수행해야 합니다. 현재 위치 업그레이드를 사용하면 설정, 서버 역할 및 데이터를 그대로 유지하면서 이전 운영 체제를 최신 운영 체제로 전환할 수 있습니다. 이 문서는 Windows Server 2012에서 Windows Server 2016으로 이동하는 데 도움이 됩니다.

Windows Server 2019로 업그레이드하려면 먼저 이 항목을 사용하여 Windows Server 2016으로 업그레이드한 다음, [Windows Server 2016에서 Windows Server 2019로 업그레이드](upgrade-2016-to-2019.md)합니다.

## <a name="before-you-begin-your-in-place-upgrade"></a>현재 위치 업그레이드를 시작하기 전에

Windows Server 업그레이드를 시작하기 전에 진단 및 문제 해결을 위해 디바이스에서 일부 정보를 수집하는 것이 좋습니다. 이 정보는 업그레이드가 실패하는 경우에만 사용할 수 있으므로 디바이스에서 정보를 가져올 수 있는 위치에 저장해야 합니다.

### <a name="to-collect-your-info"></a>정보를 수집하려면 다음을 수행합니다.

1. 명령 프롬프트를 열고 `c:\Windows\system32`로 이동한 다음, **systeminfo.exe**를 입력합니다.

2. 결과 시스템 정보를 디바이스 어딘가에 복사하여 붙여넣고 저장합니다.

3. 명령 프롬프트에 **ipconfig /all**을 입력한 다음, 결과 구성 정보를 복사하여 위와 동일한 위치에 붙여넣습니다.

4. 레지스트리 편집기를 열고 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion 하이브로 이동한 다음, Windows Server **BuildLabEx**(버전) 및 **EditionID**(버전)를 위와 동일한 위치에 복사하여 붙여넣습니다.

Windows Server 관련 정보를 모두 수집한 후에는 운영 체제, 앱 및 가상 머신을 백업하는 것이 좋습니다. 또한 서버에서 현재 실행 중인 모든 가상 머신을 **종료**하고, **빠른 마이그레이션** 또는 **실시간 마이그레이션**을 수행해야 합니다. 현재 위치 업그레이드 중에는 가상 머신을 실행할 수 없습니다.

## <a name="to-perform-the-upgrade"></a>업그레이드하려면 다음을 수행합니다.

1. **BuildLabEx** 값에 Windows Server 2012가 실행되고 있는지 확인합니다.

2. Windows Server 2016 설치 미디어를 찾은 다음, **setup.exe**를 선택합니다.

    ![setup.exe 파일을 보여주는 Windows 탐색기](media/upgrade-2012-2016/setup-2016.png)

3. **예**를 선택하여 설치 프로세스를 시작합니다.

    ![설치를 시작하기 위한 권한을 요청하는 사용자 계정 컨트롤](media/upgrade-2012-2016/start-setup-uac-box.png)

4. Windows Server 2016 화면에서 **지금 설치**를 선택합니다.

5. 인터넷에 연결된 디바이스의 경우 **업데이트 다운로드 및 설치(권장)** 를 선택합니다.

    ![중요한 Windows 업데이트를 가져오기 위해 온라인으로 전환하도록 선택하는 화면](media/upgrade-2012-2016/imp-updates-win-setup.png)

6. 설치 프로그램에서 디바이스 구성을 확인하고 작업이 완료될 때까지 기다린 다음, **다음**을 선택합니다.

7. Windows Server 미디어를 받은 배포 채널(일반 정품, 볼륨 라이선스, OEM, ODM 등)과 서버 라이선스에 따라 라이선스 키를 입력하여 계속 진행하라는 메시지가 표시될 수 있습니다.

    ![제품 키를 입력할 수 있는 화면](media/upgrade-2012-2016/enter-product-key.png)

8. 설치할 Windows Server 2016 버전을 선택한 다음, **다음**을 선택합니다.

    ![설치할 Windows Server 2016 버전을 선택하는 화면](media/upgrade-2012-2016/select-os-edition.png)

9. 배포 채널(예: 일반 정품, 볼륨 라이선스, OEM, ODM 등)에 따라 사용권 계약 조건에 동의하려면 **수락**을 선택합니다.

    ![사용권 계약에 동의하는 화면](media/upgrade-2012-2016/license-terms.png)

10. 현재 위치 업그레이드를 수행하려면 **개인 파일 및 앱 유지**를 선택한 다음, **다음**을 선택합니다.

    ![설치 유형을 선택하는 화면](media/upgrade-2012-2016/choose-install-upgrade.png)

11. 업그레이드가 권장되지 않는다는 페이지가 표시되는 경우 이를 무시하고 **확인**을 선택할 수 있습니다. 새로 설치를 묻는 메시지를 표시하기 위한 것이지만, 반드시 필요한 것은 아닙니다.

    ![업그레이드를 수행할 것인지 확인하는 확인 단추를 보여주는 화면](media/upgrade-2012-2016/confirm-upgrade-process.png)

12. 설치 프로그램에서 **프로그램 추가/제거**를 사용하여 Microsoft Endpoint Protection을 제거하라고 알려줍니다.

    이 기능은 Windows 10과 호환되지 않습니다.

13. 설치 프로그램에서 디바이스를 분석한 후 **설치**를 선택하여 업그레이드를 진행하라는 메시지가 표시됩니다.

    ![업그레이드를 시작할 준비가 되었음을 보여주는 화면](media/upgrade-2012-2016/ready-to-install.png)

    현재 위치 업그레이드가 시작되고 진행 상태와 함께 **Windows 업그레이드 중** 화면이 표시됩니다. 업그레이드가 완료되면 서버가 다시 시작됩니다.

    ![업그레이드 진행률을 보여주는 화면](media/upgrade-2012-2016/upgrading-windows-with-progress.png)

## <a name="after-your-upgrade-is-done"></a>업그레이드가 완료된 후

업그레이드가 완료된 후 Windows Server 2016으로의 업그레이드가 성공했는지 확인해야 합니다.

### <a name="to-make-sure-your-upgrade-was-successful"></a>업그레이드가 성공했는지 확인하려면 다음을 수행합니다.

1. 레지스트리 편집기를 열고 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion 하이브로 이동하여 **ProductName**을 확인합니다. Windows server 2016 버전이 표시되어야 합니다(예: **Windows Server 2016 Datacenter**).

2. 모든 애플리케이션이 실행 중이고 애플리케이션에 대한 클라이언트 연결이 성공적인지 확인합니다.

업그레이드하는 동안 문제가 발생했다고 생각되면 `%SystemRoot%\Panther`(일반적으로 `C:\Windows\Panther`) 디렉터리를 복사하여 압축하고 Microsoft 지원에 문의하세요.

## <a name="next-steps"></a>다음 단계

Windows Server 2016에서 Windows Server 2019로 한 번 더 업그레이드를 수행할 수 있습니다. 자세한 지침은 [Windows server 2016을 Windows Server 2019로 업그레이드](upgrade-2016-to-2019.md)를 참조하세요.

## <a name="related-articles"></a>관련된 문서

- Windows Server 2016에 대한 자세한 내용은 [Windows Server 2016 시작](https://docs.microsoft.com/windows-server/get-started/server-basics)을 참조하세요.