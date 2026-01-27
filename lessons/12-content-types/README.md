# Lesson 12: Content Types (Modeling Data)

In this lesson, you will learn how to define **Content Types**. Unlike pages, which are hierarchical, content types are used for structured data like Products, Events, or Speakers, which can be reused across the site.

## 🚀 MVP Exercise (Introduction)

Your goal is to define a `Speaker` content type.

1.  **Create the Content Type Definition:**
    Create a file at `contentTypes/speaker.yaml` in your module.
    ```yaml
    name: Speaker
    datasource:
      workspace: speakers
      autoCreate: true
    model:
      properties:
        firstName:
          type: String
          required: true
        lastName:
          type: String
          required: true
        bio:
          type: String
        photo:
          type: String # Stores the Asset UUID
    ```

2.  **Register the Type:**
    Magnolia automatically picks up this definition. Because we set `autoCreate: true`, it will create a new JCR workspace named `speakers` if it doesn't exist.

3.  **Verify:**
    *   Open the **JCR Browser** app.
    *   Check if you can switch to the `speakers` workspace (it might require a restart if the workspace didn't exist before).
    *   *Note: Without a Content App (next lesson), you can't easily add data yet, but the structure is there.*

---

## 📖 Explanation (Theory)

### Pages vs. Content Types
*   **Pages (`website` workspace):** Hierarchical (Parent/Child), routing-based (URL matches path), visual.
*   **Content Types (Custom workspaces):** Database-like, flat or loose hierarchy, meant to be referenced by pages or exposed via API.

### The `model` section
This defines the schema of your data.
*   **`type`**: The data type (String, Long, Boolean, Date).
*   **`required`**: Validation rules.
*   **`defaultValue`**: Initial value.

### Workspaces
Content Types usually live in their own workspace to keep data clean and separate from the website structure.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### Naming Strategy
By default, when you create a new item, Magnolia names the node `00`, `01`, `02`. This is hard to read in the JCR. Let's make it use the speaker's name.

1.  **Add a Naming Strategy:**
    Update `contentTypes/speaker.yaml`.
    ```yaml
    nodeName:
      property: lastName
    ```
    *Now, if you create a speaker with lastName "Smith", the node will be named "smith".*

### Relationships
Speakers might attend Events.
1.  **Reference another type:**
    In an `Event` content type, you could refer to a speaker.
    ```yaml
    mainSpeaker:
      type: Reference
      targetContentType: my-first-module:speaker
    ```

**Next Step:** A database definition is useless without a User Interface to manage it. In the next lesson, we will build a **Content App** to manage our Speakers.
