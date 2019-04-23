---
title: 원격 관리 서버에 대한 서버 복구 DVD 만들기
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6141fa69-5952-4e3c-a868-40ef3f4badd2
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 7bfe1686ac84962cdb4ab1cde8d6ca5226cb9d44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844354"
---
# <a name="create-a-server-recovery-dvd-for-remotely-administered-servers"></a>원격 관리 서버에 대한 서버 복구 DVD 만들기

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_HeadlessRecovery"></a> 원격으로 관리 되는 서버에 대 한 서버 복구 DVD 만들기  
 공장 기본 설정 및 서버 복구 모델에는 두 가지가 있으며, 고객에게 제공된 하드웨어에 따라 사용되는 모델이 다릅니다.  
  
 **원격 관리 서버**  
  
 이 서버 복구 옵션을 사용하려면 동일한 네트워크에 있는 클라이언트 컴퓨터에서 프로세스를 실행해야 합니다. 공장 기본 설정 복원을 위해서는 하드웨어별 이미지가 서버와 함께 출고되어야 하므로 파트너가 반드시 서버 복구 DVD를 제작해야 합니다.  
  
 **로컬 관리 서버**  
  
 서버가 서버 콘솔에서 관리되는 일반 모델입니다. 복구를 실행하는 데 서버 설치 미디어가 사용되며, 서버에 DVD 판독기 외에 비디오 출력을 볼 수 있는 기능이 있어야 합니다. 고객은 이 서버 설치 미디어에서 부팅한 다음 적절한 복구 방법을 선택합니다. 로컬로 관리되는 서버에 대한 서버 복구 DVD를 만들 필요는 없습니다.  
  
> [!NOTE]
>  로컬로 관리되는 서버 모델의 경우 고객은 새 설치를 실행하여 공장 기본 설정을 수행할 수 있습니다. 하지만 파트너 사용자 지정 내용을 잃게 됩니다.  
  
 서버 복구에는 두 가지 유형이 있습니다.  
  
 **공장 기본 설정**  
  
 이 복구 유형은 서버를 공장에서 출고될 당시의 원래 상태로 되돌립니다. 공장 기본 설정 후, 처음 서버를 켰을 때 및 모든 설정과 사용자 지정이 손실되었을 때처럼 서버의 초기 구성을 수행할 것인지 묻는 메시지가 표시됩니다. 이 라고도 0 일? 공장 기본 설정 복원을 위해서는 하드웨어별 이미지가 서버와 함께 출고되어야 하므로 파트너가 반드시 서버 복구 DVD를 제작해야 합니다.  
  
 **완전 복구**  
  
 이 복구 유형은 서버 백업을 구성했으며, 서버 오류가 발생하기 전에 한 번 이상 서버 백업이 성공적으로 완료된 것으로 가정합니다. BMR(완전 복구)은 이전 서버 백업에서의 시스템 및 부팅 드라이브 복구만 지원합니다.  
  
 BMR 후 서버는 복원에 사용되는 백업 시에 존재했던 상태로 되돌아갑니다. 이 백업은 일반적으로 가장 최근 백업이지만 경우에 따라 이전 백업일 수도 있습니다. 파일 및 폴더 복원 마법사를 사용하여 시스템이 복원된 후에 데이터 복구가 수행됩니다. 모든 설정 및 구성이 되돌려지므로 BMR이 기본 설정 서버 복구 방법인 반면, 공장 기본 설정은 서버를 0일 상태로 되돌립니다.  
  
### <a name="remotely-administered-server-recovery"></a>원격 관리 서버 복구  
 이 섹션은 파트너가 반드시 수행해야 하는 필수 사용자 지정과 각 서버와 함께 제공되어야 하는 최종 미디어에 관해 설명합니다. 세부 정보를 살펴보기 전에 먼저 고객 환경에 대해 알아보겠습니다.  
  
 이 시나리오에서는 고객이 "™의 서버가 작동 하지 않습니다. 이는 바이러스, 하드 디스크 오류 또는 다른 사유 때문일 수 있습니다. 고객이 서버 복구 DVD를 서버와 동일한 네트워크에 있는 클라이언트 컴퓨터에 삽입합니다. 서버 복구 응용 프로그램이 해당 서버를 복구하기 위한 3단계를 안내합니다.  
  
1.  서버를 복구 모드로 다시 시작하는 데 사용되는 부팅 가능 USB 플래시 드라이브를 만듭니다. USB 플래시 드라이브는 8GB 이상이어야 합니다.  
  
2.  현재 복구 모드에 있는 서버를 검색합니다.  
  
3.  고객은 공장 기본 설정 또는 완전 복구를 선택하여 서버를 작동 상태로 되돌릴 수 있습니다.  
  
### <a name="steps-for-creating-a-server-recovery-dvd-for-multiple-language-support"></a>다중 언어 지원을 위한 서버 복구 DVD를 만드는 단계  
 서버 복구 DVD 만들기는 6개의 주요 단계로 구성됩니다.  
  
1.  [(선택 사항) WinPE 업데이트](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Updating)  
  
2.  [공장 재설정 이미지 및 XML 파일 수집](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Collecting)  
  
3.  [서버 복구 DVD 만들기](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Creating)  
  
4.  [마법사 사용자 지정](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Customizing)  
  
5.  [ISO 파일 만들기](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_CreatingISO)  
  
6.  [복구 DVD 테스트](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Testing)  
  
####  <a name="BKMK_Updating"></a> 1 단계: (선택 사항) WinPE 업데이트  
 ADK에는 사용자 지정된 Windows PE가 포함되어 있습니다. 이 이미지를 부팅하면 클라이언트 복구 응용 프로그램에서 복구 모드의 서버에 연결하는 데 사용되는 탐지 장치가 자동으로 시작됩니다.  
  
 네트워크 또는 디스크 컨트롤러 드라이버와 같은 하드웨어별 드라이버를 추가하여 Windows PE를 한층 더 사용자 지정해야 합니다. WinPE에서 부팅한 후에는 시스템의 하드 디스크를 인식할 수 있어야 하며 네트워크가 작동해야 합니다.  
  
####  <a name="BKMK_Collecting"></a> 2 단계: 공장 기본 설정 이미지 및 XML 파일 수집  
 서버를 공장 기본값으로 다시 설정하려면 다음 두 이미지를 캡처해야 합니다.  
  
-   시스템 드라이브 이미지  
  
-   시스템에서 사용하는 파티션  
  
 이러한 이미지 캡처를 위해 GenDiskXML.exe 도구가 제공됩니다. GenDiskXML.exe는 복구 프로세스에서 디스크 구성을 다시 만드는 데 사용되는 disk.xml이라는 파일도 수집합니다.  
  
1.  Sysprep 후 64비트 버전의 Windows PE를 사용하여 시스템을 다시 부팅합니다.  
  
2.  .xml 및 .wim 파일을 외부 원본에 출력하려면 `GenDiskXML /outputdir:<path>` 를 실행합니다. 다음 단계에서 파일이 DVD에 추가됩니다.  
  
    > [!NOTE]
    >  파일이 4GB 이하여야 하는 FAT32 요구 사항을 충족하도록 시스템 .wim 파일이 분할됩니다. 이 프로세스가 진행되는 동안에는 .wim 파일을 캡처하는 데 사용되는 대상의 필요한 용량이 분할 프로세스를 수용할 수 있도록 8GB보다 커야 합니다.  
  
####  <a name="BKMK_Creating"></a> 3 단계: 서버 복구 DVD 만들기  
 공장에서 출고되는 각 서버는 서버 복구 DVD와 함께 제공되어야 합니다. ADK 도구 DVD에는 DVD 작성을 위해 필요한 파일이 포함되어 있습니다.  
  
###### <a name="to-create-the-server-recovery-dvd"></a>서버 복구 DVD를 만들려면  
  
1.  최종 ISO를 저장하는 위치로 사용할 작업 폴더를 만듭니다.  
  
2.  파트너 CD에서 **서버 복구** 폴더의 내용을 1단계에서 생성한 작업 폴더로 복사합니다.  
  
3.  GenDiskXML.exe를 실행했을 때 만들어진 disk.xml 파일을 **Reset** 폴더에 복사합니다.  
  
4.  **GenDiskXML.exe**를 실행했을 때 만들어진 이미지 파일을 **Reset** 폴더에 복사합니다. 이러한 파일은 .wim 및 .swm 파일이며 파일 수는 상황에 따라 다를 수 있습니다.  
  
5.  폴더에서 GenDiskXML.exe를 제거합니다. 이는 공장에서만 사용되므로 고객에게 제공되는 DVD에 포함되어서는 안 됩니다.  
  
####  <a name="BKMK_Customizing"></a> 4 단계: 마법사 사용자 지정  
 서버 복구 응용 프로그램은 장치 이미지 및 특정 장치를 복구 모드로 시작하는 방법을 설명하는 텍스트로 사용자 지정되어야 합니다. 파일 및 폴더 복원 마법사의 이 페이지는 하드웨어에 관련된 것이므로 서버를 복구 모드로 시작하는 단계는 달라질 수 있습니다.  
  
> [!NOTE]
>  나열된 파일 이름은 정확히 일치해야 합니다.  
  
1.  마법사 페이지에는 추가 도움말에 대한 링크가 포함되어 있습니다. 이 .chm 파일이 있는 경우 웹 도움말에 대한 FWLink가 이 파일로 재정의됩니다. 도움말 파일은 다음 위치에 있습니다.  
  
     < 루트 DVD\>\\$OEM$ \Customization\\< 문화권 이름\>\RestartHelp.chm  
  
2.  이 파일에는 마법사 페이지에 표시되는 텍스트가 포함되어 있습니다. 이 텍스트는 서버를 복구 모드로 부팅하는 방법을 설명합니다. 컨트롤은 스크롤 가능하므로 추가할 수 있는 텍스트 양을 실용적으로 제한합니다.  
  
     다음 파일은 마법사의 샘플 그림을 대체하는 데 사용되며 주로 브랜딩에 관한 것입니다. 이 파일은 .png 파일이며, 파일 크기는 256 x 256 픽셀이어야 합니다. 그렇지 않으면 마법사에 표시될 때 잘립니다.  
  
     < 루트 DVD\>\\$OEM$ \Customization\\< 문화권 이름\>\RestartInstructions.rtf  
  
3.  < 루트 DVD\>\\$OEM$ \Customization\\< 문화권 이름\>\ServerImage.png  
  
 다중 언어를 지원하도록 서버 복구 DVD를 변환하려면 다음을 수행해야 합니다.  
  
1.  항상 en-us 폴더가 있어야 합니다. 서버 복구 응용 프로그램이 실행되고 있는 클라이언트 컴퓨터와 일치하는 문화권별 파일이 없는 경우 en-us로 대체됩니다.  
  
2.  만드는 각 문화권 폴더에 세 가지 사용자 지정 파일(.png, .chm 및 .rtf)을 추가합니다.  
  
3.  언어 팩에서의 두 문화권 폴더를 복사\\< CultureName\>\Server Recovery 서버 복구 DVD의 루트에 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. 스페인어를 지원하려면 ES 폴더와 ES-ES 폴더를 둘 다 DVD의 루트에 복사합니다.  
  
4.  ISO 파일을 마무리합니다.  
  
 지원되는 문화권 이름은 다음과 같습니다.  

|-|-|  
|- cs-CZ<br /><br /> -DE-DE<br /><br /> -영어-미국<br /><br /> -원본: ES-ES<br /><br /> - fr-FR<br /><br /> -HU-HU<br /><br /> -it IT<br /><br /> -JA-JP<br /><br /> - ko-KR<br /><br /> -NL-NL |-PL-PL<br /><br /> -PT-BR<br /><br /> -PT-PT<br /><br /> -RU-RU<br /><br /> -SV-SE<br /><br /> -TR-TR<br /><br /> - zh-CN<br /><br /> - zh-HK<br /><br /> - zh-TW
  
####  <a name="BKMK_CreatingISO"></a> 5 단계: ISO 파일 만들기  
 만들어진 폴더 및 모든 내용을 DVD로 구울 수 있습니다. 이는 새 서버와 함께 고객에게 제공되는 DVD입니다.  
  
####  <a name="BKMK_Testing"></a> 6 단계: 복구 DVD 테스트  
 서버 설치를 완료한 후에는 서버 백업을 구성하고 실행한 다음 복구 DVD를 테스트합니다.  
  
###### <a name="to-configure-and-run-a-server-backup"></a>서버 백업을 구성하고 실행하려면  
  
1.  대시보드를 열고 **장치** 탭을 클릭한 다음 **작업** 창에서 **서버에 대한 백업 설정**을 클릭합니다.  
  
2.  마법사의 안내를 따라 백업 서버 백업을 구성합니다. 백업에는 외부 하드 디스크가 필요합니다.  
  
3.  **작업** 창에서 **서버 백업 시작** 을 클릭한 다음 마법사의 안내를 따릅니다.  
  
4.  백업이 완료되면 백업에 성공했는지 확인합니다.  
  
###### <a name="to-restore-a-server"></a>서버를 복원하려면  
  
1.  만든 복구 DVD를 허브 또는 스위치를 통해 서버와 동일한 네트워크에 연결된 클라이언트 컴퓨터에 삽입합니다.  
  
2.  **setup.exe**를 두 번 클릭합니다. 서버 복구 마법사가 고객이 수행하는 것과 동일한 프로세스를 안내합니다.  
  
3.  **백업에서 서버 복원**을 클릭한 다음 마법사의 안내를 따릅니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)