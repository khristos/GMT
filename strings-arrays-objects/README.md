
# Strings, Arrays, and Objects
https://courses.gomakethings.com/courses/strings-arrays-objects/
https://vanillajstoolkit.com/polyfills/
https://vanillajstoolkit.com/helpers/

## Remove Whitespace
1. trim()
    ```javascript
        var text = '  This sentence has whitespaces.    ';
        var trimmed = text.trim();
    ```

## String Case
1. toLowerCase()
    ```javascript
        var mixedCase = 'This sentence has some MIXED CASE LeTTeRs in it.';
        var lower = mixedCase.toLowerCase();
    ```
2. toUpperCase()
    ```javascript
        var upper = mixedCase.toUpperCase();
    ```
3. Title Case  --  https://medium.freecodecamp.org/three-ways-to-title-case-a-sentence-in-javascript-676a9175eb27

    ```javascript
        // for loop
        function titleCase(str) {
            str = str.toLowerCase().split(' ');
            for (var i = 0; i < str.length; i++) {
                str[i] = str[i].charAt(0).toUpperCase() + str[i].slice(1); 
            }
            return str.join(' ');
        }
        titleCase("I'm a little tea pot");

        // map()
        function titleCase(str) {
            return str.toLowerCase().split(' ').map(function(word) {
                return (word.charAt(0).toUpperCase() + word.slice(1));
            }).join(' ');
        }
        titleCase("I'm a little tea pot");

        // map() and replace()
        function titleCase(str) {
            return str.toLowerCase().split(' ').map(function(word) {
                return word.replace(word[0], word[0].toUpperCase());
            }).join(' ');
        }
        titleCase("I'm a little tea pot");
    ```


## Converting Strings to Numbers
1. parseInt()
    ```javascript
        console.log(parseInt('42', 10));
        console.log(parseInt('42px', 10));
    ```
2. parseFloat()
    ```javascript
        console.log(parseFloat('3.14'))
        console.log(parseFloat('3.14someRandomStuff'));
        console.log(parseFloat('3'));
    ```
3. Number()
    ```javascript
        console.log(Number('123'));
        console.log(Number('12.3'));
        console.log(Number('3.14someRandomStuff')); // NaN
    ```


## Working with String Content
1. replace()
    ```javascript
        var text = 'I love Cape Cod potato chips!';
        var lays = text.replace('Cape Cod', 'Lays');

        var moreChips = 'Cape Cod potato chips are my favorite brand of chips.';
        // Only replaces the first instance of the word "chips"
        var noChips = moreChips.replace('chips', 'deep fried potato slices');
        // Replaces all instances of the word "chips"
        var noChipsAll = moreChips.replace(new RegExp('chips', 'g'), 'deep fried potato slices');
    ```
2. String.indexOf()
    ```javascript
        // Returns the index of where the substring starts in the string, or -1 if the substring isn’t found. Case-sensitive
        var str = 'I love Cape Cod potato chips.';
        // Boolean test
        if (str.indexOf('Cape Cod') > -1) {
            console.log('It contains the string');
        }
    ```
3. String.startsWith()
    ```javascript
        var str = 'I love Cape Cod';
        str.startsWith('I love');      // true
        str.startsWith('Cape Cod');    // false
        str.startsWith('Cape Cod', 7); // true
    ```
    ```javascript
    // https://vanillajstoolkit.com/polyfills/stringstartswith/
    /**
    * String.prototype.startsWith() polyfill
    * https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith#Polyfill
    */
    if (!String.prototype.startsWith) {
        String.prototype.startsWith = function(searchString, position){
            return this.substr(position || 0, searchString.length) === searchString;
        };
    }
    ```

4. String.endsWith()
    ```javascript
        var str = 'I love Cape Cod.';
        str.endsWith('Cape Cod.');  // true
        str.endsWith('I love');     // false
    ```
    ```javascript
    // https://vanillajstoolkit.com/polyfills/stringendswith/
    // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Assignment_Operators#Bitwise_OR_assignment
    /**
    * String.prototype.endsWith() polyfill
    * https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith#Polyfill
    */
    if (!String.prototype.endsWith) {
        String.prototype.endsWith = function(searchStr, Position) {
            // This works much better than >= because
            // it compensates for NaN:
            if (!(Position < this.length)) {
                Position = this.length;
            } else {
                Position |= 0; // round position
            }
            return this.substr(Position - searchStr.length, searchStr.length) === searchStr;
        };
    }
    ```
5. slice() - 
    Get a portion of a string starting (and optionally ending) at a particular character.
    The first argument is where to start. Use 0 to include the first
    character. The second argument is where to end (and is optional).
    If either argument is a negative integer, it will start at the end of the string and work backwards.
    ```javascript
        var text = 'Cape Cod potato chips';
        var startAtFive = text.slice(5);
        var startAndEnd = text.slice(5, 8);
        var sliceFromTheEnd = text.slice(0, -6);
        // startAtFive: 'Cod potato chips'
        // startAndEnd: 'Cod'
        // sliceFromTheEnd: 'Cape Cod potato'
    ```

## String to an Array
1. split() - Convert a string into an array by splitting it 
             after a specific character (or characters).
    ```javascript
        var shoppingList = 'Soda, turkey sandwiches, potato chips, chocolate chip cookies';
        var menu = shoppingList.split(', ');
        var limitedMenu = shoppingList.split(', ', 2
        );
        // menu: ["Soda", "turkey sandwiches", "potato chips", "chocolate chip cookies"]
        // limitedMenu: ["Soda", "turkey sandwiches"
        ]
    ```

## Add/Remove Items in Array
1. Array.push()
    ```javascript
        //Use push() to add items to an array.
        var sandwiches = ['turkey', 'tuna', 'blt'];
        sandwiches.push('chicken', 'pb&j');
        // sandwiches: ['turkey', 'tuna', 'blt', 'chicken', 'pb&j']
    ```
2. Array.concat()
    ```javascript
        //Use Array.concat() to merge two or more arrays together. It returns a new array.
        var sandwiches1 = ['turkey', 'tuna', 'blt'];
        var sandwiches2 = ['chicken', 'pb&j'];
        var allSandwiches = sandwiches1.concat(sandwiches2);
        // sandwiches1: ['turkey', 'tuna', 'blt']
        // sandwiches2: ['chicken', 'pb&j']
        // allSandwiches: ['turkey', 'tuna', 'blt', 'chicken', 'pb&j']
    ```

## Copy from an Array
1. Array.slice() and Array.from()
    Use Array.slice() to copy items into a new array.
    The first argument is the array index to start at, and the second
    is the index to end on. Both are optional. If you omit the start
    index, it will start at the beginning. If you omit the end index, it will go to the end.
    ```javascript
        var sandwiches = ['turkey', 'tuna', 'chicken salad', 'italian', 'blt', 'grilled cheese'];
        // ['chicken salad', 'italian', 'blt', 'grilled cheese']
        var fewerSandwiches = sandwiches.slice(2);
        // ['chicken salad', 'italian', 'blt']
        var fewerSandwiches2 = sandwiches.slice(2, 4);

        // You can also create a new copy of an entire array with Array.from(). Pass the array to copy in as an argument.
        var sandwiches = ['turkey', 'tuna', 'chicken salad', 'italian', 'blt', 'grilled cheese'];
        var sandwichesCopy = sandwiches.from(sandwiches);
    ```

## Iterate Over Arrays and Transforming Arrays
1. Array.every() - 
    Test whether every item in array meets condition
    ```javascript
        // Returns true
        [12, 25, 42].every(function() {
            return item > 10;
        });
        // Returns false
        [1, 12, 25, 42].every(function() {
            return item > 10;
        });
    ```
2. Array.some() - 
    Test whether at least one item in array meets condition
    ```javascript
        // Returns true
        [1, 12, 25, 42].every(function() {
            return item > 10;
        });
        // Returns false
        [1, 1, 3, 7, 10].every(function() {
            return item > 10;
        });
    ```

## Transforming Arrays
1. Array.forEach() - 
    Pass a callback function into forEach(). The first argument is the current item in the loop. The second is the current index in the array.
    ```javascript
    var sandwiches = ['tuna', 'ham', 'turkey', 'pb&j'];
    sandwiches.forEach(function (sandwich, index) {
        console.log(index); // index
        console.log(sandwich); // value
    });
    // returns 0, tuna, 1, ham, 2, turkey, 3, pb&j
2. Array.filter() -
    The Array.filter() method creates a new array with only elements that pass a test you include as a callback function.
    The callback accepts three arguments: the current item in the loop’s value, its index, and the array itself.
    ```javascript
    // Create a new array with only numbers greater than 10
    var newArray = [1, 2, 7, 42, 99, 101].filter(function (item) {
        return item > 10;
    });
    // Logs [42, 99, 101]
    ```
3. Array.map()
    ```javascript
        /**
         * Double each number in an array
         */
        var numbers = [1, 4, 9];
        var doubles = numbers.map(function(num) {
            return num * 2;
        });
        console.log(doubles);

        /**
         * Get an array of just names
         */
        var data = [
            { name: 'Kyle', occupation: 'Fashion Designer' },
            { name: 'Liza', occupation: 'Web Developer' },
            { name: 'Emily', occupation: 'Web Designer' },
            { name: 'Melissa', occupation: 'Fashion Designer' },
            { name: 'Tom', occupation: 'Web Developer' }
        ];

        var names = data.map(function (item) {
            return item.name;
        });

        console.log(names);
    ```
4. Array.find()
    ```javascript
        /**
        * Get the first item greater than 10
        */
        var greaterThanTen = [1, 12, 25, 42, 99, 101].find(function (item) { return item > 10; });
        console.log(greaterThanTen);

        var alsoGreaterThanTen = [1, 2, 4, 7, 8].find(function (item) { return item > 10; });
        console.log(alsoGreaterThanTen);
    ```
3. Array.reverse()
    ```javascript
        var count = [1, 2, 3, 4, 5];
        // Reverse the array order
        count.reverse();
    ```
4. Array.join()
    ```javascript
        var strings = [
            'I love Cape Cod potato chips.',
            'What about you?'
        ];
        var concat = strings.join();
        console.log(concat);
        var concatWithSpace = strings.join(' ');
        console.log(concatWithSpace);
        var concatWithSmiley = strings.join(' =) ');
        console.log(concatWithSmiley);
    ```



## Add Items to an Object
1. Dot and Bracket Notation
    ```javascript

    ```
2. Merge Objects
    ```javascript

    ```

## Compare
1. Compare Two Arrays or Objects
    ```javascript

    ```