<p align="center">
  <img width="100px" height="100px" src="https://user-images.githubusercontent.com/15089738/111375754-a67f3a80-86c4-11eb-846d-ba33c9e22736.png">
</p>

# vue-type-check-hapyharshit

vue-type-check-hapyharshit is a type checker for typescript written Vue components.

It provides both a CLI wrapper and a programmatically API which is easy to integrate with your current workflow.

Also covers few of the needs to control CI/CD pipeline based on the unwanted code.

## Features

- type checking template code.
- type checking script code.
- exit on 1st error based on flag
- validate only the input files
- exclude multiple files/locations

## Installation
### NPM
```shell
npm i -g vue-type-check-hapyharshit
```
### Yarn
```shell
yarn add vue-type-check-hapyharshit
```

## Usage
```shell
Usage: vue-type-check-hapyharshit or vtch
Options:
  --workspace        root directory which contains vue components
  --srcDir           path to the folder which contains your Vue components, will fallback to the workspace when not passed
  --onlyTemplate     will only check the html template and skip the the script code in a single file component
  --excludeDir       directory or file to exclude from the validation, also converts multiple values into an array of files
  --failExit         flag to exit early with error code 1 at the first error found. Helpful is optimising CI/CD pipelines
  <file_names>       apart from the options any other arguments passed will be considered as input for validation.
```

#### Example

We are going to check a simple Vue component with two type errors:

```vue
<template>
  <div id="app">
    <p>{{ msg }}</p>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "app",
  data() {
    return {
      message: "Hello World!"
    };
  },
  methods: {
    printMessage() {
      console.log(this.message.toFixed(1));
    }
  }
});
</script>
```

![vue-type-check-hapyharshit](https://user-images.githubusercontent.com/15089738/111385638-1eebf880-86d1-11eb-90c1-7f6f78b75f84.gif)


### Programmatical API

```js
const { check } = require("vue-type-check-hapyharshit");

(async () => {
  await check({
    workspace: PATH_TO_WORKSPACE,
    srcDir: PATH_TO_SRC_DIR,
    excludeDir: PATH_TO_EXCLUDE_DIR,
    onlyTemplate: TRUE_OR_FALSE,
    onlyTypeScript: TRUE_OR_FALSE,
    failExit: TRUE_OR_FALSE,
  });
})();
```

## How it works

Currently, the implementation is heavily based on vetur's awesome [interpolation feature](https://vuejs.github.io/vetur/interpolation.html).


