### Introduction ###
Interview questions asked in varying formats.

### JavaScript ###
+ figure out if Browser cookies is enabled?
    - `navigator.cookiesEnabled` returns `bool` value.

+ ways to set attribute [style to DOM node]
    - [without using jQuery] `<DOMNode>.setAttribute('style', 'border: 1px solid blue')`.

+ is array passed by references 
    - YES
+ what does it return? `isNaN(<dateObject>)`
    - Not a Number: values which are   `undefined` or `0/0`
    ```
    isNaN(new Date());                // false
    isNaN(new Date().toString());     // true
    ```
+ [six] primitive data types of JavaScript
    - Number, undefined, strings, Boolean, Null, Symbol()
+ `encodeURI()` vs `encodeURIComponent()`
    - `encodeURIComponent()` encodes everything except `A-Z a-z 0-9 - _ . ! ~ * ' ( )` characters!
        + use when encoding the value of parameter
        + don't use for whole URI because it will encode `https://xxx` too.
    - `encodeURI()` only encodes `A-Z a-z 0-9 - _ . ! ~ * ' ( )` and `; , / ? : @ & = + $  #`.
    - 
+ static method of `new Date()`
    - `Date.parse()`
        + parse the string value to date, and returns number of milliseconds after Jan 1, 1970 or `NaN`
+ static method of `new String()`
    - `String.fromCharCode()`
        + returns a string created by specified sequence of UTF-16 code
        + `String.fromCharCode(65, 66, 67) //returns ABC`