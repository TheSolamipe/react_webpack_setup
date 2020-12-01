- build: This is where all the artifacts from the build output will be. This will also hold the HTML page that the React app will be injected into.

- src: This will hold our source code.

We used TypeScript in our project for type checking. But used Babel to do the code transpilation. So, the compiler options in our tsconfig.json are focused on type checking, not code transpilation.

Here’s an explanation of the settings we have used:

** lib: The standard typing to be included in the type checking process. In our case, we have chosen to use the types for the browsers DOM as well as the latest version of ECMAScript.
** allowJs: Whether to allow JavaScript files to be compiled.
** allowSyntheticDefaultImports: This allows default imports from modules with no default export in the type checking process.
** skipLibCheck: Whether to skip type checking of all the type declaration files (\*.d.ts).
** esModuleInterop: This enables compatibility with Babel.
** strict: This sets the level of type checking to very high. When this is true, the project is said to be running in strict mode.
** forceConsistentCasingInFileNames: Ensures that the casing of referenced file names is consistent during the type checking process.
** moduleResolution: How module dependencies get resolved, which is node for our project.
** resolveJsonModule: This allows modules to be in .json files which are useful for configuration files.
** noEmit: Whether to suppress TypeScript generating code during the compilation process. This is true in our project because Babel will be generating the JavaScript code.
** jsx: Whether to support JSX in .tsx files.
** include: These are the files and folders for TypeScript to check. In our project, we have specified all the files in the src folder.

- @babel/core: As the name suggests, this is the core Babel library.
- @babel/preset-env: This is a collection of plugins that allow us to use the latest JavaScript features but still target browsers that don’t support them.
- @babel/preset-react: This is a collection of plugins that enable Babel to transform React code into JavaScript.
- @babel/preset-typescript: This is a plugin that enables Babel to transform TypeScript code into JavaScript.
- @babel/plugin-transform-runtime and @babel/runtime: These are plugins that allow us to use the async and await JavaScript features.
- eslint: This is the core ESLint library.
- eslint-plugin-react: This contains some standard linting rules for React code.
- eslint-plugin-react-hooks: This includes some linting rules for React hooks code.
- @typescript-eslint/parser: This allows TypeScript code to be linted.
- @typescript-eslint/eslint-plugin: This contains some standard linting rules for TypeScript code.

- The entry field tells Webpack where to start looking for modules to bundle. In our project, this is index.tsx.
- The module field tells Webpack how different modules will be treated. Our project is telling Webpack to use the babel-loader plugin to process files with .js, .ts, and .tsx extensions.
- The resolve.extensions field tells Webpack what file types to look for in which order during module resolution.
- The output field tells Webpack where to bundle our code. In our project, this is the file called bundle.js in the build folder.
- The devServer field configures the Webpack development server. We are telling it that the root of the web server is the build folder, and to serve files on port 4000.

// we have configured ESLint to use the TypeScript parser,
// and the standard React and TypeScript rules as a base set of rules.
// We’ve explicitly added the two React hooks rules and suppressed the
// react/prop-types rule because prop types aren’t relevant in React with TypeScript projects.
// We have also told ESLint to detect the version of React we are using.

# Adding type checking into the webpack process

The Webpack process won’t do any type checking at the moment. We can use a package called fork-ts-checker-webpack-plugin to enable the Webpack process to type check the code. This means that Webpack will inform us of any type errors.

## Here’s an explanation of these ForkTsCheckerWebpackPlugin settings in the webpackconfig.ts:

- async: We have set this to false so that Webpack waits for the type checking process to finish before it emits any code.
- eslint: We have set this to point to the source files so that Webpack informs us of any linting errors.

# Adding npm scripts

We will leverage npm scripts to start our app in development mode and build a production version of our app. Let’s add a scripts section to package.json with the following scripts:
