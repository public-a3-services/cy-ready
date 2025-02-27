# cy-ready

## Chrome bookmarklet

### Procedure:

1. Create a new bookmark:
    - Right-click on the bookmarks bar and select `Add page`.
2. Set the name and URL:
    - `Name`: For example, "Check data-cy"
    - `URL`: Paste the following code:

```javascript
javascript:(function() {
  const controlElements = ['button', 'input', 'a', 'select', 'textarea', 'form'];

  const elements = document.querySelectorAll(controlElements.join(', '));
  const allElements = document.querySelectorAll('*');
  let missingDataCy = [];
  let hasDataCy = [];
  let otherWithDataCy = [];

  console.log('%c Control elements:', 'font-size: 20px; font-weight: bold; color: purple;');
  console.log(controlElements);

  elements.forEach(el => {
    if (!el.hasAttribute('data-cy')) {
      missingDataCy.push({
        'tag': el.tagName.toLowerCase(),
        'id': el.id || '-',
        'class': el.className || '-',
        'text': el.innerText.trim().substring(0, 50) || '-',
        'element': el
      });
    } else {
      hasDataCy.push({
        'tag': el.tagName.toLowerCase(),
        'id': el.id || '-',
        'class': el.className || '-',
        'text': el.innerText.trim().substring(0, 50) || '-',
        'data-cy': el.getAttribute('data-cy'),
        'element': el
      });
    }
  });

  Array.from(allElements).forEach(el => {
    if (el.hasAttribute('data-cy')) {
      if (!hasDataCy.some(item => item.element === el) && !Array.from(elements).includes(el)) {
        otherWithDataCy.push({
          'tag': el.tagName.toLowerCase(),
          'id': el.id || '-',
          'class': el.className || '-',
          'text': el.innerText.trim().substring(0, 50) || '-',
          'data-cy': el.getAttribute('data-cy'),
          'element': el
        });
      }
    }
  });

  console.log(`%c ${missingDataCy.length} Missing control data-cy selector:`, 'font-size: 20px; font-weight: bold; color: red;');
  console.table(missingDataCy);

  console.log(`%c ${hasDataCy.length} Control elements with data-cy selector:`, 'font-size: 20px; font-weight: bold; color: green;');
  console.table(hasDataCy);

  console.log(`%c ${otherWithDataCy.length} Other elements with data-cy selector:`, 'font-size: 20px; font-weight: bold; color: blue;');
  console.table(otherWithDataCy);
})();
```

### Example websites to test:

- [example1.html](example1.html)
- [example2.html](example2.html)
- [example3.html](example3.html)
- [example4.html](example4.html)
- [example5.html](example5.html)
