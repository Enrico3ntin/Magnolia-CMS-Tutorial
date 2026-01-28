# Lesson 20: Virtual URIs

In this lesson, you will learn how to create vanity URLs, redirects, and custom URL mappings using **Virtual URI Mappings**.

## 🚀 MVP Exercise (Introduction)

Your goal is to create a short "Vanity URL" that redirects to a deeper page.

1.  **Create the Mapping Definition:**
    Create a file at `virtualUriMappings/promo.yaml` in your light module.
    ```yaml
    class: info.magnolia.virtualuri.mapping.DefaultVirtualUriMapping
    fromUri: /promo
    toUri: forward:/home/marketing/campaigns/summer-sale
    ```

2.  **Verify:**
    *   Open your browser and go to `http://localhost:8080/magnoliaAuthor/promo`.
    *   Magnolia should automatically show the content of the `/home/marketing/campaigns/summer-sale` page while keeping `/promo` in the address bar (because we used `forward:`).

3.  **Try a Redirect:**
    Change `forward:` to `redirect:`:
    ```yaml
    toUri: redirect:/home/marketing/campaigns/summer-sale
    ```
    *   Now, if you visit `/promo`, the browser URL will actually change to the full path.

---

## 📖 Explanation (Theory)

### What are Virtual URIs?
Virtual URI Mappings allow you to map an incoming request URL to a different internal JCR path or an external URL. This is useful for:
*   **Vanity URLs:** Short, memorable links for marketing (e.g., `/blackfriday`).
*   **Legacy Redirects:** Handling old URLs after a site migration to prevent 404 errors.
*   **Internal Routing:** Mapping custom URL patterns to specific templates.

### `forward:` vs. `redirect:`
*   **Forward:** Internal to Magnolia. The user's browser URL does **not** change. Best for clean URLs.
*   **Redirect:** Sends an HTTP 302 (or 301) to the browser. The URL **does** change. Best for SEO and legacy links.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### Regex Mappings
You can use Regular Expressions to map entire categories of URLs.

1.  **Map all products to a single page:**
    ```yaml
    fromUri: /products/(.*)
    toUri: forward:/home/product-detail?id=$1
    ```
    *   A request to `/products/iphone-15` would be internally handled by the page `/product-detail` with the parameter `id=iphone-15`.

### Permanent Redirects (SEO)
For SEO purposes, you often want a "301 Moved Permanently" instead of a temporary "302".

1.  **Configure a 301 Redirect:**
    ```yaml
    class: info.magnolia.virtualuri.mapping.RegexpVirtualUriMapping
    fromUri: /old-blog/(.*)
    toUri: redirect:/new-blog/$1
    # Note: To force 301, you might need a custom mapping class or 
    # use the 'Regexp' variant with specific status codes.
    ```

### Priority
If multiple mappings match the same URL, Magnolia uses the `DefaultVirtualUriMapping` priority rules (usually based on the length of the `fromUri` or explicit order).

**Next Step:** Your site is now well-structured and easy to navigate. But who has access to change these things? In the next lesson, we'll explore **Security & Users**.
