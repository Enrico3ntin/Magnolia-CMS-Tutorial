# Lesson 01: Environment Setup & Hello World

In this lesson, you will set up your Magnolia development environment and start a local instance.

## 🚀 MVP Exercise (Introduction)

Your goal is to get a Magnolia instance running on your machine.

1.  **Install the Magnolia CLI:**
    Magnolia provides a command-line tool to speed up development.
    ```bash
    npm install -g @magnolia/cli
    ```
2.  **Create a project directory:**
    ```bash
    mkdir magnolia-cms && cd magnolia-cms
    ```
3.  **Download and jumpstart Magnolia:**
    This command downloads a pre-configured Tomcat bundle with Magnolia installed.
    ```bash
    mgnl jumpstart
    ```
    *Choose the `magnolia-community-demo-webapp` when prompted (or the latest stable community version).*

4.  **Start the server:**
    ```bash
    mgnl start
    ```
5.  **Log in:**
    Once the console says "Server startup in ... ms", open your browser at:
    [http://localhost:8080/magnoliaAuthor](http://localhost:8080/magnoliaAuthor)
    *   **Username:** `superuser`
    *   **Password:** `superuser`

---

## 📖 Explanation (Theory)

### What is the Magnolia CLI?
The CLI (`mgnl`) is a Node.js-based tool that automates repetitive tasks like creating modules, templates, and dialogs. It also handles the "jumpstart" process, which downloads the Magnolia webapp and a bundled Tomcat server.

### The Architecture
*   **Author Instance:** Where editors create and manage content (usually port 8080).
*   **Public Instance:** Where the end-users see the content (usually port 8080/magnoliaPublic).
*   **JCR (Java Content Repository):** The database where Magnolia stores everything (content, configuration, users).

### Light Development
Magnolia "Light Development" allows you to build sites using only YAML, HTML (FreeMarker), and JavaScript, without needing to compile Java code or restart the server for most changes.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

Now that you have it running, let's look at the "hidden" configuration.

1.  **The `light-modules` folder:**
    Look for a folder named `light-modules` in your project root. This is where all your custom code will live. Magnolia watches this folder and picks up changes instantly.
2.  **`magnolia.properties`:**
    Navigate to `apache-tomcat/webapps/magnoliaAuthor/WEB-INF/config/default/magnolia.properties`.
    *   **Task:** Find the property `magnolia.resources.dir`. This points to your `light-modules` folder.
3.  **The JCR Browser:**
    In the Magnolia App Launcher (the grid of icons), find and open the **JCR Browser** app.
    *   Explore the `website` workspace. This is where page content is stored.
    *   Explore the `config` workspace. This is where Magnolia's own configuration (modules, templates, etc.) is defined.

**Next Step:** Once you are comfortable navigating the AdminCentral UI, we will move to creating our first Light Module!
