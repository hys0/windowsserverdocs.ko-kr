---
title: 세 번째 수준의 도메인 이름 추가
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5b4a362-1881-4024-ae4e-cc3b05e50103
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 64bf24e45155fdd981e2061b3de7ebce1c53b36c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833324"
---
# <a name="add-third-level-domain-names"></a>세 번째 수준의 도메인 이름 추가

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

도메인 이름 설정 마법사에서 사용자가 세 번째 수준의 도메인 이름을 요청하는 기능을 추가할 수 있습니다. 이 작업은 운영 체제에서 도메인 관리자가 사용하는 코드 어셈블리를 만들고 설치하여 수행됩니다.  
  
## <a name="create-a-provider-of-third-level-domain-names"></a>세 번째 수준의 도메인 이름 공급자 만들기  
 마법사에 세 번째 수준의 도메인 이름을 제공하는 코드 어셈블리를 만들고 설치하여 해당 도메인 이름을 사용할 수 있습니다. 이렇게 하려면 다음 작업을 수행합니다.  
  
-   [어셈블리에 IDomainSignupProvider 인터페이스 구현 추가](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)  
  
-   [어셈블리에 IDomainMaintenanceProvider 인터페이스 구현 추가](Add-Third-Level-Domain-Names.md#BKMK_DomainMaintenance)  
  
-   [Authenticode 서명으로 어셈블리 서명](Add-Third-Level-Domain-Names.md#BKMK_SignAssembly)  
  
-   [참조 컴퓨터에서 어셈블리를 설치 합니다.](Add-Third-Level-Domain-Names.md#BKMK_InstallAssembly)  
  
-   [Windows Server 도메인 이름 관리 서비스를 다시 시작](Add-Third-Level-Domain-Names.md#BKMK_RestartService)  
  
###  <a name="BKMK_DomainSignup"></a> 어셈블리에 IDomainSignupProvider 인터페이스 구현 추가  
 IDomainSignupProvider 인터페이스는 마법사에 도메인 제품을 추가하는 데 사용됩니다.  
  
##### <a name="to-add-the-idomainsignupprovider-code-to-the-assembly"></a>어셈블리에 IDomainSignupProvider 코드를 추가하려면  
  
1.  **시작** 메뉴에서 프로그램을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택하여 관리자로 Visual Studio 2008을 엽니다.  
  
2.  **파일**, **새로 만들기**를 차례로 클릭한 다음 **프로젝트**를 클릭합니다.  
  
3.  **새 프로젝트** 대화 상자에서 **Visual C#**, **클래스 라이브러리**를 차례로 클릭하고 솔루션 이름을 입력한 다음 **확인**을 클릭합니다.  
  
4.  Class1.cs 파일의 이름을 바꿉니다. 예를 들면 MyDomainNameProvider.cs입니다.  
  
5.  Wssg.Web.DomainManagerObjectModel.dll, CertManaged.dll, WssgCertMgmt.dll 및 WssgCommon.dll 파일에 참조를 추가합니다.  
  
6.  구문을 사용하여 다음을 추가합니다.  
  
    ```c#  
  
    using System.Collections.ObjectModel;  
    using System.Net;  
    using System.Net.Sockets;  
    using Microsoft.WindowsServerSolutions.Certificates;  
    using Microsoft.WindowsServerSolutions.CertificateManagement;  
    using Microsoft.WindowsServerSolutions.Common;  
    using Microsoft.Win32;  
    ```  
  
7.  다음 예제에 맞게 네임스페이스와 클래스 헤더를 변경합니다.  
  
    ```c#  
    namespace Microsoft.WindowsServerSolutions.RemoteAccess.Domains  
    {  
        public class MyDomainNameProvider : IDomainSignupProvider  
        {  
        }  
    }  
    ```  
  
8.  클래스에 Initialize 메서드와 필요한 변수를 추가합니다. 이 클래스는 마법사에 나타나는 제품을 정의합니다.  
  
    > [!NOTE]
    >  Initialize 메서드는 고유해야 하는 도메인 공급자의 식별자를 정의합니다. 이 작업을 수행하는 일반적인 방법은 GUID를 식별자로 정의하는 것입니다. GUID 만들기에 대 한 자세한 내용은 참조 하세요. [Guid 만들기 (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098)합니다.  
  
     다음 코드 예제는 초기화 메서드를 보여줍니다.  
  
    ```c#  
  
    static readonly Guid MyID = new Guid("8C999DF5-696A-47af-822D-94F1673D3397");  
    public Guid ID { get { return MyID; } }  
    public string Name { get { return "My Provider"; } }  
    List<Offering> offerings = new List<Offering>();  
  
    public void Initialize(DomainProviderSettings config)  
    {  
       var offer1 = new Offering()  
       {  
          Description = "My Domain Provider",  
          Name = "Offering 1",  
          ProviderID = ID,  
          MoreInfoUrl = new Uri("http://www.contoso.com"),  
          MembershipServiceName = "My Membership",  
          EulaUrl = new Uri("http://www.contoso.com"),  
       };  
  
       this.offerings.Add(offer1);  
       RegistryKey key =   
          Registry.LocalMachine.CreateSubKey(@"Software\Microsoft\Windows Server\Domain Manager\Settings");  
       key.Close();  
    }  
    ```  
  
9. GetOfferings 메서드를 추가합니다. 이 메서드는 이전 단계에서 초기화된 제품 목록이 반환됩니다. 다음 코드 예제는 GetOfferings 메서드를 보여줍니다.  
  
    ```c#  
  
    public ReadOnlyCollection<Offering> GetOfferings()  
    {  
       return this.offerings.AsReadOnly();  
    }  
    ```  
  
10. FindOfferingForDomain 메서드를 추가합니다. 이 메서드는 목록에서 해당 제품을 반환합니다. 다음 코드 예제는 FindOfferingForDomain 메서드를 보여줍니다.  
  
    ```  
  
    public Offering FindOfferingForDomain(string domain)  
    {  
       // Return the offering that has the domain name.  
       return offerings[0];  
    }  
  
    ```  
  
11. SetCredentials 메서드를 정의합니다. 이 메서드는 제품에 액세스하기 위해 필요한 자격 증명을 정의합니다. 다음 코드 예제는 SetCredentials 메서드를 보여줍니다.  
  
    ```c#  
  
    private string currentUser { get; set; }  
    private string currentPassword { get; set; }  
  
    public bool SetCredentials(DomainNameRequest request,   
       DomainProviderCredentials credentials, bool validate)  
    {  
       currentUser = credentials.UserName;  
       currentPassword = credentials.Password;  
       if (validate)  
       {  
          return ValidateCredentials();  
       }  
  
       return true;  
    }  
    ```  
  
12. ValidateCredentials 메서드를 추가합니다. 이 메서드는 SetCredentials에 의해 정의된 자격 증명의 유효성을 검사합니다. 다음 코드 예제는 \ValidateCredentials 메서드를 보여줍니다.  
  
    ```c#  
  
    public static readonly string offerUser = "user1@contoso.com";  
    public static readonly string offerPassword = "password1";  
  
    public bool ValidateCredentials()  
    {  
       if (IsUser())  
          return string.Equals(currentPassword, offerPassword);  
       else  
          return false;  
    }   
  
    private bool IsUser()  
    {  
       return string.Equals(currentUser, offerUser, StringComparison.OrdinalIgnoreCase);  
    }  
    ```  
  
13. GetAvailableDomainRoots 메서드를 추가합니다. 이 메서드는 요청에서 지정한 제품이 지원하는 루트 도메인 이름 목록을 반환합니다. 이 루트 도메인 이름 목록을 비워 둘 수 없습니다. 다음 코드 예제는 GetAvailableDomainRoots 메서드를 보여줍니다.  
  
    ```c#  
  
    public ReadOnlyCollection<string> GetAvailableDomainRoots(DomainNameRequest request)  
    {  
       List<string> list = new List<string>();  
       list.Add("domain1.com");  
       list.Add("domain1.org");  
  
       return list.AsReadOnly();  
    }  
    ```  
  
14. GetUserDomainNames 메서드를 추가합니다. 이 메서드는 현재 제품과 관련하여 현재 사용자가 아직 소유하고 있는 도메인 이름 목록을 반환합니다. 이 목록은 비어 있을 수 있습니다. 다음 코드 예제는 GetUserDomainNames 메서드를 보여줍니다.  
  
    ```c#  
  
    public static readonly string AvailableDomain1 = "available.domain1.com",  
       AvailableDomain2 = "available.domain2.com";  
    public static readonly string OccupiedDomain1 = "occupied.domain1.com",  
       OccupiedDomain2 = "occupied.domain2.com";  
  
    public ReadOnlyCollection<string> GetUserDomainNames(DomainNameRequest request)  
    {  
       var userDomains = new List<string>();  
       userDomains.Add(OccupiedDomain1);  
       userDomains.Add(AvailableDomain1);  
  
       return userDomains.AsReadOnly();  
    }  
    ```  
  
15. GetUserDomainQuota 메서드를 추가합니다. 이 메서드는 지정된 제품에서 허용하는 최대 도메인 수를 반환합니다. 최대값을 적용할 수 없는 경우 메서드가 0을 반환되어야 합니다. 다음 예제는 GetUserDomainQuota 메서드를 보여줍니다.  
  
    ```c#  
  
    public int GetUserDomainQuota(DomainNameRequest request)  
    {  
       return 0;  
    }  
    ```  
  
16. CheckDomainAvailability 메서드를 추가합니다. 이 메서드는 요청된 도메인 이름 가용성을 확인하고 제안 목록을 반환할 수 있습니다. 다음 코드 예제는 CheckDomainAvailability 메서드를 보여줍니다.  
  
    ```c#  
  
    public bool CheckDomainAvailability(DomainNameRequest request,   
       out ReadOnlyCollection<string> suggestions)  
    {  
       suggestions = null;  
  
       return true;  
    }  
    ```  
  
17. CommitDomain 메서드를 추가합니다. 이 메서드는 요청된 도메인 이름을 커밋합니다. 이 메서드가 성공적으로 완료되면 도메인 이름이 사용자 계정과 연결되었으며, 상태가 FullyOperational인 경우 인증서를 즉시 검색하도록 유지 관리 공급자를 호출할 예정이며, 공급자와 제품이 활성 상태가 됩니다. 다음 코드 예제는 CommitDomain 메서드를 보여줍니다.  
  
    ```c#  
  
    public DomainStatus CommitDomain(DomainNameRequest request)  
    {              
       ReadOnlyCollection<string> suggestions;  
       if (!CheckDomainAvailability(request, out suggestions))  
       {  
          throw new DomainException(FailureReason.InvalidDomainName, null, null);  
       }  
  
       return DomainStatus.Ready;  
    }  
    ```  
  
18. ReleaseDomain 메서드를 추가합니다. 이 메서드는 공급자에게 사용자가 도메인 이름을 해제하려고 한다고 알립니다. 다음 코드 예제는 ReleaseDomain 메서드를 보여줍니다.  
  
    ```c#  
  
    public bool ReleaseDomain(DomainNameRequest request)  
    {  
       return true;  
    }  
    ```  
  
19. GetProviderLandingUrl 메서드를 추가합니다. 이 메서드는 도메인 등록 워크플로에서 방문 페이지의 URL을 반환합니다. 다음 코드 예제는 GetProviderLandingUrl 메서드를 보여줍니다.  
  
    ```c#  
  
    public Url GetProviderLandingUrl(DomainNameRequest request)  
    {  
       return new Url("www.contoso.com");  
    }  
    ```  
  
20. GetDomainMaintenanceProvider 메서드를 추가합니다. 이 메서드는 도메인 유지 관리 작업에 사용되는 IDomainMaintenanceProvider의 인스턴스를 반환합니다. 이 메서드는 CommitDomain 메서드가 성공한 후 도메인 관리자가 시작되면 호출됩니다. 다음 코드 예제는 GetDomainMaintenanceProvider 메서드를 보여줍니다.  
  
    ```c#  
  
    public IDomainMaintenanceProvider GetDomainMaintenanceProvider()  
    {  
       return new MyDomainMaintenanceProvider();  
    }  
    ```  
  
21. 해당 프로젝트를 저장하지만 그 다음 절차에서 프로젝트에 추가해야 하므로 닫지는 마세요. 다음 절차를 완료해야 프로젝트를 빌드할 수 있습니다.  
  
###  <a name="BKMK_DomainMaintenance"></a> 어셈블리에 IDomainMaintenanceProvider 인터페이스 구현 추가  
 IDomainMaintenanceProvider는 도메인을 만든 후 유지 관리하는 데 사용됩니다.  
  
##### <a name="to-add-the-idomainmaintenanceprovider-code-to-the-assembly"></a>어셈블리에 IDomainMaintenanceProvider 코드를 추가하려면  
  
1.  도메인 유지 관리 공급자에 대한 클래스 헤더를 추가합니다. 공급자에 대해 정의한 이름이 이전에 정의한 GetDomainMaintenanceProvider 메서드 이름과 일치하는지 확인합니다.  
  
    ```c#  
  
    public class MyDomainMaintenanceProvider : IDomainMaintenanceProvider  
    {  
    }  
    ```  
  
2.  Activate 메서드를 추가합니다. 이 메서드는 활성 공급자를 설정합니다. 다음 코드 예제는 Activate 메서드를 보여줍니다.  
  
    ```c#  
  
    string DomainName { get; set; }  
    protected DomainProviderSettings Settings { get; set; }  
  
    public void Activate(DomainProviderSettings settings,   
       DomainNameConfiguration config, DomainProviderCredentials credentials)  
    {  
       Settings = settings;  
       SetCredentials(credentials);  
       DomainName = config.AutoConfiguredAnywhereAccessFullName.Punycode;  
    }  
    ```  
  
3.  Deactivate 메서드를 추가합니다. 이 메서드는 모든 동작을 비활성화하는 데 사용됩니다. 다음 코드 예제는 Deactivate 메서드를 보여줍니다.  
  
    ```  
  
    public void Deactivate()  
    {  
       //Deactivate all actions  
    }  
  
    ```  
  
4.  SetCredentials 메서드를 추가합니다. 이 메서드는 사용자 자격 증명을 업데이트합니다. 예를 들어 이 메서드는 더 이상 유효하지 않은 자격 증명을 업데이트하기 위해 호출할 수 있습니다. 다음 코드 예제는 SetCredentials 메서드를 보여줍니다.  
  
    ```c#  
  
    protected DomainProviderCredentials Credentials { get; set; }  
  
    public bool SetCredentials(DomainProviderCredentials credentials)  
    {  
       this.Credentials = credentials;  
  
       return true;  
    }  
    ```  
  
5.  ValidateCredentials 메서드를 추가합니다. 이 메서드는 지정된 자격 증명의 유효성을 검사합니다. 다음 코드 예제는 \ValidateCredentials 메서드를 보여줍니다.  
  
    ```c#  
  
    public static readonly string offerUser = "user1@contoso.com";  
    public static readonly string offerPassword = "password1";  
  
    public bool ValidateCredentials()  
    {  
       if (string.Equals(this.Credentials.UserName,   
          offerUser,   
          StringComparison.OrdinalIgnoreCase) &&   
             string.Equals(this.Credentials.Password, offerPassword))  
          return true;  
  
       return false;  
    }  
    ```  
  
6.  GetPublicAddress 메서드를 추가합니다. 이 메서드는 서버의 외부 IP 주소를 반환합니다. 다음 코드 예제는 GetPublicAddress 메서드를 보여줍니다.  
  
    ```c#  
  
    public IPAddress GetPublicIPAddress()  
    {  
       string PublicIP = "0.0.0.0";  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          PublicIP = (key == null) ? "0.0.0.0" : key.GetValue("PublicIP", "0.0.0.0").ToString();  
       }  
       IPAddress ip = IPAddress.Parse(PublicIP);  
  
       if (PublicIP == "0.0.0.0")  
       {  
          string strHostName = Dns.GetHostName();  
          IPHostEntry ipEntry = Dns.GetHostEntry(strHostName);  
  
          IPAddress[] addr = ipEntry.AddressList;  
          foreach (IPAddress add in addr)  
          {  
             if (add.AddressFamily == AddressFamily.InterNetwork)  
             {  
                return add;  
             }  
          }  
       }  
       else  
       {  
          return IPAddress.Parse(PublicIP);  
       }  
  
       return null;    
    }  
    ```  
  
7.  SubmitCertificateRequest 메서드를 추가합니다. 이 메서드는 현재 구성된 도메인 이름에 대한 자격 증명 요청을 제출합니다.  
  
    ```c#  
  
    string cert=null;  
  
    public void SubmitCertificateRequest(string certificateRequest)  
    {  
       cert = CertManaged.SubmitRequest(certificateRequest, CertCommon.CAServerFQDN + "\\" +      
          CertCommon.CAName,   
          Microsoft.WindowsServerSolutions.CertificateManagement.CRFlags.Base64Header,   
          CertCommon.CATemplate,   
          EncodingFlags.Base64);  
    }  
    ```  
  
8.  GetCertificateResponse 메서드를 추가합니다. 이 메서드는 도메인 상태가 FullyOperational인 경우 인증서 응답을 반환합니다. 이 메서드는 새 인증서 요청과 인증서 갱신 요청 모두에 대해 호출됩니다. 다음 코드 예제는 GetCertificateResponse 메서드를 보여줍니다.  
  
    ```c#  
  
    public string GetCertificateResponse(bool renew)  
    {  
       return cert;  
    }  
    ```  
  
9. SubmitRenewCertificateRequest 메서드를 추가합니다. 이 메서드는 인증서 갱신을 처리합니다. 다음 코드 예제는 SubmitRenewCertificateRequest 메서드를 보여줍니다.  
  
    ```c#  
  
    public void SubmitRenewCertificateRequest()  
    {  
       // Add certificate renewal code   
    }  
    ```  
  
10. UpdateDNSRecords 메서드를 추가합니다. 이 메서드는 공급자가 저장한 DNS 레코드를 업데이트합니다. 다음 코드 예제는 UpdateDNS 메서드를 보여줍니다.  
  
    ```c#  
  
    public bool UpdateDnsRecords(IList<DnsRecord> records)  
    {  
       string UpdateDNS = "true";  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          UpdateDNS = (key == null) ? "true" : key.GetValue("UpdateDNS", "true").ToString();  
       }  
  
       return UpdateDNS == "true";  
    }  
  
    ```  
  
11. TestConnection 메서드를 추가합니다. 이 메서드는 백 엔드 서비스에 대한 연결을 설정합니다. 이 메서드에서 인증을 요구하는 경우 적절한 예외를 만들어야 합니다. 다음 코드 예제는 TestConnection 메서드를 보여줍니다.  
  
    ```c#  
  
    public bool TestConnection()  
    {  
       // Add code to test connection  
  
       return true;  
    }  
    ```  
  
12. GetDomainState 메서드를 추가합니다. 이 메서드는 현재 도메인 상태를 반환합니다. 다음 코드 예제는 GetDomainState 메서드를 보여줍니다.  
  
    ```c#  
  
    public DomainState GetDomainState()  
    {  
       string domainstatus = "FullyOperational";  
       long expirationDate = 365;  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          domainstatus = (key == null) ? "Ready" : key.GetValue("DomainStatus", "Ready").ToString();  
          expirationDate = Int64.Parse(key.GetValue("ExpirationDate", "365").ToString());  
       }  
  
       switch (domainstatus)  
       {  
          case "Failed":  
             return new DomainState(DomainStatus.Failed,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "Ready":  
             return new DomainState(DomainStatus.Ready,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "InRenewal":  
             return new DomainState(DomainStatus.InRenewal,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "InRenewalCustomerInterventionRequired":  
             return new DomainState(DomainStatus.InRenewalCustomerInterventionRequired,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "Pending":  
             return new DomainState(DomainStatus.Pending,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "PendingCustomerInterventionRequired":  
             return new DomainState(DomainStatus.PendingCustomerInterventionRequired,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "RenewalFailed":  
             return new DomainState(DomainStatus.RenewalFailed,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          default:  
             return new DomainState(DomainStatus.Unknown,   
                null,   
                DateTime.Now.AddDays(expirationDate));                   
          }  
    }  
    ```  
  
13. GetCertificateState 메서드를 추가합니다. 이 메서드는 현재 인증서 상태를 반환합니다. 다음 코드 예제는 GetCertificateState 메서드를 보여줍니다.  
  
    ```c#  
  
    public CertificateState GetCertificateState(bool renew)  
    {  
       return new CertificateState(CertificateStatus.Ready, string.Empty);  
    }  
    ```  
  
14. 솔루션을 저장하고 빌드합니다.  
  
###  <a name="BKMK_SignAssembly"></a> Authenticode 서명으로 어셈블리 서명  
 어셈블리를 운영 체제에서 사용할 수 있으려면 반드시 Authenticode 서명이 필요합니다. 어셈블리 서명에 대한 자세한 내용은 [Authenticode를 사용하여 코드 서명 및 확인](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)을 참조하세요.  
  
###  <a name="BKMK_InstallAssembly"></a> 참조 컴퓨터에서 어셈블리를 설치 합니다.  
 폴더의 어셈블리를 참조 컴퓨터에 배치합니다. 그 다음 단계에서 레지스트리에 입력할 예정이므로 폴더 경로를 확인합니다.  
  
### <a name="add-a-key-to-the-registry"></a>레지스트리에 키를 추가합니다.  
 어셈블리의 특성과 위치를 정의할 레지스트리 항목을 추가합니다.  
  
##### <a name="to-add-a-key-to-the-registry"></a>레지스트리에 키를 추가하려면  
  
1.  참조 컴퓨터에서 **시작**을 클릭하고 **regedit**를 입력한 다음 **Enter**키를 누릅니다.  
  
2.  왼쪽 창에서 **HKEY_LOCAL_MACHINE**, **소프트웨어**, **Microsoft**, **Windows Server**, **도메인 관리자**를 차례로 확장한 다음 **공급자**를 확장합니다.  
  
3.  **공급자**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **키**를 클릭합니다.  
  
4.  키 이름으로 공급자에 대한 식별자를 입력합니다. 식별자는 [Add an implementation of the IDomainSignupProvider interface to the assembly](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)의 8단계에서 공급자에 대해 정의된 GUID입니다.  
  
5.  방금 만든 키를 마우스 오른쪽 단추로 클릭한 다음 **문자열 값**을 클릭합니다.  
  
6.  문자열 이름에 **어셈블리** 를 입력한 다음 **Enter**키를 누릅니다.  
  
7.  오른쪽 창에서 새 **어셈블리** 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
8.  이전에 만든 어셈블리 파일의 전체 경로를 입력한 다음 **확인**을 클릭합니다.  
  
9. 키를 다시 마우스 오른쪽 단추로 클릭하고 **문자열 값**을 클릭합니다.  
  
10. 문자열 이름에 **Enabled**를 입력한 다음 **Enter** 키를 누릅니다.  
  
11. 오른쪽 창에서 새 **Enabled** 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
12. **True**를 입력하고 **확인**을 클릭합니다.  
  
13. 키를 다시 마우스 오른쪽 단추로 클릭하고 **문자열 값**을 클릭합니다.  
  
14. 문자열 이름에 **Type** 을 입력한 다음 **Enter**키를 누릅니다.  
  
15. 오른쪽 창에서 새 **Type** 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.  
  
16. 어셈블리에서 정의한 공급자의 전체 클래스 이름을 입력한 다음 **확인**을 클릭합니다.  
  
###  <a name="BKMK_RestartService"></a> Windows Server 도메인 이름 관리 서비스를 다시 시작  
 운영 체제에서 공급자를 사용 가능할 수 있도록 Windows Server 도메인 관리 서비스를 다시 시작해야 합니다.  
  
##### <a name="restart-the-service"></a>서비스를 다시 시작합니다.  
  
1.  **시작**을 클릭하고 **mmc**를 입력한 다음 **Enter**키를 누릅니다.  
  
2.  콘솔에 서비스 스냅인이 나열되어 있지 않으면 다음 단계를 완료하여 추가합니다.  
  
    1.  **파일**을 클릭한 다음 **스냅인 추가/제거**를 클릭합니다.  
  
    2.  **사용 가능한 스냅인** 목록에서 **서비스**를 클릭한 다음 **추가**를 클릭합니다.  
  
    3.  **서비스** 대화 상자에서 **로컬 컴퓨터**를 선택했는지 확인한 다음 **완료**를 클릭합니다.  
  
    4.  **확인**을 클릭하여 **스냅인 추가/제거**를 닫습니다.  
  
3.  **서비스**를 두 번 클릭하고 **Windows Server 도메인 관리**로 스크롤하여 선택한 다음 **서비스 다시 시작**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)