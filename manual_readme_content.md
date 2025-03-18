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
