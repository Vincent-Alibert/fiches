# Deep Seach in object

```javascript
/** allows to find value of a property name in an obj 
@nameProperty {string}
@customObj {object} 
*/
nameProperty
  .split(".")
  .reduce((prev, curr) => (prev ? prev[curr] : null), customObj);
```
