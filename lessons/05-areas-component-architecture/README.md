# Lesson 05: Areas & Component Architecture

In this lesson, you will learn how to structure your pages using **Areas**. Areas are regions of a page where editors can place components.

## 🚀 MVP Exercise (Introduction)

Your goal is to define a `main` area in your page template and render it.

1.  **Update the Page Template Definition:**
    Open `templates/pages/hello-world.yaml` and add an `areas` section.
    ```yaml
    title: Hello World Page
    renderType: freemarker
    templateScript: /my-first-module/templates/pages/hello-world.ftl
    dialog: my-first-module:pages/hello-world
    areas:
      main:
        renderType: freemarker
        type: list
    ```

2.  **Update the Script:**
    Open `templates/pages/hello-world.ftl` and use the `cmsfn` (CMS Function) to render the area.
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        <title>Hello World</title>
        [@cms.page /] 
      </head>
      <body>
        <h1>${content.greeting!"Hello"}</h1>
        
        <!-- Render the Main Area -->
        <div class="main-area">
            [@cms.area name="main" /]
        </div>

      </body>
    </html>
    ```
    *Note: `[@cms.page /]` in the head is required to load the Page Editor scripts (green bars).*

3.  **Test it:**
    *   Refresh your page in the Page Editor.
    *   You should see a new green bar labeled **main** inside your page.
    *   If you click it, nothing happens yet because we haven't defined any components available for this area.

---

## 📖 Explanation (Theory)

### What is an Area?
An area is a container node in the JCR structure (specifically, a child node of type `mgnl:area`). It serves two purposes:
1.  **Structure:** It groups content together (e.g., "Header", "Main", "Footer").
2.  **Configuration:** It defines *what* can be placed inside it (availability).

### `type: list` vs `type: single`
*   **`list`**: Can contain multiple components. Editors can add, delete, and reorder them. This is the most common type.
*   **`single`**: Can contain only one item. Useful for fixed headers or curated spots.
*   **`noComponent`**: An area that doesn't accept components but is used to group other areas or inherit properties.

### The `cms` Tag Library
The `[@cms.area /]` directive is a FreeMarker macro provided by Magnolia. It handles:
*   Rendering the green edit bars in Author mode.
*   Looping through the child components and rendering them in Public mode.
*   Adding necessary HTML attributes for the Page Editor to work.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

Let's look at inheritance and titles.

1.  **Area Title:**
    Give the area a friendly name for editors.
    ```yaml
    areas:
      main:
        title: Main Content Section
        renderType: freemarker
        type: list
    ```

2.  **Inheritance:**
    You can allow child pages to inherit content from parent pages (useful for headers/footers).
    ```yaml
    areas:
      footer:
        renderType: freemarker
        type: list
        inheritance:
          components: all
    ```
    *If you add a component to the footer on the home page, it will appear on all subpages unless overwritten.*

**Next Step:** An empty area is lonely. In the next lesson, we will build our first reusable **Component** to fill this area.
