---
description: Shopify Theme Development Guidelines and Rules
always_on: false
---

# Shopify Theme Development Rules

This workspace follows strict guidelines for Shopify Theme development based on `AGENTS.md`.

## 1. Mandatory Actions

- **Initialization**: When working with Liquid themes, verify if `learn_shopify_api` needs to be called to load context.

## 2. Architecture & Components

- **Snippets (`snippets/*.liquid`)**:
  - Use for reusable code fragments.
  - **MUST** include a `{% doc %}` header documenting purpose, parameters, and examples.
  - **MUST NOT** contain `{% schema %}`.
- **Blocks (`blocks/*.liquid`)**:
  - Use for reusable, customizable small components.
  - **MUST** include `{% schema %}`.
  - **MUST** use `{% stylesheet %}` and `{% javascript %}` for component-scoped logic.
- **Sections (`sections/*.liquid`)**:
  - Use for full-width modular components.
  - **MUST** include `{% schema %}`.
  - **MUST** use `{% stylesheet %}` and `{% javascript %}`.

## 3. Styling Standards

- **Encapsulation**: Write CSS/JS _in the component file_ (Block/Section) using `{% stylesheet %}`/`{% javascript %}`.
- **CSS Variables**: For single-property settings (e.g., padding, gap), inject CSS variables inline:
  ```liquid
  <div style="--gap: {{ block.settings.gap }}px">...</div>
  ```
- **CSS Classes**: For multi-property modes (e.g., layout style), use class switching:
  ```liquid
  <div class="collection {{ block.settings.layout }}">...</div>
  ```

## 4. Localization (i18n)

- **NO Hardcoded Text**: All user-facing strings must use the translation filter.
  - Correct: `{{ 'products.general.add_to_cart' | t }}`
  - Incorrect: `<span>Add to Cart</span>`
- **Key Structure**: Update `locales/en.default.json` with hierarchical, snake_case keys (max 3 levels deep).

## 5. Liquid Best Practices

- **Whitespace**: Use `{%-` and `- %}` carefully to control whitespace.
- **Logic**: Use `{% if %}` / `{% unless %}`. (No ternary operators).
- **Documentation**: Adhere to the LiquidDoc format for strict typing in documentation.
  ```liquid
  {% doc %}
    @param {string} title - The title text
  {% enddoc %}
  ```
