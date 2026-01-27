# Lesson 08: Web Resources & Theming

In this lesson, you will learn how to include CSS and JavaScript in your pages using the `resfn` (Resource Functions) and how to organize them into a **Theme**.

## 🚀 MVP Exercise (Introduction)

Your goal is to create a CSS file in your module and link it to your page template.

1.  **Create the CSS File:**
    Create a file at `webresources/css/style.css` in your module.
    ```css
    body {
      font-family: sans-serif;
      background-color: #f4f4f4;
      color: #333;
    }
    .teaser {
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      margin-bottom: 20px;
    }
    .teaser img {
      max-width: 100%;
      height: auto;
    }
    ```

2.  **Link the CSS in the Page Template:**
    Open `templates/pages/hello-world.ftl`. Use the `resfn` to inject the CSS link.
    ```html
    <head>
      <title>Hello World</title>
      [@cms.page /]
      
      [#-- This automatically creates the <link> tag with the correct path --]
      ${resfn.css("/my-first-module/webresources/css/.*css")}
    </head>
    ```

3.  **Test it:**
    *   Refresh your page.
    *   The background should change, and your teaser component should now have a "card" style.
    *   Check the page source; you'll see a link like `/magnoliaAuthor/.resources/my-first-module/webresources/css/style.css`.

---

## 📖 Explanation (Theory)

### The `webresources` Folder
Any file placed in the `webresources` folder of a light module is publicly accessible via the URL pattern `/.resources/<module-name>/webresources/...`. 

### `resfn` Templating Functions
*   **`resfn.css(pattern)`**: Searches for CSS files matching a regex pattern and generates `<link>` tags.
*   **`resfn.js(pattern)`**: Searches for JS files and generates `<script>` tags.
*   **Why regex?** It allows you to include multiple files at once or handle names that change (like during a build process).

### Resource Fingerprinting
By default, Magnolia appends a timestamp or a hash to the resource URL (e.g., `style.css~2023-10-27-10-00-00-000~cache`). This ensures that when you update your CSS, the browser immediately downloads the new version instead of using an old cached copy.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

Using `resfn` directly in templates is okay for small projects, but professional sites use **Themes**.

1.  **Define a Theme:**
    Create a file at `themes/my-theme.yaml`.
    ```yaml
    cssFiles:
      - path: /my-first-module/webresources/css/style.css
        media: all
    jsFiles:
      - path: /my-first-module/webresources/js/main.js
    ```

2.  **Reference the Theme in the Template:**
    Instead of hardcoding paths in the FTL, you can use the theme configured for the site.
    ```html
    [#-- In a real scenario, the theme name is retrieved from the Site Definition --]
    ${resfn.cachedCss(sitefn.theme(content).cssFiles)}
    ```

3.  **Site Definition:**
    The Theme is usually linked to a **Site Definition** (Lesson 11). This allows you to have multiple sites (e.g., "Brand A" and "Brand B") using the same templates but different CSS files just by switching the theme.

**Next Step:** A website is more than one page. In the next lesson, we will build a dynamic **Navigation Menu**.
