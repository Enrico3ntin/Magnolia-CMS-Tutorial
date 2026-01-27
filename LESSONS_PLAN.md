# Magnolia CMS Training Course - Lesson Plan

This curriculum is designed to be modular and progressive. Each lesson adheres to the **MVP -> Explanation -> Deep Dive** structure.

## Phase 1: Foundations & Light Development 🏗️

### Lesson 01: Environment Setup & Hello World
*   **Goal:** Get Magnolia running and understand the ecosystem.
*   **MVP:** Install Magnolia CLI, download a community bundle, start the server, and log in.
*   **Deep Dive:** Understanding the folder structure, the `light-modules` folder, and key configuration files (`magnolia.properties`).

### Lesson 02: Anatomy of a Light Module
*   **Goal:** Understand the packaging unit of Magnolia development.
*   **MVP:** Create a new light module using `mgnl create-light-module` and check its structure.
*   **Deep Dive:** Module definitions (`module.yaml`), dependencies, and resource loading order.

### Lesson 03: Basic Page Template
*   **Goal:** Render a URL to a custom HTML file.
*   **MVP:** Create a basic Page definition (YAML) and a corresponding FreeMarker (`.ftl`) script.
*   **Deep Dive:** Template definitions, render types, and the relationship between the JCR node and the template.

### Lesson 04: Dialogs & User Input
*   **Goal:** Allow editors to change content.
*   **MVP:** Create a dialog definition with a text field and bind it to the Page template.
*   **Deep Dive:** Field types (RichText, Link, Date), validation, default values, and the `dialog` registry.

## Phase 2: Building Blocks of Sites 🧱

### Lesson 05: Areas & Component Architecture
*   **Goal:** Define editable regions and structures.
*   **MVP:** Add a `main` area to your page template and loop through it.
*   **Deep Dive:** Area inheritance, optional vs. required areas, and `mgnl:area` vs standard nodes.

### Lesson 06: Components & Availability
*   **Goal:** Create reusable content blocks.
*   **MVP:** Create a simple component (definition + dialog + script) and make it available in the Page's area.
*   **Deep Dive:** Component groups, autogeneration, and using `availability` rules to control where components can be placed.

### Lesson 07: Asset Management (DAM) & Imaging
*   **Goal:** professionally handle images and downloads.
*   **MVP:** Add an image field to a component and render it using the `damfn` templating function.
*   **Deep Dive:** Image variations (renditions), focal points, and the Imaging API (smart cropping/resizing).

### Lesson 08: Web Resources & Theming
*   **Goal:** Style the website consistently.
*   **MVP:** Create a CSS file in the light module and link it using `resfn`.
*   **Deep Dive:** Resource fingerprinting (cache busting), Magnolia Themes (YAML), and CSS preprocessors.

### Lesson 09: Navigation & Menus
*   **Goal:** Build dynamic site navigation.
*   **MVP:** Render a dynamic header menu listing all top-level pages using `navfn`.
*   **Deep Dive:** Recursive navigation (sub-menus), checking `hideInNav` properties, and active state handling.

## Phase 3: Dynamic Logic & Data 🧠

### Lesson 10: Javascript Models (Business Logic)
*   **Goal:** Separate logic from presentation (MVC pattern).
*   **MVP:** Create a JavaScript model file that processes data (e.g., formats a date or calculates a value) before the template renders it.
*   **Deep Dive:** The `model` class definition, accessing JCR nodes in JS, and exposure to the template context.

### Lesson 11: Site Definitions & Multi-site
*   **Goal:** Configure site-wide settings and domain mappings.
*   **MVP:** Create a Site definition (YAML) mapping your templates and theme.
*   **Deep Dive:** Prototypes, site variations, and configuring multiple sites with different domains.

### Lesson 12: Content Types (Modeling Data)
*   **Goal:** Define structured data outside of pages.
*   **MVP:** Define a `Speaker` content type (YAML) with properties like name, bio, and photo.
*   **Deep Dive:** Relationships (References between types), JCR node types, and naming strategies.

### Lesson 13: Content Apps
*   **Goal:** Create a UI for editors to manage structured data.
*   **MVP:** Generate a standard app to manage `Speakers` using the CLI.
*   **Deep Dive:** Customizing the Workbench (columns, icons), defining Browser vs. Detail sub-apps, and configuring Actions.

## Phase 4: Headless & Modern Frontend 🚀

### Lesson 14: Delivery API (Headless JSON)
*   **Goal:** Expose content via JSON for external apps.
*   **MVP:** Configure a REST endpoint for the `Speaker` content type.
*   **Deep Dive:** Endpoint filters, references resolution, depth control, and Swagger documentation.

### Lesson 15: Visual SPA Editing
*   **Goal:** Make a React/Angular app editable inside Magnolia.
*   **MVP:** Configure a Page Template to wrap an SPA framework.
*   **Deep Dive:** The `magnolia-react-editor` (or similar) libraries, page editor annotations for frontend frameworks.

## Phase 5: Advanced & Enterprise Features 🛡️

### Lesson 16: Search & Querying
*   **Goal:** Implement site search.
*   **MVP:** Create a search component that queries the `website` workspace using `searchfn` or SQL2.
*   **Deep Dive:** Filtering results, paging, and searching across multiple workspaces (e.g., Pages + Content Types).

### Lesson 17: Internationalization (i18n)
*   **Goal:** Build a multi-language site.
*   **MVP:** Configure a second language in the Site definition and translate a page.
*   **Deep Dive:** Translatable content apps, `i18n` basenames, and language detection strategies.

### Lesson 18: Personalization (Traits)
*   **Goal:** Serve different content to different users.
*   **MVP:** Create a variant of a component that only shows for users from a specific country (GeoIP simulation).
*   **Deep Dive:** Traits, audiences, and previewing personas in the Page Editor.

## Phase 6: Architecture & DevOps 🏗️

### Lesson 19: Decorators
*   **Goal:** Modify existing functionality without changing original files.
*   **MVP:** Use a decorator to hide a specific field in a standard Magnolia component dialog.
*   **Deep Dive:** Decorating definitions vs. decorating classes, and regex matching for decorators.

### Lesson 20: Virtual URIs
*   **Goal:** Create vanity URLs and redirects.
*   **MVP:** Map a short URL `/promo` to a specific internal campaign page.
*   **Deep Dive:** Regex mapping, forward vs. permanent redirect, and URI mappings chains.

### Lesson 21: Security & Users
*   **Goal:** Manage access control.
*   **MVP:** Create a custom Role with specific permissions for the `Speakers` app.
*   **Deep Dive:** ACLs (Access Control Lists), user groups, and realm security.

### Lesson 22: Versioning & Publishing Workflow
*   **Goal:** Understand the publication lifecycle.
*   **MVP:** Publish a page and restore a previous version.
*   **Deep Dive:** The concept of public vs. author instances, recursive publication, and workflow commands.