## Copilot instructions for Well-Architected dashboard documentation

### Repository overview
Product: Well-architected dashboard in NetApp Console

The well-architected dashboard in NetApp Console performs daily automated scans of cloud storage system configurations, evaluating them against best practices across five pillars—reliability, security, operational excellence, cost optimization, and performance efficiency—and providing insights, recommendations, and automated remediation.

### Repository structure
- `fsx/` – Documentation for Amazon FSx for NetApp ONTAP: configuration analysis and implementing well-architected configurations
- `cvo/` – Documentation for Cloud Volumes ONTAP on Microsoft Azure: configuration analysis and implementing well-architected configurations
- `_include/` – Shared AsciiDoc content fragments included in multiple pages (FSx configuration best practices list, workloads how-it-works section)
- `_whatsnew/` – Release notes entries by date, included in the main what's-new page
- `media/` – Images and screenshots used across all pages

Root-level `.adoc` files cover the dashboard overview, custom rules (learning, creating, and managing), what's new, support registration, and legal notices.

### Product-specific context

**Architecture and components:**
- *NetApp Console* is the SaaS management platform at `console.netapp.com`; the well-architected dashboard is a feature within its *Workloads* menu under *Well-architected*
- *NetApp Console agent* or a *link* provides connectivity between storage systems and NetApp Console; both are required for comprehensive analysis
- *Workload Factory* is the underlying engine referenced for remediation actions and tracker operations
- *Rule builder* is the AI-guided interface for creating custom rules; it uses NetApp's Bedrock AI service and requires AI features to be enabled by the account administrator
- *Rules catalog* is the management interface for viewing, pausing, deleting, and running custom rules

**Key concepts:**
- *Well-architected pillars*: reliability, security, operational excellence, cost optimization, and performance efficiency—used to categorize all configuration findings
- *Configuration analysis*: the daily automated scan of storage configurations that produces an optimization score and a list of configuration issues with recommendations
- *Optimized / Not optimized*: the two states a configuration can have after analysis
- *Dismiss*: the action to exclude a specific configuration (or individual volumes) from scoring and alerts; dismissed configurations can be reactivated
- *Custom rules*: user-defined rules written in plain language, translated by AI into structured rule logic, and evaluated on a schedule against FSx for ONTAP resources
- *Dry run*: a one-time test evaluation of a custom rule to preview affected resources before scheduling
- *NetApp Autonomous Ransomware Protection with AI* (*ARP/AI*): a NetApp security feature recommended for all volumes to detect ransomware threats
- *FlexCache*: ONTAP caching technology; write-around mode suits read-heavy workloads, write-back mode suits write-heavy workloads
- *FlexGroup* and *FlexVol*: ONTAP volume types that may require periodic rebalancing

**Supported storage systems:**
- *Amazon FSx for NetApp ONTAP* (AWS) – requires AWS credentials with appropriate permissions; link or Console agent is optional but provides a comprehensive analysis
- *Cloud Volumes ONTAP on Microsoft Azure* – requires a Console agent; Azure Blob Storage serves as the capacity tier for cold data

**Naming conventions and terminology:**
- Use *well-architected dashboard* (lowercase) when referring to the feature, not "Well-Architected Dashboard"
- Use *NetApp Console* when referring to the platform, not "Console" alone on first mention
- Use *link* (not "connector" or "gateway") for the FSx for ONTAP connectivity component
- Use *Console agent* when referring to the deployable agent component
- Permissions levels follow a specific naming convention: *view, planning, and analysis* (for read-only analysis) and *operations and remediation* (for applying fixes)
- Custom rule states: *Draft*, *Dry-run*, *Scheduled (Enabled)*, *Disabled*, *Deleted*
- Execution status values: *Successful*, *Partially successful*, *Failed*

**Technical constraints:**
- Custom rules support only one resource type per rule (file system, volume, or cache)
- Minimum custom rule evaluation interval is 1 hour
- Custom rules provide read-only access and cannot make changes to the environment
- Automatic fixes are not available for custom rules; remediation is manual
- Custom rule creation requires AI features to be enabled by the account administrator
- SSD capacity and volume capacity recommendations use an 80% utilization threshold

### Typical user workflows

**Analyze and fix FSx for ONTAP configurations:** Sign in to NetApp Console → Navigate to Workloads > Well-architected → Review optimization score and configuration issues → Select *View* for a configuration → Select *Fix* (or *View and fix* for volume-level fixes) → Confirm and continue → Monitor via Tracker

**Analyze and fix Cloud Volumes ONTAP configurations:** Sign in to NetApp Console → Navigate to Workloads > Well-architected → Review configuration issues → Select *View* for a configuration → Download CSV (optional) → Select *Fix* → Confirm and continue → Monitor via Tracker

**Dismiss and reactivate a configuration analysis:** Navigate to Well-architected dashboard → Select *Dismiss* for an unwanted configuration or volume → Confirm → To reactivate, select *Dismissed configurations* → Identify the configuration → Select *Reactivate*

**Create a custom rule:** Navigate to Well-architected > Rule builder → Enter rule description in plain language → Review AI interpretation and rule definition → Answer clarifying questions → Select *Validate rule* to dry-run → Set evaluation frequency → Select *Schedule* (or *Save as draft*)

**Manage custom rules:** Navigate to Well-architected > Rule builder → Select *View your rules* to open Rules catalog → View results, pause, resume, delete, or run quick tests on rules
