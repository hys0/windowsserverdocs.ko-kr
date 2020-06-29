---
title: Windows Server의 상태 관리 서비스
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 5bc71e71-920e-454f-8195-afebd2a23725
author: cosmosdarwin
ms.date: 02/09/2018
ms.openlocfilehash: 1b607869245ff46bd01824ebe4392e283be50b0d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473080"
---
# <a name="health-service-in-windows-server"></a>Windows Server의 상태 관리 서비스

> 적용 대상: Windows Server 2019, Windows Server 2016

상태 관리 서비스는 스토리지 공간 다이렉트를 실행 하는 클러스터에 대 한 일상적인 모니터링 및 운영 환경을 개선 하는 Windows Server 2016의 새로운 기능입니다.

## <a name="prerequisites"></a>전제 조건

상태 관리 서비스는 스토리지 공간 다이렉트에서 기본적으로 사용됩니다. 설정하거나 시작하기 위해 필요한 추가 작업이 없습니다. 스토리지 공간 다이렉트에 대 한 자세한 내용은 [Windows Server 2016의 스토리지 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md)를 참조 하세요.

## <a name="reports"></a>보고서

[상태 관리 서비스 보고서](health-service-reports.md)를 참조 하세요.

## <a name="faults"></a>오류

[상태 관리 서비스 오류](health-service-faults.md)를 참조 하세요.

## <a name="actions"></a>동작

[상태 관리 서비스 작업](health-service-actions.md)을 참조 하세요.

## <a name="automation"></a>Automation

이 섹션에서는 디스크 수명 주기 동안 상태 관리 서비스에서 자동화되는 워크플로를 설명합니다.

### <a name="disk-lifecycle"></a>디스크 수명 주기

상태 관리 서비스는 실제 디스크 수명 주기의 대부분의 단계를 자동화합니다. 배포 초기 상태가 완벽한 상태, 즉 모든 실제 디스크가 올바르게 작동하는 중이라고 가정해 봅니다.

#### <a name="retirement"></a>사용 중지

더 이상 사용할 수 없고 해당하는 오류가 발생한 경우 실제 디스크가 자동으로 사용 중지됩니다. 몇 가지 사례가 있습니다.

-   미디어 오류: 실제 디스크가 최종적으로 결함이 있거나 손상된 경우 교체해야 합니다.

-   연결이 끊어짐: 실제 디스크에서 연속 15분 동안 연결이 끊어진 상태입니다.

-   응답 없음: 실제 디스크에서 1시간 이내에 5.0초 이상의 대기 시간이 3번 이상 발생한 경우입니다.

>[!NOTE]
> 여러 실제 디스크에 대한 연결이 한 번에 끊어졌거나 전체 노드 또는 스토리지 엔클로저에 대한 연결이 끊어진 경우 이러한 디스크는 근본 문제가 아니므로 상태 관리 서비스에서 이러한 디스크를 사용 중지하지 *않습니다*.

사용 중지된 디스크가 다른 여러 실제 디스크의 캐시 역할을 하는 경우 다른 캐시 디스크에 자동으로 다시 할당됩니다(사용 가능한 경우). 사용자 작업이 필요하지 않습니다.

#### <a name="restoring-resiliency"></a>복원력 복원

실제 디스크가 사용 중지되면 상태 관리 서비스에서 즉시 해당 데이터를 나머지 실제 디스크에 복사하거나 전체 복원력을 복원합니다. 이 작업이 완료되면 데이터가 완전히 안전해지고 다시 내결함성이 생깁니다.

>[!NOTE]
> 이 즉시 복원을 수행하려면 나머지 실제 디스크에 충분한 사용 가능한 용량이 있어야 합니다.

#### <a name="blinking-the-indicator-light"></a>깜박이는 표시등

가능한 경우 상태 관리 서비스는 사용 중지된 실제 디스크 또는 슬롯에서 표시등을 깜박이기 시작합니다. 이는 사용 중지된 디스크가 교체될 때까지 무기한 계속됩니다.

>[!NOTE]
> 경우에 따라 디스크가 표시등마저 작동하지 못하도록 실패할 수 있습니다(완전한 전원 손실).

#### <a name="physical-replacement"></a>물리적 교체

가능한 경우 사용 중지된 실제 디스크를 교체해야 합니다. 대부분의 경우이는 핫 스왑로 구성 됩니다. 즉, 노드 또는 저장소 인클로저를 끄는 것은 필요 하지 않습니다. 유용한 위치 및 부품 정보는 오류를 참조하세요.

#### <a name="verification"></a>확인

교체 디스크가 삽입 되 면 지원 되는 구성 요소 문서에 대해 확인 됩니다 (다음 섹션 참조).

#### <a name="pooling"></a>Pooling

허용되는 경우 대체 디스크는 이전 디스크의 풀에 자동으로 대체되므로 바로 사용할 수 있습니다. 이때 시스템은 완전한 상태의 초기 상태로 되돌아가므로 오류가 사라집니다.

## <a name="supported-components-document"></a>지원 되는 구성 요소 문서

상태 관리 서비스는 관리자 또는 솔루션 공급 업체에서 제공 하는 지원 되는 구성 요소 문서에 스토리지 공간 다이렉트에 사용 되는 구성 요소를 제한 하는 적용 메커니즘을 제공 합니다. 이를 통해 사용자 또는 다른 사람이 실수로 지원되지 않는 하드웨어를 사용하는 것을 방지할 수 있으며, 이는 보증 또는 지원 계약을 준수하는 데 도움이 될 수 있습니다. 이 기능은 현재 Ssd, Hdd 및 NVMe 드라이브를 비롯 한 실제 디스크 장치로 제한 됩니다. 지원 되는 구성 요소 문서는 모델, 제조업체 (선택 사항) 및 펌웨어 버전 (선택 사항)을 제한할 수 있습니다.

### <a name="usage"></a>사용량

지원 되는 구성 요소 문서에서는 XML로 구성 된 구문을 사용 합니다. 사용 가능한 [Visual Studio Code](https://code.visualstudio.com/) 또는 메모장과 같은 원하는 텍스트 편집기를 사용 하 여 저장 하 고 다시 사용할 수 있는 XML 문서를 만드는 것이 좋습니다.

#### <a name="sections"></a>섹션

문서에는와 라는 두 개의 독립적인 섹션이 있습니다. `Disks` `Cache`

섹션이 제공 되는 경우에는 목록에 있는 `Disks` 드라이브만 `Disk` 풀에 가입할 수 있습니다. 나열 되지 않은 모든 드라이브가 풀을 조인 하는 것을 방지 하므로 프로덕션에서 효과적으로 사용 되지 않습니다. 이 섹션을 비워 두면 모든 드라이브가 풀에 가입할 수 있습니다.

섹션이 제공 되는 경우에는 `Cache` (as) 나열 된 드라이브만 `CacheDisk` 캐싱에 사용 됩니다. 이 섹션을 비워 두면 [미디어 유형 및 버스 유형을 기반으로 추측](../storage/storage-spaces/understand-the-cache.md#cache-drives-are-selected-automatically)을 스토리지 공간 다이렉트 시도 합니다. 여기에 나열 된 드라이브는에도 나열 되어 `Disks` 있습니다.

>[!IMPORTANT]
> 지원 되는 구성 요소 문서는 이미 풀링 되어 사용 중인 드라이브에 소급 적용 되지 않습니다.

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
        <BinaryPath>C:\ClusterStorage\path\to\image.bin</BinaryPath>
      </TargetFirmware>
    </Disk>
    <Disk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </Disk>
  </Disks>

  <Cache>
    <CacheDisk>
      <Manufacturer>Fabrikam</Manufacturer>
      <Model>QRSTUV</Model>
    </CacheDisk>
  </Cache>

</Components>

```

여러 드라이브를 나열 하려면 또는 태그를 추가 하기만 하면 됩니다 `<Disk>` `<CacheDisk>` .

스토리지 공간 다이렉트를 배포할 때이 XML을 삽입 하려면 매개 변수를 사용 합니다 `-XML` .

```PowerShell
$MyXML = Get-Content <Filepath> | Out-String
Enable-ClusterS2D -XML $MyXML
```

스토리지 공간 다이렉트 배포 되 면 지원 되는 구성 요소 문서를 설정 하거나 수정 하려면 다음을 수행 합니다.

```PowerShell
$MyXML = Get-Content <Filepath> | Out-String
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.SupportedComponents.Document" -Value $MyXML
```

>[!NOTE]
>모델, 제조업체 및 펌웨어 버전 속성이 **Get-physicaldisk** cmdlet을 사용하여 가져온 값과 정확히 일치해야 합니다. 이는 공급업체의 구현에 따라 "상식적인" 예상과 다를 수 있습니다. 예를 들어 제조업체가 "Contoso" 대신 "CONTOSO-LTD"이거나, 모델이 "Contoso XZY9000"인 경우 비어 있을 수 있습니다.

다음 PowerShell cmdlet을 사용하여 확인할 수 있습니다.

```PowerShell
Get-PhysicalDisk | Select Model, Manufacturer, FirmwareVersion
```

## <a name="settings"></a>설정

[상태 관리 서비스 설정](health-service-settings.md)을 참조 하세요.

## <a name="additional-references"></a>추가 참조

- [상태 관리 서비스 보고서](health-service-reports.md)
- [상태 관리 서비스 오류](health-service-faults.md)
- [작업 상태 관리 서비스](health-service-actions.md)
- [상태 관리 서비스 설정](health-service-settings.md)
- [Windows Server 2016의 스토리지 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md)
