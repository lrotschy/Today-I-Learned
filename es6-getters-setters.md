# ES6 Classes: Getters and Setters

Getters and Setters in ES6 seem superfluous when you can just access the property directly, but they are intended to be used
in cases where you want to do some kind of conversion on a value, so you can set them for properties that aren't pre-defined. 
For example, you could use them to compute a full name from first and last name properties. In this example, I use them to 
perform a conversion and to "encrypt" and "decrypt" a secret value stored in the constructor function's closure.

```
class Thing {
  constructor() {
    let shh = 'secret!';

    this.value = 4;

    this.getSecret = function () {
      return shh.split('').reverse().join('');
    }

    this.setSecret = function (value) {
      shh = value.split('').reverse().join('');
    }
  }

  get bigVal() {
    return this.value * 2;
  }

  set bigVal(n) {
    this.value = n / 2;
  }

  get secret() {
    return this.getSecret();
  }

  set secret(value) {
    this.setSecret(value);
  }

}

bob = new Thing();
console.log(bob.value); // 4
bob.value = 5; 
console.log(bob.value); // 5
console.log(bob.bigVal); // 10
bob.bigVal = 50; 
console.log(bob.bigVal); // 50
console.log(bob.value); // 25
console.log(bob.secret); // !terces
bob.secret = 'blah blah'; 
console.log(bob.secret); // blah blah
```

