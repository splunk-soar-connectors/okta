# Okta

Publisher: Splunk <br>
Connector Version: 2.3.2 <br>
Product Vendor: Okta <br>
Product Name: Okta <br>
Minimum Product Version: 5.2.0

This app supports various identity management actions on Okta

## Pagination

The pagination mechanism has been implemented for the investigative actions mentioned below.

- list users
- list user groups
- list providers
- list roles

The pagination mechanism has been explained below.

- Limit Parameter: This input parameter is used to limit the total number of items (a valid
  positive integer) to be fetched in action results.

**Examples**\
Total items in the end system for reference in the below examples are 950 and internally, every page
fetched will have 200 result items. Based on the value of the limit and other parameters combined,
the required items from every page will be fetched and added to the action results output. The
'after' field (for navigating to next pages) used in API calls is handled internally by the
pagination mechanism.

- **Example 1:** Limit = 50

  - This will fetch the first 50 items

- **Example 2:** Limit = 200

  - This will fetch the first 200 items

- **Example 3:** Limit = 240

  - This will fetch all 200 items from the first page and 40 items from the second page. Hence,
    in total, it will fetch 240 items.

- **Example 4:** Limit = 1000

  - This will fetch all 950 items

- **Example 6:** Limit = None

  Here the None is considered as empty parameter value

  - This will fetch all 950 items

## Port Information

The app uses HTTP/ HTTPS protocol for communicating with the Okta server. Below are the default
ports used by Splunk SOAR.

|         Service Name | Transport Protocol | Port |
|----------------------|--------------------|------|
|         http | tcp | 80 |
|         https | tcp | 443 |

## Permissions

Super admins can assign admin permissions to individuals or groups.\
**Individual** assignments are better for a manageable number of admin accounts. When you assign
admin permissions to individuals, you do so one at a time, whenever necessary. Remember that every
organization must always have at least one individual assigned super admin.\
**Admin groups** work better when you need to onboard a large number of admins quickly. Assign those
admins to one group, and then grant admin permissions to that group. Okta groups, AD groups, and
LDAP groups are all eligible.

To assign the roles to any user, it is required to run the **"assign role"** action using the asset
configured with the API token of a **Super admin user(SUPER_ADMIN)** in the OKTA server to assign
appropriate permissions to that normal user.

Step to assign a Super admin role to user or group.

- 1\. In the Admin Console, go to **Security > Administrators** .
- 2\. Click **Add Administrator** , depending on whether you are assigning privileges to an
  individual or group.
- 3\. In the **Grant administrator role to** field, begin typing the name of the user that we want
  to assign admin privileges to and select the correct user from the search list.
- 4\. Select the **Super Administrator** roles you want the user or group to have. You can assign
  multiple admin roles to an individual or group.
- 5\. Some admin roles require additional input. If you selected Application Administrator, Group
  Administrator, Help Desk Administrator, Group Membership Administrator, you need to indicate
  whether that role administers all users, groups, apps, just specific ones. (Copy and Paste
  commands allow you to apply the same assignments to multiple roles).
- 6\. Click Add Administrator to complete the assignment.

The following tables show the Details of the roles and what they can perform.

| Role type | Label | Detail |
|-----------------------------|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SUPER_ADMIN | Super Administrator | Perform all admin activities for an organization. Super admins have full management access. |
| ORG_ADMIN | Organization Administrator | Perform most admin activities for an organization. Note: organization admins cannot manage applications, authorization servers, hooks, Okta Mobile, or other admins. |
| APP_ADMIN | Application Administrator | View and manage user permissions in an application. Note: You can specify one or more applications after selecting this role. |
| USER_ADMIN | Group Administrator | Manage users, their profiles, and their credentials. Note: You can specify one or more groups after selecting this role. |
| HELP_DESK_ADMIN | Help Desk Administrator | View and unlock users, reset passwords and reset MFA. Note: You can specify one or more groups after selecting this role. |
| GROUP_MEMBERSHIP_ADMIN | Group Membership Administrator | Manages the membership of groups. Note: You can specify one or more groups after selecting this role. |
| READ_ONLY_ADMIN | Read Only Administrator | View most data in the Admin Console. |
| API_ACCESS_MANAGEMENT_ADMIN | API Access Management Administrator | Build custom authorization servers to protect your API endpoints. |
| REPORT_ADMIN | Report Administrator | View all reports and the System log. |
| MOBILE_ADMIN | Mobile Administrator | Perform actions related to mobile policies, sign-on policies, mobile devices, and Okta Mobile. |

Port Information

The app uses HTTP/ HTTPS protocol for communicating with the Okta server. Below are the default
ports used by Splunk SOAR.

|         Service Name | Transport Protocol | Port |
|----------------------|--------------------|------|
|         http | tcp | 80 |
|         https | tcp | 443 |

### Configuration variables

This table lists the configuration variables required to operate Okta. These variables are specified when configuring a Okta asset in Splunk SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**api_key** | required | password | API token |
**base_url** | required | string | Your organization's url. Example: https://your-org.okta.com |
**verify_server_cert** | optional | boolean | Verify server certificate |

### Supported Actions

[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration <br>
[send push notification](#action-send-push-notification) - Validate the user prompt with push notification <br>
[list users](#action-list-users) - Get the list of users <br>
[list user groups](#action-list-user-groups) - Enumerates Groups in your organization with pagination. A subset of Groups can be returned that match a supported filter expression or query <br>
[add group](#action-add-group) - Add a group <br>
[reset password](#action-reset-password) - Generate a one-time token that can be used to reset the user's password <br>
[set password](#action-set-password) - Set the password of a user without validating existing credentials <br>
[disable user](#action-disable-user) - Disables the specified user <br>
[clear user sessions](#action-clear-user-sessions) - Clears the specified user's sessions <br>
[enable user](#action-enable-user) - Enables the specified user <br>
[get user](#action-get-user) - Get information about a user <br>
[get group](#action-get-group) - Get information about a group <br>
[list providers](#action-list-providers) - List identity providers (IdPs) in your organization <br>
[list roles](#action-list-roles) - Lists all roles assigned to a user <br>
[assign role](#action-assign-role) - Assign a role to a user <br>
[unassign role](#action-unassign-role) - Unassign a role to a user <br>
[add group user](#action-add-group-user) - Add a user to an Okta group <br>
[remove group user](#action-remove-group-user) - Remove a user from a group <br>
[get user groups](#action-get-user-groups) - List groups the user is part of

## action: 'test connectivity'

Validate the asset configuration for connectivity using supplied configuration

Type: **test** <br>
Read only: **True**

#### Action Parameters

No parameters are required for this action

#### Action Output

No Output

## action: 'send push notification'

Validate the user prompt with push notification

Type: **contain** <br>
Read only: **False**

The action has not yet been implemented for the "sms" and the "token:software:totp" factortypes.<br>Currently, the action would generate a new OTP for the "sms" factortype and will not verify it.<br>The action would fail for the "token:software:totp" factortype as it has not yet been implemented.<br>One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>USER_ADMIN</li><li>HELP_DESK_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**email** | required | Okta User id, email address, or username | string | `okta user id` `okta email address` `okta username` `user name` `email` |
**factortype** | required | Okta Factor Type | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.email | string | `okta user id` `okta email address` `okta username` `user name` `email` | 00uby4va2hynIj0mS0h7 test@test.com |
action_result.parameter.factortype | string | | |
action_result.data.\*.\_links.activate.href | string | | https://your-org.okta.com/api/v1/users/00uw82w5q56RZvUYK0h7/factors/mblwbi82gd6xSc4Cv0h7/lifecycle/activate |
action_result.data.\*.\_links.cancel.href | string | | https://test.okta.com/api/v1/users/00uwd6q3pq9glsd4y0h7/factors/opfxrtgfpsdvlnBMb10h7/transactions/v2qwt.OkKjplesRECb9iDlchH6eg |
action_result.data.\*.\_links.factor.href | string | | https://test.okta.com/api/v1/users/00plrdygpq950Wt4y0h7/factors/opfx5ppoleDlnBMb10h7 |
action_result.data.\*.\_links.poll.href | string | | https://test.okta.com/api/v1/users/00uwd6wesd950Wt4y0h7/factors/opfx5wiuhyDlnBMb10h7/transactions/v2mst.OkKjcB4cRwsbniDlchH6eg |
action_result.data.\*.\_links.resend.\*.href | string | | https://your-org.okta.com/api/v1/users/00uw82w5q56RZvUYK0h7/factors/mblwbi82gd6xSc4Cv0h7/resend |
action_result.data.\*.\_links.resend.\*.name | string | | sms |
action_result.data.\*.\_links.self.href | string | | https://your-org.okta.com/api/v1/users/00uw82w5q56RZvUYK0h7/factors/mblwbi82gd6xSc4Cv0h7 |
action_result.data.\*.\_links.user.href | string | | https://your-org.okta.com/api/v1/users/00uw82w5q56RZvUYK0h7 |
action_result.data.\*.\_links.verify.href | string | | https://your-org.okta.com/api/v1/users/00uw82w5q56RZvUYK0h7/factors/opfwbi0w6kZD0l8Fn0h7/verify |
action_result.data.\*.created | string | | 2021-01-11T07:25:35.000Z |
action_result.data.\*.expiresAt | string | | 2022-05-25T14:15:27.000Z |
action_result.data.\*.factorResult | string | | SUCCESS |
action_result.data.\*.factorType | string | | sms |
action_result.data.\*.id | string | | mblwbi82gd6xSc4Cv0h7 |
action_result.data.\*.lastUpdated | string | | 2021-01-11T07:25:35.000Z |
action_result.data.\*.profile.credentialId | string | | test@example.com |
action_result.data.\*.profile.deviceType | string | | SmartPhone_Android |
action_result.data.\*.profile.keys.\*.e | string | | AQAB |
action_result.data.\*.profile.keys.\*.kid | string | | default |
action_result.data.\*.profile.keys.\*.kty | string | | RSA |
action_result.data.\*.profile.keys.\*.n | string | | 7iO7JaNuKfrqZI8fkWfwpeKfSMgJQ1iX2N-jsA1yFqV6lhyThmwus5BRTyVGmAYrKH9vnQTTTT9R1viHO5yJ5cBZS1fFmiQJ-VK9MpqiKKps6ozvYu1Xd2v9w1mdqljqFndvwoK7kGgvAP5BPAkEbVnS-ponoCPy9d5itHmcRKdN91l86WpIQ8X8R-BjPBFMZpt69MnzwzBBW6z3Y98GTwgb55qpzNDuMN4YU_KorvRhcFlUJ5chMU8Pe3nrR0UN6L9cTc89f1oULldvEF-OOmuEovm9smOYnAKH_Ugi7Aple7HpoKHpYEEp8mbfS5QFzfhkBwhE4fUQJ4RUgCJ5JQ |
action_result.data.\*.profile.keys.\*.use | string | | sig |
action_result.data.\*.profile.name | string | | test |
action_result.data.\*.profile.phoneNumber | string | | |
action_result.data.\*.profile.platform | string | | ANDROID |
action_result.data.\*.profile.version | string | | 28 |
action_result.data.\*.provider | string | | OKTA |
action_result.data.\*.status | string | | PENDING_ACTIVATION |
action_result.data.\*.vendorName | string | | OKTA |
action_result.summary | string | | |
action_result.summary.result.\_links.cancel.href | string | | https://test.okta.com/api/v1/users/00uwwww3pq950Wt4y0h7/factors/opfwwwixcyDlnBMb10h7/transactions/v2mtt.OkKjcwwwwECb9iDlchH6eg |
action_result.summary.result.\_links.factor.href | string | | https://test.okta.com/api/v1/users/00plrdygpq950Wt4y0h7/factors/opfx5ppoleDlnBMb10h7 |
action_result.summary.result.\_links.poll.href | string | | https://dev-567809.oktapreview.com/api/v1/users/00uwwww3pq950Wt4y0h7/factors/opfx5piwwwDlnBMb10h7/transactions/vert.OkKjcB4cRECb9egrddeg |
action_result.summary.result.\_links.verify.href | string | | https://test.okta.com/api/v1/users/00plrdygpq950Wt4y0h7/factors/opfx5ppoleDlnBMb10h7/verify |
action_result.summary.result.expiresAt | string | | 2022-05-25T14:15:27.000Z |
action_result.summary.result.factorResult | string | | WAITING REJECTED SUCCESS TIMEOUT |
action_result.summary.result.profile.credentialId | string | | test@example.com |
action_result.summary.result.profile.deviceType | string | | SmartPhone_Android |
action_result.summary.result.profile.keys.\*.e | string | | AQAB |
action_result.summary.result.profile.keys.\*.kid | string | | default |
action_result.summary.result.profile.keys.\*.kty | string | | RSA |
action_result.summary.result.profile.keys.\*.n | string | | sjBjRC1kl3CKBaKfvlu4i1jkhgfjyfgjhbkjbjkygkjhbkjnkuguyfvbFqGWxEGMvq7wyanETL4Q6JyhQ6VlYoaTXenN2cuER4hbxYgLCyOcDOvuPBNa3nVFwfMY_gGIwAfvMP0s7Ige-ZsFZ4qkoOK-OVTk4wEuFEwYOlXVjdc6TSv3AsC0Vry-MWg2tXNS-c3yNTe5GI2OR8L_jM7y4csTkTOKx4fQSnsq6A9zEfIs1eqw8xDbUbzdGtwvi2BB_QtWqPfMXsex3crW-K-GYMrw7teCGVjf-JwN3r7Bxle4yn9VSFnWlzwgymukugR0ekw_dNpL0IdIPw |
action_result.summary.result.profile.keys.\*.use | string | | sig |
action_result.summary.result.profile.name | string | | AC2001 |
action_result.summary.result.profile.platform | string | | ANDROID |
action_result.summary.result.profile.version | string | | 29 |
action_result.message | string | | Successfully sent push notification |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list users'

Get the list of users

Type: **investigate** <br>
Read only: **True**

Limit parameter is used to provide total number of users to be fetched. Please provide a valid positive integer value for limit. Use the <strong>query</strong> parameter for a simple lookup of users by name, for example when creating a people picker. The value of <strong>query</strong> is matched against <strong>firstName</strong>, <strong>lastName</strong>, or <strong>email</strong>. <br />Use the <strong>filter</strong> parameter to filter on the following properties:<ul><li>status</li><li>lastUpdated</li><li>id</li><li>profile.login</li><li>profile.email</li><li>profile.firstName</li><li>profile.lastName</li></ul><p>Use the <strong>search</strong> parameter to do a case-insensitive search on the following properties:</p><ul><li>id</li><li>status</li><li>created</li><li>activated</li><li>statusChanged</li><li>lastUpdated</li></ul><p>Filter and search operators:</p><ul><li>eq: equal</li><li>sw: starts with</li><li>pr: present (has value)</li><li>gt: greater than</li><li>ge: greater than or equal</li><li>lt: less than</li><li>le: less than or equal</li></ul><p>Filter and search examples:</p><ul><li>status eq "STAGED"</li><li>lastUpdated lt "yyyy-MM-dd'T'HH:mm:ss.SSSZ"</li><li>lastUpdated gt "yyyy-MM-dd'T'HH:mm:ss.SSSZ"</li></ul><br>One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>APP_ADMIN</li><li>USER_ADMIN</li><li>HELP_DESK_ADMIN</li><li>GROUP_MEMBERSHIP_ADMIN</li><li>READ_ONLY_ADMIN</li><li>API_ACCESS_MANAGEMENT_ADMIN</li><li>REPORT_ADMIN</li><li>MOBILE_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**query** | optional | Find a user that matches firstName, lastName, and email properties | string | |
**filter** | optional | Filters users with a supported expression for a subset of properties | string | |
**search** | optional | Searches for users with a supported filtering expression for most properties | string | |
**limit** | optional | Specifies the number of results returned | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.filter | string | | test |
action_result.parameter.limit | numeric | | 10 100 |
action_result.parameter.query | string | | test |
action_result.parameter.search | string | | |
action_result.data.\*.\_links.self.href | string | `url` | https://your-org.okta.com/api/v1/users/00uf6qknlgEVQhDIF0h7 |
action_result.data.\*.activated | string | | 2018-05-25T21:01:55.000Z |
action_result.data.\*.created | string | | 2018-05-25T21:01:54.000Z |
action_result.data.\*.credentials.emails.\*.status | string | | VERIFIED |
action_result.data.\*.credentials.emails.\*.status | string | | VERIFIED |
action_result.data.\*.credentials.emails.\*.type | string | | PRIMARY |
action_result.data.\*.credentials.emails.\*.type | string | | PRIMARY |
action_result.data.\*.credentials.emails.\*.value | string | `email` | test@splunk.com |
action_result.data.\*.credentials.emails.\*.value | string | `email` | test@splunk.com |
action_result.data.\*.credentials.provider.name | string | | OKTA |
action_result.data.\*.credentials.provider.type | string | | OKTA |
action_result.data.\*.credentials.recovery_question.question | string | | What is the food you least liked as a child? |
action_result.data.\*.id | string | `okta user id` | 00uf6qknlgEVQhDIF0h7 |
action_result.data.\*.lastLogin | string | | 2018-10-09T00:20:11.000Z |
action_result.data.\*.lastUpdated | string | | 2018-05-25T21:01:55.000Z |
action_result.data.\*.passwordChanged | string | | 2018-10-09T00:20:11.000Z |
action_result.data.\*.profile.city | string | | Palo Alto |
action_result.data.\*.profile.department | string | | Human Resources |
action_result.data.\*.profile.displayName | string | | First Last |
action_result.data.\*.profile.email | string | `email` | test@splunk.com |
action_result.data.\*.profile.firstName | string | | First |
action_result.data.\*.profile.lastName | string | | Last Name |
action_result.data.\*.profile.login | string | `user name` | test@test.com |
action_result.data.\*.profile.middleName | string | | Middle |
action_result.data.\*.profile.mobilePhone | string | | |
action_result.data.\*.profile.nickName | string | | |
action_result.data.\*.profile.primaryPhone | string | | |
action_result.data.\*.profile.secondEmail | string | `email` | test@splunk.com |
action_result.data.\*.profile.streetAddress | string | | 123 Anystreet |
action_result.data.\*.profile.title | string | | Software Engineer |
action_result.data.\*.status | string | | ACTIVE PROVISIONED |
action_result.data.\*.statusChanged | string | | 2018-05-25T21:01:55.000Z |
action_result.data.\*.type.id | string | | otyaa8hod6wG1QvhR0h7 |
action_result.summary | string | | |
action_result.summary.num_users | numeric | | 2 4 |
action_result.message | string | | Num users: 4 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list user groups'

Enumerates Groups in your organization with pagination. A subset of Groups can be returned that match a supported filter expression or query

Type: **investigate** <br>
Read only: **True**

Limit parameter is used to provide total number of user groups to be fetched. Please provide a valid positive integer value for limit. Use the <strong>query</strong> parameter for a simple lookup of groups by name, for example when creating a people picker. The value of <strong>query</strong> is matched against <strong>name</strong>. <br />Use the <strong>filter</strong> parameter to filter on the following properties:<ul><li>type</li><li>lastMembershipUpdated</li><li>id</li><li>lastUpdated</li></ul><br>One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>APP_ADMIN</li><li>USER_ADMIN</li><li>HELP_DESK_ADMIN</li><li>GROUP_MEMBERSHIP_ADMIN</li><li>READ_ONLY_ADMIN</li><li>API_ACCESS_MANAGEMENT_ADMIN</li><li>MOBILE_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**query** | optional | Find a group that matches name property | string | |
**filter** | optional | Filters groups with a supported expression for a subset of properties | string | |
**limit** | optional | Specifies the number of results returned | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.filter | string | | test |
action_result.parameter.limit | numeric | | 10 100 |
action_result.parameter.query | string | | test |
action_result.data.\*.\_links.apps.href | string | `url` | https://your-org.okta.com/api/v1/groups/00gaa8hocsNAbvEyn0h7/apps |
action_result.data.\*.\_links.logo.\*.href | string | `url` | https://op1static.oktacdn.com/assets/img/logos/groups/okta-medium.d7fb831bc4e7e1a5d8bd35dfaf405d9e.png |
action_result.data.\*.\_links.logo.\*.name | string | | medium |
action_result.data.\*.\_links.logo.\*.type | string | | image/png |
action_result.data.\*.\_links.source.href | string | | https://your-org.okta.com/api/v1/apps/0oambdtud0Skc25180h7 |
action_result.data.\*.\_links.users.href | string | `url` | https://your-org.okta.com/api/v1/groups/00gaa8hocsNAbvEyn0h7/users |
action_result.data.\*.created | string | | 2017-04-26T01:37:27.000Z |
action_result.data.\*.id | string | `okta group id` | 00gaa8hocsNAbvEyn0h7 |
action_result.data.\*.lastMembershipUpdated | string | | 2017-09-07T21:27:50.000Z |
action_result.data.\*.lastUpdated | string | | 2017-04-26T01:37:27.000Z |
action_result.data.\*.objectClass | string | | okta:user_group |
action_result.data.\*.profile.description | string | | All users in your organization |
action_result.data.\*.profile.dn | string | | CN=test,CN=Users,DC=corp,DC=contoso,DC=com |
action_result.data.\*.profile.externalId | string | | LJyUsvmUbEym1qdAPg8usg== |
action_result.data.\*.profile.groupScope | string | | Universal |
action_result.data.\*.profile.groupType | string | | Distribution |
action_result.data.\*.profile.name | string | | Everyone |
action_result.data.\*.profile.objectSid | string | | S-1-5-21-3790544232-372029393-2474287633-1631 |
action_result.data.\*.profile.samAccountName | string | | test |
action_result.data.\*.profile.windowsDomainQualifiedName | string | | CORP\\test |
action_result.data.\*.source.id | string | | 0oambdtud0Skc25180h7 |
action_result.data.\*.type | string | | BUILT_IN |
action_result.summary | string | | |
action_result.summary.num_groups | numeric | | 4 |
action_result.message | string | | Num groups: 4 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'add group'

Add a group

Type: **generic** <br>
Read only: **False**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** | required | Name of the group | string | |
**description** | required | Description of the group | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.description | string | | This is my test group from an action |
action_result.parameter.name | string | | Test Group |
action_result.data.\*.\_links.apps.href | string | `url` | https://your-org.okta.com/api/v1/groups/00gesvnn7wvqbyKSY0h7/apps |
action_result.data.\*.\_links.logo.\*.href | string | `url` | https://op1static.oktacdn.com/assets/img/logos/groups/okta-medium.d7fb831bc4e7e1a5d8bd35dfaf405d9e.png |
action_result.data.\*.\_links.logo.\*.name | string | | medium |
action_result.data.\*.\_links.logo.\*.type | string | | image/png |
action_result.data.\*.\_links.users.href | string | `url` | https://your-org.okta.com/api/v1/groups/00gesvnn7wvqbyKSY0h7/users |
action_result.data.\*.created | string | | 2018-04-23T17:48:55.000Z |
action_result.data.\*.id | string | `okta group id` | 00gesvnn7wvqbyKSY0h7 |
action_result.data.\*.lastMembershipUpdated | string | | 2018-04-23T17:48:55.000Z |
action_result.data.\*.lastUpdated | string | | 2018-04-23T17:48:55.000Z |
action_result.data.\*.objectClass | string | | okta:user_group |
action_result.data.\*.profile.description | string | | This is my test group from an action |
action_result.data.\*.profile.name | string | | Test Group |
action_result.data.\*.type | string | | OKTA_GROUP |
action_result.summary | string | | |
action_result.summary.group_id | string | `okta group id` | 00gesvtfjhpW2IyC00h7 |
action_result.message | string | | Group id: 00gesvtfjhpW2IyC00h7 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'reset password'

Generate a one-time token that can be used to reset the user's password

Type: **correct** <br>
Read only: **False**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>USER_ADMIN</li><li>HELP_DESK_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user_id** | required | User id | string | `okta user id` |
**receive_type** | required | Return one-time token via email or in UI | string | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.receive_type | string | | UI |
action_result.parameter.user_id | string | `okta user id` | 00uby4va2hynIj0mS0h7 |
action_result.data.\*.resetPasswordUrl | string | `url` | https://your-org.okta.com/reset_password/s-HbbqSmqoCLn0pdYTzx |
action_result.summary | string | | |
action_result.message | string | | Successfully created one-time token for user to reset password |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'set password'

Set the password of a user without validating existing credentials

Type: **contain** <br>
Read only: **False**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>USER_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**new_password** | required | Password string to set | string | |
**id** | required | ID of user | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.id | string | `okta user id` | 00uby4va2hynIj0mS0h7 |
action_result.parameter.new_password | string | | newPassword |
action_result.data.\*.\_links.activate.href | string | | https://your-org.okta.com/api/v1/users/00uvgl84d0wO31Lr60h7/lifecycle/activate |
action_result.data.\*.\_links.activate.method | string | | POST |
action_result.data.\*.\_links.changePassword.href | string | `url` | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7/credentials/change_password |
action_result.data.\*.\_links.changePassword.method | string | | POST |
action_result.data.\*.\_links.changeRecoveryQuestion.href | string | `url` | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7/credentials/change_recovery_question |
action_result.data.\*.\_links.changeRecoveryQuestion.method | string | | POST |
action_result.data.\*.\_links.deactivate.href | string | `url` | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7/lifecycle/deactivate |
action_result.data.\*.\_links.deactivate.method | string | | POST |
action_result.data.\*.\_links.expirePassword.href | string | `url` | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7/lifecycle/expire_password |
action_result.data.\*.\_links.expirePassword.method | string | | POST |
action_result.data.\*.\_links.forgotPassword.href | string | `url` | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7/credentials/forgot_password |
action_result.data.\*.\_links.forgotPassword.method | string | | POST |
action_result.data.\*.\_links.resetPassword.href | string | `url` | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7/lifecycle/reset_password |
action_result.data.\*.\_links.resetPassword.method | string | | POST |
action_result.data.\*.\_links.schema.href | string | | https://your-org.okta.com/api/v1/meta/schemas/user/oscaa8hod6wG1QvhR0h7 |
action_result.data.\*.\_links.self.href | string | `url` | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7 |
action_result.data.\*.\_links.suspend.href | string | `url` | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7/lifecycle/suspend |
action_result.data.\*.\_links.suspend.method | string | | POST |
action_result.data.\*.\_links.type.href | string | | https://your-org.okta.com/api/v1/meta/types/user/otyaa8hod6wG1QvhR0h7 |
action_result.data.\*.\_links.unsuspend.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugdwq3wbdAwsSQA0h7/lifecycle/unsuspend |
action_result.data.\*.\_links.unsuspend.href | numeric | `url` | 1 |
action_result.data.\*.\_links.unsuspend.method | string | | POST |
action_result.data.\*.activated | string | | 2018-09-27T10:27:52.000Z |
action_result.data.\*.created | string | | 2017-04-26T01:37:30.000Z |
action_result.data.\*.credentials.emails.\*.status | string | | VERIFIED |
action_result.data.\*.credentials.emails.\*.status | string | | VERIFIED |
action_result.data.\*.credentials.emails.\*.type | string | | PRIMARY |
action_result.data.\*.credentials.emails.\*.value | string | `email` | test@splunk.com |
action_result.data.\*.credentials.emails.\*.value | string | `email` | test@splunk.com |
action_result.data.\*.credentials.provider.name | string | | OKTA |
action_result.data.\*.credentials.provider.type | string | | OKTA |
action_result.data.\*.credentials.recovery_question.question | string | | What is the name of your first stuffed animal? |
action_result.data.\*.id | string | `okta user id` | 00uaa8hodkEIHTO1s0h7 |
action_result.data.\*.lastLogin | string | | 2018-10-01T07:17:10.000Z |
action_result.data.\*.lastUpdated | string | | 2018-10-09T08:58:22.000Z |
action_result.data.\*.passwordChanged | string | | 2018-10-09T08:58:22.000Z |
action_result.data.\*.profile.city | string | | Palo Alto |
action_result.data.\*.profile.department | string | | Human Resources |
action_result.data.\*.profile.displayName | string | | First Last |
action_result.data.\*.profile.email | string | `email` | test@splunk.com |
action_result.data.\*.profile.firstName | string | | First Name |
action_result.data.\*.profile.lastName | string | | Last Name |
action_result.data.\*.profile.login | string | `user name` | test@splunk.com |
action_result.data.\*.profile.middleName | string | | Middle |
action_result.data.\*.profile.mobilePhone | string | | |
action_result.data.\*.profile.nickName | string | | |
action_result.data.\*.profile.secondEmail | string | `email` | test@splunk.com |
action_result.data.\*.profile.streetAddress | string | | 123 Anystreet |
action_result.data.\*.profile.title | string | | Software Engineer |
action_result.data.\*.status | string | | ACTIVE SUSPENDED |
action_result.data.\*.statusChanged | string | | 2018-10-09T08:58:22.000Z |
action_result.data.\*.type.id | string | | otyaa8hod6wG1QvhR0h7 |
action_result.summary | string | | |
action_result.message | string | | Successfully set user password |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'disable user'

Disables the specified user

Type: **contain** <br>
Read only: **False**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>USER_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | ID of user to disable | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.id | string | `okta user id` | 00uby4va2hynIj0mS0h7 |
action_result.data | string | | |
action_result.summary | string | | |
action_result.message | string | | Successfully disabled the user |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'clear user sessions'

Clears the specified user's sessions

Type: **contain** <br>
Read only: **False**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>USER_ADMIN</li>clear user sessions</ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | ID of user to clear sessions for | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.id | string | `okta user id` | 00uby4va2hynIj0mS0h7 |
action_result.data | string | | |
action_result.summary | string | | |
action_result.message | string | | Successfully cleared user sessions |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'enable user'

Enables the specified user

Type: **correct** <br>
Read only: **False**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>USER_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** | required | ID of user to enable | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.id | string | `okta user id` | 00uby4va2hynIj0mS0h7 |
action_result.data | string | | |
action_result.summary | string | | |
action_result.message | string | | Successfully enabled the user |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get user'

Get information about a user

Type: **investigate** <br>
Read only: **True**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>APP_ADMIN</li><li>USER_ADMIN</li><li>HELP_DESK_ADMIN</li><li>GROUP_MEMBERSHIP_ADMIN</li><li>READ_ONLY_ADMIN</li><li>API_ACCESS_MANAGEMENT_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user_id** | required | User ID | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.user_id | string | `okta user id` | 00ugfn1pbgCsesAga0h7 |
action_result.data.\*.\_links.activate.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugfn1pbgCsesAga0h7/lifecycle/activate |
action_result.data.\*.\_links.activate.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugfn1pbgCsesAga0h7/lifecycle/activate |
action_result.data.\*.\_links.activate.method | string | | POST |
action_result.data.\*.\_links.activate.method | string | | POST |
action_result.data.\*.\_links.changePassword.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugdwq3wbdAwsSQA0h7/credentials/change_password |
action_result.data.\*.\_links.changePassword.method | string | | POST |
action_result.data.\*.\_links.changeRecoveryQuestion.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugdwq3wbdAwsSQA0h7/credentials/change_recovery_question |
action_result.data.\*.\_links.changeRecoveryQuestion.method | string | | POST |
action_result.data.\*.\_links.deactivate.href | string | `url` | https://your-org.okta.com/api/v1/users/00uf6qknlgEVQhDIF0h7/lifecycle/deactivate |
action_result.data.\*.\_links.deactivate.method | string | | POST |
action_result.data.\*.\_links.expirePassword.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugdwq3wbdAwsSQA0h7/lifecycle/expire_password |
action_result.data.\*.\_links.expirePassword.method | string | | POST |
action_result.data.\*.\_links.forgotPassword.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugdwq3wbdAwsSQA0h7/credentials/forgot_password |
action_result.data.\*.\_links.forgotPassword.method | string | | POST |
action_result.data.\*.\_links.reactivate.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugdwq3wbdAwsSQA0h7/lifecycle/reactivate |
action_result.data.\*.\_links.reactivate.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugdwq3wbdAwsSQA0h7/lifecycle/reactivate |
action_result.data.\*.\_links.reactivate.method | string | | POST |
action_result.data.\*.\_links.reactivate.method | string | | POST |
action_result.data.\*.\_links.resetFactors.href | string | | https://your-org.okta.com/api/v1/users/00uaa8hodkEIHTO1s0h7/lifecycle/reset_factors |
action_result.data.\*.\_links.resetFactors.method | string | | POST |
action_result.data.\*.\_links.resetPassword.href | string | `url` | https://your-org.okta.com/api/v1/users/00uf6qknlgEVQhDIF0h7/lifecycle/reset_password |
action_result.data.\*.\_links.resetPassword.method | string | | POST |
action_result.data.\*.\_links.schema.href | string | | https://your-org.okta.com/api/v1/meta/schemas/user/oscaa8hod6wG1QvhR0h7 |
action_result.data.\*.\_links.self.href | string | `url` | https://your-org.okta.com/api/v1/users/00ugfn1pbgCsesAga0h7 |
action_result.data.\*.\_links.suspend.href | string | `url` | https://your-org.okta.com/api/v1/users/00uf6qknlgEVQhDIF0h7/lifecycle/suspend |
action_result.data.\*.\_links.suspend.method | string | | POST |
action_result.data.\*.\_links.type.href | string | | https://your-org.okta.com/api/v1/meta/types/user/otyaa8hod6wG1QvhR0h7 |
action_result.data.\*.\_links.unsuspend.href | string | | https://your-org.okta.com/api/v1/users/00uvgl84d0wO31Lr60h7/lifecycle/unsuspend |
action_result.data.\*.\_links.unsuspend.method | string | | POST |
action_result.data.\*.activated | string | | 2018-05-25T21:01:55.000Z |
action_result.data.\*.created | string | | 2018-10-01T07:20:36.000Z |
action_result.data.\*.credentials.emails.\*.status | string | | VERIFIED |
action_result.data.\*.credentials.emails.\*.status | string | | VERIFIED |
action_result.data.\*.credentials.emails.\*.type | string | | PRIMARY |
action_result.data.\*.credentials.emails.\*.type | string | | PRIMARY |
action_result.data.\*.credentials.emails.\*.value | string | `email` | test@splunk.com |
action_result.data.\*.credentials.emails.\*.value | string | `email` | test@splunk.com |
action_result.data.\*.credentials.provider.name | string | | OKTA |
action_result.data.\*.credentials.provider.type | string | | OKTA |
action_result.data.\*.credentials.recovery_question.question | string | | What is your favorite color? |
action_result.data.\*.id | string | `okta user id` | 00ugfn1pbgCsesAga0h7 |
action_result.data.\*.lastLogin | string | | 2018-10-09T00:20:11.000Z |
action_result.data.\*.lastUpdated | string | | 2018-10-01T07:20:36.000Z |
action_result.data.\*.passwordChanged | string | | 2018-10-09T00:20:11.000Z |
action_result.data.\*.profile.city | string | | Palo Alto |
action_result.data.\*.profile.department | string | | Human Resources |
action_result.data.\*.profile.displayName | string | | First Last |
action_result.data.\*.profile.email | string | `email` | test@splunk.com |
action_result.data.\*.profile.firstName | string | | First |
action_result.data.\*.profile.lastName | string | | Last |
action_result.data.\*.profile.login | string | `user name` | test@splunk.com |
action_result.data.\*.profile.middleName | string | | Middle |
action_result.data.\*.profile.mobilePhone | string | | |
action_result.data.\*.profile.nickName | string | | |
action_result.data.\*.profile.secondEmail | string | `email` | test@splunk.com |
action_result.data.\*.profile.streetAddress | string | | 123 Anystreet |
action_result.data.\*.profile.title | string | | Software Engineer |
action_result.data.\*.status | string | | ACTIVE PROVISIONED STAGED |
action_result.data.\*.statusChanged | string | | 2018-09-27T10:27:52.000Z |
action_result.data.\*.type.id | string | | otyaa8hod6wG1QvhR0h7 |
action_result.summary | string | | |
action_result.message | string | | Successfully retrieved user |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'get group'

Get information about a group

Type: **investigate** <br>
Read only: **True**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>APP_ADMIN</li><li>USER_ADMIN</li><li>HELP_DESK_ADMIN</li><li>GROUP_MEMBERSHIP_ADMIN</li><li>READ_ONLY_ADMIN</li><li>API_ACCESS_MANAGEMENT_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**group_id** | required | Group id | string | `okta group id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.group_id | string | `okta group id` | 00gesha2ooDwDRfRI0h7 |
action_result.data.\*.\_links.apps.href | string | `url` | https://your-org.okta.com/api/v1/groups/00gesha2ooDwDRfRI0h7/apps |
action_result.data.\*.\_links.logo.\*.href | string | `url` | https://op1static.oktacdn.com/assets/img/logos/groups/okta-medium.d7fb831bc4e7e1a5d8bd35dfaf405d9e.png |
action_result.data.\*.\_links.logo.\*.name | string | | medium |
action_result.data.\*.\_links.logo.\*.type | string | | image/png |
action_result.data.\*.\_links.source.href | string | | https://your-org.okta.com/api/v1/apps/0oambdtud0Skc25180h7 |
action_result.data.\*.\_links.users.href | string | `url` | https://your-org.okta.com/api/v1/groups/00gesha2ooDwDRfRI0h7/users |
action_result.data.\*.created | string | | 2018-04-22T02:45:22.000Z |
action_result.data.\*.id | string | `okta group id` | 00gesha2ooDwDRfRI0h7 |
action_result.data.\*.lastMembershipUpdated | string | | 2018-04-22T02:45:22.000Z |
action_result.data.\*.lastUpdated | string | | 2018-04-22T02:45:22.000Z |
action_result.data.\*.objectClass | string | | okta:user_group |
action_result.data.\*.profile.description | string | | All users in your organization West Coast Users |
action_result.data.\*.profile.dn | string | | CN=Allowed RODC Password Replication Group,CN=Users,DC=corp,DC=contoso,DC=com |
action_result.data.\*.profile.externalId | string | | ytek0Im3QUKSXkLUVICyig== |
action_result.data.\*.profile.groupScope | string | | Domain Local |
action_result.data.\*.profile.groupType | string | | Security |
action_result.data.\*.profile.name | string | | Everyone West Coast Users |
action_result.data.\*.profile.objectSid | string | | S-1-5-21-3790544232-372029393-2474287633-571 |
action_result.data.\*.profile.samAccountName | string | | Allowed RODC Password Replication Group |
action_result.data.\*.profile.windowsDomainQualifiedName | string | | CORP\\Allowed RODC Password Replication Group |
action_result.data.\*.source.id | string | | 0oambdtud0Skc25180h7 |
action_result.data.\*.type | string | | BUILT_IN OKTA_GROUP |
action_result.summary | string | | |
action_result.message | string | | Successfully retrieved group |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list providers'

List identity providers (IdPs) in your organization

Type: **investigate** <br>
Read only: **True**

Limit parameter is used to provide total number of identity providers to be fetched from your organization. Please provide a valid positive integer value for limit. Use the <strong>query</strong> parameter for a simple lookup of idps by name, for example when creating a people picker. The value of <strong>query</strong> is matched against <strong>name</strong>.<br>One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li><li>ORG_ADMIN</li><li>READ_ONLY_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**query** | optional | Find the identity providers that matches name property | string | |
**type** | optional | Filter IdPs by type | string | |
**limit** | optional | Specifies the number of results returned | numeric | |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.limit | numeric | | 10 1 |
action_result.parameter.query | string | | |
action_result.parameter.type | string | | MICROSOFT GOOGLE |
action_result.data.\*.\_links.authorize.hints.allow | string | | GET |
action_result.data.\*.\_links.authorize.href | string | `url` | https://your-org.okta.com/oauth2/v1/authorize?idp=0oaby5kenyrbKcB3P0h7&client_id={clientId}&response_type={responseType}&response_mode={responseMode}&scope={scopes}&redirect_uri={redirectUri}&state={state}&nonce={nonce} |
action_result.data.\*.\_links.authorize.templated | boolean | | True False |
action_result.data.\*.\_links.clientRedirectUri.hints.allow | string | | POST |
action_result.data.\*.\_links.clientRedirectUri.href | string | `url` | https://your-org.okta.com/oauth2/v1/authorize/callback |
action_result.data.\*.created | string | | 2017-09-07T22:01:15.000Z |
action_result.data.\*.id | string | `okta idps id` | 0oaby5kenyrbKcB3P0h7 |
action_result.data.\*.issuerMode | string | | ORG_URL |
action_result.data.\*.lastUpdated | string | | 2017-09-07T22:01:15.000Z |
action_result.data.\*.name | string | | O365-phantomcyberdev |
action_result.data.\*.policy.accountLink.action | string | | AUTO |
action_result.data.\*.policy.accountLink.filter | string | | |
action_result.data.\*.policy.maxClockSkew | numeric | | 0 |
action_result.data.\*.policy.provisioning.action | string | | AUTO |
action_result.data.\*.policy.provisioning.conditions.deprovisioned.action | string | | NONE |
action_result.data.\*.policy.provisioning.conditions.suspended.action | string | | NONE |
action_result.data.\*.policy.provisioning.groups.action | string | | NONE |
action_result.data.\*.policy.provisioning.profileMaster | boolean | | True False |
action_result.data.\*.policy.subject.filter | string | | |
action_result.data.\*.policy.subject.matchAttribute | string | | |
action_result.data.\*.policy.subject.matchType | string | | USERNAME_OR_EMAIL |
action_result.data.\*.policy.subject.userNameTemplate.template | string | | idpuser.userPrincipalName |
action_result.data.\*.protocol.credentials.client.client_id | string | | 2904b0a4-ebb7-42db-9d35-3280c656c121 |
action_result.data.\*.protocol.credentials.client.client_secret | string | | qw8y7gztT5DznvmPfmdEmHo |
action_result.data.\*.protocol.endpoints.authorization.binding | string | | HTTP-REDIRECT |
action_result.data.\*.protocol.endpoints.authorization.url | string | `url` | https://login.microsoftonline.com/common/oauth2/v2.0/authorize |
action_result.data.\*.protocol.endpoints.token.binding | string | | HTTP-POST |
action_result.data.\*.protocol.endpoints.token.url | string | `url` | https://login.microsoftonline.com/common/oauth2/v2.0/token |
action_result.data.\*.protocol.scopes | string | `url` | https://graph.microsoft.com/User.Read |
action_result.data.\*.protocol.type | string | | OIDC |
action_result.data.\*.status | string | | ACTIVE |
action_result.data.\*.type | string | | MICROSOFT |
action_result.summary | string | | |
action_result.summary.num_idps | numeric | | 1 0 |
action_result.message | string | | Num idps: 1 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'list roles'

Lists all roles assigned to a user

Type: **investigate** <br>
Read only: **True**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user_id** | required | User ID | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.user_id | string | `okta user id` | 00uaa8hodkEIHTO1s0h7 |
action_result.data.\*.\_links.assignee.href | string | | https://your-org.okta.com/api/v1/users/00uvgl84d0wO31Lr60h7 |
action_result.data.\*.\_links.self.href | string | | https://your-org.okta.com/api/v1/users/00uqeqeo07E1ALkVG0h7 |
action_result.data.\*.activated | string | | |
action_result.data.\*.assignmentType | string | | USER |
action_result.data.\*.created | string | | 2018-04-21T02:42:31.000Z |
action_result.data.\*.credentials.emails.\*.status | string | | VERIFIED |
action_result.data.\*.credentials.emails.\*.type | string | | PRIMARY |
action_result.data.\*.credentials.emails.\*.value | string | | test@example.com |
action_result.data.\*.credentials.provider.name | string | | OKTA |
action_result.data.\*.credentials.provider.type | string | | OKTA |
action_result.data.\*.credentials.recovery_question.question | string | | What is the food you least liked as a child? |
action_result.data.\*.id | string | `okta role id` | IFIFAX2BIRGUSTQ |
action_result.data.\*.label | string | | Application Administrator |
action_result.data.\*.lastLogin | string | | |
action_result.data.\*.lastUpdated | string | | 2018-04-21T02:42:31.000Z |
action_result.data.\*.passwordChanged | string | | |
action_result.data.\*.profile.city | string | | Palo Alto |
action_result.data.\*.profile.department | string | | cédille |
action_result.data.\*.profile.displayName | string | | cédille |
action_result.data.\*.profile.email | string | | test@example.com |
action_result.data.\*.profile.firstName | string | | Herman2 |
action_result.data.\*.profile.lastName | string | | Edwards |
action_result.data.\*.profile.login | string | `user name` | test@example.com |
action_result.data.\*.profile.middleName | string | | cédille |
action_result.data.\*.profile.mobilePhone | string | | |
action_result.data.\*.profile.nickName | string | | cédille |
action_result.data.\*.profile.primaryPhone | string | | |
action_result.data.\*.profile.secondEmail | string | | |
action_result.data.\*.profile.streetAddress | string | | 123 Anystreet |
action_result.data.\*.profile.title | string | | Leader of Herman's Hermits |
action_result.data.\*.status | string | | ACTIVE |
action_result.data.\*.statusChanged | string | | |
action_result.data.\*.type | string | | APP_ADMIN |
action_result.data.\*.type.id | string | | otyaa8hod6wG1QvhR0h7 |
action_result.summary | string | | |
action_result.summary.num_roles | numeric | | 2 |
action_result.message | string | | Num roles: 2 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'assign role'

Assign a role to a user

Type: **generic** <br>
Read only: **False**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** | required | Type of role | string | |
**user_id** | required | User ID | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.type | string | | MOBILE_ADMIN |
action_result.parameter.user_id | string | `okta user id` | 00uaa8hodkEIHTO1s0h7 |
action_result.data.\*.\_links.assignee.href | string | | https://your-org.okta.com/api/v1/users/00uvgl84d0wO31Lr60h7 |
action_result.data.\*.assignmentType | string | | USER |
action_result.data.\*.created | string | | 2018-04-21T06:56:01.000Z |
action_result.data.\*.id | string | `okta role id` | ra1esbjllgTr0yoz60h7 |
action_result.data.\*.label | string | | Mobile Administrator |
action_result.data.\*.lastUpdated | string | | 2018-04-21T06:56:01.000Z |
action_result.data.\*.status | string | | ACTIVE |
action_result.data.\*.type | string | | MOBILE_ADMIN |
action_result.summary | string | | |
action_result.message | string | | Successfully assigned role to user |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'unassign role'

Unassign a role to a user

Type: **generic** <br>
Read only: **False**

One of the following roles is required to run this action:<ul><li>SUPER_ADMIN</li></ul>

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user_id** | required | User ID | string | `okta user id` |
**role_id** | required | ID of rule | string | `okta role id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.role_id | string | `okta role id` | KVJUKUS7IFCE2SKO |
action_result.parameter.user_id | string | `okta user id` | 00uby4va2hynIj0mS0h7 |
action_result.data | string | | |
action_result.summary | string | | |
action_result.message | string | | Role is not assigned to user |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'add group user'

Add a user to an Okta group

Type: **generic** <br>
Read only: **False**

Adds a user to a group of OKTA_GROUP type. You can modify only memberships for groups of OKTA_GROUP type.
Application imports are responsible for managing group memberships for groups of APP_GROUP type such as Active Directory groups.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**group_id** | required | Group id | string | `okta group id` |
**user_id** | required | User id | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.group_id | string | `okta group id` | |
action_result.parameter.user_id | string | `okta user id` | |
action_result.data.\*.group_id | string | `okta group id` | |
action_result.data.\*.group_name | string | | |
action_result.data.\*.user_id | string | `okta user id` | |
action_result.data.\*.user_name | string | `user name` `email` | |
action_result.summary.group_id | string | | 00gw7z0fzcJdhfDSb0h7 |
action_result.summary.group_name | string | | test_group |
action_result.summary.user_id | string | | 00u149z08g1Ln68zy0h8 |
action_result.summary.user_name | string | | john.doe@email.com |
action_result.message | string | | |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

## action: 'remove group user'

Remove a user from a group

Type: **generic** <br>
Read only: **False**

Removes a user from a group of OKTA_GROUP type. You can modify only memberships for groups of OKTA_GROUP type. Application imports are responsible for managing group memberships for groups of APP_GROUP type such as Active Directory groups.

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**group_id** | required | Group id | string | `okta group id` |
**user_id** | required | User id | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.group_id | string | `okta group id` | |
action_result.parameter.user_id | string | `okta user id` | |
action_result.data.\*.group_id | string | `okta group id` | |
action_result.data.\*.group_name | string | | |
action_result.data.\*.user_id | string | `okta user id` | |
action_result.data.\*.user_name | string | `user name` `email` | |
action_result.summary.group_id | string | | 00gw7z0fzcJdhfDSb0h7 |
action_result.summary.group_name | string | | test_group |
action_result.summary.user_id | string | | 00u149z08g1Ln68zy0h8 |
action_result.summary.user_name | string | | john.doe@email.com |
action_result.message | string | | |
summary.total_objects | numeric | | |
summary.total_objects_successful | numeric | | 1 |

## action: 'get user groups'

List groups the user is part of

Type: **investigate** <br>
Read only: **True**

#### Action Parameters

PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user_id** | required | User id | string | `okta user id` |

#### Action Output

DATA PATH | TYPE | CONTAINS | EXAMPLE VALUES
--------- | ---- | -------- | --------------
action_result.status | string | | success failed |
action_result.parameter.user_id | string | `okta user id` | Retrived 00u14plts1Ln68zy0h8 groups |
action_result.data.\*.\_links.apps.href | string | | https://test.okta.com/api/v1/groups/00erfdscocsNAbvEyn0h7/apps |
action_result.data.\*.\_links.logo.\*.href | string | | https://op1static.oktacdn.com/assets/img/logos/groups/odyssey/okta-medium.1a5ebrgdfdvb796c235d86b47e3bb.png |
action_result.data.\*.\_links.logo.\*.name | string | | medium |
action_result.data.\*.\_links.logo.\*.type | string | | image/png |
action_result.data.\*.\_links.users.href | string | | https://test.okta.com/api/v1/groups/00gaa8hergfbvEyn0h7/users |
action_result.data.\*.created | string | | 2017-04-26T01:37:27.000Z |
action_result.data.\*.id | string | `okta group id` | 00gaa8rtgdsvAbvEyn0h7 |
action_result.data.\*.lastMembershipUpdated | string | | 2022-04-18T13:26:01.000Z |
action_result.data.\*.lastUpdated | string | | 2017-04-26T01:37:27.000Z |
action_result.data.\*.profile.description | string | | All users in your organization |
action_result.data.\*.profile.name | string | | Everyone |
action_result.data.\*.type | string | | BUILT_IN |
action_result.summary | string | | |
action_result.summary.total_groups | numeric | | |
action_result.message | string | | Total groups: 3 |
summary.total_objects | numeric | | 1 |
summary.total_objects_successful | numeric | | 1 |

______________________________________________________________________

Auto-generated Splunk SOAR Connector documentation.

Copyright 2025 Splunk Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.
