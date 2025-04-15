---
title: "Midterm Review"
date: 2022-09-30T11:25:19-07:00
draft: false
---
CSCI-571 Web Technology Midterm Review

<!--more-->

HTML + CSS
DOM
JavaScript
HTTP
Networking
JavaScript Advanced (including RegEx)
Web Servers

# Forms + CGI + Server-Side Programming

**Input element type**

checkbox, file, hidden, image, password, radio, reset, submit, text

HIDDEN: The field is not rendered, so servers can maintain state information

**Others**

Can only choose on radio with the same name.

# Python

**Comments**

```python
# comments
'''
comments
'''
"""
comments
"""
```

**Data Types**

Text Type:	str 
Numeric Types:	int, float, complex 
Sequence Types:	list, tuple, range 
Mapping Type:	dict 
Set Types:	set, frozenset 
Boolean Type:	bool 
Binary Types:	bytes, bytearray, memoryview 
None Type:	NoneType

**Constants**

Constants are not really part of Python specification but part of community usage

**Other**

1. Python does not support '++' and '--' notation for auto increments and decrement
2. True or False(the first letter is uppercase)
3. List slice returns a shallow copy of the list

# JSON

**JSON Data Types**

object, array, string, number, boolean, null

**Json VS XML**

| Json                                                         | XML                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| JSON supports only strings, numbers, arrays, Booleans, and objects. | XML supports many complex data types including charts, images, and other non-primitive data types. |

**Decode & Encode JSON**

eval() function is very fast. However, it can compile and execute any JS program, so there can be security issues.

JSON.parse() compiles faster than eval()

JSON.parse it uses a single call to eval to do the conversion, guarded by a single regexp test to assure that the input is safe.

```javascript
JSON.parse('{"name": "Mike", "age": 24}');
let obj={
  name: "mike",
  age: 24
};
let json = JSON.stringify(obj);
```

```python
import json
json.dumps(['foo', {'bar': ('baz', None, 1.0, 2)}])
# '["foo", {"bar": ["baz", null, 1.0, 2]}]'
json.loads('["foo", {"bar":["baz", null, 1.0, 2]}]')
# ['foo', {'bar': ['baz', None, 1.0, 2]}]
json.JSONDecoder
json.JSONEncoder
```

**JSONP**

Requesting a file from another domain can cause problems, due to cross-domain policy. Requesting an external script from another domain does not have this problem. JSONP uses this advantage, and request files using the script tag instead of XMLHttpRequest object.

**Arguments against JSON**

* JSON has no validator
* JSON doesn't have namespace
