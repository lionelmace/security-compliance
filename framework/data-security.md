---

copyright:
  years: 2020, 2023
lastupdated: "2023-03-31"

keywords: data encryption in {{site.data.keyword.compliance_short}}, data storage for {{site.data.keyword.compliance_short}}, bring your own keys for {{site.data.keyword.compliance_short}}, BYOK for {{site.data.keyword.compliance_short}}, key management for {{site.data.keyword.compliance_short}}, key encryption for {{site.data.keyword.compliance_short}}, personal data in {{site.data.keyword.compliance_short}}, data deletion for {{site.data.keyword.compliance_short}}, data in {{site.data.keyword.compliance_short}}, data security in {{site.data.keyword.compliance_short}}

subcollection: security-compliance

---

{{site.data.keyword.attribute-definition-list}}

# Storing and encrypting data in {{site.data.keyword.compliance_short}}
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.compliance_full}}, it is important to know exactly what data is stored and encrypted, and how you can delete any stored personal data.
{: shortdesc}

For more information about how {{site.data.keyword.cloud_notm}} platform secures your data, see [How do I know that my data is safe.
{: tip}

## How is my configuration data obtained?
{: #data-obtained}

To evaluate your resource configuration, {{site.data.keyword.compliance_short}} gathers configuration information from your targeted environment. Collected data includes the properties and configurations for supported services, network objects, hosts, databases, Kubernetes platforms, and virtual machines.

Data is collected differently depending on whether you're working the new experience or continuing to work with collectors.

Data obtained during an API-based evaluation
:   In the new version of the service, your resource configuration is obtained through an internal service-to-service authorization. The policy allows for {{site.data.keyword.compliance_short}} to read the configuration but the service is unable to change it in any way.

[deprecated]{: tag-deprecated} Data obtained during a collector-based evaluation
:   When you work with the hybrid cloud section of the service, the data is gathered by using a collector, which acts as an intermediary between your resources and the service.

	All communication between the collector and service is TLS 1.2+ encrypted and signed with a public key. All traffic is transported over the public internet by using Cloud Internet Service with TLS termination, DDoS protection, and a Web Application Firewall (WAF).

	To read your resource configurations, a collector uses the credentials that you associate with it through the {{site.data.keyword.compliance_short}} UI. The level of access assigned to your credential is the level of access that a collector has to your resource. 

	The credentials that you provide to the service are securely stored. At no time are your credentials available in clear text while they are stored or used by the service. 

## How is data stored?
{: #data-storage}

Depending on whether you're working with the API-based or collector-based architecture, the way that data is generated and stored is different.

Data storage in {{site.data.keyword.compliance_short}}
:   In the new version of the service, the results data that is generated by the service is stored in a Cloud Object Storage bucket that is owned by the customer.

	For help configuring storage, see [Storing data in {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-storage).
	{: note}

[deprecated]{: tag-deprecated} Data storage for collector-based evaluations
:   When you work with the hybrid cloud version of the service, the results data that is generated by the service is stored in a database that is managed by IBM.

## [deprecated]{: tag-deprecated} Protecting your sensitive data (Collectors)
{: #data-encryption}

If you're working in the hybrid cloud flow, you can add a higher level of encryption control to your data at rest (when it is stored) by enabling integration with {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}}. [{{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started) is a single-tenant key management service that is backed by a FIPS140-2 level 4 certified Hardware Security Model (HSM).

{{site.data.keyword.compliance_short}} encrypts the results that are generated by the service by using either IBM or customer-managed keys. By default, the encryption keys that secure your data are generated on your behalf through {{site.data.keyword.keymanagementserviceshort}} and managed by IBM. If you want to use and manage your own key, you can integrate a key management service by using the **Settings** tab in the {{site.data.keyword.compliance_short}} UI.

For help with configuring your own encryption, see [Configuring encryption (collectors)](/docs/security-compliance?topic=security-compliance-storage#data-encryption-configure).
{: note}

The following table describes your options for managing the encryption of selected {{site.data.keyword.compliance_short}} components.

| Encryption | Description |
| ---- | ---- |
| IBM-managed | The data that you store in {{site.data.keyword.compliance_short}} is encrypted at rest by using an IBM-managed key. This is the default setting. |
| Customer-managed | The data that is stored in selected {{site.data.keyword.compliance_short}} components is encrypted at rest by using a key that you own and manage. You can use a root key that you manage in [{{site.data.keyword.keymanagementserviceshort}}](/catalog/services/key-protect) or [{{site.data.keyword.hscrypto}}](/catalog/services/hs-crypto). |
{: caption="Table 2. Encryption options for {{site.data.keyword.compliance_short}}" caption-side="top"}


### What are some best practices when managing my own encryption in {{site.data.keyword.compliance_short}}?
{: #key-best-practices}

When you work with {{site.data.keyword.compliance_short}} data, there are a few best practices to keep in mind to ensure that your data is always secure.

- [Rotate your keys.](/docs/key-protect?topic=key-protect-key-rotation)
- [Set fine-grained access control policies.](/docs/key-protect?topic=key-protect-manage-access)

In {{site.data.keyword.keymanagementserviceshort}}, you can assign various levels of access to limit the number of people who have access to your keys. You can also update the access later if a need to tighten security around your data occurs.


### About customer-managed keys
{: #about-encryption}

{{site.data.keyword.compliance_short}} uses [envelope encryption](#x9860393){: term} to implement customer-managed keys. Envelope encryption describes encrypting one encryption key with another encryption key. The key used to encrypt the actual data is known as a [data encryption key (DEK)](#x4791827){: term}. The DEK itself is never stored but is wrapped by a second key that is known as the key encryption key (KEK) to create a wrapped DEK. To decrypt data, the wrapped DEK is unwrapped to get the DEK. This process is possible only by accessing the KEK, which in this case is your root key that is stored in your key management service.

Depending on your use case and security requirements, the key management service that is most suited for your organization's needs can vary. To learn more about which key management solution is best for you, see [How is {{site.data.keyword.hscrypto}} different from {{site.data.keyword.keymanagementserviceshort}}?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-differentiators-key-protect)
{: note}



## Deleting your data
{: #data-delete}

When you work with the API-based version of the service, you own the data that is generated. It is automatically forwarded to a Cloud Object Storage bucket that you connect. Managing the data is your responsibility. 

[deprecated]{: tag-deprecated} In the collector-based architecture flow, your data is stored by {{site.data.keyword.compliance_short}} and is automatically deleted after 180 days. You don't need to take any action for this process to happen. 

If you are working with the Trial plan, and you choose not to convert your account to Standard, then your data is automatically deleted in 30 days.
{: note} 

