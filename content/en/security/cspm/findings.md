---
title: Security Findings Explorer
kind: documentation
aliases:
  - /security_platform/findings
  - /security_platform/cspm/findings
further_reading:
- link: "security/default_rules"
  tag: "Documentation"
  text: "Explore default Posture Management cloud configuration compliance rules"
- link: "security/cspm/frameworks_and_benchmarks"
  tag: "Documentation"
  text: "Learn about frameworks and industry benchmarks"
---

{{< site-region region="gov" >}}
<div class="alert alert-warning">
Cloud Security Posture Management is not available in this site.
</div>
{{< /site-region >}}

The Cloud Security Posture Management (CSPM) [Security Findings Explorer][1] allows you to:

- Review the detailed configuration of a resource.
- Review the compliance rules applied to your resources by CSPM.
- Review tags for more context about who owns the resource and where it resides in your environment.
- Read descriptions and guidelines based on industry resources for remediating a misconfigured resource.
- Use the time selector to explore your security configuration posture at any point in the past.

In addition to reviewing and responding to findings, you can set notifications for failed findings, and configure signals to correlate and triage misconfigurations in the same view as real-time threats generated by [Cloud SIEM][2] and [Cloud Workload Security][3]. This enables you to accelerate investigations, as the root causes for many of today's cloud breaches are misconfigured services that have been exploited by attackers.

## Findings

A finding is the primary primitive for a rule evaluation against a resource. Every time a resource is evaluated against a rule, a finding is generated with a **Pass** or **Fail** status. Resources are evaluated in increments between 15 minutes and four hours (depending on type). Datadog generates new findings as soon as a scan is completed, and stores a complete history of all findings for the past 15 months so they are available in case of an investigation or audit.

## Explore your cloud misconfigurations

Findings are displayed on the [Security Findings Explorer][1]. Aggregate findings by rule using the **Group by** filters and query search bar. For example, filtering by `evaluation:fail` narrows the list to all compliance rules that have issues that need to be addressed. Findings can also be aggregated by resource to rank resources that have the most failed findings so you can prioritize remediation.

{{< img src="security/cspm/findings/posture-management-overview3.png" alt="An overview of the Posture Management Findings page" style="width:100%;">}}

Select a finding to view the resources that have been evaluated by the rule, the rule description, its framework or industry benchmark mappings, and suggested remediation steps.

{{< img src="security/cspm/findings/finding-side-panel3.png" alt="A list of impacted resources in the side panel" style="width:65%;">}}

Group by **Resources** on the Security Findings Explorer and select a resource to see the full list of compliance rules that were evaluated against the resource, along with their statuses.

{{< img src="security/cspm/findings/resource-rules-evaluated2.png" alt="Group and aggregate by resource in search" style="width:65%;">}}

## Export findings

To export the list of findings as a CSV, click **Download as CSV** on the Security Findings Explorer, select the maximum number of findings to export, and then click **Download as CSV**. You can export up to a maximum of 50,000 findings.

{{< img src="security/cspm/findings/export-csv.png" alt="The Export Findings as CSV dialog box with option to specify the maximum number of findings to export" style="width:65%;">}}

## Mute findings

Sometimes a finding does not match the use case for your business, or you choose to accept it as a known risk. To ignore these findings, you can mute the finding for the impacted resources so you can focus on high-severity and critical findings.

For example, the ['Block Public Access' feature is enabled for S3 bucket][4] rule evaluates whether an S3 bucket is publicly accessible. If you have an S3 bucket with static assets that are meant to be publicly shared, you can mute the finding for the S3 bucket.

You can mute up to 50 findings at a single time. Muting a finding removes it from the calculation of your posture score.

{{< img src="security/cspm/findings/muted-findings3.png" alt="The Mute findings dialog box contains fields for specifying the reason and duration of the mute" style="width:100%;">}}

1. On the [finding side panel](#explore-your-cloud-misconfigurations), select one or more resources.
2. Select **Actions** > **Mute**.
3. Select a reason for the mute, for example, a fix is pending, it's a false positive, or it's an accepted risk.
4. Enter an optional **Description**.
5. Select the duration of the mute.
6. Click **Mute**.

### Unmute a finding

Muted findings automatically unmute after the specified mute duration expires. You can also manually unmute a finding.

1. On the [finding side panel](#explore-your-cloud-misconfigurations), select the resources with the muted finding.
2. Select **Actions** > **Unute**.
3. Select a reason for the unmute, for example, there's no pending fix, it was a human error, or it's no longer an accepted risk.
4. Enter an optional **Description**.
5. Click **Unmute**.

### Audit your muted findings

You can view your organization's muted findings, review whether a muted finding is currently in a pass or fail state, and audit the history for a resource to determine when and by whom a finding was muted.

To view your organization's muted findings:

- Sort by the **Muted** column on the Security Findings Explorer.
- Filter the Security Findings Explorer using the **Muted** facet.

To audit the history for a resource:

1. Open the [finding side panel](#explore-your-cloud-misconfigurations).
2. Select the resource with the muted finding.
3. If the finding status has changed, click **See Latest State**.
4. Click **View Finding**.

{{< img src="security/cspm/findings/muted-findings-timeline-graph2.png" alt="The resource evaluation over time timeline shows the history of the finding including periods when it was muted" style="width:100%;">}}

On the **Message** tab, use the **Resource evaluation over time** timeline to view when the finding was muted or unmuted over a specified period of time (up to six months).

{{< img src="security/cspm/findings/muted-findings-timeline2.png" alt="The Timeline tab shows a chronological history of the finding including details on when a finding was muted" style="width:100%;">}}

Click the **Timeline** tab to view a chronological history of the finding. Hover over a mute or unmute action to view additional details, such as the reason for the mute, how long the mute was intended to last, and who muted it.

## Further reading

{{< partial name="whats-next/whats-next.html" >}}

[1]: https://app.datadoghq.com/security/compliance?time=now
[2]: /security/cloud_siem/
[3]: /security/cloud_workload_security/
[4]: /security/default_rules/cis-aws-1.5.0-2.1.5/