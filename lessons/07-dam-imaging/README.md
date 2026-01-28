# Lesson 07: Asset Management (DAM) & Imaging

In this lesson, you will learn how to properly handle images using Magnolia's Digital Asset Management (DAM) and the `damfn` templating functions.

## 🚀 MVP Exercise (Introduction)

Your goal is to add an image selection field to your Teaser component and render the image.

1.  **Update the Dialog:**
    Open `dialogs/components/teaser.yaml` and add a Link field configured for the DAM.
    ```yaml
        image:
          $type: damLinkField
          targetWorkspace: dam
          appName: assets
          label: Teaser Image
    ```

2.  **Update the Template Script:**
    Open `templates/components/teaser.ftl`. Use `damfn` to retrieve the asset and its link.
    ```html
    [#assign asset = damfn.getAsset(content.image!)! /]
    [#if asset?has_content]
        <img src="${asset.link}" alt="${asset.caption!asset.title!''}" />
    [#else]
        <p>No image</p>
    [/#if]
    ```

3.  **Test it:**
    *   Upload an image to the **Assets** app in Magnolia.
    *   Go to your page, edit the Teaser component.
    *   Select the image you just uploaded.
    *   Save and verify the image appears.

---

## 📖 Explanation (Theory)

### The DAM (Digital Asset Management)
Magnolia stores binary files (images, PDFs, videos) in a dedicated workspace called `dam`. Do not store large binaries directly in the `website` workspace (page properties). Always reference them by ID.

### `LinkFieldDefinition`
This field stores the **UUID** (Unique ID) of the selected item. It does not store the path. This means if you move or rename the image in the Assets app, the link on your page will NOT break.

### `damfn` Templating Functions
*   **`damfn.getAsset(key)`**: Takes the UUID (stored in `content.image`) and returns an Asset object.
*   **`asset.link`**: The public URL to the image.
*   **`asset.caption` / `asset.title`**: Metadata stored with the image.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

Loading a 4K image for a small thumbnail is bad for performance. Let's use **Renditions**.

1.  **Using `damfn.getRendition`:**
    Modify your template to request a specific size.
    ```html
    [#if asset?has_content]
      [#-- Request a rendition named "480" --]
      [#assign rendition = damfn.getRendition(asset, "480")! /]
      
      [#if rendition?has_content]
         <img src="${rendition.link}" alt="${asset.title!''}" />
      [#else]
         [#-- Fallback if rendition doesn't exist --]
         <img src="${asset.link}" alt="${asset.title!''}" />
      [/#if]
    [/#if]
    ```

2.  **Imaging Module Configuration:**
    The rendition named "480" must be defined in the Imaging module configuration.
    *   Navigate to the **Configuration** app -> `modules/imaging/config/generators`.
    *   Standard Magnolia installations come with some default generators.
    *   *Self-Study:* Explore how to define a custom "Smart Crop" generator that focuses on the most important part of the image automatically.

**Next Step:** Your site has structure and content, but it looks unstyled. In the next lesson, we will handle **Web Resources (CSS/JS) & Theming**.
