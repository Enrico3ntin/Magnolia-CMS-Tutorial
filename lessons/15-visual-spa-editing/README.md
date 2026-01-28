# Lesson 15: Visual SPA Editing

In this lesson, you will learn how to bridge the gap between a modern Single Page Application (SPA) and Magnolia's visual Page Editor.

## 🚀 MVP Exercise (Introduction)

Your goal is to configure a Page Template that points to a frontend application.

1.  **Create a "Headless" Page Template:**
    Create a file at `templates/pages/spa-home.yaml` in your light module.
    ```yaml
    title: SPA Home Page
    renderType: spa
    baseUrl: http://localhost:3000
    dialog: my-first-module:pages/spa-home
    ```

2.  **Define the Template Script (Proxy):**
    Unlike standard templates that use FreeMarker, an SPA template often just acts as a container or proxies to the dev server.
    Create `templates/pages/spa-home.ftl`:
    ```html
    <!DOCTYPE html>
    <html>
      <head>
        [@cms.page /]
      </head>
      <body>
        <div id="root"></div>
        <script src="http://localhost:3000/static/js/bundle.js"></script>
      </body>
    </html>
    ```

3.  **Verify:**
    *   Create a new page in the **Pages** app using the "SPA Home Page" template.
    *   If you have a React/Vue app running on port 3000, Magnolia will attempt to render it inside the iframe of the Page Editor.

---

## 📖 Explanation (Theory)

### What is Visual SPA Editing?
Normally, headless CMSs only provide a form-based UI. Magnolia's Visual SPA editing allows frontend developers to use their preferred framework (React, Angular, Vue) while still giving editors an "On-Page" editing experience (drag-and-drop, click-to-edit).

### How it works:
1.  **Template Definition:** You tell Magnolia that the `renderType` is `spa`.
2.  **Magnolia Frontend Helper Libraries:** Libraries like `@magnolia/react-editor` are used in the frontend code to interpret the "annotations" Magnolia sends.
3.  **The Template Annotation:** The `[@cms.page /]` tag (and others) injects HTML comments that the frontend library uses to identify where areas and components should be rendered.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### The Component Mapping
In a headless scenario, Magnolia doesn't render the HTML for a component; the frontend does.

1.  **Mapping in the Frontend (React Example):**
    In your React application, you would map Magnolia component names to React components:
    ```javascript
    const config = {
      componentMappings: {
        'my-first-module:components/text-image': TextImageComponent,
        'my-first-module:components/hero': HeroComponent
      }
    };
    ```

2.  **Handling Areas:**
    You use the `<EditableArea />` component from the Magnolia helper library. It communicates with the Page Editor to allow editors to drop new components into that specific part of your React app.

### Why use `baseUrl`?
In development, your SPA is usually running on a different port (e.g., 3000) than Magnolia (8080). The `baseUrl` property tells the Page Editor where to fetch the frontend assets from during the editing session.

**Next Step:** We've covered how to display and edit content. But what if the site has thousands of pages? In the next lesson, we will implement **Search & Querying**.
