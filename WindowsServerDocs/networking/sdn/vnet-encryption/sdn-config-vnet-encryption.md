---
title: 가상 네트워크에 대 한 암호화 구성
description: 이 항목에 대해 설명 가상 네트워크 암호화 Windows Server에서 네트워킹 정의 된 소프트웨어에 대 한
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: pashort
author: grcusanz
ms.openlocfilehash: 7d1de535e7758793e5ddaa7eeefada0aa55d3328
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>가상 서브넷에 대 한 암호화 구성

>Windows Server에 적용 됩니다.

이 항목 가상 네트워크의 암호화를 사용 하는 데 필요한 단계를 설명 하는 다음 섹션에 있습니다.

- [암호화 인증서 만들기](#bkmk_Certificate)
- [인증서 자격 증명을 만드는](#bkmk_credential)
- [가상 네트워크 암호화 구성](#bkmk_vnet)

## <a name="bkmk_Certificate"></a>암호화 인증서 만들기
한 암호화 인증서가 암호화 사용 되는지 각 호스트 설치 해야 합니다.  동일한 인증서를 사용 하 여 모든 테 넌에 대 한 하거나 필요한 경우 테 당 고유한 인증서를 생성할 수 있습니다.

1 단계: 인증서를 생성 합니다.

    $subjectName = "EncryptedVirtualNetworks"
    $cryptographicProviderName = "Microsoft Base Cryptographic Provider v1.0";
    [int] $privateKeyLength = 1024;
    $sslServerOidString = "1.3.6.1.5.5.7.3.1";
    $sslClientOidString = "1.3.6.1.5.5.7.3.2";
    [int] $validityPeriodInYear = 5;

    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"
    $name.Encode("CN=" + $SubjectName, 0)

    #Generate Key
    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"
    $key.ProviderName = $cryptographicProviderName
    $key.KeySpec = 1 #X509KeySpec.XCN_AT_KEYEXCHANGE
    $key.Length = $privateKeyLength
    $key.MachineContext = 1
    $key.ExportPolicy = 0x2 #X509PrivateKeyExportFlags.XCN_NCRYPT_ALLOW_EXPORT_FLAG 
    $key.Create()

    #Configure Eku
    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $serverauthoid.InitializeFromValue($sslServerOidString)
    $clientauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $clientauthoid.InitializeFromValue($sslClientOidString)
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"
    $ekuoids.add($serverauthoid)
    $ekuoids.add($clientauthoid)
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"
    $ekuext.InitializeEncode($ekuoids)

    # Set the hash algorithm to sha512 instead of the default sha1
    $hashAlgorithmObject = New-Object -ComObject X509Enrollment.CObjectId
    $hashAlgorithmObject.InitializeFromAlgorithmName( $ObjectIdGroupId.XCN_CRYPT_HASH_ALG_OID_GROUP_ID, $ObjectIdPublicKeyFlags.XCN_CRYPT_OID_INFO_PUBKEY_ANY, $AlgorithmFlags.AlgorithmFlagsNone, "SHA512")


    #Request Certificate
    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"

    $cert.InitializeFromPrivateKey(2, $key, "")
    $cert.Subject = $name
    $cert.Issuer = $cert.Subject
    $cert.NotBefore = (get-date).ToUniversalTime()
    $cert.NotAfter = $cert.NotBefore.AddYears($validityPeriodInYear);
    $cert.X509Extensions.Add($ekuext)
    $cert.HashAlgorithm = $hashAlgorithmObject
    $cert.Encode()

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"
    $enrollment.InitializeFromRequest($cert)
    $certdata = $enrollment.CreateRequest(0)
    $enrollment.InstallResponse(2, $certdata, 0, "")

위의 실행 한 후에 새 인증서 나타납니다는 컴퓨터의 내 스토어 스크립트를 실행할:

    PS D:\> dir cert:\\localmachine\my


    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

2 단계: 인증서, 개인 키와 함께 및 없이 복사본을 2 개 해야 하는 파일을 인증서를 내보냅니다.

    $subjectName = "EncryptedVirtualNetworks"
    $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"}
    [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret"))
    Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert

위의 실행 한 후 이제 두 인증서 파일 해야 합니다.  이러한 각 hyper v 호스트 설치 해야 합니다.

    PS C:\> dir c:\$subjectname.*


        Directory: C:\


    Mode                LastWriteTime         Length Name
    ----                -------------         ------ ----
    -a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer
    -a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx

3 단계: Hyper-v 호스트에 설치

    $server = "Server01"

    $subjectname = "EncryptedVirtualNetworks"
    copy c:\$SubjectName.* \\$server\c$
    invoke-command -computername $server -ArgumentList $subjectname,"secret" {
        param (
            [string] $SubjectName,
            [string] $Secret
        )
        $certFullPath = "c:\$SubjectName.cer"

        # create a representation of the certificate file
        $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
        $certificate.import($certFullPath){$_}

        # import into the store
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("Root", "LocalMachine")
        $store.open("MaxAllowed")
        $store.add($certificate)
        $store.close()

        $certFullPath = "c:\$SubjectName.pfx"
        $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
        $certificate.import($certFullPath, $Secret, "MachineKeySet,PersistKeySet")

        # import into the store
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My", "LocalMachine")
        $store.open("MaxAllowed")
        $store.add($certificate)
        $store.close()

        # Important: Remove the certficate files when finished
        remove-item C:\$SubjectName.cer
        remove-item C:\$SubjectName.pfx
    }    

각 서버 귀하의 환경에 대해 반복 합니다.  이제 인증서 루트 및 각 Hyper-v 호스트의 내 스토어에서 설치 있어야

내용을 확인 하 여 인증서를 설치를 확인할 수는 내 루트 인증서 저장소 및:

    PS C:\> enter-pssession Server1

    [Server1]: PS C:\> get-childitem cert://localmachine/my,cert://localmachine/root | ? {$_.Subject -eq "CN=EncryptedVirtualNetworks"}

    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks


    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\root

    Thumbprint                                Subject
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

네트워크 컨트롤러의 인증서 자격 증명 개체를 만들기 위한 필요는 지문 기록해 둡니다.

## <a name="bkmk_Certificate"></a>인증서 자격 증명을 만드는

각 Hyper-v 호스트 컨트롤러 네트워크에 연결에 인증서를 설치 성공적으로 사용 하 여 네트워크 컨트롤러를 구성할 수 있습니다.

인증서 지문 포함 된 자격 증명 개체를 만드는 해야 합니다.  이렇게 하려면 컴퓨터에서 네트워크 컨트롤러 powershell 모듈을 설치 해야 할 수 있습니다.

    # Replace with thumbprint from your certificate
    $thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"  
    
    # Replace with your Network Controller URI
    $uri = "https://nc.contoso.com"

    Import-module networkcontroller
    
    $credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
    $credproperties.Type = "X509Certificate"
    $credproperties.Value = $thumbprint
    New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force

각 암호화 된 가상 netwokr에 대 한이 자격 증명을 다시 사용할 수 있고 배포 각 테에 대 한 고유한 인증서를 사용 하 여 수 있습니다.

## <a name="bkmk_Certificate"></a>가상 네트워크 암호화 구성

이 단계 가정 가상 네트워크 이름을 "내 네트워크" 이미 만든 하나 이상 가상 서브넷 포함 합니다.  가상 네트워크를 만드는 방법에 대 한 정보를 참조 하세요. [만들기, 삭제 또는 업데이트 테 가상 네트워크](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md)합니다.

1 단계: 가상 네트워크 및 자격 증명 개체 네트워크 컨트롤러에서 검색

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork"
    $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"

2 단계: 인증서 자격 증명에 대 한 언급을 추가 하 고 개별 서브넷의 암호화를 사용 하도록 설정 합니다.

    $vnet.properties.EncryptionCredential = $certcred

    # Replace the Subnets index with the value corresponding to the subnet you want encrypted.  
    # Repeat for each subnet where encryption is needed
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true

3 단계: 업데이트 된 가상 네트워크 개체 네트워크 컨트롤러도 전환

    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force

완료 되 면 없이 추가 단계는 필요 합니다.  현재 연결 된 모든 VM 및 위의 서브넷 나중에 연결 된 모든 VM 같은 서브넷에 다른 VM와 통신할 때 자동으로 암호화 하는 교통을 갖게 됩니다.


