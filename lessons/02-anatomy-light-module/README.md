# Lesson 02: Anatomy of a Light Module

In this lesson, you will learn about the fundamental packaging unit of Magnolia development: the **Light Module**.

## 🚀 MVP Exercise (Introduction)

Your goal is to create your first custom module and see it recognized by Magnolia.

1.  **Navigate to your project root** (where the `light-modules` folder is located or configured).
2.  **Create the module:**
    Use the CLI to generate the folder structure.
    ```bash
    cd light-modules
    mgnl create-light-module my-first-module
    ```
3.  **Verify the structure:**
    You should see a folder `my-first-module` created with some subdirectories.
    ```text
    my-first-module/
    ├── decorations/
    ├── dialogs/
    ├── i18n/
    ├── templates/
    ├── webresources/
    └── module.yaml
    ```
4.  **Check Magnolia:**
    Check your running Magnolia instance console logs or the **Resource Files** app in AdminCentral. You should see a message indicating that the new module has been detected and registered.

---

## 📖 Explanation (Theory)

### What is a Light Module?
A Light Module is simply a folder on your filesystem that contains configuration, templates, and static resources. Magnolia "watches" these folders. When you add or change a file, Magnolia updates immediately—no Java compilation or server restart required.

### The Standard Directory Structure
*   **`templates/`**: Holds your Page, Component, and Area definitions (YAML) and their rendering scripts (FreeMarker `.ftl`).
*   **`dialogs/`**: Defines the forms editors use to enter content.
*   **`webresources/`**: Static assets like CSS, JavaScript, and fonts. These are served directly by Magnolia.
*   **`decorations/`**: Used to modify definitions from *other* modules without touching their original code.
*   **`i18n/`**: Translation files (properties files) for your module's UI.
*   **`module.yaml`**: The descriptor file for your module.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

Let's look closer at `module.yaml`. This file is crucial for dependency management and versioning.

1.  **Open `my-first-module/module.yaml`:**
    It looks something like this:
    ```yaml
    name: my-first-module
    version: 1.0.0
    dependencies:
      magnolia-rendering:
        version: 5.4/*
    ```

2.  **Dependencies:**
    The `dependencies` section tells Magnolia that your module relies on other modules.
    *   **Exercise:** Add a dependency to `magnolia-dam-app`.
        ```yaml
        dependencies:
          magnolia-dam-app:
             version: 2.0/*
        ```
    *   *Why?* If you try to start Magnolia and the `dam-app` is missing, Magnolia will warn you or refuse to start, preventing broken features.

3.  **Resource Loading:**
    Magnolia loads resources from two places:
    *   **Classpath:** Java modules (JAR files) inside `WEB-INF/lib`.
    *   **Filesystem:** Your `light-modules` folder.
    
    *Filesystem resources (Light Modules) usually override Classpath resources if they have the exact same path. This is powerful but requires care!*

**Next Step:** Now that we have a module, let's put something inside it. In the next lesson, we will build a **Basic Page Template**.
