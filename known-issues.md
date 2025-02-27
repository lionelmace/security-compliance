---

copyright:
  years: 2020, 2023
lastupdated: "2023-03-31"

keywords: known limitations, rules, limits, configuration, ibm remediation, ssh key

subcollection: security-compliance

---

{{site.data.keyword.attribute-definition-list}}


# Known issues
{: #known-issues}

Review the following known issues that you might encounter while you work with {{site.data.keyword.compliance_full}}.
{: shortdesc}
 
| Issue  | Workaround |
|:-------|:-----------|
| Remediation is unavailable for {{site.data.keyword.cloud_notm}}. | If you're working with Amazon Web Services (AWS), Azure, or Google Cloud Platform, you can [remediate issues](/docs/security-compliance?topic=security-compliance-remediation) directly from the service UI. If you're working with {{site.data.keyword.cloud_notm}}, you must manually remediate your issues. |
| Results for the resource view are not returned. | The resource view is unavailable if the total number of goals in a profile that is attached to your scan exceeds 560. If you are processing a large scan, you can use the control view or drift view to see your results. |
| Your scan does not run when you're working with an IBM-managed collector. | IBM-managed collectors are configured to scan a maximum of 900 resources at a time. To use an IBM-managed collector, you can narrow your scope to a smaller set of resources, or you can use a customer-managed collector. |
| You cannot create a second integration. | Only one integration can be created for each name or URL. If you need to update your integration in some way, delete the integration and create a new one. |
{: caption="Table 1. Known issues and workarounds" caption-side="top"}


