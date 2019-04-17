---
title: "원격으로 관리 되는 서버에 대 한 서버 복구 DVD 만들기"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-server-recovery-dvd-for-remotely-administered-servers"></a>원격으로 관리 되는 서버에 대 한 서버 복구 DVD 만들기

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

##  <a name="BKMK_HeadlessRecovery"></a>원격으로 관리 되는 서버에 대 한 서버 복구 DVD 만들기  
 두 가지 모델 공장 초기화 서버 복구 하 고 고객이 받은 하드웨어에 따라 달라 집니다.  
  
 **원격 서버 관리**  
  
 이 서버 복구 옵션을 사용 하려면 같은 네트워크에 프로세스가 클라이언트 컴퓨터에서 실행 됩니다. 하드웨어 관련 이미지를 서버와 배송 될 공장 초기화 하므로 파트너 서버 복구 DVD 작성 합니다.  
  
 **로컬에서 서버 관리**  
  
 클래식 모델 서버 콘솔에서 서버 관리 되는 위치입니다. 서버 설치 미디어 복구를 실행 하는 데 사용 됩니다. 서버 비디오 출력 DVD 판독기 외에도 볼 수 있는 함께 제공 되 필요 합니다. 고객이 해당 서버 설치 미디어에서 부팅 하 고 적절 한 복구 방법을 선택 합니다. 로컬에서 관리 하는 서버에 대 한 서버 복구 DVD 만들기 필요가 없습니다.  
  
> [!NOTE]
>  로컬 관리 서버 모델에 대 한 고객 새로 설치 하 여 초기화 공장을 수행할 수 있습니다. 그러나 분실 됩니다 파트너 사용자 지정 합니다.  
  
 두 가지 유형의 서버 복구 가지가 있습니다.  
  
 **공장 초기화**  
  
 이 복구 서버 공장에서 배송 때을 원래 상태로 서버를 반환 합니다. 공장 초기화를 수행 서버 초기 구성 처음으로 켰을 때, 된 것 처럼 작업을 수행 하 라는 메시지가 표시 되 고 모든 설정 및 사용자 지정 손실 됩니다. 이 라고도 일 0? 하드웨어 관련 이미지를 서버와 배송 될 공장 초기화 하므로 파트너 서버 복구 DVD 작성 합니다.  
  
 **완전 복원**  
  
 이 복구 가정 서버 백업 구성 되어 있는지와 서버 백업 한 번 이상 서버 오류 전에 성공적으로 완료 합니다. 완전 복원 (BMR) 서버 이전 백업에서 시스템 및 부팅 드라이브 복구를 지원합니다.  
  
 이후에 BMR 서버 백업 복원에 사용 되는 시간에 존재 하는 상태로 돌아갑니다. 이 일반적으로 최신 백업 있지만 경우에 따라 이전 백업 것일 수 있습니다. 복원할 파일 및 폴더 마법사를 사용 하 여 시스템 복원 된 후 데이터 복구가 이루어집니다. BMR 되므로 기본 서버 복구 방법을 모든 설정 및 구성 반환 됩니다 공장 초기화 하루 0 상태로 서버 반환 반면 합니다.  
  
### <a name="remotely-administered-server-recovery"></a>원격 서버 관리  
 파트너 수행 해야 하는 필요한 사용자 지정 하 고 각 서버와 함께 제공 해야 하는 최종 미디어에 설명 합니다. 세부 정보를 살펴보기 하기 전에 사용자 환경 개선에 찾습니다 알려 주세요.  
  
 이 경우 고객의에서 "s 서버™ 더 이상 작동 합니다. 바이러스, 하드 디스크 오류 또는 기타 원인을 때문일 수 있습니다. 고객이 서버와 같은 네트워크에 있는 클라이언트 컴퓨터에 DVD 서버 복구를 삽입 합니다. 서버 복구 응용 프로그램을 단계별로 자신의 서버를 복구 하려면 다음 3 단계:  
  
1.  복구 모드로 서버를 다시 시작 하는 데 사용 되는 부팅 가능한 USB 플래시 드라이브를 만듭니다. USB 플래시 드라이브에는 8GB 있어야 더 크게 또는 합니다.  
  
2.  이제 복구 모드에 있는 서버를 검색 합니다.  
  
3.  고객 공장 초기화 또는 복원 완전 선택할 수 있게 하 고 서버 작업 상태로 돌아갑니다.  
  
### <a name="steps-for-creating-a-server-recovery-dvd-for-multiple-language-support"></a>여러 언어에 대 한 서버 복구 DVD 만들기 위한 단계 지원  
 6 가지 주요 단계로 서버 복구 DVD 만들기  
  
1.  [(선택 사항) 업데이트 WinPE](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Updating)  
  
2.  [수집 공장 초기화 이미지 및 XML 파일](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Collecting)  
  
3.  [서버 복구 DVD 만들기](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Creating)  
  
4.  [마법사를 사용자 지정](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Customizing)  
  
5.  [ISO 파일 만들기](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_CreatingISO)  
  
6.  [복구 DVD 테스트](Create-a-Server-Recovery-DVD-for-Remotely-Administered-Servers.md#BKMK_Testing)  
  
####  <a name="BKMK_Updating"></a>1 단계: 업데이트 (선택 사항) WinPE  
 ADK은 사용자 지정 된 Windows PE의 복사본을 포함 합니다. 이 이미지 부팅 되 면 자동으로 복구 모드로 서버에 연결 하는 클라이언트 복구 응용 프로그램에서 사용 되는 신호를 시작 합니다.  
  
 Windows PE 추가 된 하드웨어 관련 드라이버가 네트워크나 디스크 컨트롤러 드라이버 등을 추가 하 여 사용자 지정 해야 합니다. WinPE에서 부팅 후 시스템에서 하드 디스크 인식할 수 없는 고 네트워크를 사용할 수 있어야 합니다.  
  
####  <a name="BKMK_Collecting"></a>2 단계: 수집 공장 초기화 이미지 및 XML 파일  
 서버를 다시 설정 방법, 다음 두 가지 이미지가 캡처될 수 해야 합니다.  
  
-   드라이브 시스템 이미지  
  
-   예약 된 시스템 파티션  
  
 이러한 이미지 캡처를 GenDiskXML.exe 도구가 제공 됩니다. 또한 GenDiskXML.exe disk.xml 복구 과정을 다시 디스크 구성 하는 데 사용 되는 파일을 수집 합니다.  
  
1.  Sysprep, 다음 Windows PE의 모든 64 비트 버전을 사용 하 여 시스템을 다시 부팅 합니다.  
  
2.  출력 외부 원본.xml 및.wim 파일을 실행 `GenDiskXML /outputdir:<path>`출력 외부 소스.xml 및.wim 파일을 합니다. 파일을 DVD 다음 단계에 추가 됩니다.  
  
    > [!NOTE]
    >  시스템.wim 파일 4GB 보다 큰 없는 파일의 f a t 32 요구 사항에 맞게 분할 됩니다. 프로세스 중 캡처.wim 파일에 사용 되는 대상 필요한 용량이 8GB 분할 프로세스에 맞게 보다 큰 수 있어야 합니다.  
  
####  <a name="BKMK_Creating"></a>3 단계: 서버 복구 DVD 만들기  
 각 서버 공장에서 배송 서버 복구 DVD가 포함 되어 있어야 합니다. ADK 도구 DVD DVD 만드는 데 필요한 파일을 포함 합니다.  
  
###### <a name="to-create-the-server-recovery-dvd"></a>서버 복구 DVD를 만들려면  
  
1.  작동 위치와 최종 ISO를 저장 하는 데 사용 하 여 폴더를 만듭니다.  
  
2.  파트너 CD에서 복사의 내용을 **서버 복구** 1 단계에서에서 만든 작업 폴더에 폴더 합니다.  
  
3.  GenDiskXML.exe를 실행할 때 만든 disk.xml 파일 복사는 **초기화** 폴더 합니다.  
  
4.  이미지를 실행할 때 생성 된 파일을 복사 **GenDiskXML.exe** 하 고 **초기화** 폴더 합니다. 파일은.wim 및.swm 파일 및 파일 수 다를 수 있습니다.  
  
5.  GenDiskXML.exe 폴더에서 제거 합니다. 공장 목적 으로만 사용 되 고 고객에 게 제공 되는 DVD에 포함 되지 않은 해야 합니다.  
  
####  <a name="BKMK_Customizing"></a>4 단계: 마법사를 사용자 지정  
 디바이스와 특정 디바이스를 복구 모드로 시작 하는 방법을 설명 하는 텍스트 이미지 서버 복구 응용 프로그램을 사용자 지정 해야 합니다. 이 페이지 복원 된 파일 및 폴더 마법사의 특정 하드웨어 때문 서버 복구 모드로 시작 하려면 단계가 달라 집니다.  
  
> [!NOTE]
>  나열 된 파일 이름을 정확 하 게 일치 해야 합니다.  
  
1.  마법사 페이지에 대 한 추가 도움말 링크가 있습니다. 이.chm 파일이 있는 경우 홈 그룹에 대 한 웹 도움말 FWLink 무시 합니다. 도움말 파일은 위치에 있습니다.  
  
     < DVD Root\ > < 문화 name\ > \\$OEM$\Customization\\ \RestartHelp.chm  
  
2.  이 파일 마법사 페이지에서 고객에 게 표시 되는 텍스트를 포함 합니다. 텍스트 서버 복구 모드로 부팅 하는 방법을 설명 해야 합니다. 컨트롤을 스크롤, 텍스트 추가할 수 있는 금액에 제한이 장소입니다.  
  
     다음 파일 마법사에 예제 그림을 대체 하는 데 사용 되 고 브랜드 정도 떨어진 주로 합니다. .Png 파일 여야 합니다. 파일 크기 256 x 256 픽셀 픽셀 이거나 마법사에 표시 되 면 잘립니다.  
  
     < DVD Root\ > < 문화 name\ > \\$OEM$\Customization\\ \RestartInstructions.rtf  
  
3.  < DVD Root\ > < 문화 name\ > \\$OEM$\Customization\\ \ServerImage.png  
  
 여러 언어를 지원 하기 위해 DVD 서버 복구 변환 하는 경우 다음을 수행 하면 있는지 확인 합니다.  
  
1.  En는 항상 있어야-데 폴더 합니다. En을 다시 폭포 서버 복구 응용 프로그램에서 실행 되는 클라이언트 컴퓨터와 일치 하는 특정 문화의 파일을 찾지 못하면 경우-해 주세요.  
  
2.  사용자가 만든 각 문화의 폴더를 추가 세 가지 사용자 지정 파일 (.png,.chm, 및.rtf).  
  
3.  서버 복구 DVD 루트 \Server 언어 Packs\\ < CultureName\ > 복구에서에서 문화 폴더를 모두 복사 합니다. 예를 들어: ES 및 ES ES 폴더 스페인어 지원 하기 위해 DVD 루트 복사할 수는 있습니다.  
  
4.  ISO 파일을 완료 합니다.  
  
 지원 되는 문화의 이름 다음과 같습니다.  

|-|-|  
|-Cs-CZ<br /><br /> -De-DE<br /><br /> -En-US<br /><br /> -Es-ES<br /><br /> -Fr-FR<br /><br /> -Hu-HU<br /><br /> -It-IT<br /><br /> -Ja-JP<br /><br /> -Ko-KR<br /><br /> -Nl-NL |-PL-PL<br /><br /> -Pt-BR<br /><br /> -Pt-PT<br /><br /> -Ru-RU<br /><br /> -Sv-SE<br /><br /> -Tr-TR<br /><br /> -Zh-CN<br /><br /> -Zh-HK<br /><br /> -Zh-TW
  
####  <a name="BKMK_CreatingISO"></a>5 단계: ISO 파일 만들기  
 DVD로 작성 된 폴더 한 모든 내용을 구울 수 있습니다. DVD와 새로운 서버를 함께 고객에 게 제공할 수 있는입니다.  
  
####  <a name="BKMK_Testing"></a>6 단계: 테스트 DVD 복구  
 서버 설치를 완료 한 후 서버 백업을 구성, 서버 백업의 실행 하 고 복구 DVD를 테스트 합니다.  
  
###### <a name="to-configure-and-run-a-server-backup"></a>구성 하 고 서버 백업 실행 하려면  
  
1.  대시보드 열을 클릭는 **디바이스** 탭을 클릭 한 다음 **서버에 대 한 백업 설정** 에 **작업** 창 합니다.  
  
2.  백업 서버 백업을 구성 하 고 마법사의 지침을 따릅니다. 백업 외장 하드 디스크 필요합니다.  
  
3.  클릭 **서버에 대 한 백업을 시작** 에 **작업** 창 한 다음 마법사의 지침을 따릅니다.  
  
4.  백업을 완료 되 면 성공 했는지 확인 합니다.  
  
###### <a name="to-restore-a-server"></a>서버를 복원 하려면  
  
1.  허브 나 스위치를 통해 서버와 같은 네트워크에 연결 하는 클라이언트 컴퓨터 복구를 만든 DVD를 넣습니다.  
  
2.  두 번 클릭 **setup.exe**합니다. 서버 복구 묻는 고객 나오는 동일한 프로세스를 진행 합니다.  
  
3.  클릭 **서버 백업에서 복원**, 한 다음 마법사의 지침을 따릅니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)