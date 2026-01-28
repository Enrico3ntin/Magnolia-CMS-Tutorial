# Lesson 13: Content Apps

In this lesson, you will create a User Interface (UI) that allows editors to create, read, update, and delete (CRUD) the `Speaker` data you defined in Lesson 12.

## 🚀 MVP Exercise (Introduction)

Your goal is to generate a basic Content App for the `Speaker` content type.

1.  **Create the App Definition:**
    Create a file at `apps/speakers.yaml` in your light module.
    ```yaml
    label: Speakers
    datasource:
      $type: jcrDatasource
      workspace: speakers
    subApps:
      browser:
        $type: contentBrowserSubApp
        workbench:
          contentViews:
            list:
              $type: listView
              columns:
                lastName:
                  $type: propertyColumnDefinition
                  name: lastName
                  label: Last Name
                firstName:
                  $type: propertyColumnDefinition
                  name: firstName
                  label: First Name
    ```

2.  **Verify in Magnolia:**
    *   Refresh the Magnolia App Launcher.
    *   You should now see a **Speakers** app icon.
    *   Open it. You can see the list (currently empty), but you still can't add items because we haven't defined the **Detail sub-app** (the form).

---

## 📖 Explanation (Theory)

### What is a Content App?
A Content App is a Magnolia tool that provides a UI for interacting with data. Most apps consist of two main parts:
1.  **Browser Sub-app:** The "view" where you browse items (List, Thumbnail, or Tree views).
2.  **Detail Sub-app:** The "editor" where you add or modify a single item (the form).

### The Workbench
The `workbench` defines how data is displayed in the Browser sub-app. You can define multiple `contentViews` (like a list for data and a thumbnail view for images).

### Datasource
The `datasource` tells the app where to look for data. Since we are using Content Types, we point it to the `speakers` JCR workspace.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

To make the app fully functional, we need to add the ability to add and edit speakers.

1.  **Add the Detail Sub-app:**
    Update `apps/speakers.yaml` to include the `detail` sub-app and actions.
    ```yaml
    # ... (previous code)
    subApps:
      browser:
        # ... (previous browser code)
        actions:
          addSpeaker:
            $type: openDetailSubAppActionDefinition
            subAppId: detail
            appName: speakers
            creation: true
          editSpeaker:
            $type: openDetailSubAppActionDefinition
            subAppId: detail
            appName: speakers

      detail:
        $type: contentDetailSubApp
        form:
          properties:
            lastName:
              $type: textFieldDefinition
              label: Last Name
            firstName:
              $type: textFieldDefinition
              label: First Name
            bio:
              $type: textFieldDefinition
              label: Biography
              rows: 5
        actions:
          commit:
            $type: commitActionDefinition
            label: Save
          cancel:
            $type: cancelActionDefinition
            label: Cancel
    ```

2.  **Add the Action Bar:**
    In the `browser` section, you need to define an `actionbar` so the "Add" and "Edit" buttons actually appear in the UI.

    ```yaml
    # Inside browser:
    actionbar:
      sections:
        main:
          groups:
            speakerActions:
              items:
                - addSpeaker
                - editSpeaker
    ```

**Next Step:** Now that we can manage our data through a nice UI, we need to make it accessible to the outside world. In the next lesson, we will explore the **Delivery API** to expose our speakers as JSON.
