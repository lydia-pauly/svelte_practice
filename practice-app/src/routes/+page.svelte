<script>
//Notes about Svelte
// An application is composed from one or more components
// Components are just reusable bits of code
// Svelte defines components as reusable self-contained blocks of code thart encapsulates HTML, CSS
// and JS / TS into a .svelte file.

//Adding data
// This is how we assign a variable
let name = 'Svelte';

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

//Using in-string HTML
// You can use HTML within a string with the @html tag
// Note that there is no sanitisation - be very careful about XSS
let html_string = "this string contains some <strong>STRONG HTML!!!!</strong>"
</script>


<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
<!-- This is how you'd refer to the data variable in the DOM, including using methods -->
<h1>HELLO { name.toUpperCase() }</h1>

<!-- This is how to use data in attributes - note the src shorthand -->
<img { src } alt= { alt } />

<!-- This is how to inject imported components into the main app -->
 <Nested />

<!-- This is how to render a string with in-string HTML -->
 <p> { @html html_string } </p>

<!-- This is how you add in-app styling -->
<!-- These changes are scoped to the app only -->
<!-- Note how the Nested component styling doesn't apply to all paragraphs here - it is local -->
<style>
  p {
    color: firebrick;
    font-size: 2em;
  }
</style>
