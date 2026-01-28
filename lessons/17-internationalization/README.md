# Lesson 17: Internationalization (i18n)

In this lesson, you will learn how to configure Magnolia to support multiple languages and how to provide translations for your site's content and UI.

## 🚀 MVP Exercise (Introduction)

Your goal is to enable a second language (e.g., German) for your site.

1.  **Update the Site Definition:**
    If you have a site definition (Lesson 11), add the `locales` configuration. If not, you can create a simple one at `site-definitions/my-site.yaml`:
    ```yaml
    i18n:
      defaultLocale: en
      locales:
        en:
          enabled: true
        de:
          enabled: true
    ```

2.  **Translate a Page:**
    *   Open the **Pages** app.
    *   In the status bar at the bottom, you should now see a language switcher (EN / DE).
    *   Switch to **DE**.
    *   Edit a component and enter some German text.
    *   Save and publish.

3.  **Verify via URL:**
    *   View your page at `http://localhost:8080/magnoliaAuthor/your-page.html` (English).
    *   View your page at `http://localhost:8080/magnoliaAuthor/de/your-page.html` (German).

---

## 📖 Explanation (Theory)

### How i18n Works in Magnolia
Magnolia stores translations in the JCR by appending the locale to the property name (e.g., `title`, `title_de`). This allows a single node to hold content for all languages.

### Two Types of i18n:
1.  **Content i18n:** Translating the actual content editors enter (like the body text of a page). This is handled automatically by Magnolia when multiple locales are defined.
2.  **UI/System i18n:** Translating the labels of dialogs, buttons, and static text in templates. This uses **Message Bundles** (property files).

### The Locale Resolver
Magnolia determines the current language based on the URL (e.g., the `/de/` prefix). This is handled by the `LocaleResolver`.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### UI Translations (Message Bundles)
You don't want to hardcode "Read More" in your FreeMarker template.

1.  **Create a Message Bundle:**
    Create `i18n/messages.properties` in your module:
    ```properties
    search.button=Search
    read.more=Read more...
    ```
    Create `i18n/messages_de.properties`:
    ```properties
    search.button=Suche
    read.more=Mehr erfahren...
    ```

2.  **Use it in FreeMarker:**
    Use the `i18n` templating function:
    ```html
    <button>${i18n['search.button']}</button>
    ```

3.  **Translate Dialog Labels:**
    You can use these same keys in your YAML dialog definitions:
    ```yaml
    label: i18n:read.more
    ```

### Fallback Mechanism
If a translation is missing for German (`title_de`), Magnolia will automatically fall back to the `defaultLocale` (English).

**Next Step:** Multi-language is great for reaching a wider audience. But what if you want to show different content to different users even in the same language? Next up: **Personalization**.
