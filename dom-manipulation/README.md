
# DOM Manipulation
https://courses.gomakethings.com/courses/dom-manipulation/
https://vanillajstoolkit.com/polyfills/
https://vanillajstoolkit.com/helpers/

## Selectors

1. querySelectorAll()
  ```javascript
   var elemsRed = document.querySelectorAll( '.bg-red' );
   var elemsSnacks = document.querySelectorAll( '[data-snack]' );
  ```

2. querySelector()
  ```javascript
    // The first div with a data attribute of snack equal to carrots
    var elemCarrots = document.querySelector('[data-snack="carrots"]');
    // If an element isn’t found, querySelector() returns null.

    // An element that doesn't exist
    var elemNone = document.querySelector( '.bg-orange' );
    console.log(elemNone);

    // This throws an error if uncommented
    // elemNone.id = 'new-id';

    // Verify element exists before doing anything with it
    if ( elemNone ) {
      // Do something...
    }

    // Get an element, and if not found, return a shadow element instead to prevent chaining errors
    var getElem = function ( selector ) {
      return document.querySelector( selector ) || document.createElement( '_' );
    };

    // This won't throw an error
    getElem( '.does-not-exist' ).id = 'why-bother';
    ```

3. getElementById()
  ```javascript
   var elem = document.getElementById('some-selector');
  ```

4. getElementsByClassName()
  ```javascript
   var elemsWithMultipleClasses = document.getElementsByClassName('some-class another-class');
  ```

5. getElementsByTagName()
  ```javascript
     var divs = document.getElementsByTagName('div');
     // Returns live HTML collection
  ```

6. matches()
  ```javascript
    // Get our elements
    var elemRed = document.querySelector( '.bg-red' );
    // Check for a turkey sandwich
    if ( elemRed.matches( '[data-sandwich="turkey"]' ) ) {
      console.log( 'turkey sandwich!' );
    } else {
      console.log( 'Something else, ick... =(' );
    }

    // Polyfill - https://developer.mozilla.org/en-US/docs/Web/API/Element/matches#Polyfill
    if (!Element.prototype.matches) {
      Element.prototype.matches =
        Element.prototype.matchesSelector ||
        Element.prototype.mozMatchesSelector ||
        Element.prototype.msMatchesSelector ||
        Element.prototype.oMatchesSelector ||
        Element.prototype.webkitMatchesSelector ||
        function(s) {
          var matches = (this.document || this.ownerDocument).querySelectorAll(s),
            i = matches.length;
          while (--i >= 0 && matches.item(i) !== this) {}
          return i > -1;
        };
    }

    // Polyfill - simple version
    if (!Element.prototype.matches) {
        Element.prototype.matches = Element.prototype.msMatchesSelector;
    }

  ```


## Loops
  1. for loops and scoping
  ```javascript
    var sandwiches = [
      'tuna', 'ham', 'turkey', 'pb&j'
    ];

    // Log each sandwich
    for (var i = 0; i < sandwiches.length; i++) {
      console.log(i); // index
      console.log(sandwiches[i]); // value
    }

    // Log each sandwich, skipping ham and ending with turkey
    for (var n = 0; n < sandwiches.length; n++) {
      // Skip to the next in the loop
      if (sandwiches[n] === 'ham') continue;
      // End the loop
      if (sandwiches[n] === 'turkey') break;
      console.log(sandwiches[n]);
    }

    // Scoping: Changing variable values
    var sandwiches = ['turkey', 'tuna', 'chicken salad', 'pb&j'];
    for (var i = 0; i < sandwiches.length; i++) {
      window.setTimeout(function () {
        // This will always log "3"
        console.log(i);
      }, 1000)
    }
  ```

  2. for...in
  ```javascript
    var lunch = {
      sandwich: 'ham',
      snack: 'chips',
      drink: 'soda',
      desert: 'cookie',
      guests: 3,
      alcohol: false,
    };

    for (var key in lunch) {
      if (lunch.hasOwnProperty(key)) {
        if (key === 'drink') break;
        console.log(key); // key
        console.log(lunch[key]); // value
      }
    }
  ```

  3. Array.forEach()
  ```javascript
    var sandwiches = [
      'tuna', 'ham', 'turkey', 'pb&j'
    ];

    // Log each sandwich
    sandwiches.forEach(function(sandwich, index) {
      console.log(index); // index
      console.log(sandwich); // value
    });

    // Skip "ham"
    sandwiches.forEach(function (sandwich, index) {
      if (sandwich === 'ham') return;
      console.log(index) // index
      console.log(sandwich) // value
    });


    /**
     * Array.prototype.forEach() polyfill
     * @author Chris Ferdinandi
     * @license MIT
     */
    if (window.Array && !Array.prototype.forEach) {
      Array.prototype.forEach = function (callback, thisArg) {
        thisArg = thisArg || window;
        for (var i = 0; i < this.length; i++) {
          callback.call(thisArg, this[i], i, this);
        }
      };
    }
  ```

  4. NodeList.forEach()
  ```html
		<p class="sandwiches">Tuna</p>
		<p class="sandwiches">Ham</p>
		<p class="sandwiches">Turkey</p>
		<p class="sandwiches">PB&J</p>
  ```
  ```javascript
    Array.from(document.querySelectorAll('.sandwiches')).forEach(function (sandwich, index) {
      console.log(sandwich.textContent);
    });


    //https://developer.mozilla.org/en-US/docs/Web/API/NodeList/forEach#Polyfill
    if (window.NodeList && !NodeList.prototype.forEach) {
      NodeList.prototype.forEach = function (callback, thisArg) {
        thisArg = thisArg || window;
        for (var i = 0; i < this.length; i++) {
          callback.call(thisArg, this[i], i, this);
        }
      };
    }

    OR

    if (window.NodeList && !NodeList.prototype.forEach) {
      NodeList.prototype.forEach = Array.prototype.forEach;
    }
  ```

  5. Object.keys(obj).forEach()  [^IE9]
  ```javascript
      var lunch = {
        sandwich: 'ham', snack: 'chips',
        drink: 'soda', desert: 'cookie',
        guests: 3, alcohol: false,
      };
      Object.keys(lunch).forEach(function (item) {
        console.log(item); // key
        console.log(lunch[item]); // value
      });
      console.log(Object.keys(lunch));
  ```

  ```javascript
  //
  // Object.keys() polyfill
  //
  // From https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys#Polyfill
  if (!Object.keys) {
    Object.keys = (function () {
      'use strict';
      var hasOwnProperty = Object.prototype.hasOwnProperty,
        hasDontEnumBug = !({ toString: null }).propertyIsEnumerable('toString'),
        dontEnums = [
          'toString',
          'toLocaleString',
          'valueOf',
          'hasOwnProperty',
          'isPrototypeOf',
          'propertyIsEnumerable',
          'constructor'
        ],
        dontEnumsLength = dontEnums.length;

      return function (obj) {
        if (typeof obj !== 'function' && (typeof obj !== 'object' || obj === null)) {
          throw new TypeError('Object.keys called on non-object');
        }

        var result = [], prop, i;

        for (prop in obj) {
          if (hasOwnProperty.call(obj, prop)) {
            result.push(prop);
          }
        }

        if (hasDontEnumBug) {
          for (i = 0; i < dontEnumsLength; i++) {
            if (hasOwnProperty.call(obj, dontEnums[i])) {
              result.push(dontEnums[i]);
            }
          }
        }
        return result;
      };
    }());
  }
  ```


### Classes
  1. The classList API - Element.classList  [^IE10]
  ```javascript
    var elem = document.querySelector('#sandwich');
    // Add a class
    elem.classList.add('turkey');
    // Remove a class
    elem.classList.remove('tuna');
    // Toggle a class
    // (Add the class if it's not already on the element, remove it if it is.)
    elem.classList.toggle('tomato');
    // Check if an element has a specific class
    if (elem.classList.contains('mayo')) {
      console.log('add mayo!');
    }

    // https://vanillajstoolkit.com/polyfills/classlist/
    // https://github.com/eligrey/classList.js/
  ```

  2. Element.className  [^IE6]
  ```javascript
    var elem = document.querySelector('#sandwich');
    // Get all of the classes on an element
    var elemClasses = elem.className;
    console.log(elemClasses);
    // Add a class to an element
    elem.className += ' tomato';
    // Completely replace all classes on an element
    elem.className = 'turkey';
  ```

### Styles
  1. Camel Case
  2. The style property
      https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference
  ```javascript
    var elem = document.querySelector('#sandwich');
    // Get an inline style
    // If this style is not set as an inline style directly on the element, it returns an empty string
    var bgColor = elem.style.backgroundColor;
    var fontWeight = elem.style.fontWeight;
    // Set an inline style
    elem.style.backgroundColor = 'purple';
  ```

  3. getComputedStyle()  -- Browser defaults and external style
  ```javascript
    var elem = document.querySelector('#sandwich');
    // Get the computed style
    var bgColor = window.getComputedStyle(elem).backgroundColor;
    var height = window.getComputedStyle(elem).height;
  ```

### Attributes
  1. Attribute Methods - getAttribute(), setAttribute(),
                         removeAttribute(), hasAttribute().
  ```html
    <p id="lunch" data-sandwich="tuna" data-chips="Cape Cod" data-drink="soda">Lunch Order</p>
  ```
  ```javascript
      var elem = document.querySelector('#lunch');
      // Get the value of an attribute
      var sandwich = elem.getAttribute('data-sandwich');
      console.log(sandwich);
      // Set an attribute value
      elem.setAttribute('data-sandwich', 'turkey');
      // Remove an attribute
      elem.removeAttribute('data-chips');
      // Check if an element has an attribute
      if (elem.hasAttribute('data-drink')) {
        console.log('Add a drink!');
      }
  ```
  2. Attribute Properties - https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes
  ```javascript
    var elem = document.querySelector('#some-elem');
    // Get attributes
    var id = elem.id;
    var name = elem.name;
    var tabindex = elem.tabindex;
    // Set attributes
    elem.id = 'new-id';
    elem.title = 'The title';
    elem.tabindex = '-1';
    // Remove attributes
    elem.id = '';
    elem.title = '';
    elem.tabindex = '';
  ```


### Events
  1. addEventListener() - https://developer.mozilla.org/en-US/docs/Web/Events
  ```javascript
      // Listen for clicks on an element
      var btn = document.querySelector( '#click-me-1' );
      btn.addEventListener('click', function ( event ) {
        console.log('The button was clicked!');
        console.log(event); // The event details
        console.log(event.target); // The clicked element
      }, false);
  ```
  2. Multiple Target Elements
  ```javascript
      // Listen for clicks on the entire window
      window.addEventListener('click', function ( event ) {
        // If the clicked element has the `.click-me` class, it's a match!
        // if (event.target.classList.contains('.click-me')) {
        if ( event.target.matches('.click-me')) {
          console.log('A button as clicked.');
        } else {
          console.log('Not a match!');
        }
      }, false);

      // Doesn't work!
      var btns = document.querySelector( '#click-me' );
      btns.addEventListener('click', function (event) {[code here]}, false);
      OR
      for (var i = 0; i < btns.length; i++) {
        btns[i].addEventListener('click', function (event) {[code here]}, false);
      }
      OR
      // Bad performance
      var btns = document.querySelectorAll('.click-me');
      Array.from(btns).forEach(function (btn) {
        btn.addEventListener('click', function (event) {
          console.log(event); // The event details
          console.log(event.target); // The clicked element
        }, false);
      });
  ```

  3. Multiple Events
  ```javascript
    // Setup our function to run on various events
    var logTheEvent = function (event) {
      console.log('The following event happened: ' + event.type);
    };
    // Add our event listeners
    document.addEventListener('click', logTheEvent, false);
    window.addEventListener('scroll', logTheEvent, false);
    // You don’t need to include the parentheses (()) on the function.
    // The event object is automatically passed in as an argument.

    // This won't work!
    var btns = document.querySelectorAll('.click-me');
    btns.addEventListener('click, scroll', function (event) {
      console.log(event); // The event details
      console.log(event.target); // The clicked element
    }, false);
  ```

  4. Event Debouncing - https://www.paulirish.com/2009/throttled-smartresize-jquery-event-handler/
  https://gomakethings.com/debouncing-your-javascript-events/
  https://vanillajstoolkit.com/helpers/debounce/


  5. Use Capture -
  The last argument in addEventListener() is useCapture,
  and it specifies whether or not you want to “capture” the event.
  For most event types, this should be set to false. But certain
  events, like focus, don’t bubble.
  Setting useCapture to true allows you to take advantage of
  event bubbling for events that otherwise don’t support it.

  ```javascript
    // Listen for all focus events in the document
    document.addEventListener('focus', function(event) {
      // Run functions whenever an element in the document comes into focus
    }, true);
  ```

### Project
1. Project Intro
2. Getting Setup
3. Show and hide the content
4. Toggle content visibility
5. Prevent default anchor behavior
6. Add accordion functionality

  ```html
  	<p><a class="accordion-toggle" href="#content-3">Show More 3</a></p>
		<div class="accordion-content" id="content-3">
			<h2>Corsair</h2>
			<p>Line Corsair haul wind pink provost hardtack keelhaul hang the jib.</p>
    </div>
  ```
  ```javascript
    // Listen for clicks on the document
    document.addEventListener('click', function (event) {
      // Bail if our clicked element doesn't have the .accordion-toggle class
      if (!event.target.classList.contains('accordion-toggle')) return;

      // Get the target content
      var content = document.querySelector(event.target.hash);
      if (!content) return;

      // Prevent default link behavior
      event.preventDefault();

      // If the content is already expanded, collapse it and quit
      if (content.classList.contains('active')) {
        content.classList.remove('active');
        return;
      }

      // Get all active accordion content, loop through it, and close it
      var accordions = Array.from(document.querySelectorAll('.accordion-content.active'));
      accordions.forEach(function (accordion) {
        accordion.classList.remove('active');
      });

      // Open our target content area
      content.classList.add('active');

    }, false);
```