[comment]: # "Auto-generated SOAR connector documentation"
# Okta

Publisher: Splunk  
Connector Version: 2\.2\.1  
Product Vendor: Okta  
Product Name: Okta  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 5\.0\.0  

This app supports various identity management actions on Okta

[comment]: # " File: readme.md"
[comment]: # "  Copyright (c) 2018-2022 Splunk Inc."
[comment]: # ""
[comment]: # "  Licensed under the Apache License, Version 2.0 (the 'License');"
[comment]: # "  you may not use this file except in compliance with the License."
[comment]: # "  You may obtain a copy of the License at"
[comment]: # ""
[comment]: # "      http://www.apache.org/licenses/LICENSE-2.0"
[comment]: # ""
[comment]: # "  Unless required by applicable law or agreed to in writing, software distributed under"
[comment]: # "  the License is distributed on an 'AS IS' BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,"
[comment]: # "  either express or implied. See the License for the specific language governing permissions"
[comment]: # "  and limitations under the License."
[comment]: # ""
## Pagination

The pagination mechanism has been implemented for the investigative actions mentioned below.

-   list users
-   list user groups
-   list providers
-   list roles

The pagination mechanism has been explained below.

-   Limit Parameter: This input parameter is used to limit the total number of items (a valid
    positive integer) to be fetched in action results.

**Examples**  
Total items in the end system for reference in the below examples are 950 and internally, every page
fetched will have 200 result items. Based on the value of the limit and other parameters combined,
the required items from every page will be fetched and added to the action results output. The
'after' field (for navigating to next pages) used in API calls is handled internally by the
pagination mechanism.

-   **Example 1:** Limit = 50

      

    -   This will fetch the first 50 items

      

-   **Example 2:** Limit = 200

      

    -   This will fetch the first 200 items

      

-   **Example 3:** Limit = 240

      

    -   This will fetch all 200 items from the first page and 40 items from the second page. Hence,
        in total, it will fetch 240 items.

      

-   **Example 4:** Limit = 1000

      

    -   This will fetch all 950 items

      

-   **Example 6:** Limit = None

      

    Here the None is considered as empty parameter value

    -   This will fetch all 950 items

## Port Information

The app uses HTTP/ HTTPS protocol for communicating with the Okta server. Below are the default
ports used by Splunk SOAR.

|         Service Name | Transport Protocol | Port |
|----------------------|--------------------|------|
|         http         | tcp                | 80   |
|         https        | tcp                | 443  |

## Permissions

Super admins can assign admin permissions to individuals or groups.  
**Individual** assignments are better for a manageable number of admin accounts. When you assign
admin permissions to individuals, you do so one at a time, whenever necessary. Remember that every
organisation must always have at least one individual assigned super admin.  
**Admin groups** work better when you need to onboard a large number of admins quickly. Assign those
admins to one group, and then grant admin permissions to that group. Okta groups, AD groups, and
LDAP groups are all eligible.  
  
To assign the roles to any user, it is required to run the **"assign role"** action using the asset
configured with the API token of a **Super admin user(SUPER_ADMIN)** in the OKTA server to assign
appropriate permissions to that normal user.  
  
Step to assign a Super admin role to user or group.  

-   1\. In the Admin Console, go to **Security \> Administrators** .
-   2\. Click **Add Administrator** , depending on whether you are assigning privileges to an
    individual or group.
-   3\. In the **Grant administrator role to** field, begin typing the name of the user that we want
    to assign admin privileges to and select the correct user from the search list.
-   4\. Select the **Super Administrator** roles you want the user or group to have. You can assign
    multiple admin roles to an individual or group.
-   5\. Some admin roles require additional input. If you selected Application Administrator, Group
    Administrator, Help Desk Administrator, Group Membership Administrator, you need to indicate
    whether that role administers all users, groups, apps, just specific ones. (Copy and Paste
    commands allow you to apply the same assignments to multiple roles).
-   6\. Click Add Administrator to complete the assignment.

  

The following tables show the Details of the roles and what they can perform.

| Role type                   | Label                               | Detail                                                                                                                                                               |
|-----------------------------|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SUPER_ADMIN                 | Super Administrator                 | Perform all admin activities for an organisation. Super admins have full management access.                                                                          |
| ORG_ADMIN                   | Organization Administrator          | Perform most admin activities for an organisation. Note: Organisation admins cannot manage applications, authorization servers, hooks, Okta Mobile, or other admins. |
| APP_ADMIN                   | Application Administrator           | View and manage user permissions in an application. Note: You can specify one or more applications after selecting this role.                                        |
| USER_ADMIN                  | Group Administrator                 | Manage users, their profiles, and their credentials. Note: You can specify one or more groups after selecting this role.                                             |
| HELP_DESK_ADMIN             | Help Desk Administrator             | View and unlock users, reset passwords and reset MFA. Note: You can specify one or more groups after selecting this role.                                            |
| GROUP_MEMBERSHIP_ADMIN      | Group Membership Administrator      | Manages the membership of groups. Note: You can specify one or more groups after selecting this role.                                                                |
| READ_ONLY_ADMIN             | Read Only Administrator             | View most data in the Admin Console.                                                                                                                                 |
| API_ACCESS_MANAGEMENT_ADMIN | API Access Management Administrator | Build custom authorization servers to protect your API endpoints.                                                                                                    |
| REPORT_ADMIN                | Report Administrator                | View all reports and the System log.                                                                                                                                 |
| MOBILE_ADMIN                | Mobile Administrator                | Perform actions related to mobile policies, sign-on policies, mobile devices, and Okta Mobile.                                                                       |


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Okta asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**api\_key** |  required  | password | API token
**base\_url** |  required  | string | Your organization's url\. Example\: https\://your\-org\.okta\.com
**verify\_server\_cert** |  optional  | boolean | Verify server certificate

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[send push notification](#action-send-push-notification) - Validate the user prompt with push notification  
[list users](#action-list-users) - Get the list of users  
[list user groups](#action-list-user-groups) - Get the groups that the user is a member of  
[add group](#action-add-group) - Add a group  
[reset password](#action-reset-password) - Generate a one\-time token that can be used to reset the user's password  
[set password](#action-set-password) - Set the password of a user without validating existing credentials  
[disable user](#action-disable-user) - Disables the specified user  
[clear user sessions](#action-clear-user-sessions) - Clears the specified user's sessions  
[enable user](#action-enable-user) - Enables the specified user  
[get user](#action-get-user) - Get information about a user  
[get group](#action-get-group) - Get information about a group  
[list providers](#action-list-providers) - List identity providers \(IdPs\) in your organization  
[list roles](#action-list-roles) - Lists all roles assigned to a user  
[assign role](#action-assign-role) - Assign a role to a user  
[unassign role](#action-unassign-role) - Unassign a role to a user  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'send push notification'
Validate the user prompt with push notification

Type: **contain**  
Read only: **False**

The action has not yet been implemented for the "sms" and the "token\:software\:totp" factortypes\.<br>Currently, the action would generate a new OTP for the "sms" factortype and will not verify it\.<br>The action would fail for the "token\:software\:totp" factortype as it has not yet been implemented\.<br>One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>USER\_ADMIN</li><li>HELP\_DESK\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**email** |  required  | Okta User id, email address, or username | string |  `okta user id`  `okta email address`  `okta username` 
**factortype** |  required  | Okta Factor Type | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.email | string |  `okta user id`  `okta email address`  `okta username` 
action\_result\.parameter\.factortype | string | 
action\_result\.data\.\*\.factorResult | string | 
action\_result\.data\.\*\.id | string | 
action\_result\.data\.\*\.\_links\.self\.href | string | 
action\_result\.data\.\*\.\_links\.user\.href | string | 
action\_result\.data\.\*\.\_links\.resend\.\*\.href | string | 
action\_result\.data\.\*\.\_links\.resend\.\*\.name | string | 
action\_result\.data\.\*\.\_links\.activate\.href | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.profile\.phoneNumber | string | 
action\_result\.data\.\*\.provider | string | 
action\_result\.data\.\*\.factorType | string | 
action\_result\.data\.\*\.vendorName | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.\_links\.verify\.href | string | 
action\_result\.data\.\*\.profile\.keys\.\*\.e | string | 
action\_result\.data\.\*\.profile\.keys\.\*\.n | string | 
action\_result\.data\.\*\.profile\.keys\.\*\.kid | string | 
action\_result\.data\.\*\.profile\.keys\.\*\.kty | string | 
action\_result\.data\.\*\.profile\.keys\.\*\.use | string | 
action\_result\.data\.\*\.profile\.name | string | 
action\_result\.data\.\*\.profile\.version | string | 
action\_result\.data\.\*\.profile\.platform | string | 
action\_result\.data\.\*\.profile\.deviceType | string | 
action\_result\.data\.\*\.profile\.credentialId | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.result\.factorResult | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list users'
Get the list of users

Type: **investigate**  
Read only: **True**

Limit parameter is used to provide total number of users to be fetched\. Please provide a valid positive integer value for limit\. Use the <strong>query</strong> parameter for a simple lookup of users by name, for example when creating a people picker\. The value of <strong>query</strong> is matched against <strong>firstName</strong>, <strong>lastName</strong>, or <strong>email</strong>\. <br />Use the <strong>filter</strong> parameter to filter on the following properties\:<ul><li>status</li><li>lastUpdated</li><li>id</li><li>profile\.login</li><li>profile\.email</li><li>profile\.firstName</li><li>profile\.lastName</li></ul><p>Use the <strong>search</strong> parameter to do a case\-insensitive search on the following properties\:</p><ul><li>id</li><li>status</li><li>created</li><li>activated</li><li>statusChanged</li><li>lastUpdated</li></ul><p>Filter and search operators\:</p><ul><li>eq\: equal</li><li>sw\: starts with</li><li>pr\: present \(has value\)</li><li>gt\: greater than</li><li>ge\: greater than or equal</li><li>lt\: less than</li><li>le\: less than or equal</li></ul><p>Filter and search examples\:</p><ul><li>status eq "STAGED"</li><li>lastUpdated lt "yyyy\-MM\-dd'T'HH\:mm\:ss\.SSSZ"</li><li>lastUpdated gt "yyyy\-MM\-dd'T'HH\:mm\:ss\.SSSZ"</li></ul><br>One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>APP\_ADMIN</li><li>USER\_ADMIN</li><li>HELP\_DESK\_ADMIN</li><li>GROUP\_MEMBERSHIP\_ADMIN</li><li>READ\_ONLY\_ADMIN</li><li>API\_ACCESS\_MANAGEMENT\_ADMIN</li><li>REPORT\_ADMIN</li><li>MOBILE\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**query** |  optional  | Find a user that matches firstName, lastName, and email properties | string | 
**filter** |  optional  | Filters users with a supported expression for a subset of properties | string | 
**search** |  optional  | Searches for users with a supported filtering expression for most properties | string | 
**limit** |  optional  | Specifies the number of results returned | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.filter | string | 
action\_result\.parameter\.limit | numeric | 
action\_result\.parameter\.query | string | 
action\_result\.parameter\.search | string | 
action\_result\.data\.\*\.\_links\.self\.href | string |  `url` 
action\_result\.data\.\*\.activated | string | 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.status | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.type | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.value | string |  `email` 
action\_result\.data\.\*\.credentials\.provider\.name | string | 
action\_result\.data\.\*\.credentials\.provider\.type | string | 
action\_result\.data\.\*\.credentials\.recovery\_question\.question | string | 
action\_result\.data\.\*\.id | string |  `okta user id` 
action\_result\.data\.\*\.lastLogin | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.passwordChanged | string | 
action\_result\.data\.\*\.profile\.city | string | 
action\_result\.data\.\*\.profile\.department | string | 
action\_result\.data\.\*\.profile\.displayName | string | 
action\_result\.data\.\*\.profile\.email | string |  `email` 
action\_result\.data\.\*\.profile\.firstName | string | 
action\_result\.data\.\*\.profile\.lastName | string | 
action\_result\.data\.\*\.profile\.login | string |  `email` 
action\_result\.data\.\*\.profile\.middleName | string | 
action\_result\.data\.\*\.profile\.mobilePhone | string | 
action\_result\.data\.\*\.profile\.nickName | string | 
action\_result\.data\.\*\.profile\.secondEmail | string |  `email` 
action\_result\.data\.\*\.profile\.streetAddress | string | 
action\_result\.data\.\*\.profile\.title | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.statusChanged | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.status | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.type | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.value | string |  `email` 
action\_result\.data\.\*\.type\.id | string | 
action\_result\.data\.\*\.profile\.primaryPhone | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.num\_users | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list user groups'
Get the groups that the user is a member of

Type: **investigate**  
Read only: **True**

Limit parameter is used to provide total number of user groups to be fetched\. Please provide a valid positive integer value for limit\. Use the <strong>query</strong> parameter for a simple lookup of groups by name, for example when creating a people picker\. The value of <strong>query</strong> is matched against <strong>name</strong>\. <br />Use the <strong>filter</strong> parameter to filter on the following properties\:<ul><li>type</li><li>lastMembershipUpdated</li><li>id</li><li>lastUpdated</li></ul><br>One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>APP\_ADMIN</li><li>USER\_ADMIN</li><li>HELP\_DESK\_ADMIN</li><li>GROUP\_MEMBERSHIP\_ADMIN</li><li>READ\_ONLY\_ADMIN</li><li>API\_ACCESS\_MANAGEMENT\_ADMIN</li><li>MOBILE\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**query** |  optional  | Find a group that matches name property | string | 
**filter** |  optional  | Filters groups with a supported expression for a subset of properties | string | 
**limit** |  optional  | Specifies the number of results returned | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.filter | string | 
action\_result\.parameter\.limit | numeric | 
action\_result\.parameter\.query | string | 
action\_result\.data\.\*\.\_links\.apps\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.logo\.\*\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.logo\.\*\.name | string | 
action\_result\.data\.\*\.\_links\.logo\.\*\.type | string | 
action\_result\.data\.\*\.\_links\.users\.href | string |  `url` 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.id | string |  `okta group id` 
action\_result\.data\.\*\.lastMembershipUpdated | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.objectClass | string | 
action\_result\.data\.\*\.profile\.description | string | 
action\_result\.data\.\*\.profile\.name | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.\_links\.source\.href | string | 
action\_result\.data\.\*\.source\.id | string | 
action\_result\.data\.\*\.profile\.dn | string | 
action\_result\.data\.\*\.profile\.groupType | string | 
action\_result\.data\.\*\.profile\.objectSid | string | 
action\_result\.data\.\*\.profile\.externalId | string | 
action\_result\.data\.\*\.profile\.groupScope | string | 
action\_result\.data\.\*\.profile\.samAccountName | string | 
action\_result\.data\.\*\.profile\.windowsDomainQualifiedName | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.num\_groups | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'add group'
Add a group

Type: **generic**  
Read only: **False**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**name** |  required  | Name of the group | string | 
**description** |  required  | Description of the group | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.description | string | 
action\_result\.parameter\.name | string | 
action\_result\.data\.\*\.\_links\.apps\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.logo\.\*\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.logo\.\*\.name | string | 
action\_result\.data\.\*\.\_links\.logo\.\*\.type | string | 
action\_result\.data\.\*\.\_links\.users\.href | string |  `url` 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.id | string |  `okta group id` 
action\_result\.data\.\*\.lastMembershipUpdated | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.objectClass | string | 
action\_result\.data\.\*\.profile\.description | string | 
action\_result\.data\.\*\.profile\.name | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.group\_id | string |  `okta group id` 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'reset password'
Generate a one\-time token that can be used to reset the user's password

Type: **correct**  
Read only: **False**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>USER\_ADMIN</li><li>HELP\_DESK\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user\_id** |  required  | User id | string |  `okta user id` 
**receive\_type** |  required  | Return one\-time token via email or in UI | string | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.receive\_type | string | 
action\_result\.parameter\.user\_id | string |  `okta user id` 
action\_result\.data\.\*\.resetPasswordUrl | string |  `url` 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'set password'
Set the password of a user without validating existing credentials

Type: **contain**  
Read only: **False**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>USER\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**new\_password** |  required  | Password string to set | string | 
**id** |  required  | ID of user | string |  `okta user id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `okta user id` 
action\_result\.parameter\.new\_password | string | 
action\_result\.data\.\*\.\_links\.changePassword\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.changePassword\.method | string | 
action\_result\.data\.\*\.\_links\.changeRecoveryQuestion\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.changeRecoveryQuestion\.method | string | 
action\_result\.data\.\*\.\_links\.deactivate\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.deactivate\.method | string | 
action\_result\.data\.\*\.\_links\.expirePassword\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.expirePassword\.method | string | 
action\_result\.data\.\*\.\_links\.forgotPassword\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.forgotPassword\.method | string | 
action\_result\.data\.\*\.\_links\.resetPassword\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.resetPassword\.method | string | 
action\_result\.data\.\*\.\_links\.self\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.suspend\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.suspend\.method | string | 
action\_result\.data\.\*\.\_links\.unsuspend\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.unsuspend\.method | string | 
action\_result\.data\.\*\.activated | string | 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.status | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.type | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.value | string |  `email` 
action\_result\.data\.\*\.credentials\.provider\.name | string | 
action\_result\.data\.\*\.credentials\.provider\.type | string | 
action\_result\.data\.\*\.credentials\.recovery\_question\.question | string | 
action\_result\.data\.\*\.id | string |  `okta user id` 
action\_result\.data\.\*\.lastLogin | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.passwordChanged | string | 
action\_result\.data\.\*\.profile\.city | string | 
action\_result\.data\.\*\.profile\.department | string | 
action\_result\.data\.\*\.profile\.displayName | string | 
action\_result\.data\.\*\.profile\.email | string |  `email` 
action\_result\.data\.\*\.profile\.firstName | string | 
action\_result\.data\.\*\.profile\.lastName | string | 
action\_result\.data\.\*\.profile\.login | string |  `email` 
action\_result\.data\.\*\.profile\.middleName | string | 
action\_result\.data\.\*\.profile\.mobilePhone | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.status | string | 
action\_result\.data\.\*\.profile\.nickName | string | 
action\_result\.data\.\*\.profile\.secondEmail | string |  `email` 
action\_result\.data\.\*\.credentials\.emails\.\*\.value | string |  `email` 
action\_result\.data\.\*\.profile\.streetAddress | string | 
action\_result\.data\.\*\.profile\.title | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.statusChanged | string | 
action\_result\.data\.\*\.\_links\.unsuspend\.href | numeric |  `url` 
action\_result\.data\.\*\.type\.id | string | 
action\_result\.data\.\*\.\_links\.type\.href | string | 
action\_result\.data\.\*\.\_links\.schema\.href | string | 
action\_result\.data\.\*\.\_links\.activate\.href | string | 
action\_result\.data\.\*\.\_links\.activate\.method | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'disable user'
Disables the specified user

Type: **contain**  
Read only: **False**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>USER\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | ID of user to disable | string |  `okta user id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `okta user id` 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'clear user sessions'
Clears the specified user's sessions

Type: **contain**  
Read only: **False**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>USER\_ADMIN</li>clear user sessions</ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | ID of user to clear sessions for | string |  `okta user id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `okta user id` 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'enable user'
Enables the specified user

Type: **correct**  
Read only: **False**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>USER\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**id** |  required  | ID of user to enable | string |  `okta user id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.id | string |  `okta user id` 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get user'
Get information about a user

Type: **investigate**  
Read only: **True**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>APP\_ADMIN</li><li>USER\_ADMIN</li><li>HELP\_DESK\_ADMIN</li><li>GROUP\_MEMBERSHIP\_ADMIN</li><li>READ\_ONLY\_ADMIN</li><li>API\_ACCESS\_MANAGEMENT\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user\_id** |  required  | User ID | string |  `okta user id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.user\_id | string |  `okta user id` 
action\_result\.data\.\*\.\_links\.activate\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.activate\.method | string | 
action\_result\.data\.\*\.\_links\.changePassword\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.changePassword\.method | string | 
action\_result\.data\.\*\.\_links\.changeRecoveryQuestion\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.changeRecoveryQuestion\.method | string | 
action\_result\.data\.\*\.\_links\.deactivate\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.deactivate\.method | string | 
action\_result\.data\.\*\.\_links\.expirePassword\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.expirePassword\.method | string | 
action\_result\.data\.\*\.\_links\.forgotPassword\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.forgotPassword\.method | string | 
action\_result\.data\.\*\.\_links\.reactivate\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.reactivate\.method | string | 
action\_result\.data\.\*\.\_links\.resetPassword\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.resetPassword\.method | string | 
action\_result\.data\.\*\.\_links\.self\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.suspend\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.suspend\.method | string | 
action\_result\.data\.\*\.activated | string | 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.status | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.type | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.value | string |  `email` 
action\_result\.data\.\*\.credentials\.provider\.name | string | 
action\_result\.data\.\*\.credentials\.provider\.type | string | 
action\_result\.data\.\*\.credentials\.recovery\_question\.question | string | 
action\_result\.data\.\*\.id | string |  `okta user id` 
action\_result\.data\.\*\.lastLogin | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.passwordChanged | string | 
action\_result\.data\.\*\.profile\.city | string | 
action\_result\.data\.\*\.profile\.department | string | 
action\_result\.data\.\*\.profile\.displayName | string | 
action\_result\.data\.\*\.profile\.email | string |  `email` 
action\_result\.data\.\*\.profile\.firstName | string | 
action\_result\.data\.\*\.profile\.lastName | string | 
action\_result\.data\.\*\.profile\.login | string |  `email` 
action\_result\.data\.\*\.profile\.middleName | string | 
action\_result\.data\.\*\.profile\.mobilePhone | string | 
action\_result\.data\.\*\.profile\.nickName | string | 
action\_result\.data\.\*\.profile\.secondEmail | string |  `email` 
action\_result\.data\.\*\.profile\.streetAddress | string | 
action\_result\.data\.\*\.profile\.title | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.statusChanged | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.status | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.type | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.value | string |  `email` 
action\_result\.data\.\*\.\_links\.reactivate\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.reactivate\.method | string | 
action\_result\.data\.\*\.\_links\.activate\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.activate\.method | string | 
action\_result\.data\.\*\.type\.id | string | 
action\_result\.data\.\*\.\_links\.type\.href | string | 
action\_result\.data\.\*\.\_links\.schema\.href | string | 
action\_result\.data\.\*\.\_links\.resetFactors\.href | string | 
action\_result\.data\.\*\.\_links\.resetFactors\.method | string | 
action\_result\.data\.\*\.\_links\.unsuspend\.href | string | 
action\_result\.data\.\*\.\_links\.unsuspend\.method | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'get group'
Get information about a group

Type: **investigate**  
Read only: **True**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>APP\_ADMIN</li><li>USER\_ADMIN</li><li>HELP\_DESK\_ADMIN</li><li>GROUP\_MEMBERSHIP\_ADMIN</li><li>READ\_ONLY\_ADMIN</li><li>API\_ACCESS\_MANAGEMENT\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**group\_id** |  required  | Group id | string |  `okta group id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.group\_id | string |  `okta group id` 
action\_result\.data\.\*\.\_links\.apps\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.logo\.\*\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.logo\.\*\.name | string | 
action\_result\.data\.\*\.\_links\.logo\.\*\.type | string | 
action\_result\.data\.\*\.\_links\.users\.href | string |  `url` 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.id | string |  `okta group id` 
action\_result\.data\.\*\.lastMembershipUpdated | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.objectClass | string | 
action\_result\.data\.\*\.profile\.description | string | 
action\_result\.data\.\*\.profile\.name | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.\_links\.source\.href | string | 
action\_result\.data\.\*\.source\.id | string | 
action\_result\.data\.\*\.profile\.dn | string | 
action\_result\.data\.\*\.profile\.groupType | string | 
action\_result\.data\.\*\.profile\.objectSid | string | 
action\_result\.data\.\*\.profile\.externalId | string | 
action\_result\.data\.\*\.profile\.groupScope | string | 
action\_result\.data\.\*\.profile\.samAccountName | string | 
action\_result\.data\.\*\.profile\.windowsDomainQualifiedName | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list providers'
List identity providers \(IdPs\) in your organization

Type: **investigate**  
Read only: **True**

Limit parameter is used to provide total number of identity providers to be fetched from your organization\. Please provide a valid positive integer value for limit\. Use the <strong>query</strong> parameter for a simple lookup of idps by name, for example when creating a people picker\. The value of <strong>query</strong> is matched against <strong>name</strong>\.<br>One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li><li>ORG\_ADMIN</li><li>READ\_ONLY\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**query** |  optional  | Find the identity providers that matches name property | string | 
**type** |  optional  | Filter IdPs by type | string | 
**limit** |  optional  | Specifies the number of results returned | numeric | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.limit | numeric | 
action\_result\.parameter\.query | string | 
action\_result\.parameter\.type | string | 
action\_result\.data\.\*\.\_links\.authorize\.hints\.allow | string | 
action\_result\.data\.\*\.\_links\.authorize\.href | string |  `url` 
action\_result\.data\.\*\.\_links\.authorize\.templated | boolean | 
action\_result\.data\.\*\.\_links\.clientRedirectUri\.hints\.allow | string | 
action\_result\.data\.\*\.\_links\.clientRedirectUri\.href | string |  `url` 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.id | string |  `okta idps id` 
action\_result\.data\.\*\.issuerMode | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.name | string | 
action\_result\.data\.\*\.policy\.accountLink\.action | string | 
action\_result\.data\.\*\.policy\.accountLink\.filter | string | 
action\_result\.data\.\*\.policy\.maxClockSkew | numeric | 
action\_result\.data\.\*\.policy\.provisioning\.action | string | 
action\_result\.data\.\*\.policy\.provisioning\.conditions\.deprovisioned\.action | string | 
action\_result\.data\.\*\.policy\.provisioning\.conditions\.suspended\.action | string | 
action\_result\.data\.\*\.policy\.provisioning\.groups\.action | string | 
action\_result\.data\.\*\.policy\.provisioning\.profileMaster | boolean | 
action\_result\.data\.\*\.policy\.subject\.filter | string | 
action\_result\.data\.\*\.policy\.subject\.matchAttribute | string | 
action\_result\.data\.\*\.policy\.subject\.matchType | string | 
action\_result\.data\.\*\.policy\.subject\.userNameTemplate\.template | string | 
action\_result\.data\.\*\.protocol\.credentials\.client\.client\_id | string | 
action\_result\.data\.\*\.protocol\.credentials\.client\.client\_secret | string | 
action\_result\.data\.\*\.protocol\.endpoints\.authorization\.binding | string | 
action\_result\.data\.\*\.protocol\.endpoints\.authorization\.url | string |  `url` 
action\_result\.data\.\*\.protocol\.endpoints\.token\.binding | string | 
action\_result\.data\.\*\.protocol\.endpoints\.token\.url | string |  `url` 
action\_result\.data\.\*\.protocol\.scopes | string |  `url` 
action\_result\.data\.\*\.protocol\.type | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.num\_idps | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list roles'
Lists all roles assigned to a user

Type: **investigate**  
Read only: **True**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user\_id** |  required  | User ID | string |  `okta user id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.user\_id | string |  `okta user id` 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.id | string |  `okta role id` 
action\_result\.data\.\*\.label | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.\_links\.assignee\.href | string | 
action\_result\.data\.\*\.assignmentType | string | 
action\_result\.data\.\*\.type\.id | string | 
action\_result\.data\.\*\.\_links\.self\.href | string | 
action\_result\.data\.\*\.profile\.email | string | 
action\_result\.data\.\*\.profile\.login | string | 
action\_result\.data\.\*\.profile\.lastName | string | 
action\_result\.data\.\*\.profile\.firstName | string | 
action\_result\.data\.\*\.profile\.mobilePhone | string | 
action\_result\.data\.\*\.profile\.secondEmail | string | 
action\_result\.data\.\*\.activated | string | 
action\_result\.data\.\*\.lastLogin | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.type | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.value | string | 
action\_result\.data\.\*\.credentials\.emails\.\*\.status | string | 
action\_result\.data\.\*\.credentials\.provider\.name | string | 
action\_result\.data\.\*\.credentials\.provider\.type | string | 
action\_result\.data\.\*\.statusChanged | string | 
action\_result\.data\.\*\.passwordChanged | string | 
action\_result\.data\.\*\.profile\.city | string | 
action\_result\.data\.\*\.profile\.title | string | 
action\_result\.data\.\*\.profile\.nickName | string | 
action\_result\.data\.\*\.profile\.department | string | 
action\_result\.data\.\*\.profile\.middleName | string | 
action\_result\.data\.\*\.profile\.displayName | string | 
action\_result\.data\.\*\.profile\.streetAddress | string | 
action\_result\.data\.\*\.credentials\.recovery\_question\.question | string | 
action\_result\.data\.\*\.profile\.primaryPhone | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
action\_result\.summary\.num\_roles | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'assign role'
Assign a role to a user

Type: **generic**  
Read only: **False**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**type** |  required  | Type of role | string | 
**user\_id** |  required  | User ID | string |  `okta user id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.type | string | 
action\_result\.parameter\.user\_id | string |  `okta user id` 
action\_result\.data\.\*\.created | string | 
action\_result\.data\.\*\.id | string |  `okta role id` 
action\_result\.data\.\*\.label | string | 
action\_result\.data\.\*\.lastUpdated | string | 
action\_result\.data\.\*\.status | string | 
action\_result\.data\.\*\.type | string | 
action\_result\.data\.\*\.\_links\.assignee\.href | string | 
action\_result\.data\.\*\.assignmentType | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'unassign role'
Unassign a role to a user

Type: **generic**  
Read only: **False**

One of the following roles is required to run this action\:<ul><li>SUPER\_ADMIN</li></ul>

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**user\_id** |  required  | User ID | string |  `okta user id` 
**role\_id** |  required  | ID of rule | string |  `okta role id` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.role\_id | string |  `okta role id` 
action\_result\.parameter\.user\_id | string |  `okta user id` 
action\_result\.data | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 