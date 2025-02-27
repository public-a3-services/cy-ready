# cy-ready

## Chrome bookmarklet

### Procedure:

1. Create a new bookmark:
    - Right-click on the bookmarks bar and select "Add page."
2. Set the name and URL:
    - `Name`: For example, "Check data-cy"
    - `URL`: Paste the following code:

```javascript
javascript:(function() {
  const elements = document.querySelectorAll('button, input, a, select, textarea, form');
  let missingDataCy = [];
  let hasDataCy = [];

  elements.forEach(el => {
    if (!el.hasAttribute('data-cy')) {
      missingDataCy.push({
        'Tag': el.tagName.toLowerCase(),
        'ID': el.id || '-',
        'Class': el.className || '-',
        'Text': el.innerText.trim().substring(0, 50) || '-',
        'Element': el
      });
    } else {
      hasDataCy.push({
        'Tag': el.tagName.toLowerCase(),
        'ID': el.id || '-',
        'Class': el.className || '-',
        'Text': el.innerText.trim().substring(0, 50) || '-',
        'Data-Cy': el.getAttribute('data-cy'),
        'Element': el
      });
    }
  });

  console.log('%cMissing data-cy selectors:', 'font-size: 20px; font-weight: bold; color: red;');
  console.table(missingDataCy);

  console.log('%cElements with data-cy selectors:', 'font-size: 20px; font-weight: bold; color: green;');
  console.table(hasDataCy);
})();
```

### Example websites to test:

- [example1.html](example1.html)
- [example2.html](example2.html)
- [example3.html](example3.html)
- [example4.html](example4.html)
- [example5.html](example5.html)
