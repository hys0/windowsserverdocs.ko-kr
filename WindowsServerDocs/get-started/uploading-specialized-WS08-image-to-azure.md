---
title: Windows Server 2008/2008 R2 특수 이미지를 Azure에 업로드
description: Windows Server 2008 및 2008 R2 서비스가 종료될 예정입니다. 클라우드에서 Windows Server를 호스팅하여 Azure로 이동하는 방법을 알아봅니다.
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: mikeblodge
ms.author: mikeblodge
ms.date: 07/11/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.localizationpriority: high
ms.openlocfilehash: 19e4abf1573b8d3ee99b8e8828c1674f24d27695
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391497"
---
# <a name="upload-a-windows-server-20082008-r2-specialized-image-to-azure"></a>Windows Server 2008/2008 R2 특수 이미지를 Azure에 업로드 

![WS08 이미지 항목을 소개하는 배너](media/WS08-image-banner-large.png)

이제 Azure를 통해 클라우드에서 Windows Server 2008/2008 R2 VM을 실행할 수 있습니다. 

## <a name="prep-the-windows-server-20082008-r2-specialized-image"></a>Windows Server 2008/2008 R2 특수 이미지 준비
이미지를 업로드하기 전에 다음과 같이 변경합니다.

- 아직 이미지에 설치하지 않은 경우 Windows Server 2008 Service Pack 2(SP2)를 다운로드하여 설치합니다.

- 원격 데스크톱(RDP) 설정을 구성합니다.
  1. **제어판** > **시스템 설정**으로 이동합니다.   
  2. 왼쪽 메뉴에서 **원격 설정**을 선택합니다.

     !["원격 설정"을 강조 표시하는 시스템 설정의 스크린샷](media/1a_remote_settings.png)

  3. 시스템 속성에서 **원격** 탭을 선택합니다.   

     ![시스템 속성의 원격 탭 스크린샷](media/2c_sysprops.png)

  4. 모든 버전의 원격 데스크톱(보안 수준 낮음)을 실행하는 컴퓨터에서 연결 허용을 선택합니다.   
  5. **적용**, **확인**을 차례로 클릭합니다.
- Windows 방화벽 설정을 구성합니다.   
   1. 관리자 모드로 명령 프롬프트에서 Windows 방화벽 및 고급 보안 설정에 대해 "**wf.msc**"를 입력합니다.   
   2. 결과를 **포트**로 정렬하고 **포트 3389**를 선택합니다.   
     ![WIndows 방화벽 설정의 인바운드 규칙 스크린샷](media/3b_inboundrules.png)   
   3. 다음 프로필에 대해 원격 데스크톱(TCP-IN)을 사용하도록 설정합니다. **도메인**, **프라이빗** 및 **공용**(위에 표시 됨)

- 모든 설정을 저장하고 이미지를 종료합니다.   
- Hyper-V를 사용하는 경우 자식 AVHD가 지속적인 변경에 대해 상위 VHD에 병합되었는지 확인합니다.

현재 알려진 버그는 업로드된 이미지의 관리자 암호가 24시간 내에 만료되는 것입니다. 이 문제를 방지하려면 다음 단계를 수행합니다. 

1. **시작** > **실행**으로 이동
2. **lusrmgr.msc** 입력
3. 로컬 사용자 및 그룹에서 **사용자** 선택
4. **관리자**를 마우스 오른쪽 단추로 클릭하고 **속성** 선택
5. **암호 사용 기간 제한 없음**을 선택하고 **확인**
![관리자 속성의 스크린샷](media/6_adminprops.png) 선택

## <a name="uploading-the-image-vhd"></a>이미지 VHD 업로드
아래의 스크립트를 사용하여 VHD를 업로드할 수 있습니다. 이 작업을 수행하기 전에 Azure 계정에 대한 게시 설정 파일이 필요합니다. [Azure 파일 설정](https://azure.microsoft.com/downloads/)을 가져옵니다.

스크립트는 다음과 같습니다.

```powershell
Get-AzurePublishSettingsFile 

Login-AzureRmAccount
 
      # Import publishsettings
      Import-AzurePublishSettingsFile -PublishSettingsFile <LocationOfPublishingFile>
      $subscriptionId = 'xxxx-xxxx-xxxx-xxxx-xxxxx'
 
      # Set NodeFlight subscription as default subscription
      Select-AzureRmSubscription -SubscriptionId $subscriptionId
      Set-AzureRmContext -SubscriptionId $subscriptionId
      $rgName = "<resourcegroupname>"
    
      $urlOfUploadedImageVhd = "<BlobUrl>/<NameForVHD>.vhd"
      Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd -LocalFilePath "<FilePath>"  
```
## <a name="deploy-the-image-in-azure"></a>Azure의 이미지 배포
이 섹션에서는 Azure의 VHD 이미지를 배포합니다. 

> [!IMPORTANT]
> Azure의 미리 정의된 사용자 이미지를 사용하지 마십시오.

1.  새 [리소스 그룹](https://docs.microsoft.com/rest/api/resources/resourcegroups/createorupdate)을 만듭니다. 
2.  리소스 그룹 내에 새 [스토리지 Blob](https://docs.microsoft.com/rest/api/storageservices/put-blob)을 만듭니다.
3.  스토리지 Blob 내에 [컨테이너](https://docs.microsoft.com/rest/api/storageservices/create-container)를 만듭니다.
4.  속성에서 Blob 스토리지의 URL을 복사합니다.
5.  새 스토리지 Blob에 이미지를 업로드하려면 위에 제공된 스크립트를 사용합니다.
6.  VHD에 대한 [디스크](https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image)를 만듭니다.   
     a. 디스크로 이동하여 **추가**를 클릭합니다.  
     b. 디스크의 이름을 입력합니다. 사용할 구독을 선택하고 영역을 설정하고 계정 유형을 선택합니다.   
     c. 원본 유형에 대해 스토리지를 선택합니다. 스크립트를 사용하여 만든 Blob VHD 위치를 찾습니다.  
     d. 운영 체제 유형 Windows와 크기(기본값: 1023)를 선택합니다.   
     e. **만들기**를 클릭합니다.   

7.  만든 디스크로 이동하여 **VM 만들기**를 클릭합니다.   
     a. VM의 이름을 지정합니다.   
     b. 디스크를 업로드한 5단계에서 만든 기존 그룹을 선택합니다.   
     c. 크기와 VM에 대한 SKU 요금제를 선택합니다.   
     d. 설정 페이지에서 네트워크 인터페이스를 선택합니다. 네트워크 인터페이스에 다음과 같은 규칙이 지정되었는지 확인합니다.
 
        PORT:3389 Protocol: TCP Action: Allow Priority: 1000 Name: ‘RDP-Rule'.   
     e. **만들기**를 클릭합니다.




