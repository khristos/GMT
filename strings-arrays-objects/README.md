
# Strings, Arrays, and Objects
https://courses.gomakethings.com/courses/strings-arrays-objects/
https://github.com/cferdinandi/string-array-object-source-code/
https://vanillajstoolkit.com/polyfills/
https://vanillajstoolkit.com/helpers/
https://polyfill.io/

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
3. toTitleCase() - Title Case
    https://medium.freecodecamp.org/three-ways-to-title-case-a-sentence-in-javascript-676a9175eb27
    https://vanillajstoolkit.com/helpers/totitlecase/
    ```javascript
        // for loop
        function toTitleCase(str) {
            str = str.toLowerCase().split(' ');
            for (var i = 0; i < str.length; i++) {
                str[i] = str[i].charAt(0).toUpperCase() + str[i].slice(1); 
            }
            return str.join(' ');
        }
        toTitleCase("I'm a little tea pot");

        // map()
        function toTitleCase(str) {
            return str.toLowerCase().split(' ').map(function(word) {
                return (word.charAt(0).toUpperCase() + word.slice(1));
            }).join(' ');
        }
        toTitleCase("I'm a little tea pot");

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
        // https://vanillajstoolkit.com/polyfills/arrayfrom/
        var sandwiches = ['turkey', 'tuna', 'chicken salad', 'italian', 'blt', 'grilled cheese'];
        var sandwichesCopy = sandwiches.from(sandwiches);
    ```

## Iterate Over Arrays
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
    Pass a callback function into forEach(). The first argument is the current item in the loop. The second is the current index in the array. https://vanillajstoolkit.com/polyfills/arrayforeach/
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
    https://vanillajstoolkit.com/polyfills/arrayfilter/
    ```javascript
    // Create a new array with only numbers greater than 10
    var newArray = [1, 2, 7, 42, 99, 101].filter(function (item) {
        return item > 10;
    });
    // Logs [42, 99, 101]
    ```
3. Array.map() - https://vanillajstoolkit.com/polyfills/arraymap/
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
        var strings = [ 'I love Cape Cod potato chips.', 'What about you?' ];
        var concat = strings.join();
        console.log(concat);
        var concatWithSpace = strings.join(' ');
        console.log(concatWithSpace);
        var concatWithSmiley = strings.join(' =) ');
        console.log(concatWithSmiley);
    ```


## Add Items to an Object and Merge Objects
1. Dot and Bracket Notation - Add key/value pairs
    ```javascript
        var lunch = { sandwich: 'turkey', chips: 'cape cod', drink: 'soda' };
        // Add items to the object
        lunch.alcohol = false;
        lunch["dessert"] = 'cookies';
        // Update a key value
        lunch.sandwich = 'tuna';
        // Using a variable
        var key = 'drink';
        lunch[key] = 'water';
    ```
2. Object.assign - Merge Objects
    The Object.assign() method performs a shallow merge of
    two or more objects. Pass in each object to merge as an
    argument.  
    Note: in a shallow merge, nested objects are overwritten
    completely rather than having their values merged together.  
    https://vanillajstoolkit.com/polyfills/objectassign/  
    https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign#Polyfill
    ```javascript
        // Example objects
        var object1 = {
            apple: 0,
            banana: {
                weight: 52,
                price: 100
            },
            cherry: 97
        };
        var object2 = {
            banana: {
                price: 200
            },
            durian: 100
        };
        var object3 = {
            apple: 'yum',
            pie: 3.214,
            applePie: true
        };
        // Merge objects together
        var mergedObjs = Object.assign(object1, object2, object3);
        console.log(mergedObjs);
    ```
3. extend.js - Merge (deep) two or more objects together  
    https://vanillajstoolkit.com/helpers/extend/ 
    ```javascript
        // Example objects
        var object1 = {
            apple: 0,
            banana: {
                weight: 52,
                price: 100
            },
            cherry: 97
        };
        var object2 = {
            banana: {
                price: 200
            },
            durian: 100
        };
        var object3 = {
            apple: 'yum',
            pie: 3.214,
            applePie: true
        };

        // Deep extend
        console.log(extend(object1, object2, object3));
        // Shallow extend
        console.log(extend(true, object1, object2, object3));
        // Clone object1
        console.log(extend(object1));
    ```

## Compare
1. isEqual.js - Compare Two Arrays or Objects  
    https://vanillajstoolkit.com/helpers/isequal/
    ```javascript
        isEqual(arrObject1, arrObject2);
    ```

## Delete
1. delete
    ```javascript
        // Remove the chips key from the lunch object
        delete lunch.chips;
    ```

## Object.keys
    The Object.keys() method returns an array of keys from an object. Pass in the object as an argument.  
    https://vanillajstoolkit.com/polyfills/objectkeys/

    ```javascript
        var lunch = {
            sandwich: 'turkey',
            chips: 'cape cod',
            drink: 'soda'
        };
        console.log(Object.keys(lunch));
        Object.keys(lunch).forEach(function (key) {
            console.log(key); // The key
            console.log(lunch[key]); // The value
        });
    ```


## Template Literals
    ```javascript
        // Basic template literal
        var concat = `I love Cape Cod potato chips. What about you?`;
        console.log(concat);
        // Template literal with placeholder variables
        var brand = 'Cape Cod';
        var person = 'you';
        var concat2 = `I love ${brand} potato chips. What about ${person}?`;
        console.log(concat2);
    ```

## Project
Getting Setup - Dog listing

    ```html
    	<h1>Adoptable Dogs</h1>
        <div id="dogs">Fetching our adoptable dogs...</div>
    ```

    ```javascript
        var apiData = [
            {
                name: 'Rufus',
                breeds: [
                    'Lab',
                    'German Shepard',
                    'Border Collie'
                ],
                age: 'Adult',
                size: 'M',
                gender: 'M',
                details: 'No Cats, No Dogs',
                photo: 'img/rufus.jpg',
                description: '      Hail-shot bounty barque  chase guns. Brigantine gibbet haul wind line.  Barque chandler lookout clap of thunder. Transom hogshead trysail league.  '
            },
            {
                name: 'Kylie Jane',
                breeds: [
                    'Shih Tzu'
                ],
                age: 'Baby',
                size: 'S',
                gender: 'F',
                details: 'Neutered',
                photo: 'img/kylie.jpg',
                description: '   Hands loaded to the gunwalls topgallant long clothes. Crack Jennys tea cup topsail flogging handsomely. Bounty blow the man down nipper pillage. Chantey landlubber or just lubber red ensign warp.'
            },
            {
                name: 'Jacque ',
                breeds: [
                    'Chihuahua',
                    'Rat Terrier'
                ],
                age: 'Senior',
                size: 'S',
                gender: 'M',
                details: 'No Cats, No Dogs, Neutered, Special Medical Needs',
                photo: 'img/jacque.jpg',
                description: 'Interloper tackle   yo-ho-ho yard. Gangway keelhaul no prey, no pay sheet. Hang the jib snow careen transom. Broadside gabion bilged on her anchor sloop.'
            },
            {
                name: 'Elsa',
                breeds: [
                    'Irish Wolfhound',
                    'Wirehaired Terrier',
                    'Staffordshire Terrier'
                ],
                age: 'Adult',
                size: 'XL',
                gender: 'F',
                details: 'Neutered',
                photo: 'img/elsa.jpg',
                description: 'Take a caulk league pink main sheet. Letter of Marque avast coxswain fire in the hole. Yardarm schooner piracy Jack Tar. Yardarm hardtack rutters poop deck.'
            },
            {
                name: 'Colt',
                breeds: [
                    'Staffordshire Terrier',
                    'Dalmation'
                ],
                age: 'Baby',
                size: 'L',
                gender: 'M',
                details: '',
                photo: 'img/colt.jpg',
                description: '     Come about Nelsons folly  black jack measured fer yer chains.  Hail-shot tack sloop grapple.  Boom sheet spirits man-of-war.  Scuttle bounty hulk sloop.'
            }
        ];

        // Create a list of other details
        var getOtherDetails = function (dogDetails) {

            // If the array is empty, return a messsage
            if (dogDetails === '') {
                return ' No additional details.';
            }

            // Convert the dog details string to an array,
            // then create a list item for each detail
            var details = dogDetails.split(', ').map(function (detail) {
                return '<li>' + detail + '</li>';
            });

            // Convert the details array into a string and wrap in an unordered list
            return '<ul>' + details.join('') + '</ul>';

        };

        // Create a list of adoptable dogs
        var getDogs = function () {
            // Template
            // <h2>{Dog Name}</h2>
            // <p><img alt="A photo of {Dog Name}" src="photo.jpg"></p>
            //
            // <p>
            // 		Age: {age}<br>
            // 		Size: {size}<br>
            // 		Gender: {gender}<br>
            // 		Breeds: {breed1}, {breed2}
            // </p>
            //
            // <strong>Other Details:</strong>
            // <ul>
            // 		<li>{detail1: ex. No Cats}</li>
            // </ul>
            //
            // <p>{description}</p>
            return apiData.map(function (dog) {
                var html =
                    '<h2>' + dog.name + '</h2>' +

                    '<p><img alt="A photo of ' + dog.name + '" src="' + dog.photo + '"></p>' +

                    '<p>' +
                        'Age: ' + dog.age.replace('Baby', 'Puppy') + '<br>' +
                        'Size: ' + toTitleCase(dog.size.replace('S', 'Small').replace('M', 'Medium').replace('XL', 'very large').replace('L', 'large') + '<br>' +
                        'Gender: ' + dog.gender.replace('M', 'Male').replace('F', 'Female')) + '<br>' +
                        'Breeds: ' + dog.breeds.join(', ') +
                    '</p>' +

                    '<strong>Other Details:</strong>' + getOtherDetails(dog.details) +

                    '<p>' + dog.description.replace('  ', ' ') + '</p>';

                return html;
            }).join('');
        };

        // Get the app and generate the HTML
        var app = document.querySelector('#dogs');
        app.innerHTML = getDogs();

    ```