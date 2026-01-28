# Lesson 19: Decorators

In this lesson, you will learn how to use **Decorators** to modify existing functionality or configurations in Magnolia without editing the original source files. This is essential for customizing standard modules or third-party additions safely.

## 🚀 MVP Exercise (Introduction)

Your goal is to "decorate" a standard Magnolia dialog to hide a field you don't need.

1.  **Identify the Target:**
    Let's say you want to modify the standard `textImage` component dialog from a module called `standard-templating-kit` to remove the "Link" field.

2.  **Create the Decorator File:**
    In your light module, create a folder named `decorations`.
    Create a file at `decorations/standard-templating-kit/dialogs/components/textImage.yaml`:
    ```yaml
    actions:
      # We want to remove the 'link' property from the form
      link: !deleted
    ```
    *Note: The folder structure inside `decorations` must match the module and path you are targeting.*

3.  **Verify:**
    *   Open the **Pages** app.
    *   Edit a `textImage` component.
    *   Check the dialog—the "Link" field should now be gone.

---

## 📖 Explanation (Theory)

### What are Decorators?
Decorators are a "non-invasive" way to change configuration. Instead of copying a file and changing it (which makes updates difficult), you define a small YAML file that describes only the *changes* you want to apply.

### How it works:
When Magnolia loads a configuration (like a dialog or a template), it first looks for any decorators that target that specific path. It then merges the decorator's properties into the original definition.

### Types of Decorators:
*   **YAML Decorators:** Best for Light Development. You can add, modify, or delete properties using the `!deleted` or `!override` tags.
*   **Java Decorators:** Used for more complex logic (e.g., dynamically changing a field based on the current user's role).

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### Decorating Templates
You can also decorate template definitions to add new areas or change the available components.

1.  **Add a new area to a standard page:**
    `decorations/standard-templating-kit/templates/pages/main.yaml`:
    ```yaml
    areas:
      sidebar:
        renderType: freemarker
        templateScript: /my-module/templates/areas/sidebar.ftl
    ```

### Regex Matching
Sometimes you want to decorate many things at once.
*   You can use filenames like `.*.yaml` in your decorations folder to apply a change to every dialog in a module.

### Why use Decorators?
*   **Maintainability:** Your changes are isolated in your own module.
*   **Upgradeability:** When you update Magnolia, the original files are replaced, but your decorators are re-applied on top of the new versions.

**Next Step:** Now that we can tweak the system, let's look at how to manage the URLs that point to it. In the next lesson, we will cover **Virtual URIs**.
