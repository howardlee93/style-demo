Part of my current responsibilites at work is to unify the differing styles found across our web platform. Right now, there is a mix of CSS modules, Tailwind, and Material UI styles in conjunciton with NextJs, the framework we're using.

However, that led to problems, as the styles wouldn't render upon reloading, or apply inconsistently. 

After investigation, we discovered that Next.Js, the framework we use, and the Material UI styles were improperly integrated. Some of the errors we encountered were:

-Navigational bar not adhering to the layout across the page

-CSS works only on first load then is missing

-CSS only applying after changes are made in VSCode

-CSS not updating 



FIX:

The reason was that we had not integrated Material UI properly with NextJs. 

The solution: remove the server-side injected CSS and fix the resolution to inject the Material UI styles.

To begin, we will assume that NextJS is up and running.

1. Install Material UI via NPM

   npm install @material-ui/core

2. create or modify _document.js in /pages directory

   1. _document.js is processed on server-side only
   2. You need to inject an instance of the stylesheet into the intial props and context through getInitialProps
   3. This will inject the CSS styles into the document as a string

3. Then we need to remove the server-generated CSS from client-side app that was from the server side through useEffect so the client-side styles can take over 



There you go! The flickering issue should be gone and the styles should apply properly now.



