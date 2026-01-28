# Lesson 21: Security & Users

In this lesson, you will learn how Magnolia manages access control and how to configure permissions for both editors and public users.

## 🚀 MVP Exercise (Introduction)

Your goal is to create a custom **Role** that only allows access to the "Speakers" app we built in Lesson 13.

1.  **Open the Security App:**
    Go to the App Launcher and open the **Security** app.

2.  **Create a New Role:**
    *   Switch to the **Roles** tab.
    *   Click **Add role** and name it `speaker-editor`.
    *   **Web access:** Add a permission for `GET` and `POST` for `/.rest/delivery/speakers*` (if using APIs).
    *   **App permissions:** Add the `speakers` app to the allowed list.
    *   **ACLs:**
        *   Workspace: `speakers` -> Type: `Read/Write` -> Path: `/` (selected recursively).
        *   Workspace: `website` -> Type: `Read-only` -> Path: `/` (editors usually need to see the site structure).

3.  **Assign the Role to a User:**
    *   Switch to the **Users** tab.
    *   Create a new user `editor-joe`.
    *   In the **Roles** tab for this user, assign the `speaker-editor` role.

4.  **Verify:**
    *   Logout of Magnolia.
    *   Log back in as `editor-joe`.
    *   You should see a very limited App Launcher with only the **Speakers** app (and basic tools) available.

---

## 📖 Explanation (Theory)

### The Security Model: Users, Groups, and Roles
*   **Users:** Individual accounts.
*   **Groups:** Collections of users (e.g., "Marketing Team"). Roles assigned to a group are inherited by all its users.
*   **Roles:** The core of the security system. Roles define *what* can be done.

### Access Control Lists (ACLs)
ACLs define permissions on specific JCR workspaces and paths.
*   **Read-only:** Can see the content but not change it.
*   **Read/Write:** Can create, edit, and delete.
*   **Deny:** Explicitly prevents access (overrides other permissions).

### Web Access
This controls access to URLs (the HTTP layer). Even if a user has JCR access, they might be blocked from visiting a specific AdminCentral URL or a REST endpoint by Web Access rules.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### The `anonymous` User
Magnolia has a special user named `anonymous`. This represents any visitor who is not logged in.
1.  **Public Site Access:** To make your website visible to the world, the `anonymous` user must have a role (usually `rest-anonymous` or `viewer`) with `Read-only` ACLs on the `website` workspace.

### Password Policies
In the `config` workspace under `/server/security/passwordPolicy`, you can configure requirements for password length, complexity, and expiration.

### External Security (LDAP/SSO)
For Enterprise environments, Magnolia can integrate with external identity providers like Active Directory (LDAP), SAML, or OAuth/OIDC. This is configured in the `jaas.config` file and the Magnolia Security filter chain.

**Next Step:** You've built the site and secured it. Now it's time to go live! In the final lesson, we'll look at the **Versioning & Publishing Workflow**.
