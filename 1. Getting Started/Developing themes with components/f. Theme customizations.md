# Styling customizations

Now, let's address the styling changes requested in the [Figma file](https://www.figma.com/file/wfOE30Q8piyj5Q7zJhXI2o/Reference-Theme-Demo-V2), focusing on elements like the buy buttons and making product details sticky. To achieve this, we will add some CSS to the `theme.css` file in our reference theme workspace to override the existing styling.

## CSS adjustments
Looking at the figma file there are also a few styling changes being requested, in this case we’re seeing some styling for the product page buy buttons as well as the product details needing to be a sticky element.

To do this let’s add some CSS to the `theme.css` file in our reference theme workspace to override the existing styling:

```css
.shopify-payment-button__button {
  border-radius: var(--radius-xs, 4px);
  background: #141811;

 &:hover {
    background-color: #000;
 }
}

.block-buy-buttons__submit {
  background-color: transparent;
  border-radius: var(--radius-xs, 4px);
  border: 1px solid #141811;
  color: #141811;
}

.main-product__info {
  position: sticky;
  top: 0;
  align-self: flex-start;
  padding: 0 var(--page-width-padding) var(--size-10);
}

.button {
  cursor: pointer;
}
```

---

### [> Next Step: Committing changes and review](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20themes%20with%20components/g.%20Committing%20changes%20and%20review.md)