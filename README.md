# data-test-id

## Chrome bookmarklet

### Procedure:

1. Create a new bookmark:
    - Right-click on the bookmarks bar and select `Add page`.
2. Set the name and URL:
    - `Name`: For example, "data-test-id"
    - `URL`: Paste the following code:

```javascript
javascript:(function() {
  const controlElements = ['button', 'input', 'a', 'select', 'textarea', 'form'];

  const elements = document.querySelectorAll(controlElements.join(', '));
  const allElements = document.querySelectorAll('*');
  let missingDataTestId = [];
  let hasDataTestId = [];
  let otherWithDataTestId = [];

  console.log('%c Control elements:', 'font-size: 20px; font-weight: bold; color: purple;');
  console.log(controlElements);

  elements.forEach(el => {
    if (!el.hasAttribute('data-test-id')) {
      missingDataTestId.push({
        'tag': el.tagName.toLowerCase(),
        'id': el.id || '-',
        'class': el.className || '-',
        'text': el.innerText.trim().substring(0, 50) || '-',
        'element': el
      });
    } else {
      hasDataTestId.push({
        'tag': el.tagName.toLowerCase(),
        'id': el.id || '-',
        'class': el.className || '-',
        'text': el.innerText.trim().substring(0, 50) || '-',
        'data-test-id': el.getAttribute('data-test-id'),
        'element': el
      });
    }
  });

  Array.from(allElements).forEach(el => {
    if (el.hasAttribute('data-test-id')) {
      if (!hasDataTestId.some(item => item.element === el) && !Array.from(elements).includes(el)) {
        otherWithDataTestId.push({
          'tag': el.tagName.toLowerCase(),
          'id': el.id || '-',
          'class': el.className || '-',
          'text': el.innerText.trim().substring(0, 50) || '-',
          'data-test-id': el.getAttribute('data-test-id'),
          'element': el
        });
      }
    }
  });

  console.log(`%c ${missingDataTestId.length} Missing control data-test-id selector:`, 'font-size: 20px; font-weight: bold; color: red;');
  console.table(missingDataTestId);

  console.log(`%c ${hasDataTestId.length} Control elements with data-test-id selector:`, 'font-size: 20px; font-weight: bold; color: green;');
  console.table(hasDataTestId);

  console.log(`%c ${otherWithDataTestId.length} Other elements with data-test-id selector:`, 'font-size: 20px; font-weight: bold; color: blue;');
  console.table(otherWithDataTestId);
})();
```

### Example websites to test:

- [example1.html](example1.html)
- [example2.html](example2.html)
- [example3.html](example3.html)
- [example4.html](example4.html)
- [example5.html](example5.html)
