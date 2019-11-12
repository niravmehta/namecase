# NameCase

A Javascript library for fixing the capitalization of people's names.

Derived from [emgee3's namecase module](https://github.com/emgee3/namecase). Since the original library wasn't updated for a long time, I forked and merged pull requests 
from other folks.

The original library is heavily based on the Perl [Lingua-EN-NameCase](http://cpansearch.perl.org/src/SUMMER/Lingua-EN-NameCase-1.15/) module.

It's always best to let the user capitalize their own name as there are too many variations
to programmatically catch them all. However, when working with legacy databases, sometimes
such a module is needed.

## Usage

NameCase provides two functions:

`NameCase.checkName()` which returns true if the name is in all `UPPERCASE` or `lowercase`.

`NameCase(string or array, { individualFields : boolean })` returns a properly capitalized name.

The option ```individualFields``` defaults to false which works best when the person's names
are combined into a single field. If ```individualFields``` is set to true, it means you're
passing in given and surnames separately. The only difference between these two options is
with ```individualFields``` set to false, the first character is always capitalized.

Namecase can also be executed from the command line via ```namecase```, which accepts data
from stdin and outputs the formatted names to stdout.


## Examples

### Browser

```javascript
<script source="namecase.js"></script>

<script>

  var name = "GEORGE WASHINGTON";

  if (NameCase.checkName(name)) {
    document.write(
      NameCase(name)
    );
  } else {
    document.write(name);
  }

</script>
```

### Node

```javascript
var nc = require('namecase');

String.prototype.toNameCase = function () {
  var name = this.toString();

  if (nc.checkName(name)) {
    return nc(name, { individualFields : true } );
  }
}

console.log("WILLIAM".toNameCase());
console.log("MCKINLEY".toNameCase());
```

### Command line

Install with ```npm install -g namecase```.

```bash
namecase < input.txt > ouput.txt
```