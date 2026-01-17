---
description: Refactor section code to use proper CSS/JS encapsulation
---

1. Open the target section file (e.g., `sections/header.liquid`).
2. Move static CSS from `<style>` or `{% style %}` to `{% stylesheet %}`.
   - Keep dynamic Liquid variables (e.g., `{{ section.settings.pad }}`) in the HTML `style` attribute (CSS variables).
3. Encapsulate JavaScript logic:
   - Wrap logic in a Web Component class extending `HTMLElement`.
   - Use `connectedCallback` for initialization.
   - Define custom element using `customElements.define`.
   - Move code to `{% javascript %}` tag.
4. Verify no global scope pollution.
