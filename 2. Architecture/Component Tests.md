# Component tests

The [Component Explorer](https://github.com/archetype-themes/devkit/blob/main/2.%20Architecture/Component%20Explorer.md) provides a platform to develop theme components in an isolated environment. As part of this setup, we have integrated [Playwright](https://playwright.dev/) into the development workflow to facilitate testings of these components.

> [!NOTE]
> This testing environment is still a work in progress. The long-term vision is to develop a more robust version of what we currently offer. We aim to demonstrate that enhanced testing capabilities are possible and we're committed to delivering a long-awaited feature to the Shopify theme developer community.

![2023-11-09 15-25-05](https://github.com/archetype-themes/explorer/assets/4837696/e23acff7-7c28-45e4-923b-5478881013f2)
_^^ Replace with Playwright demo_

## Getting started

### Prerequisites

Before proceeding, we recommend familiarizing yourself with the [Playwright documentation](https://playwright.dev/docs/intro) as our tests are entirely built on top of this tool.

### Running tests

To run tests within the `reference-components` repository, run the following command:

```bash
npm run test
```

This command builds the latest version of your theme components, launches Playwright, and allows you to run tests for all or selected theme components.

### Writing a component test

To add tests to a theme component, create a `test/` folder inside of your component's folder. Include your individual test files there, named as `{component}.spec.js`.

#### Generate tests with Playwright Inspector

For writing straightforward tests, use the Playwright Inspector by running:

```bash
npx playwright codegen
```

![img](#)
\_^^ Replace with Playwright Codegen

This tool lets you interact with your components and automatically generates tests based on your actions. You can then copy and paste these tests into your spec file.

For information, we recommend you read the [Playwright Codegen](https://playwright.dev/docs/codegen#generate-tests-with-the-playwright-inspector) documentation.

#### Real-world example

For a practical example, see the [`cart-icon.spec.js`](https://github.com/archetype-themes/reference-components/blob/main/components/cart-icon/test/cart-icon.spec.js) file. This tests the functionality of the cart icon. Here's what the test performs:

```js
import { test, expect } from "@playwright/test";
import { EVENTS } from "@archetype-themes/utils/pubsub";

test("cart-icon", async ({ page }) => {
  // Given: Navigate to the homepage and click the cart icon
  await page.goto("/");
  await page.getByRole("link", { name: "cart-icon" }).click();

  // Setup data for simulating a cart change event
  let cartIcon = 5;
  let data = {
    eventName: EVENTS.cartChange,
    options: { detail: { cart: { item_count: cartIcon } } },
  };

  // When: Dispatch a custom event to simulate cart change
  await page.evaluate(
    ({ eventName, options }) =>
      Promise.resolve(
        setTimeout(
          () => document.dispatchEvent(new CustomEvent(eventName, options)),
          300
        )
      ),
    data
  );

  // Then: Verify the cart count is updated correctly on the page
  await expect(page.locator("cart-count")).toContainText(cartIcon.toString());
});
```

- **Given**: Initializes the test by navigating to the homepage and simulating a user clicking on the cart icon.
- **Setup**: Prepares the data to simulate a cart change. This involves setting up a custom event with the number of items that should appear in the cart.
- **When**: Triggers the event that simulates changing the number of items in the cart.
- **Then**: Checks if the cart count on the page matches the expected number of items. This is crucial for ensuring that the user interface accurately reflects changes to the cart's contents.

Defining an effective test involves simulating user interactions and custom events to ensure that your theme components function as expected.

While writing tests is optional, we highly encourage it! Playwright offers robust tools for building comprehensive tests, thereby enhancing the reliability and user experience of your theme components. We recommend reading through the [Playwright documentation](https://playwright.dev/docs/intro) to learn more.
