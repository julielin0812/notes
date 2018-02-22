- Transpilation with Babel:
  - `npm install babel-cli`
  - `npm install babel-preset-env`
  - `npm run build`
- Set up a JS project that transpiles code when you run `npm run build`
  - place ES6 JS file in a directory called **src**
  - Set up project to use node package mananager (npm)
    - Node packages are directories that contain JS code written by other devs used to reduce duplication of work and avoid bugs.
  - Run `npm init` - this command creates a **package.json** file in the root directory.
    - **package.json** file contains information about the current JS project such as:
      - Metadata - includes project title, description, authors, and more.
      - A list of node packages required for the project. If another dev wants to run your project, npm looks inside the **package.json** file and downloads the packages in this list.
      - Key-value pairs for command line scripts - you can use npm to run these shorthand scripts to perform some process.
  - Install babel
    - `npm install babel-cli -D`
    - `npm install babel-preset-env -D`
      - `-D` flag instructs npm to add each package to a property called `devDependencies` in **package.json**
    - specify the version of the source JS code in **.babelrc**
      - `touch .babelrc` in root directory
      - add `{ 'presets': ['env'] }`
    - Specify script in **package.json** that initiates ES6+ to ES5 transpilation
      - in the `"scripts"` property and underneath `"test"` property, add `"build": "babel src -d lib"`
        - `babel` - the Babel command
        - `src` - instructs Babel to transpile all JS code inside the src directory
        - `-d` - instructors Babel to transpile code to a directory
        - `lib` - Babel writes the transpiled code to a directory called `lib`
      - run `npm run build`


### Modules
- JS *modules* are reusable pieces of code that can be exported from one program and imported for use in another program.
- Separating code with similar logic into files called modules, we can:
  - find, fix and debug code more easily,
  - reuse and recycle defined logic in difference parts of our app,
  - keep information private and protected from other modules,
  - and prevent pollution of the global namespace and potential naming collisions, by cautiously selecting variables and behavior we load into a program.