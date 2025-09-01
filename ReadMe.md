# Assessment - ECT

Simply open `assesment.html` in a web browser to see the deep copy demonstration in action.
## 1. Function to create a deep copy of an object

```javascript
    function deepCopy(obj) {
    if (obj === null || typeof obj !== 'object') {
        return obj;
    }

    if (obj instanceof Date) {
        return new Date(obj.getTime());
    }

    if (Array.isArray(obj)) {
        let newArr = [];
        for (let i = 0; i < obj.length; i++) {
            newArr[i] = deepCopy(obj[i]);
        }
        return newArr;
    }

    let newObj = {};
    for (let key in obj) {
        if (Object.prototype.hasOwnProperty.call(obj, key)) {
            newObj[key] = deepCopy(obj[key]);
        }
    }
    return newObj;
}
```
### Alternative approach using `JSON.parse(JSON.stringify(obj))` (mentioned but not implemented in the demo)


