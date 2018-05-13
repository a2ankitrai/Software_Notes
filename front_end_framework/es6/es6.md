ES6
---

`package.json` file to begin executing with babel

```json

{
  "name": "es6-crash",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build":"babel-node index.js"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-preset-env": "^1.6.1"
  }
}


```

---

# Creating Prototype

```javascript


function Person(name, age) {

  this.name = name;
  this.age = age;

}

Person.prototype.speak = function () {
  console.log(`Hi !! my name is ${this.name} and my age is ${this.age}.`);
};

const p1 = new Person("Jack",28);

console.log(p1);

p1.speak();


```

---

# Creating Classes in ES6

```javascript

class Person {

  constructor(name, age, certificates) {
    this.name=name;
    this.age=age;
    this.certificates=certificates;
  }

   speak() {
    console.log(`Hi !! my name is ${this.name} and my age is ${this.age}.`);

    console.log(`My certificates are: ${this.certificates}`);
  }

   addCertification(certificate) {
      this.certificates.push(certificate);
      return this.certificates;
  }
};


const tChaka = new Person("T'Chaka",35,["ocjp","ccna",]);

tChaka.speak();

tChaka.addCertification("AWS")

console.log(tChaka);

tChaka.speak();

```

# Spread Operator in ES6

```javascript

const names = ['IronMan','Hulk','Thor'];

const namesX = ['Black Widow','Captain America','Hawk Eye']

// ES5 concatination

let combiNames = [];
combiNames = combiNames.concat(names);
combiNames.push('Groot');
combiNames = combiNames.concat(namesX);

//console.log(combiNames);

// ES6 spread operator

const allNames = [...names, 'Groot', ... namesX];

console.log(allNames);

```