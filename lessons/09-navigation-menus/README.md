# Lesson 09: Navigation & Menus

In this lesson, you will learn how to create a dynamic navigation menu that automatically lists the pages of your site using the `navfn` (Navigation Function).

## 🚀 MVP Exercise (Introduction)

Your goal is to add a navigation bar to your page template that links to all top-level pages.

1.  **Update the Page Template:**
    Open `templates/pages/hello-world.ftl`. Add this logic, usually inside a `<header>` or `<nav>` tag.

    ```html
    [#-- Get the root node of the current site --]
    [#assign root = navfn.rootPage(content)! /]
    
    [#if root?has_content]
    <nav>
      <ul>
        [#-- Loop through the children of the root page --]
        [#list navfn.navItems(root) as navItem]
          <li>
            <a href="${navfn.link(navItem)!}">${navItem.title!navItem.@name}</a>
          </li>
        [/#list]
      </ul>
    </nav>
    [/#if]
    ```

2.  **Create More Pages:**
    *   Go to the Pages app.
    *   Create a few sibling pages at the top level (e.g., "About", "Services", "Contact").
    *   Use your "Hello World" template for all of them.

3.  **Test it:**
    *   Open any of the pages.
    *   You should see a list of links to all the top-level pages.
    *   Clicking them should navigate correctly.

---

## 📖 Explanation (Theory)

### `navfn` (Navigation Functions)
This is a helper library specifically for menus.
*   **`navfn.rootPage(node)`**: Finds the home page (root) for the given page. It's smart enough to stop at the site root even in multi-site setups.
*   **`navfn.navItems(node)`**: Returns a list of child pages *that are meant to be in the navigation*. It automatically filters out:
    *   Nodes that are not pages (e.g., folders).
    *   Pages that have the property `hideInNav` set to true.
*   **`navfn.link(node)`**: Generates the correct URL for the page.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

A real menu needs to show which page is active and handle nested levels.

1.  **Active State:**
    Check if the `navItem` is the current page (or an ancestor of the current page).
    ```html
    [#assign active = navfn.isActive(content, navItem) /]
    <li class="${active?string('active', '')}">
    ```

2.  **"Hide in Nav" Toggle:**
    Standard Magnolia page properties usually have a checkbox named `hideInNav`. If your custom page properties dialog doesn't have it, you can add it:
    ```yaml
    - name: hideInNav
      class: info.magnolia.ui.form.field.definition.CheckboxFieldDefinition
      label: Hide in Navigation
    ```
    *If you check this box for a page, `navfn.navItems` will automatically skip it.*

3.  **Recursive Navigation (Submenus):**
    You can nest the loop to show children of the top-level pages.
    ```html
    [#list navfn.navItems(root) as navItem]
      <li>
        <a href="${navfn.link(navItem)!}">${navItem.title!}</a>
        [#-- Submenu --]
        [#assign subItems = navfn.navItems(navItem) /]
        [#if subItems?has_content]
           <ul>
             [#list subItems as subItem]
               <li><a href="${navfn.link(subItem)!}">${subItem.title!}</a></li>
             [/#list]
           </ul>
        [/#if]
      </li>
    [/#list]
    ```

**Next Step:** We have completed Phase 2! We have a structured site with pages, components, styles, and navigation. In Phase 3, we will separate logic from presentation using **JavaScript Models**.
