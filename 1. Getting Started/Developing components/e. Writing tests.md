# Testing and debugging

Following up on the enhancements made to the `block-title` component in the previous chapter on [Code Adjustments](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20components/d.%20Code%20adjustments.md), it's important to verify its functionality and reliability through effective testing. 

This section guides you through writing and running end-to-end testing using [Playwright](https://playwright.dev/), a powerful tool for browser automation.

## Setting up end-to-end testing with Playwright

To begin, set up an end-to-end test for your `block-title` component. Create a test file named `block-title.spec.js` in the `test/` directory of your component and add the following code:
```js
import { test, expect } from '@playwright/test'

test('block-title', async ({ page }) => {
  // Given: Navigate to the homepage and click on the block-title link
  await page.goto('/');
  await page.getByRole('link', { name: 'block-title' }).click();

  // Retrieve product data from the page
  let data = JSON.parse(await page.getByTestId('product-json').innerText());

  // When: Locate the last block-title element
  let blockTitle = page.locator('.block-title').last();

  // Then: Verify the block-title contains expected text elements
  await expect(blockTitle).toContainText(data.title);
  if (data.vendor) {
    await expect(blockTitle).toContainText(data.vendor);
  }
  if (data.selectedOrFirstAvailableVariant.sku) {
    await expect(blockTitle).toContainText(data.selectedOrFirstAvailableVariant.sku);
  }
});
```

### Understanding the test

- **Navigation and interaction**: The test starts by navigating to the homepage and interacting with the `block-title` link.
- **Data retrieval**: It retrieves product details from the page, extracting them into a JSON object which includes attributes like title, vendor, and SKU.
- **Verification**: The test ensures that the `block-title` element displays the correct title from the data retrieved. It also checks for the presence of vendor and SKU information if they are available.

## Running the tests

First make sure your `.env` file has the values needed to run your tests. You can get the `[live]` theme id for `SHOPIFY_CLI_THEME_ID` by calling `shopify theme list`:

```
SHOPIFY_CLI_THEME_ID=123792457878
SHOPIFY_STORE_PASSWORD=your-password
```

Execute your tests with the following command:

```bash
$ npm run test
```

This command will run all the tests defined in your project, providing feedback on each test's success or failure.

## Benefits of testing

By conducting tests like these, you can:
- **Detect issues early**: Identify and resolve potential problems early in the development cycle.
- **Ensure reliability**: Confirm that your component performs as expected in various scenarios.
- **Improve code quality**: Enhance the overall quality of your components through thorough testing.

Testing with Playwright not only confirms that your components meet your team's design specifications but also ensures their robustness and functionality all in one place.

---

### [> Next Step: Commiting changes and review](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20components/g.%20Committing%20changes%20and%20review.md)
