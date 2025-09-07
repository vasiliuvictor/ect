# Assessment - ECT. Please open the html file

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

## 2. Function to check two objects are equals

```javascript
function check(obj1, obj2) {
    if ((obj1 === null || obj1 === undefined) && (obj2 === null || obj2 === undefined)) {
        return true;
    }

    if ((obj1 === null || obj1 === undefined) || (obj2 === null || obj2 === undefined)) {
        return false;
    }

    if (typeof obj1 !== 'object' && typeof obj2 !== 'object') {
        return obj1 === obj2;
    }

    if (typeof obj1 !== 'object' || typeof obj2 !== 'object') {
        return false;
    }

    if (obj1 instanceof Date && obj2 instanceof Date) {
        return obj1.getTime() === obj2.getTime();
    }

    if (obj1 instanceof Date || obj2 instanceof Date) {
        return false;
    }

    if (Array.isArray(obj1) && Array.isArray(obj2)) {
        if (obj1.length !== obj2.length) {
            return false;
        }
        for (let i = 0; i < obj1.length; i++) {
            if (!check(obj1[i], obj2[i])) {
                return false;
            }
        }
        return true;
    }

    if (Array.isArray(obj1) || Array.isArray(obj2)) {
        return false;
    }

    const keys1 = Object.keys(obj1);
    const keys2 = Object.keys(obj2);
    const allKeys = [...new Set([...keys1, ...keys2])];

    for (let key of allKeys) {
        const val1 = obj1.hasOwnProperty(key) ? obj1[key] : undefined;
        const val2 = obj2.hasOwnProperty(key) ? obj2[key] : undefined;
        
        if (!check(val1, val2)) {
            return false;
        }
    }

    return true;
}
```
