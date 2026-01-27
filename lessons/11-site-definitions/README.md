# Lesson 11: Site Definitions & Multi-site

In this lesson, you will learn how to configure a **Site Definition**. This is the central configuration file that links your templates, themes, and domains together, and enables Magnolia's multi-site capabilities.

## 🚀 MVP Exercise (Introduction)

Your goal is to create a formal definition for your site and assign your theme to it.

1.  **Create the Site Definition:**
    Create a file at `site/my-site.yaml` in your module (or `sites/my-site.yaml` depending on configuration, but `site/` is standard for light modules representing a single site).
    ```yaml
    name: My First Site
    theme:
      name: my-theme
    templates:
      availability:
        templates:
          homepage:
            id: my-first-module:pages/hello-world
    mappings:
      website:
        handlePrefix: /my-site
        uris:
          - /
    ```

2.  **Verify the Theme:**
    Ensure you have `themes/my-theme.yaml` from Lesson 08. The `name` in the site definition must match the filename of the theme (minus `.yaml`) or the name defined inside it.

3.  **Update the Page Template (Optional but Recommended):**
    Instead of hardcoding the CSS link in your template, use the `sitefn`:
    ```html
    ${resfn.cachedCss(sitefn.theme(content).cssFiles)}
    ```

4.  **Test it:**
    *   Open the **Site Definitions** app (if available) or check the log to see your site is registered.
    *   This specific configuration tells Magnolia that pages under `/my-site` belong to "My First Site" and should use "my-theme".

---

## 📖 Explanation (Theory)

### The Role of a Site Definition
A Site Definition answers:
*   **What theme** should be used? (CSS/JS)
*   **Which templates** are available? (preventing editors from using a "Press Release" template on a "Product" site).
*   **What domains** point here? (e.g., `example.com` -> `/my-site`, `example.org` -> `/charity-site`).
*   **Localization:** What languages are available?

### Prototype vs. Variation
*   **Prototype:** You can define a "master" site definition that others inherit from.
*   **Variation:** You can have variations of a site (e.g., "Mobile", "Tablet") though this is less common with modern responsive design.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### Multi-Language Setup (i18n)
Let's prepare our site for multiple languages.

1.  **Add Locales:**
    Update your `site/my-site.yaml`:
    ```yaml
    i18n:
      fallbackLocale: en
      locales:
        en:
          enabled: true
          country: US
          language: en
        de:
          enabled: true
          country: DE
          language: de
    ```

2.  **What happens?**
    *   In the Pages app, if you edit a page under this site, you will see a language switcher (EN | DE).
    *   You can enter different content for each language.
    *   The URL will adapt (e.g., `/de/my-page`).

**Next Step:** We have pages and sites. Now we need to handle structured data that *isn't* a page (like products, speakers, or events). In the next lesson, we will look at **Content Types**.
