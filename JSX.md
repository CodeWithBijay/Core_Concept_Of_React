# JSX

## What is JSX?

*JSX* is a syntax extension for JavaScript. It was written to be used with React. JSX code looks a lot like HTML.

What does “syntax extension” mean?

In this case, it means that JSX is not valid JavaScript. Web browsers can’t read it!

If a JavaScript file contains JSX code, then that file will have to be *compiled*. That means that before the file reaches a web browser, a *JSX compiler* will translate any JSX into regular JavaScript.

## JSX Elements

A basic unit of JSX is called a JSX *element*.

Here’s an example of a JSX element:

```
<h1>Hello world</h1>
```

This JSX element looks exactly like HTML! The only noticeable difference is that you would find it in a JavaScript file, instead of in an HTML file.

## JSX Elements And Their Surroundings

JSX elements are treated as JavaScript *expressions*. They can go anywhere that JavaScript expressions can go.

That means that a JSX element can be saved in a variable, passed to a function, stored in an object or array…you name it.

Here’s an example of a JSX element being saved in a variable:

```
const navBar = <nav>I am a nav bar</nav>;
```

Here’s an example of several JSX elements being stored in an object:

```
const myTeam = {
  center: <li>Benzo Walli</li>,
  powerForward: <li>Rasha Loa</li>,
  smallForward: <li>Tayshaun Dasmoto</li>,
  shootingGuard: <li>Colmar Cumberbatch</li>,
  pointGuard: <li>Femi Billon</li>
};
```

## Attributes In JSX

JSX elements can have *attributes*, just like HTML elements can.

A JSX attribute is written using HTML-like syntax: a *name*, followed by an equals sign, followed by a *value*. The *value* should be wrapped in quotes, like this:

```
my-attribute-name="my-attribute-value"
```

Here are some JSX elements with *attributes:*

```
<a href='http://www.example.com'>Welcome to the Web</a>;
 
const title = <h1 id='title'>Introduction to React.js: Part I</h1>; 
```

A single JSX element can have many attributes, just like in HTML:

```
const panda = <img src='images/panda.jpg' alt='panda' width='500px' height='500px' />;
```

## Nested JSX

You can *nest* JSX elements inside of other JSX elements, just like in HTML.

Here’s an example of a JSX `<h1>` element, *nested* inside of a JSX `<a>` element:

```
<a href="https://www.example.com"><h1>Click me!</h1></a>
```

To make this more readable, you can use HTML-style line breaks and indentation:

```
<a href="https://www.example.com">
  <h1>
    Click me!
  </h1>
</a>
```

If a JSX expression takes up more than one line, then you must wrap the multi-line JSX expression in parentheses. This looks strange at first, but you get used to it:

```
(
  <a href="https://www.example.com">
    <h1>
      Click me!
    </h1>
  </a>
)
```

*Nested* JSX expressions can be saved as variables, passed to functions, etc., just like non-nested JSX expressions can! Here’s an example of a *nested* JSX expression being saved as a variable:

```
 const theExample = (
   <a href="https://www.example.com">
     <h1>
       Click me!
     </h1>
   </a>
 );
```

## JSX Outer Elements

There’s a rule that we haven’t mentioned: a JSX expression must have exactly *one* outermost element.

In other words, this code will work:

```
const paragraphs = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph.</p>
    <p>I, too, am a paragraph.</p>
  </div>
);
```

But this code will not work:

```
const paragraphs = (
  <p>I am a paragraph.</p> 
  <p>I, too, am a paragraph.</p>
);
```

The *first opening tag* and the *final closing tag* of a JSX expression must belong to the same JSX element!

It’s easy to forget about this rule, and end up with errors that are tough to diagnose.

If you notice that a JSX expression has multiple outer elements, the solution is usually simple: wrap the JSX expression in a `<div></div>`.

## Rendering JSX

You’ve learned how to write JSX elements! Now it’s time to learn how to *render* them.

To *render* a JSX expression means to make it appear onscreen.

```
import React from 'react';
import ReactDOM from 'react-dom';
ReactDOM.render(<h1>Hello world</h1>, document.getElementById('app'));
```

## ReactDOM.render() I

`ReactDOM` is the name of a JavaScript library. This library contains several React-specific methods, all of which deal with [the DOM](http://www.w3schools.com/js/js_htmldom.asp) in some way or another.

`ReactDOM.render()` is the most common way to *render* JSX. It takes a JSX expression, creates a corresponding tree of DOM nodes, and adds that tree to the DOM. That is the way to make a JSX expression appear onscreen.

```
import React from 'react';
import ReactDOM from 'react-dom';
ReactDOM.render(<h1>Hello world</h1>, document.getElementById('app'));
```

'<h1>Hello world</h1>' is the first *argument* being passed to `ReactDOM.render()`. `ReactDOM.render()`‘s first argument should be a JSX expression, and it will be rendered to the screen.

## Passing a Variable to ReactDOM.render()

`ReactDOM.render()`‘s first argument should *evaluate* to a JSX expression, it doesn’t have to literally *be* a JSX expression.

The first argument could also be a variable, so long as that variable evaluates to a JSX expression.

In this example, we save a JSX expression as a *variable* named `toDoList`. We then pass `toDoList` as the first argument to `ReactDOM.render()`:

```
const toDoList = (
  <ol>
    <li>Learn React</li>
    <li>Become a Developer</li>
  </ol>
);
 
ReactDOM.render(
  toDoList, 
  document.getElementById('app')
);
```

## React: The Virtual DOM 

## Fighting Wasteful DOM Manipulation



## The Problem

[DOM manipulation](https://www.codecademy.com/courses/build-interactive-websites/lessons/javascript-dom/exercises/document) is the heart of the modern, interactive web. Unfortunately, it is also a lot slower than most JavaScript operations.

This slowness is made worse by the fact that **most JavaScript frameworks update the DOM much more than they have to.**

As an example, let’s say that you have a list that contains ten items. You check off the first item. Most JavaScript frameworks would rebuild *the entire list*. That’s ten times more work than necessary! Only one item changed, but the remaining nine get rebuilt exactly how they were before.

Rebuilding a list is no big deal to a web browser, but modern websites can use huge amounts of DOM manipulation. Inefficient updating has become a serious problem.

To address this problem, the people at React popularized something called the *virtual DOM.*

## The Virtual DOM

In React, for every [DOM object](http://eloquentjavascript.net/13_dom.html), there is a corresponding “virtual DOM object.” A virtual DOM object is a *representation* of a DOM object, like a lightweight copy.

A virtual DOM object has the same properties as a real DOM object, but it lacks the real thing’s power to directly change what’s on the screen.

Manipulating the DOM is slow. Manipulating the virtual DOM is much faster, because nothing gets drawn onscreen. Think of manipulating the virtual DOM as editing a blueprint, as opposed to moving rooms in an actual house.

## How it helps

When you render a JSX element, every single virtual DOM object gets updated.

This sounds incredibly inefficient, but the cost is insignificant because the virtual DOM can update so quickly.

Once the virtual DOM has updated, then React compares the virtual DOM with a virtual DOM *snapshot* that was taken right before the update.

By comparing the new virtual DOM with a pre-update version, React figures out *exactly which virtual DOM objects have changed.* This process is called “diffing.”

Once React knows which virtual DOM objects have changed, then React updates those objects, *and only those objects,* on the real DOM. In our example from earlier, React would be smart enough to rebuild your one checked-off list-item, and leave the rest of your list alone.

This makes a big difference! React can update only the necessary parts of the DOM. React’s reputation for performance comes largely from this innovation.

In summary, here’s what happens when you try to update the DOM in React:

1. The entire virtual DOM gets updated.
2. The virtual DOM gets compared to what it looked like before you updated it. React figures out which objects have changed.
3. The changed objects, and the changed objects only, get updated on the *real* DOM.
4. Changes on the real DOM cause the screen to change.

If you’d like to learn more about the virtual DOM, [here’s a good place to start](http://reactkungfu.com/2015/10/the-difference-between-virtual-dom-and-dom/).

------

## The Virtual DOM

One special thing about `ReactDOM.render()` is that it *only updates DOM elements that have changed*.

That means that if you render the exact same thing twice in a row, the second render will do nothing:

```
const hello = <h1>Hello world</h1>;
 
// This will add "Hello world" to the screen:
 
ReactDOM.render(hello, document.getElementById('app'));
 
// This won't do anything at all:
 
ReactDOM.render(hello, document.getElementById('app'));
```

This is significant! Only updating the necessary DOM elements is a large part of what makes React so successful.

## class vs className

Grammar in JSX is mostly the same as in HTML, but there are subtle differences to watch out for. Probably the most frequent of these involves the word `class`.

In HTML, it’s common to use `class` as an attribute name:

```
<h1 class="big">Hey</h1>
```

In JSX, you can’t use the word `class`! You have to use `className` instead:

```
<h1 className="big">Hey</h1>
```

This is because JSX gets translated into JavaScript, and `class` is a reserved word in JavaScript.

When JSX is *rendered*, JSX `className` attributes are automatically rendered as `class` attributes.

## Self-Closing Tags

Another JSX ‘gotcha’ involves *self-closing tags*.

What’s a self-closing tag?

Most HTML elements use two tags: an *opening tag* (`<div>`), and a *closing tag* (`</div>`). However, some HTML elements such as `<img>` and `<input>` use only one tag. The tag that belongs to a single-tag element isn’t an opening tag nor a closing tag; it’s a *self-closing tag.*

When you write a self-closing tag in HTML, it is *optional* to include a forward-slash immediately before the final angle-bracket:

```
Fine in HTML with a slash:
 
  <br />
 
Also fine, without the slash:
 
  <br>
```

But!

In JSX, you *have to* include the slash. If you write a self-closing tag in JSX and forget the slash, you will raise an error:

```
Fine in JSX:
 
  <br />
 
NOT FINE AT ALL in JSX:
 
  <br>
```

## Concept-1  ( JavaScript In Your JSX In Your JavaScript)

```
import React from 'react';
import ReactDOM from 'react-dom';

// Write code here:
ReactDOM.render(
  <h1>2 + 3</h1>,// 2 + 3
  document.getElementById('app')
);
```

## Concept-2  ( Curly Braces in JSX )

```
import React from 'react';
import ReactDOM from 'react-dom';

// Write code here:
ReactDOM.render(
  <h1>{2 + 3}</h1>,//5
  document.getElementById('app')
);
```

## Concept-3  ( 20 Digits of Pi in JSX )

You can now inject regular JavaScript into JSX expressions! This will be extremely useful.

In the code editor, you can see a JSX expression that displays the first twenty digits of pi.

```
import React from 'react';
import ReactDOM from 'react-dom';

const pi = (
  <div>
    <h1>
      PI, YALL!
    </h1>
    <p>
      {Math.PI.toFixed(20)}
    </p>
  </div>
);

ReactDOM.render(
	pi,
	document.getElementById('app')
);
```

Study the expression and notice the following:

- The code is written in a JavaScript file. By default, it will all be treated as regular JavaScript.
- Find `<div>` on line 5. From there up through `</div>`, the code will be treated as JSX.
- Find `Math`. From there up through `(20)`, the code will be treated as regular JavaScript again.
- The curly braces themselves won’t be treated as JSX nor as JavaScript. They are *markers* that signal the beginning and end of a JavaScript injection into JSX, similar to the quotation marks that signal the boundaries of a string.

## Concept-3  (Variables in JSX)

When you inject JavaScript into JSX, that JavaScript is part of the same environment as the rest of the JavaScript in your file.

That means that you can access variables while inside of a JSX expression, even if those variables were declared on the outside.

```
// Declare a variable:
const name = 'Gerdo';
 
// Access your variable 
// from inside of a JSX expression:
const greeting = <p>Hello, {name}!</p>;
```

## Concept-4   (Variable Attributes in JSX)

When writing JSX, it’s common to use variables to set *attributes*.

Here’s an example of how that might work:

```
// Use a variable to set the `height` and `width` attributes:
 
const sideLength = "200px";
 
const panda = (
  <img 
    src="images/panda.jpg" 
    alt="panda" 
    height={sideLength} 
    width={sideLength} />
);
```

Notice how in this example, the `<img />`‘s attributes each get their own line. This can make your code more readable if you have a lot of attributes on one element.

 (Object properties are also often used to set attributes)

```
const pics = {
  panda: "http://bit.ly/1Tqltv5",
  owl: "http://bit.ly/1XGtkM3",
  owlCat: "http://bit.ly/1Upbczi"
}; 
 
const panda = (
  <img 
    src={pics.panda} 
    alt="Lazy Panda" />
);
 
const owl = (
  <img 
    src={pics.owl} 
    alt="Unimpressed Owl" />
);
 
const owlCat = (
  <img 
    src={pics.owlCat} 
    alt="Ghastly Abomination" />
); 
```

## Event Listeners in JSX

JSX elements can have *event listeners*, just like HTML elements can. Programming in React means constantly working with event listeners.

You create an event listener by giving a JSX element a special *attribute*. Here’s an example:

```
<img onClick={myFunc} />
```

An event listener attribute’s *name* should be something like `onClick` or `onMouseOver`: the word `on`, plus the type of event that you’re listening for. You can see a list of valid event names [here](http://facebook.github.io/react/docs/events.html#supported-events).

An event listener attribute’s *value* should be a function. The above example would only work if `myFunc` were a valid function that had been defined elsewhere:

```
function myFunc() {
  alert('Make myFunc the pFunc... omg that was horrible i am so sorry');
}
 
<img onClick={myFunc} />
```

Note that in HTML, event listener *names* are written in all lowercase, such as `onclick` or `onmouseover`. In JSX, event listener names are written in camelCase, such as `onClick` or `onMouseOver`.

Example:

```
import React from 'react';
import ReactDOM from 'react-dom';

function makeDoggy(e) {
  // Call this extremely useful function on an <img>.
  // The <img> will become a picture of a doggy.
  e.target.setAttribute('src', 'https://content.codecademy.com/courses/React/react_photo-puppy.jpeg');
  e.target.setAttribute('alt', 'doggy');
}

const kitty = (
	<img 
		src="https://content.codecademy.com/courses/React/react_photo-kitty.jpg" 
		alt="kitty" onClick={makeDoggy} />
);
ReactDOM.render(kitty, document.getElementById('app'));
```

## Concept-5  ( JSX Conditionals: If Statements That Don't Work )

Here’s a rule that you need to know: you can not inject an `if` statement into a JSX expression.

This code will break:

```
(
  <h1>
    {
      if (purchase.complete) {
        'Thank you for placing an order!'
      }
    }
  </h1>
)
```

The reason why has to do with the way that JSX is compiled. [here](http://facebook.github.io/react/tips/if-else-in-JSX.html).What if you want a JSX expression to render, but only under certain circumstances? You can’t inject an `if` statement. What can you do?

## Concept-6 ( JSX Conditionals: If Statements That Do Work ) 

How can you write a *conditional*, if you can’t inject an `if` statement into JSX?

Well, one option is to write an `if` statement, and *not* inject it into JSX.

Look at **if.js**. Follow the `if` statement, all the way from line 6 down to line 18.

**if.js** works, because the words `if` and `else` are *not* injected in between JSX tags. The `if` statement is on the outside, and no JavaScript injection is necessary.

This is a common way to express conditionals in JSX.

```
import React from 'react';
import ReactDOM from 'react-dom';

let message;

if (user.age >= drinkingAge) {
  message = (
    <h1>
      Hey, check out this alcoholic beverage!
    </h1>
  );
} else {
  message = (
    <h1>
      Hey, check out these earrings I got at Claire's!
    </h1>
  );
}

ReactDOM.render(
  message, 
  document.getElementById('app')
);
```

## Concept-7 ( JSX Conditionals: The Ternary Operator )

There’s a more compact way to write conditionals in JSX: the *ternary operator*.

The ternary operator works the same way in React as it does in regular JavaScript. However, it shows up in React surprisingly often.

Recall how it works: you write `x ? y : z`, where x, y, and z are all JavaScript expressions. When your code is executed, `x` is evaluated as either “truthy” or “falsy.” If `x` is truthy, then the entire ternary operator returns `y`. If `x` is falsy, then the entire ternary operator returns `z`. [Here’s](http://stackoverflow.com/questions/6259982/how-to-use-the-ternary-operator-in-javascript) a nice explanation if you need a refresher.

Here’s how you might use the ternary operator in a JSX expression:

```
const headline = (
  <h1>
    { age >= drinkingAge ? 'Buy Drink' : 'Do Teen Stuff' }
  </h1>
);
```

In the above example, if `age` is greater than or equal to `drinkingAge`, then `headline` will equal `<h1>Buy Drink</h1>`. Otherwise, `headline` will equal `<h1>Do Teen Stuff</h1>`.

## Concept-8  ( JSX Conditionals: &&)

Like the ternary operator, `&&` is not React-specific, but it shows up in React surprisingly often.

In the last two lessons, you wrote statements that would sometimes render a kitty and other times render a doggy. `&&` would *not* have been the best choice for those lessons.

`&&` works best in conditionals that will sometimes do an action, but other times do *nothing at all*.

Here’s an example:

```
const tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```

If the expression on the left of the `&&` evaluates as true, then the JSX on the right of the `&&` will be rendered. If the first expression is false, however, then the JSX to the right of the `&&` will be ignored and not rendered.

.map in JSX

The array method `.map()` comes up often in React. It’s good to get in the habit of using it alongside JSX.

If you want to create a list of JSX elements, then `.map()` is often your best bet. It can look odd at first:

```
const strings = ['Home', 'Shop', 'About Me'];
 
const listItems = strings.map(string => <li>{string}</li>);
 
<ul>{listItems}</ul>
```

In the above example, we start out with an array of strings. We call `.map()` on this array of strings, and the `.map()` call returns a new array of `<li>`s.

On the last line of the example, note that `{listItems}` will evaluate to an array, because it’s the returned value of `.map()`! JSX `<li>`s don’t have to be in an array like this, but they *can* be.

```
// This is fine in JSX, not in an explicit array:
 
<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>
 
// This is also fine!
 
const liArray = [
  <li>item 1</li>, 
  <li>item 2<li>, 
  <li>item 3</li>
];
 
<ul>{liArray}</ul>
```

## Concept-8  ( Keys )

When you make a list in JSX, sometimes your list will need to include something called `keys`:

```
<ul>
  <li key="li-01">Example1</li>
  <li key="li-02">Example2</li>
  <li key="li-03">Example3</li>
</ul>
```

A `key` is a JSX attribute. The attribute’s *name* is `key`. The attribute’s *value* should be something unique, similar to an `id` attribute.

`keys` don’t do anything that you can see! React uses them internally to keep track of lists. If you don’t use keys when you’re supposed to, React might accidentally scramble your list-items into the wrong order.

Not all lists need to have `keys`. A list needs `keys` if either of the following are true:

1. The list-items have *memory* from one render to the next. For instance, when a to-do list renders, each item must “remember” whether it was checked off. The items shouldn’t get amnesia when they render.
2. A list’s order might be shuffled. For instance, a list of search results might be shuffled from one render to the next.

If neither of these conditions are true, then you don’t have to worry about `keys`. If you aren’t sure then it never hurts to use them!

Example

```
import React from 'react';
import ReactDOM from 'react-dom';

const people = ['Rowe', 'Prevost', 'Gare'];

const peopleLis = people.map((person, i) =>
  // expression goes here:
  <li key={'person_' + i}>{person}</li>
);

// ReactDOM.render goes here:
ReactDOM.render(<ul>{peopleLis}</ul>, document.getElementById('app'));
```

## Concept- 9 (  React.createElement  )

You can write React code without using JSX at all!

The majority of React programmers do use JSX, and we will use it for the remainder of this tutorial, but you should understand that it is possible to write React code without it.

The following JSX expression:

```
const h1 = <h1>Hello world</h1>;
```

can be rewritten without JSX, like this:

```
const h1 = React.createElement(
  "h1",
  null,
  "Hello, world"
);
```

When a JSX element is compiled, the compiler *transforms* the JSX element into the method that you see above: `React.createElement()`. Every JSX element is secretly a call to `React.createElement()`.