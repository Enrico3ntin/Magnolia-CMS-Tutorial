# Lesson 03: Basic Page Template

In this lesson, you will create your first Page Template, allowing you to render a URL to a custom HTML file.

## 🚀 MVP Exercise (Introduction)

Your goal is to create a "Hello World" page template and create a new page in the Pages app using it.

1.  **Create the Definition File:**
    In your module folder (`my-first-module`), create a file at `templates/pages/hello-world.yaml`.
    ```yaml
    title: Hello World Page
    renderType: freemarker
    templateScript: /my-first-module/templates/pages/hello-world.ftl
    ```

2.  **Create the Script File:**
    Create a file at `templates/pages/hello-world.ftl`.
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <title>Hello World</title>
      </head>
      <body>
        <h1>Welcome to Magnolia!</h1>
        <p>This is my first custom page template.</p>
      </body>
    </html>
    ```

3.  **Create a Page:**
    *   Open the **Pages** app in Magnolia AdminCentral.
    *   Click **Add page**.
    *   You should see "Hello World Page" in the list of available templates. Select it.
    *   Name the page `hello` and click Next/Save.
    *   Open the page (Preview or View on website). You should see your HTML!

---

## 📖 Explanation (Theory)

### The Template Definition (`.yaml`)
This file tells Magnolia *what* a template is.
*   **`title`**: The name shown to editors when creating a new page.
*   **`renderType`**: Tells Magnolia which engine to use to render the content. `freemarker` is the standard for Light Development.
*   **`templateScript`**: The path to the actual code that generates the HTML. Note that it starts with the module name.

### The Template Script (`.ftl`)
FreeMarker is a Java-based template engine. For now, we are just using standard HTML, but soon we will inject dynamic content into it.

### The Connection
When you create a page in the Pages app, Magnolia creates a **Node** in the JCR (Java Content Repository) and assigns your template definition to it (property `mgnl:template`). When a user requests that page's URL, Magnolia looks up the node, reads the template definition, and executes the script.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

Let's make the template smarter.

1.  **Dynamic Title:**
    Update your `.ftl` file to display the name of the page as entered by the editor.
    ```html
    <h1>Welcome to ${content.title!}</h1>
    ```
    *   **`content`**: This is a special variable available in all templates. It represents the current page node.
    *   **`.title`**: This is a standard property of the page node.
    *   **`!`**: This tells FreeMarker "if the title is missing, don't crash, just show nothing."

2.  **Verify:**
    Refresh your page. If you named your page "hello", the header might just say "Welcome to". Go back to the Pages app, edit the page properties, and ensure the "Page title" (or name) is set.
    *Note: Standard page properties often require a dialog to edit, which we haven't built yet. For now, `content.@name` will always give you the URL node name.*
    ```html
    <h1>Welcome to page: ${content.@name}</h1>
    ```

**Next Step:** Static HTML is boring. In the next lesson, we will build a **Dialog** so editors can enter custom text without touching the code.
