---
title: "Windows Server 2016에에서 상태 서비스"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 5bc71e71-920e-454f-8195-afebd2a23725
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 834fcfb749e89e4768dce3f229564feea550a432
ms.sourcegitcommit: 30fcae929ce7b611f5d3a5f8fee64b0299272110
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2017
---
# <a name="health-service-in-windows-server-2016"></a>Windows Server 2016에에서 상태 서비스
> Windows Server 2016 적용 됩니다.

상태 서비스는 Storage Spaces Direct 실행 클러스터에 대 한 작동 경험과 일상적인 모니터링 개선 하는 Windows Server 2016의 새로운 기능입니다.

## <a name="prerequisites"></a>필수  

상태 서비스는 기본적으로 Storage Spaces Direct 함께 사용할 수 있습니다. 추가 작업 없이 시작 또는 설정 해야 합니다. Storage Spaces Direct에 대 한 자세한 내용은 [Windows Server 2016에 Storage Spaces Direct](../storage/storage-spaces/storage-spaces-direct-overview.md)합니다.  

## <a name="reports"></a>보고서

참조 [상태 서비스 보고](health-service-reports.md)합니다.

## <a name="faults"></a>오류

참조 [상태 서비스 오류](health-service-faults.md)합니다.

## <a name="actions"></a>작업

참조 [상태 서비스 작업](health-service-actions.md)합니다.

## <a name="automation"></a>자동화  

어떤 디스크 수명 주기의 Health 서비스에 의해 자동 워크플로에 대해 설명 합니다.  

### <a name="disk-lifecycle"></a>디스크 수명 주기   

상태 서비스의 하 여 실제 디스크 수명 주기 대부분 단계 자동화합니다. 이렇게 말 하세요 실제 디스크를 모두 제대로 작동 하는 완벽 한 건강-배포의 초기 상태 인지 봅시다 말하십시오.  

#### <a name="retirement"></a>사용 중지  

실제 디스크 더 이상 사용할 수와 해당 오류 발생 하는 경우 사용이 중지 자동으로 됩니다. 경우에 여러 가지가 있습니다.  

-   미디어 오류: 실제 디스크는 확실히 못했거나 깨진 하며 교체 해야 합니다.  

-   손실된 통신: 실제 디스크 연결이 끊긴 연속 넘는 15 분 동안 유지 합니다.  

-   응답 하지 않는 경우: 실제 디스크 대기 넘는 5.0 3 초 또는 번 1 시간 내 발생 했습니다.  

>[!NOTE]
> 연결이 끊어진 많은 실제 디스크를 한 번에 하거나 전체 노드 또는 스토리지 엔클로저, 건강 서비스는 *하지* 루트 문제가 있을 가능성이 하지 않으므로이 디스크를 중지 합니다.  

많은 실제 디스크에 대 한 캐시도 사용 중지 된 디스크 된 서비스 제공이 자동으로 다시 할당 다른 캐시 디스크를 사용할 수 있는 경우 합니다. 더 특별 한 사용자 작업이 필요 합니다.  

#### <a name="restoring-resiliency"></a>복구 복원  

하 여 실제 디스크는 사용이 중단 되 면 상태 서비스 즉시 시작 전체 복구를 복원 하려면 나머지 실제 디스크를에 해당 데이터를 복사 합니다. 완료 되 면 데이터가 완전히 안전한 되 고 오류 새롭게 허용 합니다.  

>[!NOTE]
> 즉시이 복원을 나머지 실제 디스크 충분 한 사용 가능한 용량이 필요합니다.  

#### <a name="blinking-the-indicator-light"></a>깜박이 표시등  

가능 하면 상태 서비스 깜박이 표시등 사용 중지 실제 디스크 또는 슬롯에 시작 됩니다. 이 무기한 때까지 계속 사용 중지 된 디스크 대체 됩니다.  

>[!NOTE]
> 경우에 따라 디스크 되지 않았습니다도 표시등에 불이 작동-에 의해 지 원하는 방식으로 예를 들어, 총 정전.  

#### <a name="physical-replacement"></a>실제 교체  

가능한 한 사용 중지 실제 디스크를 교체 해야 합니다. 대부분의 경우이 이루어져는 핫-교체-즉 전원 끄기 노드 또는 저장소 엔클로저 필요 하지 않습니다. 유용한 위치와 일부 정보에 대 한 오류를 표시 합니다.  

#### <a name="verification"></a>확인

교체 디스크를 넣은 경우에 대해 지원 되는 구성 요소 문서 확인할 수 됩니다 (다음 섹션 참조).

#### <a name="pooling"></a>풀링을  

이 허용 교체 디스크를 사용 하 여 입력 풀은 이전 버전에 자동으로 대체 됩니다. 이 시점 시스템 초기 상태로 완벽 한 상태를 반환 되 고 오류 사라집니다.  

## <a name="supported-components-document"></a>지원 되는 구성 요소 문서  

상태 서비스는 구성 요소 Storage Spaces Direct 관리자 계정 또는 솔루션 공급 업체에서 제공 하는 지원 되는 구성 요소 문서에서 사람에 게 사용을 제한 하는 집행 메커니즘을 제공 합니다. 이 사용할 수 지원 되지 않는 하드웨어가 잘못된 사용 하지 못하도록 사용자나 다른 앱에서 있는 보증 또는 지원 계약 준수 하는 데 도움이 될 수 있습니다. 이 기능은 현재 제한 Ssd Hdd를 포함 하 여 실제 디스크를 디바이스 및 NVMe 드라이브. (옵션) 제조업체 모델과 펌웨어 버전 (선택 사항)에서 지원 되는 구성 요소 문서 제한할 수 있습니다.

### <a name="usage"></a>사용  

지원 되는 구성 요소 문서 XML 표하고자 구문을 사용합니다. Visual Studio 코드 등의 사용자 좋아하는 텍스트 편집기를 사용 하는 것이 좋습니다 (사용할 수 있는 무료 [여기](http://code.visualstudio.com/)) 또는 메모장 저장 하 고 다시 사용할 수 있는 XML 문서를 만듭니다.

#### <a name="sections"></a>섹션

문서에는 두 가지 독립 섹션이: **디스크** 및 **캐시**합니다.

하는 경우는 **디스크** 풀에 나열 된 드라이브에만 허용, 섹션 제공 됩니다. 드라이브가 나열 되지 않은 프로덕션에서 자녀가 사용 하는 효과적으로 의해 풀에 참석 방지 됩니다. 이 섹션을 비워 풀에 참여 하는 모든 드라이브 허용 됩니다.

하는 경우는 **캐시** 섹션을 캐싱에 나열 된 드라이브에만 사용 됩니다. 이 섹션은 비어 Storage Spaces Direct는 하려고 추측 미디어 유형과 버스 종류에 따라 합니다. 예를 들어, 배포 반도체 드라이브 (SSD)와 하드 디스크 드라이브 (HDD)를 사용 하는 경우 이전는 자동으로 선택 캐싱; 그러나 모든 flash를 사용 하는 배포 캐싱 여기에 사용 하려는 높은 지속 시간과 장치 지정 해야 합니다.

>[!IMPORTANT]
> 지원 되는 구성 요소 문서 및 사용을 이미 풀 드라이브로 이전의 적용 되지 않습니다.  

#### <a name="example"></a>예제  

```XML
<Components>

  <Disks>
    <Disk>
      <Manufacturer>Contoso</Manufacturer>
      <Model>XYZ9000</Model>
      <AllowedFirmware>
        <Version>2.0</Version>
        <Version>2.1</Version>
        <Version>2.2</Version>
      </AllowedFirmware>
      <TargetFirmware>
        <Version>2.1</Version>
        <BinaryPath>\\path\to\image.bin</BinaryPath>
      </TargetFirmware>
    </Disk>
  </Disks>

  <Cache>
    <Disk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </Disk>
  </Cache>

</Components>

```

여러 개의 드라이브를 표시 하려면 추가 하기만 하면 추가 ** &lt;디스크&gt; ** 태그 중 섹션에 있습니다.

Storage Spaces Direct 배포할 때이 XML 넣기를 사용 하 여 **XML** 플래그:

```PowerShell
Enable-ClusterS2D -XML <MyXML>
```

를 설정 하거나 Storage Spaces Direct 배포한 (즉, 건강 서비스가 실행 되 면 이미) 되 면 구성 요소 지원 되는 문서를 수정 하려면 다음 PowerShell cmdlet 사용:

```PowerShell
$MyXML = Get-Content <\\path\to\file.xml> | Out-String  
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $MyXML  
```

>[!NOTE]
>모델, 제조업체 및 펌웨어 버전 속성 사용 하 여 다운로드 값 일치 해야는 **Get 실제 디스크** cmdlet 합니다. 공급 업체의 구현 따라 "상식"도 기대에서 다를 수 있습니다. 예를 들어, "Contoso" 대신 제조업체 "CONTOSO-LTD" 중이거나 모델은 "Contoso XZY9000" 비어 있을 수 있습니다.  

다음 PowerShell cmdlet 사용 하 여 확인할 수 있습니다.  

```PowerShell
Get-PhysicalDisk | Select Model, Manufacturer, FirmwareVersion  
```

## <a name="settings"></a>설정

참조 [상태 서비스 설정](health-service-settings.md)합니다.

## <a name="see-also"></a>참조 하십시오

- [건강 서비스 보고서](health-service-reports.md)
- [건강 서비스 오류](health-service-faults.md)
- [건강 서비스 작업](health-service-actions.md)
- [건강 서비스 설정](health-service-settings.md)
- [Windows Server 2016에에서 저장소 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md)
