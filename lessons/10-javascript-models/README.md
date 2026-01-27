# Lesson 10: Javascript Models (Business Logic)

In this lesson, you will learn how to separate logic from presentation using **JavaScript Models**. This allows you to keep your FreeMarker templates clean and handle complex data processing in JavaScript.

## 🚀 MVP Exercise (Introduction)

Your goal is to create a component that displays a "Last Updated" message, where the date is formatted by a JavaScript model.

1.  **Create the JS Model File:**
    Create a file at `templates/components/info-model.js` in your module.
    ```javascript
    var InfoModel = function() {
        this.getFormattedDate = function() {
            var lastModified = content['mgnl:lastModified'];
            if (lastModified) {
                // simple JS formatting
                return "Last updated on: " + lastModified.format("yyyy-MM-dd");
            }
            return "Not yet modified";
        };
        
        this.getMessage = function() {
            return "Hello from the JS Model!";
        };
    };

    new InfoModel();
    ```

2.  **Create the Component Definition:**
    Create `templates/components/info.yaml`. Note the `modelClass` property pointing to the JS file.
    ```yaml
    title: Info Component
    renderType: freemarker
    templateScript: /my-first-module/templates/components/info.ftl
    modelClass: /my-first-module/templates/components/info-model.js
    ```

3.  **Create the Component Script:**
    Create `templates/components/info.ftl`. You can access the model via the `model` variable.
    ```html
    <div class="info-box">
        <p>${model.message}</p>
        <p><em>${model.formattedDate}</em></p>
    </div>
    ```

4.  **Test it:**
    *   Add this component to your page's `availableComponents` (in `hello-world.yaml`).
    *   Add it to a page.
    *   You should see the message and the date rendered correctly!

---

## 📖 Explanation (Theory)

### Why use Models?
FreeMarker is a *templating* language, not a *programming* language. Putting complex loops, math, or date formatting in FTL makes it hard to read and maintain.
By using a Model:
*   **FTL (View):** Only handles HTML structure and simple variable printing.
*   **JS/Java (Controller/Model):** Handles data fetching, formatting, and business rules.

### How it works
When Magnolia renders a component with a `modelClass`:
1.  It instantiates the JavaScript class (or Java class).
2.  It makes the instance available in the FTL context as the variable `model`.
3.  Any public function in your JS class (starting with `get...`) can be accessed in FTL as a property (e.g., `getFormattedDate()` becomes `model.formattedDate`).

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### Accessing Context
Inside the JS model, several global objects are automatically available:
*   **`content`**: The JCR node of the current component.
*   **`damfn`**, **`cmsfn`**, **`navfn`**: All the helper functions we used in FTL are also available in JS.

### Passing Parameters
You can pass data from the template back to the model if needed, but usually, the model pulls what it needs from the `content` object.

### Exercise: A "Reading Time" Calculator
1.  Create a "Blog" component with a large text area.
2.  In the JS model, get the text from `content.body`.
3.  Count the words and divide by 200 (average reading speed).
4.  Return a string like "5 min read" to the FTL.

**Next Step:** Now that we can handle complex logic, let's look at how to organize multiple sites and global configurations using **Site Definitions**.
