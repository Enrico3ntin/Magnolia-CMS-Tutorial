# Lesson 04: Dialogs & User Input

In this lesson, you will learn how to create input forms (Dialogs) so that editors can manage the content of your pages.

## 🚀 MVP Exercise (Introduction)

Your goal is to add a text field to your "Hello World" page so an editor can change the greeting message.

1.  **Create the Dialog Definition:**
    Create a file at `dialogs/pages/hello-world.yaml`.
    ```yaml
    form:
      properties:
        title:
          $type: textField
          label: Title
        greeting:
          $type: textField
          label: Greeting
    footerLayout:
      $type: defaultEditorActionLayout
      primaryActions:
        commit: commit
    ```

2.  **Bind the Dialog to the Template:**
    Open `templates/pages/hello-world.yaml` and add the `dialog` property.
    ```yaml
    title: Hello World Page
    renderType: freemarker
    templateScript: /my-first-module/templates/pages/hello-world.ftl
    dialog: my-first-module:pages/hello-world
    ```

3.  **Update the Script:**
    Edit `templates/pages/hello-world.ftl` to use the new content.
    ```html
    <h1>${content.greeting!"Hello (default)"}</h1>
    ```

4.  **Test it:**
    *   Go to the Pages app.
    *   Select your `hello` page.
    *   Click **Edit**. The green edit bar should appear.
    *   Click **Page properties** (top right) or the Edit icon.
    *   Enter "Hola Mundo" in the text field and save.
    *   The page should update immediately!

---

## 📖 Explanation (Theory)

### The Dialog Registry
Magnolia loads all dialog definitions from the `dialogs` folders of all modules. The ID of a dialog is constructed as `<module-name>:<path/to/dialog>`.
*   In our case: `my-first-module:pages/hello-world` (the `.yaml` extension is dropped).

### Form Structure
*   **`form`**: The root element.
*   **`tabs`**: Dialogs are organized into tabs. Even if you have only one, you must define it.
*   **`fields`**: The actual inputs.
*   **`class`**: The Java class that defines the field's behavior. The `TextFieldDefinition` is the most basic one. *Note: In newer Magnolia versions (6.2+), you can often use `className` or short-hand aliases, but full class names are the most compatible.*

### Content Storage
When you save the dialog, Magnolia takes the value of the field `greeting` and saves it as a property named `greeting` on the JCR node of the page. That is why `${content.greeting}` works in the template.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

Let's explore more field types and validation.

1.  **Rich Text Field:**
    Add a field for a longer description.
    ```yaml
            - name: description
              class: info.magnolia.ui.form.field.definition.RichTextFieldDefinition
              label: Description
    ```

2.  **Validation (Required Field):**
    Make the greeting mandatory.
    ```yaml
            - name: greeting
              class: info.magnolia.ui.form.field.definition.TextFieldDefinition
              label: Greeting Message
              required: true
              validationMessage: "You must say hello!"
    ```

3.  **Render the Rich Text:**
    Update your `.ftl`. Note that Rich Text stores HTML, so you need to tell FreeMarker not to escape it using `?no_esc`.
    ```html
    <div>
      ${content.description!""?no_esc}
    </div>
    ```

**Next Step:** You can now create pages with fixed structures. But what if you want to let editors choose which content to add? In the next lesson, we will introduce **Areas & Component Architecture**.
