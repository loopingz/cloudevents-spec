# GitHub CloudEvents Adapter

This document describes how to convert
[GitHub webhook events](https://docs.github.com/en/webhooks/webhook-events-and-payloads)
into a CloudEvents.

GitHub webhook event documentation:
https://docs.github.com/en/webhooks/webhook-events-and-payloads

Each section below describes how to determine the CloudEvents attributes
based on the specified event.

For time attribute, if the proposed value is null, the default timestamp SHOULD be used.

### BranchProtectionConfigurationEvent

| CloudEvents Attribute | Value                                                          |
| :-------------------- | :------------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                          |
| `source`              | "repository.url" value                                         |
| `specversion`         | `1.0`                                                          |
| `type`                | `com.github.branch_protection_configuration.` + "action" value |
| `datacontentencoding` | Omit                                                           |
| `datacontenttype`     | `application/json`                                             |
| `dataschema`          | Omit                                                           |
| `subject`             | Omit                                                           |
| `time`                | Current time                                                   |
| `data`                | Content of HTTP request body                                   |

### BranchProtectionRuleEvent

| CloudEvents Attribute | Value                                                 |
| :-------------------- | :---------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                 |
| `source`              | "repository.url" value                                |
| `specversion`         | `1.0`                                                 |
| `type`                | `com.github.branch_protection_rule.` + "action" value |
| `datacontentencoding` | Omit                                                  |
| `datacontenttype`     | `application/json`                                    |
| `dataschema`          | Omit                                                  |
| `subject`             | "rule.id" value                                       |
| `time`                | "rule.updated_at" value                               |
| `data`                | Content of HTTP request body                          |

### CheckRunEvent

| CloudEvents Attribute | Value                                                                            |
| :-------------------- | :------------------------------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                                            |
| `source`              | "repository.url" value                                                           |
| `specversion`         | `1.0`                                                                            |
| `type`                | `com.github.check_run.` + "action" value                                         |
| `datacontentencoding` | Omit                                                                             |
| `datacontenttype`     | `application/json`                                                               |
| `dataschema`          | Omit                                                                             |
| `subject`             | "check_run.id" value                                                             |
| `time`                | "check_run.completed_at" value, unless "null", then "check_run.started_at" value |
| `data`                | Content of HTTP request body                                                     |

### CheckSuiteEvent

| CloudEvents Attribute | Value                                      |
| :-------------------- | :----------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value      |
| `source`              | "repository.url" value                     |
| `specversion`         | `1.0`                                      |
| `type`                | `com.github.check_suite.` + "action" value |
| `datacontentencoding` | Omit                                       |
| `datacontenttype`     | `application/json`                         |
| `dataschema`          | Omit                                       |
| `subject`             | "check_suite.id" value                     |
| `time`                | "check_suite.updated_at" value             |
| `data`                | Content of HTTP request body               |

### CodeScanningAlertEvent

| CloudEvents Attribute | Value                                              |
| :-------------------- | :------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value              |
| `source`              | "repository.url" value                             |
| `specversion`         | `1.0`                                              |
| `type`                | `com.github.code_scanning_alert.` + "action" value |
| `datacontentencoding` | Omit                                               |
| `datacontenttype`     | `application/json`                                 |
| `dataschema`          | Omit                                               |
| `subject`             | "alert.number" value                               |
| `time`                | Current time                                       |
| `data`                | Content of HTTP request body                       |

### CommitCommentEvent

| CloudEvents Attribute | Value                                                 |
| :-------------------- | :---------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                 |
| `source`              | "comment.url" value + `/` + "comment.commit_id" value |
| `specversion`         | `1.0`                                                 |
| `type`                | `com.github.commit_comment.` + "action" value         |
| `datacontentencoding` | Omit                                                  |
| `datacontenttype`     | `application/json`                                    |
| `dataschema`          | Omit                                                  |
| `subject`             | "comment.id" value                                    |
| `time`                | "comment.updated_at" value                            |
| `data`                | Content of HTTP request body                          |

### ContentReferenceEvent

| CloudEvents Attribute | Value                                            |
| :-------------------- | :----------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value            |
| `source`              | "repository.url" value                           |
| `specversion`         | `1.0`                                            |
| `type`                | `com.github.content_reference.` + "action" value |
| `datacontentencoding` | Omit                                             |
| `datacontenttype`     | `application/json`                               |
| `dataschema`          | Omit                                             |
| `subject`             | "content_reference.id" value                     |
| `time`                | Current time                                     |
| `data`                | Content of HTTP request body                     |

### CreateEvent

| CloudEvents Attribute | Value                                   |
| :-------------------- | :-------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value   |
| `source`              | "repository.url" value                  |
| `specversion`         | `1.0`                                   |
| `type`                | `com.github.create.` + "ref_type" value |
| `datacontentencoding` | Omit                                    |
| `datacontenttype`     | `application/json`                      |
| `dataschema`          | Omit                                    |
| `subject`             | "ref" value                             |
| `time`                | Current time                            |
| `data`                | Content of HTTP request body            |

### CustomPropertyEvent

| CloudEvents Attribute | Value                                          |
| :-------------------- | :--------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value          |
| `source`              | "repository.url" value                         |
| `specversion`         | `1.0`                                          |
| `type`                | `com.github.custom_property.` + "action" value |
| `datacontentencoding` | Omit                                           |
| `datacontenttype`     | `application/json`                             |
| `dataschema`          | Omit                                           |
| `subject`             | "definition.property_name" value               |
| `time`                | Current time                                   |
| `data`                | Content of HTTP request body                   |

### CustomPropertyValuesEvent

| CloudEvents Attribute | Value                                                 |
| :-------------------- | :---------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                 |
| `source`              | "repository.url" value                                |
| `specversion`         | `1.0`                                                 |
| `type`                | `com.github.custom_property_values.` + "action" value |
| `datacontentencoding` | Omit                                                  |
| `datacontenttype`     | `application/json`                                    |
| `dataschema`          | Omit                                                  |
| `subject`             | Omit                                                  |
| `time`                | Current time                                          |
| `data`                | Content of HTTP request body                          |

### DeleteEvent

| CloudEvents Attribute | Value                                   |
| :-------------------- | :-------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value   |
| `source`              | "repository.url" value                  |
| `specversion`         | `1.0`                                   |
| `type`                | `com.github.delete.` + "ref_type" value |
| `datacontentencoding` | Omit                                    |
| `datacontenttype`     | `application/json`                      |
| `dataschema`          | Omit                                    |
| `subject`             | "ref" value                             |
| `time`                | Current time                            |
| `data`                | Content of HTTP request body            |

### DependabotAlertEvent

| CloudEvents Attribute | Value                                           |
| :-------------------- | :---------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value           |
| `source`              | "repository.url" value                          |
| `specversion`         | `1.0`                                           |
| `type`                | `com.github.dependabot_alert.` + "action" value |
| `datacontentencoding` | Omit                                            |
| `datacontenttype`     | `application/json`                              |
| `dataschema`          | Omit                                            |
| `subject`             | "alert.id" value                                |
| `time`                | Current time                                    |
| `data`                | Content of HTTP request body                    |

### DeployKeyEvent

| CloudEvents Attribute | Value                                                           |
| :-------------------- | :-------------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                           |
| `source`              | "repository.url" value                                          |
| `specversion`         | `1.0`                                                           |
| `type`                | `com.github.deploy_key.` + "action" value                       |
| `datacontentencoding` | Omit                                                            |
| `datacontenttype`     | `application/json`                                              |
| `dataschema`          | Omit                                                            |
| `subject`             | "key.id" value                                                  |
| `time`                | "key.deleted_at" value, unless null then "key.created_at" value |
| `data`                | Content of HTTP request body                                    |

### DeploymentEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.deployment`               |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "deployment.id" value # task?         |
| `time`                | "deployment.updated_at" value         |
| `data`                | Content of HTTP request body          |

### DeploymentProtectionRuleEvent

| CloudEvents Attribute | Value                                                     |
| :-------------------- | :-------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                     |
| `source`              | "deployment.url" value                                    |
| `specversion`         | `1.0`                                                     |
| `type`                | `com.github.deployment_protection_rule.` + "action" value |
| `datacontentencoding` | Omit                                                      |
| `datacontenttype`     | `application/json`                                        |
| `dataschema`          | Omit                                                      |
| `subject`             | "deployment.id" value if exists                           |
| `time`                | Current time                                              |
| `data`                | Content of HTTP request body                              |

### DeploymentReviewEvent

| CloudEvents Attribute | Value                                            |
| :-------------------- | :----------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value            |
| `source`              | "deployment.url" value                           |
| `specversion`         | `1.0`                                            |
| `type`                | `com.github.deployment_review.` + "action" value |
| `datacontentencoding` | Omit                                             |
| `datacontenttype`     | `application/json`                               |
| `dataschema`          | Omit                                             |
| `subject`             | "workflow_run.id" value                          |
| `time`                | Current time                                     |
| `data`                | Content of HTTP request body                     |

### DeploymentStatusEvent

| CloudEvents Attribute | Value                                                             |
| :-------------------- | :---------------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                             |
| `source`              | "deployment.url" value                                            |
| `specversion`         | `1.0`                                                             |
| `type`                | `com.github.deployment_status.` + "deployment_status.state" value |
| `datacontentencoding` | Omit                                                              |
| `datacontenttype`     | `application/json`                                                |
| `dataschema`          | Omit                                                              |
| `subject`             | "deployment_status.url" value                                     |
| `time`                | "deployment_status.updated_at" value                              |
| `data`                | Content of HTTP request body                                      |

### DiscussionEvent

| CloudEvents Attribute | Value                                     |
| :-------------------- | :---------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value     |
| `source`              | "repository.url" value                    |
| `specversion`         | `1.0`                                     |
| `type`                | `com.github.discussion.` + "action" value |
| `datacontentencoding` | Omit                                      |
| `datacontenttype`     | `application/json`                        |
| `dataschema`          | "discussion.updated_at" value             |
| `subject`             | "discussion.id" value                     |
| `time`                | Current time                              |
| `data`                | Content of HTTP request body              |

### DiscussionCommentEvent

| CloudEvents Attribute | Value                                             |
| :-------------------- | :------------------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value             |
| `source`              | "repository.url" value                            |
| `specversion`         | `1.0`                                             |
| `type`                | `com.github.discussion_comment.` + "action" value |
| `datacontentencoding` | Omit                                              |
| `datacontenttype`     | `application/json`                                |
| `dataschema`          | Omit                                              |
| `subject`             | "discussion.id" value                             |
| `time`                | "comment.updated_at" value                        |
| `data`                | Content of HTTP request body                      |

### ForkEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.fork`                     |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "forkee.url" value                    |
| `time`                | "forkee.created_at" value             |
| `data`                | Content of HTTP request body          |

### GitHubAppAuthorizationEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "sender.url" value                    |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.github_app_authorization` |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | Omit                                  |
| `time`                | Current time                          |
| `data`                | Content of HTTP request body          |

### GollumEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.gollum`                   |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | Omit                                  |
| `time`                | Current time                          |
| `data`                | Content of HTTP request body          |

### InstallationEvent

| CloudEvents Attribute | Value                                               |
| :-------------------- | :-------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value               |
| `source`              | "installation.account.url" value                    |
| `specversion`         | `1.0`                                               |
| `type`                | `com.github.installation.` + "action" value         |
| `datacontentencoding` | Omit                                                |
| `datacontenttype`     | `application/json`                                  |
| `dataschema`          | Omit                                                |
| `subject`             | "installation.id" value                             |
| `time`                | "installation.updated_at" value # not a timestamp?? |
| `data`                | Content of HTTP request body                        |

### InstallationRepositoryEvent

| CloudEvents Attribute | Value                                                    |
| :-------------------- | :------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                    |
| `source`              | "installation.account.url" value                         |
| `specversion`         | `1.0`                                                    |
| `type`                | `com.github.installation_repositories.` + "action" value |
| `datacontentencoding` | Omit                                                     |
| `datacontenttype`     | `application/json`                                       |
| `dataschema`          | Omit                                                     |
| `subject`             | "installation.id" value                                  |
| `time`                | "installation.updated_at" value                          |
| `data`                | Content of HTTP request body                             |

### InstallationTargetEvent

| CloudEvents Attribute | Value                                              |
| :-------------------- | :------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value              |
| `source`              | "installation.account.url" value                   |
| `specversion`         | `1.0`                                              |
| `type`                | `com.github.installation_target.` + "action" value |
| `datacontentencoding` | Omit                                               |
| `datacontenttype`     | `application/json`                                 |
| `dataschema`          | Omit                                               |
| `subject`             | "installation.id" value                            |
| `time`                | Current time                                       |
| `data`                | Content of HTTP request body                       |

### IssueCommentEvent

| CloudEvents Attribute | Value                                        |
| :-------------------- | :------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value        |
| `source`              | "issue.url" value                            |
| `specversion`         | `1.0`                                        |
| `type`                | `com.github.issue_comment.` + "action" value |
| `datacontentencoding` | Omit                                         |
| `datacontenttype`     | `application/json`                           |
| `dataschema`          | Omit                                         |
| `subject`             | "comment.id" value                           |
| `time`                | "comment.updated_at" value                   |
| `data`                | Content of HTTP request body                 |

### IssuesEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.issues.` + "action" value |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "issue.number" value                  |
| `time`                | "issue.updated_at" value              |
| `data`                | Content of HTTP request body          |

### LabelEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.label.` + "action" value  |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "label.name" value                    |
| `time`                | Current time                          |
| `data`                | Content of HTTP request body          |

### MarketplacePurchaseEvent

| CloudEvents Attribute | Value                                               |
| :-------------------- | :-------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value               |
| `source`              | "sender.url" value without the `/username` portion  |
| `specversion`         | `1.0`                                               |
| `type`                | `com.github.marketplace_purchase.` + "action" value |
| `datacontentencoding` | Omit                                                |
| `datacontenttype`     | `application/json`                                  |
| `dataschema`          | Omit                                                |
| `subject`             | "marketplace_purchase.account.login" value          |
| `time`                | "effective_date" value                              |
| `data`                | Content of HTTP request body                        |

### MemberEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.member.` + "action" value |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "member.login" value                  |
| `time`                | Current time                          |
| `data`                | Content of HTTP request body          |

### MembershipEvent

| CloudEvents Attribute | Value                                                           |
| :-------------------- | :-------------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                           |
| `source`              | "team.url" value                                                |
| `specversion`         | `1.0`                                                           |
| `type`                | `com.github.membership.` + "scope" value + `.` + "action" value |
| `datacontentencoding` | Omit                                                            |
| `datacontenttype`     | `application/json`                                              |
| `dataschema`          | Omit                                                            |
| `subject`             | "member.login" value ### or `id` ?                              |
| `time`                | Current time                                                    |
| `data`                | Content of HTTP request body                                    |

### MergeGroupEvent

| CloudEvents Attribute | Value                                      |
| :-------------------- | :----------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value      |
| `source`              | "repository.url" value                     |
| `specversion`         | `1.0`                                      |
| `type`                | `com.github.merge_group.` + "action" value |
| `datacontentencoding` | Omit                                       |
| `datacontenttype`     | `application/json`                         |
| `dataschema`          | Omit                                       |
| `subject`             | "merge_group.head_ref" value               |
| `time`                | Current time                               |
| `data`                | Content of HTTP request body               |

### MetaEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.meta.` + "action" value   |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "hook_id" value                       |
| `time`                | "hook.updated_at" value               |
| `data`                | Content of HTTP request body          |

### MilestoneEvent

| CloudEvents Attribute | Value                                    |
| :-------------------- | :--------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value    |
| `source`              | "repository.url" value                   |
| `specversion`         | `1.0`                                    |
| `type`                | `com.github.milestone.` + "action" value |
| `datacontentencoding` | Omit                                     |
| `datacontenttype`     | `application/json`                       |
| `dataschema`          | Omit                                     |
| `subject`             | "milestone.number" value                 |
| `time`                | "milestone.updated_at" value             |
| `data`                | Content of HTTP request body             |

### OrganizationEvent

| CloudEvents Attribute | Value                                        |
| :-------------------- | :------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value        |
| `source`              | "organization.url" value                     |
| `specversion`         | `1.0`                                        |
| `type`                | `com.github.organization.` + "action" value  |
| `datacontentencoding` | Omit                                         |
| `datacontenttype`     | `application/json`                           |
| `dataschema`          | Omit                                         |
| `subject`             | "membership.user.login" value when available |
| `time`                | Current time                                 |
| `data`                | Content of HTTP request body                 |

### OrgBlockEvent

| CloudEvents Attribute | Value                                    |
| :-------------------- | :--------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value    |
| `source`              | "organization.url" value                 |
| `specversion`         | `1.0`                                    |
| `type`                | `com.github.org_block.` + "action" value |
| `datacontentencoding` | Omit                                     |
| `datacontenttype`     | `application/json`                       |
| `dataschema`          | Omit                                     |
| `subject`             | "blocked_user.login" value               |
| `time`                | Current time                             |
| `data`                | Content of HTTP request body             |

### PackageEvent

| CloudEvents Attribute | Value                                                                      |
| :-------------------- | :------------------------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                                      |
| `source`              | "repository.url" value                                                     |
| `specversion`         | `1.0`                                                                      |
| `type`                | `com.github.package.` + "action" value                                     |
| `datacontentencoding` | Omit                                                                       |
| `datacontenttype`     | `application/json`                                                         |
| `dataschema`          | Omit                                                                       |
| `subject`             | "package.id" value                                                         |
| `time`                | "package.updated_at" value, unless "null", then "package.created_at" value |
| `data`                | Content of HTTP request body                                               |

### PageBuildEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.page_build`               |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "build.url" value                     |
| `time`                | "pusher.updated_at" value             |
| `data`                | Content of HTTP request body          |

### ProjectCardEvent

| CloudEvents Attribute | Value                                       |
| :-------------------- | :------------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value       |
| `source`              | "repository.url" value                      |
| `specversion`         | `1.0`                                       |
| `type`                | `com.github.project_card.` + "action" value |
| `datacontentencoding` | Omit                                        |
| `datacontenttype`     | `application/json`                          |
| `dataschema`          | Omit                                        |
| `subject`             | "project_card.id" value                     |
| `time`                | "project_card.updated_at" value             |
| `data`                | Content of HTTP request body                |

### ProjectColumnEvent

| CloudEvents Attribute | Value                                         |
| :-------------------- | :-------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value         |
| `source`              | "repository.url" value                        |
| `specversion`         | `1.0`                                         |
| `type`                | `com.github.project_column.` + "action" value |
| `datacontentencoding` | Omit                                          |
| `datacontenttype`     | `application/json`                            |
| `dataschema`          | Omit                                          |
| `subject`             | "project_column.id" value                     |
| `time`                | "project_column.updated_at" value             |
| `data`                | Content of HTTP request body                  |

### ProjectEvent

| CloudEvents Attribute | Value                                  |
| :-------------------- | :------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value  |
| `source`              | "repository.url" value                 |
| `specversion`         | `1.0`                                  |
| `type`                | `com.github.project.` + "action" value |
| `datacontentencoding` | Omit                                   |
| `datacontenttype`     | `application/json`                     |
| `dataschema`          | Omit                                   |
| `subject`             | "project.id" value                     |
| `time`                | "project.updated_at" value             |
| `data`                | Content of HTTP request body           |

### ProjectsV2Event

| CloudEvents Attribute | Value                                      |
| :-------------------- | :----------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value      |
| `source`              | "repository.url" value                     |
| `specversion`         | `1.0`                                      |
| `type`                | `com.github.projects_v2.` + "action" value |
| `datacontentencoding` | Omit                                       |
| `datacontenttype`     | `application/json`                         |
| `dataschema`          | Omit                                       |
| `subject`             | "projects_v2.id" value                     |
| `time`                | "projects_v2.updated_at" value             |
| `data`                | Content of HTTP request body               |

### ProjectsV2ItemEvent

| CloudEvents Attribute | Value                                           |
| :-------------------- | :---------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value           |
| `source`              | "repository.url" value                          |
| `specversion`         | `1.0`                                           |
| `type`                | `com.github.projects_v2_item.` + "action" value |
| `datacontentencoding` | Omit                                            |
| `datacontenttype`     | `application/json`                              |
| `dataschema`          | Omit                                            |
| `subject`             | "projects_v2_item.id" value                     |
| `time`                | "projects_v2_item.updated_at" value             |
| `data`                | Content of HTTP request body                    |

### ProjectsV2StatusUpdateEvent

| CloudEvents Attribute | Value                                                    |
| :-------------------- | :------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                    |
| `source`              | "repository.url" value                                   |
| `specversion`         | `1.0`                                                    |
| `type`                | `com.github.projects_v2_status_update.` + "action" value |
| `datacontentencoding` | Omit                                                     |
| `datacontenttype`     | `application/json`                                       |
| `dataschema`          | Omit                                                     |
| `subject`             | "projects_v2_status_update.id" value                     |
| `time`                | "projects_v2_status_update.updated_at" value             |
| `data`                | Content of HTTP request body                             |

### PublicEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.owner.url" value          |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.public`                   |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "repository.name" value               |
| `time`                | "repository.updated_at" value         |
| `data`                | Content of HTTP request body          |

### PullRequestEvent

| CloudEvents Attribute | Value                                       |
| :-------------------- | :------------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value       |
| `source`              | "repository.url" value                      |
| `specversion`         | `1.0`                                       |
| `type`                | `com.github.pull_request.` + "action" value |
| `datacontentencoding` | Omit                                        |
| `datacontenttype`     | `application/json`                          |
| `dataschema`          | Omit                                        |
| `subject`             | "number" value                              |
| `time`                | "pull_request.updated_at" value             |
| `data`                | Content of HTTP request body                |

### PullRequestReviewEvent

| CloudEvents Attribute | Value                                              |
| :-------------------- | :------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value              |
| `source`              | "pull_request.url" value                           |
| `specversion`         | `1.0`                                              |
| `type`                | `com.github.pull_request_review.` + "action" value |
| `datacontentencoding` | Omit                                               |
| `datacontenttype`     | `application/json`                                 |
| `dataschema`          | Omit                                               |
| `subject`             | "review.id" value                                  |
| `time`                | "review.submitted_at" value                        |
| `data`                | Content of HTTP request body                       |

### PullRequestReviewCommentEvent

| CloudEvents Attribute | Value                                                      |
| :-------------------- | :--------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                      |
| `source`              | "pull_request.url" value                                   |
| `specversion`         | `1.0`                                                      |
| `type`                | `com.github.pull_request_review_comment.` + "action" value |
| `datacontentencoding` | Omit                                                       |
| `datacontenttype`     | `application/json`                                         |
| `dataschema`          | Omit                                                       |
| `subject`             | "comment.id" value                                         |
| `time`                | "pull_request.updated_at" value                            |
| `data`                | Content of HTTP request body                               |

### PullRequestReviewThreadEvent

| CloudEvents Attribute | Value                                                     |
| :-------------------- | :-------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                     |
| `source`              | "pull_request.url" value                                  |
| `specversion`         | `1.0`                                                     |
| `type`                | `com.github.pull_request_review_thread.` + "action" value |
| `datacontentencoding` | Omit                                                      |
| `datacontenttype`     | `application/json`                                        |
| `dataschema`          | Omit                                                      |
| `subject`             | "pull_request.id" value                                   |
| `time`                | Current time                                              |
| `data`                | Content of HTTP request body                              |

### PushEvent

| CloudEvents Attribute | Value                                   |
| :-------------------- | :-------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value   |
| `source`              | "repository.url" value                  |
| `specversion`         | `1.0`                                   |
| `type`                | `com.github.push`                       |
| `datacontentencoding` | Omit                                    |
| `datacontenttype`     | `application/json`                      |
| `dataschema`          | Omit                                    |
| `subject`             | "ref" value                             |
| `time`                | Current time # repository.updated_at ?? |
| `data`                | Content of HTTP request body            |

### RegistryPackageEvent

| CloudEvents Attribute | Value                                           |
| :-------------------- | :---------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value           |
| `source`              | "repository.url" value                          |
| `specversion`         | `1.0`                                           |
| `type`                | `com.github.registry_package.` + "action" value |
| `datacontentencoding` | Omit                                            |
| `datacontenttype`     | `application/json`                              |
| `dataschema`          | Omit                                            |
| `subject`             | "registry_package.html_url" value               |
| `time`                | "registry_package.updated_at" value             |
| `data`                | Content of HTTP request body                    |

### ReleaseEvent

| CloudEvents Attribute | Value                                  |
| :-------------------- | :------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value  |
| `source`              | "repository.url" value                 |
| `specversion`         | `1.0`                                  |
| `type`                | `com.github.release.` + "action" value |
| `datacontentencoding` | Omit                                   |
| `datacontenttype`     | `application/json`                     |
| `dataschema`          | Omit                                   |
| `subject`             | "release.id" value                     |
| `time`                | "release.\*\_at" value based on action |
| `data`                | Content of HTTP request body           |

### RepositoryEvent

| CloudEvents Attribute | Value                                     |
| :-------------------- | :---------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value     |
| `source`              | "repository.owner.url" value              |
| `specversion`         | `1.0`                                     |
| `type`                | `com.github.repository.` + "action" value |
| `datacontentencoding` | Omit                                      |
| `datacontenttype`     | `application/json`                        |
| `dataschema`          | Omit                                      |
| `subject`             | "repository.name" value                   |
| `time`                | "repository.updated_at" value             |
| `data`                | Content of HTTP request body              |

### RepositoryAdvisoryEvent

| CloudEvents Attribute | Value                                              |
| :-------------------- | :------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value              |
| `source`              | "repository.url" value                             |
| `specversion`         | `1.0`                                              |
| `type`                | `com.github.repository_advisory.` + "action" value |
| `datacontentencoding` | Omit                                               |
| `datacontenttype`     | `application/json`                                 |
| `dataschema`          | Omit                                               |
| `subject`             | "repository_advisory.ghsa_id" value                |
| `time`                | "repository_advisory.updated_at" value             |
| `data`                | Content of HTTP request body                       |

### RepositoryDispatchEvent

| CloudEvents Attribute | Value                                             |
| :-------------------- | :------------------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value             |
| `source`              | "repository.owner.url" value                      |
| `specversion`         | `1.0`                                             |
| `type`                | `com.github.repository_dispatch` + "action" value |
| `datacontentencoding` | Omit                                              |
| `datacontenttype`     | `application/json`                                |
| `dataschema`          | Omit                                              |
| `subject`             | Omit                                              |
| `time`                | Current time                                      |
| `data`                | Content of HTTP request body                      |

### RepositoryImportEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.owner.url" value          |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.repository_import`        |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "repository.name" value               |
| `time`                | "repository.updated_at" value         |
| `data`                | Content of HTTP request body          |

### RepositoryRulesetEvent

| CloudEvents Attribute | Value                                            |
| :-------------------- | :----------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value            |
| `source`              | "repository.owner.url" value                     |
| `specversion`         | `1.0`                                            |
| `type`                | `com.github.repository_ruleset` + "action" value |
| `datacontentencoding` | Omit                                             |
| `datacontenttype`     | `application/json`                               |
| `dataschema`          | Omit                                             |
| `subject`             | "repository.name" value                          |
| `time`                | "repository.updated_at" value                    |
| `data`                | Content of HTTP request body                     |

### RepositoryVulnerabilityAlertEvent

| CloudEvents Attribute | Value                                                         |
| :-------------------- | :------------------------------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value                         |
| `source`              | "repository.url" value                                        |
| `specversion`         | `1.0`                                                         |
| `type`                | `com.github.repository_vulnerability_alert.` + "action" value |
| `datacontentencoding` | Omit                                                          |
| `datacontenttype`     | `application/json`                                            |
| `dataschema`          | Omit                                                          |
| `subject`             | "alert.id" value                                              |
| `time`                | Current time # repository.updated_id ?                        |
| `data`                | Content of HTTP request body                                  |

### SecretScanningAlertEvent

| CloudEvents Attribute | Value                                                                   |
| :-------------------- | :---------------------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                                   |
| `source`              | "repository.url" value                                                  |
| `specversion`         | `1.0`                                                                   |
| `type`                | `com.github.secret_scanning_alert.` + "action" value                    |
| `datacontentencoding` | Omit                                                                    |
| `datacontenttype`     | `application/json`                                                      |
| `dataschema`          | Omit                                                                    |
| `subject`             | "alert.number" value                                                    |
| `time`                | "alert.updated_at" value , unless "null", then "alert.created_at" value |
| `data`                | Content of HTTP request body                                            |

### SecretScanningAlertLocationEvent

| CloudEvents Attribute | Value                                                                   |
| :-------------------- | :---------------------------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                                   |
| `source`              | "repository.url" value                                                  |
| `specversion`         | `1.0`                                                                   |
| `type`                | `com.github.secret_scanning_alert_location.` + "action" value           |
| `datacontentencoding` | Omit                                                                    |
| `datacontenttype`     | `application/json`                                                      |
| `dataschema`          | Omit                                                                    |
| `subject`             | "alert.number" value                                                    |
| `time`                | "alert.updated_at" value , unless "null", then "alert.created_at" value |
| `data`                | Content of HTTP request body                                            |

### SecurityAdvisoryEvent

| CloudEvents Attribute | Value                                            |
| :-------------------- | :----------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value            |
| `source`              | `github.com`                                     |
| `specversion`         | `1.0`                                            |
| `type`                | `com.github.security_advisory.` + "action" value |
| `datacontentencoding` | Omit                                             |
| `datacontenttype`     | `application/json`                               |
| `dataschema`          | Omit                                             |
| `subject`             | "security_advisory.ghsa_id" value                |
| `time`                | "security_advisory.updated_at" value             |
| `data`                | Content of HTTP request body                     |

### SecurityAndAnalysisEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.security_and_analysis`    |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | Omit                                  |
| `time`                | Current time                          |
| `data`                | Content of HTTP request body          |

### SponsorshipEvent

| CloudEvents Attribute | Value                                      |
| :-------------------- | :----------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value      |
| `source`              | "repository.url" value                     |
| `specversion`         | `1.0`                                      |
| `type`                | `com.github.sponsorship.` + "action" value |
| `datacontentencoding` | Omit                                       |
| `datacontenttype`     | `application/json`                         |
| `dataschema`          | Omit                                       |
| `subject`             | "sponsorship.sponsor.login"                |
| `time`                | Current time                               |
| `data`                | Content of HTTP request body               |

### StarEvent

| CloudEvents Attribute | Value                                                 |
| :-------------------- | :---------------------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value                 |
| `source`              | "repository.url" value                                |
| `specversion`         | `1.0`                                                 |
| `type`                | `com.github.star.` + "action" value                   |
| `datacontentencoding` | Omit                                                  |
| `datacontenttype`     | `application/json`                                    |
| `dataschema`          | Omit                                                  |
| `subject`             | Omit                                                  |
| `time`                | "starred_at" value, if present otherwise Current time |
| `data`                | Content of HTTP request body                          |

### StatusEvent

| CloudEvents Attribute | Value                                    |
| :-------------------- | :--------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value    |
| `source`              | "repository.url" value                   |
| `specversion`         | `1.0`                                    |
| `type`                | `com.github.status.` # + "state" value ? |
| `datacontentencoding` | Omit                                     |
| `datacontenttype`     | `application/json`                       |
| `dataschema`          | Omit                                     |
| `subject`             | "sha" value                              |
| `time`                | "updated_at" value                       |
| `data`                | Content of HTTP request body             |

### TeamEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.team.` + "action" value   |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "team.id" value                       |
| `time`                | "updated_at" value                    |
| `data`                | Content of HTTP request body          |

### TeamAddEvent

| CloudEvents Attribute | Value                                   |
| :-------------------- | :-------------------------------------- |
| `id`                  | "X-GitHub-Delivery" HTTP header value   |
| `source`              | "repository.url" value                  |
| `specversion`         | `1.0`                                   |
| `type`                | `com.github.team_add.` + "action" value |
| `datacontentencoding` | Omit                                    |
| `datacontenttype`     | `application/json`                      |
| `dataschema`          | Omit                                    |
| `subject`             | "team.id" value                         |
| `time`                | Current time                            |
| `data`                | Content of HTTP request body            |

### WatchEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.watch.` + "action" value  |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | Omit                                  |
| `time`                | Current time                          |
| `data`                | Content of HTTP request body          |

### WorkflowDispatchEvent

| CloudEvents Attribute | Value                                 |
| :-------------------- | :------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value |
| `source`              | "repository.url" value                |
| `specversion`         | `1.0`                                 |
| `type`                | `com.github.workflow_dispatch`        |
| `datacontentencoding` | Omit                                  |
| `datacontenttype`     | `application/json`                    |
| `dataschema`          | Omit                                  |
| `subject`             | "workflow" value                      |
| `time`                | Current time                          |
| `data`                | Content of HTTP request body          |

### WorkflowJobEvent

| CloudEvents Attribute | Value                                       |
| :-------------------- | :------------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value       |
| `source`              | "repository.url" value                      |
| `specversion`         | `1.0`                                       |
| `type`                | `com.github.workflow_job.` + "action" value |
| `datacontentencoding` | Omit                                        |
| `datacontenttype`     | `application/json`                          |
| `dataschema`          | Omit                                        |
| `subject`             | "workflow_job.name" value                   |
| `time`                | Current time                                |
| `data`                | Content of HTTP request body                |

### WorkflowRunEvent

| CloudEvents Attribute | Value                                       |
| :-------------------- | :------------------------------------------ |
| `id`                  | "X-GitHub-Delivery" HTTP header value       |
| `source`              | "repository.url" value                      |
| `specversion`         | `1.0`                                       |
| `type`                | `com.github.workflow_run.` + "action" value |
| `datacontentencoding` | Omit                                        |
| `datacontenttype`     | `application/json`                          |
| `dataschema`          | Omit                                        |
| `subject`             | "workflow.name" value                       |
| `time`                | Current time                                |
| `data`                | Content of HTTP request body                |
