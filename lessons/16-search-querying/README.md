# Lesson 16: Search & Querying

In this lesson, you will learn how to implement a search feature that allows users to find content across your website and custom content types.

## 🚀 MVP Exercise (Introduction)

Your goal is to create a simple search results component using the `searchfn` templating function.

1.  **Create the Search Component Definition:**
    Create `templates/components/search-results.yaml`:
    ```yaml
    title: Search Results
    dialog: my-first-module:components/search-results
    ```

2.  **Create the Template Script:**
    Create `templates/components/search-results.ftl`:
    ```html
    [#-- Get the query from the URL parameter 'q' --]
    [#assign query = ctx.getParameter('q')! /]

    <h2>Search Results for: "${query}"</h2>

    [#if query?has_content]
      [#-- Search the 'website' workspace --]
      [#assign results = searchfn.searchPages(query, '/manual') /]
      
      <ul>
        [#list results as item]
          <li>
            <a href="${cmsfn.link(item)}">${item.title!item.@name}</a>
          </li>
        [#else]
          <li>No results found.</li>
        [#list]
      </ul>
    [/#if]
    ```

3.  **Verify:**
    *   Add the component to a page.
    *   Navigate to that page in your browser and append `?q=hello` to the URL.
    *   The component should list pages containing the word "hello".

---

## 📖 Explanation (Theory)

### How Search Works in Magnolia
Magnolia uses **Apache Jackrabbit (JCR)**, which provides built-in indexing for all content. When you save a page or a content type, it is automatically indexed and becomes searchable.

### Templating Functions
*   **`searchfn`**: A simplified helper for common search tasks (like searching pages).
*   **`cmsfn`**: Used here to generate the links to the results.

### Query Languages
While `searchfn` is great for simple text search, Magnolia supports:
*   **JCR-SQL2**: A SQL-like language for complex queries (filtering by specific properties, dates, or node types).
*   **XPath**: An older but still supported query language.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### Searching Multiple Workspaces
Sometimes you want to search both Pages (`website`) and Speakers (`speakers`).

1.  **Using JCR-SQL2:**
    You can use the `query` service to run advanced searches.
    ```freemarker
    [#assign statement = "SELECT * FROM [mgnl:content] WHERE CONTAINS(*, '${query}')" /]
    [#assign results = cmsfn.search('speakers', statement, 'JCR-SQL2') /]
    ```

2.  **Filtering Results:**
    You can refine your search to only return specific templates or exclude certain paths (like a "hidden" folder).

3.  **Pagination:**
    For sites with many results, you shouldn't render everything at once. Use the `offset` and `limit` parameters in your query to implement pagination.
    ```freemarker
    [#-- Example of a paged query --]
    [#assign results = searchfn.searchPages(query, '/', 10, 0) /] [#-- Limit 10, Offset 0 --]
    ```

**Next Step:** Search is great for finding content, but what if your audience speaks different languages? In the next lesson, we'll dive into **Internationalization (i18n)**.
