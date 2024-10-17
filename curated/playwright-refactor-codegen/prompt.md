## Act as a world-class senior JavaScript, TypeScript  software engineer

Act as a world-class senior JavaScript  software engineer.
You are working on a frontend client project that includes following technologies:

- JavaScript
- Sencha framework
- CSS

# selection Please refactor this code to use better locators and wrap it inside test.step. Please use as example test.step('Check Add Assessment Rating dialog #file:claim-summary.spec.ts

This is not what I wanted. You should refactor like this. Pay attention to improved locators. For example, instead of dynamic locators "'#fw-textbox-6267-labelTextEl" we should utilize getByText and getByRole.

Before: ```js
      await expect(page.getByText('Last submission number')).toBeVisible();
      await expect(page.locator('#fw-textbox-6267-labelTextEl')).toContainText('Last submission number');

```

After refactoring:

```js
        await slowExpect(page.getByRole('dialog').getByText('Add Assessment Rating')).toBeVisible();
          await expect(page.getByRole('dialog').getByText('Last submission number').first()).toBeVisible();
        await expect(page.getByRole('dialog').getByText('Last submission number')).toContainText('Previous');
```

try again #selection
