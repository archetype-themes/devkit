# Testing and debugging

Continuing from the previous chapter on Code Adjustments, where we adjusted and enhanced the `block-title` component, it's now time to ensure its reliability and functionality through testing and debugging. Let's dive into how you can conduct end-to-end testing using Playwright, a powerful tool for browser automation.

To begin, let's set up an end-to-end test for your component using Playwright. Create a test file named `block-title.spec.js` in the `test` directory of your component, and add the following code:
```js
import { test, expect } from '@playwright/test'

test('block-price', async ({ page }) => {
  // Given
  await page.goto('/')
  await page.getByRole('link', { name: 'block-title' }).click()
  let data = JSON.parse(await page.getByTestId('product-json').innerText())
  // When
  let blockTitle = page.locator('.block-title').last()
  // Then
  await expect(blockTitle).toContainText(data.title)
  if (data.vendor) await expect(blockTitle).toContainText(data.vendor)
  if (data.selectedOrFirstAvailableVariant.sku)
    await expect(blockTitle).toContainText(data.selectedOrFirstAvailableVariant.sku)
})
```

In this test:

* We navigate to the page where the component is rendered and get some product details.
* We get the `block-title` element.
* We verify the expected behavior of the component, ensuring specific text is present.

Execute your tests with the following command:

```bash
$ npm run test
```

This command runs all tests defined in your project, providing feedback on each test's success or failure.

By conducting tests like these, you can identify and resolve potential issues early in the development process, ensuring your component functions reliably in various scenarios.
