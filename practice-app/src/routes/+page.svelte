<script>
//Notes about Svelte
// An application is composed from one or more components
// Components are just reusable bits of code
// Svelte defines components as reusable self-contained blocks of code thart encapsulates HTML, CSS
// and JS / TS into a .svelte file.

//Adding data
// This is how we assign a variable
let name = 'Svelte';
const arrow = "<---";
let numbers = [1,2,3,4];

//Controlling attributes
// You can also use curly braces to refer to attributes
let src = 'static/favicon.png';
let alt = 'test image';

//Importing components
// This is how you'd import other components into the main app
// $lib is a default alias used to reference the lib folder
// You can define custom aliases in svelte.config.js
// Also note that component names are always *Capitalised*
import Nested from "$lib/Nested.svelte";
import Package from "$lib/Package.svelte";

//Using in-string HTML
// You can use HTML within a string with the @html tag
// Note that there is no sanitisation - be very careful about XSS
let html_string = "this string contains some <strong>STRONG HTML!!!!</strong>"

//Reactivity
// Note that Svelte will automatically change when there are changes in the DOM
// However, sometimes some parts of the component will need to be computed from parent parts
// For these, you have reactive declarations

//Reactive declarations
let count = 0;
// Notice how the let is implied in this reactive declaration
// Note how you can have further reactive declarative children from a source declaration
// Changes will be passed upwards automatically
$: doubled = count * 2;
$: doubledoubled = doubled * 2;
$: answer = "Hello";

// Variables below for spread prop exercise - see DOM element Package
const pkg = {
  name: "my-pkg",
  speed: "super fast",
  version: 5,
  website: "https://supercoolsite.com"
};

// Note: reactive declarations and statements will run after other script code and
// before component mark up is rendered

//Reactive statements
// It is not only variables that can be reactive - so can statements
$: console.log(`the count is ${count}`);
// You can also group together statements into one declarative block
$: {
  console.log(`This is also logging the value of ${doubled}`);
  console.log(`This is also logging the value of ${doubledoubled}`);
};
// You can also do conditional reactivity for blocks
$: if (count>10) {
  alert("Count is dangerously high!!");
  count = 0;
}

//Updating arrays and lists
// Note that, because Svelte is reactive to **assignments**, in place methods such as push and splice
// won't actually trigger updates.
// You will have to either add in a redundant assignment, like so:
function addNumberRedundent() {
  numbers.push(numbers.length+1);
  numbers = numbers;
} // Note that reassignment on one line here with the method won't work

// Or you use more idiomatic assignment methods to trigger the updates, like so:
function addNumberIdiomatic() {
  numbers = [...numbers, numbers.length+1];
}
//As a rule of thumb for assignment-based updates, the name of the updated variable must appear on the left hand side of the assignment

//Functions
// You can define functions in-app that are reactive within the DOM - see the button element
// with the id="reactive-button-01"
function increment() {
  count += 1;
};

function reset() {
  count = 0;
};
</script>


<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<!-- This is how you'd refer to the data variable in the DOM, including using methods -->
<h1>HELLO { name.toUpperCase() }</h1>

<!-- This is how to use data in attributes - note the src shorthand -->
<img { src } alt= { alt } />

<!-- This is how to inject imported components into the main app -->
<!-- If we are passing props down, then we define it here -->
<!-- Note that the lack of argument will trigger the default inside the child, if defined -->
 <Nested answer={answer}/>
 <Nested />

<!-- This is how to render a string with in-string HTML -->
 <p> { @html html_string } </p>

<!-- This is how to add in reactive elements -->
 <button id="reactive-button-01" on:click={increment}>
  Clicked {count}
  <!-- Note the reactive wording here by evaluating the value of count -->
  <!-- This checks whether count is 1, and chooses the first option if true -->
  {count === 1 ? 'time' : 'times'}
</button>

<button on:click={reset}>{arrow} Reset me!</button>

<p>{count} is {doubled} doubled</p>
<p>{doubled} is {doubledoubled} doubled again</p>

<!-- Svelte also adds in conditional rendering into the DOM, like so: -->
{#if count > 8}
  <p>{count} is greater than 8</p>
{:else if count > 0}
  <p>{count} is between 0 and 8</p>
{:else}
  <p>{count} is zero!!!</p>
{/if}
<!-- Note that # indicates an OPENING to a conditional, whereas : indicates a CONTINUATION -->
<!-- and / indicates an ENDING to a conditional -->

<p>Numbers is {numbers}</p>
<button on:click={addNumberRedundent}>Redundent method</button>
<button on:click={addNumberIdiomatic}>Idiomatic method</button>

<!-- Note how below that the imported module has to explicitly define all props -->
<Package
  name={pkg.name}
  speed={pkg.speed}
  website={pkg.website}
  version = {pkg.version}
/>
<!-- ...Or you can simply reference a spread, like so -->
<Package {...pkg} />

<!-- This is how you add in-app styling -->
<!-- These changes are scoped to the app only -->
<!-- Note how the Nested component styling doesn't apply to all paragraphs here - it is local -->
<style>
  p {
    color: firebrick;
    font-size: 2em;
  }
</style>
