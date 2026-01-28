# Lesson 18: Personalization (Traits)

In this lesson, you will learn how to deliver tailored content to different audience segments using Magnolia's Personalization features.

## 🚀 MVP Exercise (Introduction)

Your goal is to create a component variant that only appears for a specific "Persona."

1.  **Enable Personalization:**
    Personalization is usually enabled by default in Enterprise editions. Ensure you have the **Personalization** app in your launcher.

2.  **Create a Component Variant:**
    *   Open a page in the **Pages** app.
    *   Select a component (e.g., a "Hero" component).
    *   In the action bar, click **Add variant**.
    *   Give the variant a name (e.g., "Returning Visitor").
    *   Modify the content of this variant (e.g., change the headline to "Welcome back!").

3.  **Define the Audience:**
    *   In the component variant's properties, look for **Choose audience**.
    *   Select a trait (e.g., `Cookie` or `Request Header`).
    *   Set it to trigger if a specific cookie like `returning_user=true` is present.

4.  **Verify with Preview:**
    *   In the Page Editor, click the **Preview** icon.
    *   Use the **Persona** switcher in the top bar to simulate being a "Returning Visitor."
    *   The component should change dynamically.

---

## 📖 Explanation (Theory)

### What is Personalization?
Personalization allows you to serve different versions (variants) of a page or component based on information about the visitor.

### Core Concepts:
*   **Traits:** Specific attributes of a visitor (e.g., Location, Device type, Date, Cookies, or custom traits).
*   **Audiences:** A collection of traits that define a segment (e.g., "Smartphone users from France").
*   **Variants:** The actual content that differs from the default.
*   **Personas:** "Mock users" that editors use to test the site. A persona has a set of traits (e.g., "John is from London and uses an iPhone").

### How it works:
When a request comes in, Magnolia's `PersonalizationVoter` checks the visitor's traits against the defined variants. If a match is found, the variant is rendered instead of the default content.

---

## 🛠️ Deep Dive & Configuration (Consolidation)

### Custom Traits
You can define your own traits if the built-in ones (Date, Cookie, etc.) aren't enough.

1.  **Define a Trait (Java/Configuration):**
    Traits are usually registered in the `personalization` module configuration. For light development, you can often use the `Request Header` or `Cookie` traits to simulate complex logic.

2.  **Page-Level Personalization:**
    You can personalize entire pages, not just components. This is useful for completely different landing pages for different marketing campaigns.

3.  **A/B Testing:**
    While similar, A/B testing is a specific form of personalization where variants are served randomly to measure performance. Magnolia's personalization engine can be used as a foundation for this.

**Next Step:** We've looked at how to change content for users. But what if you need to change how Magnolia itself works? In the next lesson, we will explore **Decorators** to modify existing definitions.
