# Lesson 14: Delivery API (Headless JSON)

In this lesson, you will learn how to expose your structured data (like the Speakers created in the previous lessons) as a JSON REST API for use in external applications.

## 🚀 MVP Exercise (Introduction)

Your goal is to configure a Delivery Endpoint to fetch Speakers via JSON.

1.  **Create the REST Endpoint Definition:**
    Create a file at `restEndpoints/delivery/speakers_v1.yaml` in your light module.
    ```yaml
    class: info.magnolia.rest.delivery.jcr.v2.JcrDeliveryEndpointDefinition
    workspace: speakers
    rootPath: /
    defaultLevel: 2
    ```

2.  **Verify the API:**
    Magnolia automatically registers this endpoint. You can test it using `curl` or your browser:
    ```bash
    curl "http://localhost:8080/magnoliaAuthor/.rest/delivery/speakers_v1/"
    ```
    *Note: By default, you might need to be logged in or configure anonymous access to see the results.*

3.  **Check the Output:**
    You should see a JSON response containing the list of speakers you added in the previous lesson.

---

## 📖 Explanation (Theory)

### What is the Delivery API?
The Delivery API is a high-level REST API provided by Magnolia to deliver JCR content as JSON. It handles:
*   **JSON Serialization:** Converting JCR nodes and properties to JSON objects.
*   **Reference Resolution:** Automatically fetching referenced assets or other nodes.
*   **Filtering & Sorting:** Querying content through URL parameters.

### Endpoint Configuration
*   **`workspace`**: The JCR workspace to read from (e.g., `website`, `dam`, `speakers`).
*   **`rootPath`**: Limits the API to a specific branch of the JCR tree.
*   **`defaultLevel`**: Controls how many levels of child nodes or references are automatically expanded.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### Filtering and Querying
The Delivery API is powerful because it allows front-end developers to filter data directly in the URL without changing backend code.

1.  **Filter by property:**
    Try fetching only speakers with a specific last name:
    `.../.rest/delivery/speakers_v1/?lastName=Smith`

2.  **Sorting:**
    Sort speakers alphabetically by first name:
    `.../.rest/delivery/speakers_v1/?orderBy=firstName%20asc`

### Security (Anonymous Access)
By default, REST endpoints are protected. In a production headless scenario, you often want the public to see this data.
1.  **The `rest-anonymous` role:**
    In the **Security** app, find the `rest-anonymous` role.
    *   Add a **Web access** permission: `GET` for `/.rest/delivery/speakers_v1/*`.
    *   Add **ACL** (Access Control List) permissions: `Read-only` for the `speakers` workspace.

### Swagger Documentation
Magnolia includes a built-in Swagger UI to explore and test your APIs.
*   Open: [http://localhost:8080/magnoliaAuthor/.rest/swagger-ui/](http://localhost:8080/magnoliaAuthor/.rest/swagger-ui/)
*   You can see your `speakers_v1` endpoint listed there and try out different parameters.

**Next Step:** Now that we can serve content via JSON, how do we make a modern frontend (like React or Vue) editable inside Magnolia? In the next lesson, we'll look at **Visual SPA Editing**.
