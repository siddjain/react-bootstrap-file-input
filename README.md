# README

Bare-bones file picker for react with no dependencies (other than `react >= 16.8`, `bootstrap` and `react-bootstrap`) or bells and whistles.
What it does - it allows you to select multiple files and order and / or delete them. That's it.
You can also set a limit on the number of files user can select and the file types.
This package will not install `react` or `bootstrap` for you. It assumes you will add those dependencies
(all such dependencies that this package relies on you to install are declared under `peerDependencies` in `package.json`)
in your `package.json` along-side `react-bootstrap-file-input`. Example screenshot:

![Screenshot](screenshot.PNG)

# How to use it

Assuming you know how to write a React app:

```
import FileInput from "@siddjain/react-bootstrap-file-input";
import "bootstrap/dist/css/bootstrap.min.css";

export default function App() {
  return (
    <div className="App">
      <FileInput maxFileCount={3} accept=".png,.jpg,.jpeg" />
    </div>
  );
}
```

[Demo](https://codesandbox.io/s/react-bootstrap-file-input-ijw2fe)

**Note**: please use following command to build your app (the app which will use this package as a dependency):

```
GENERATE_SOURCEMAP=false npm run build
```

You need to set `GENERATE_SOURCEMAP=false` or you will get a warning when you run the app. See [this](https://stackoverflow.com/a/70834076/147530).

# API

`FileInput` takes following optional inputs:

- `onChange`: an event handler that is called whenever the file list changes (addition, deletion or change in order of items in the list)
- `maxFileSize`: a number. units: bytes. If user selects a file whose size is greater than `maxFileSize` a warning symbol is displayed. The file is still selected and added to list of files.
- `maxFileCount`: a number. maximum number of files user should be able to select.
- `accept`: same as [accept](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#accept). a string that defines the file types the file input should accept.
- `value`: (for advanced users) this is useful if you will be using `FileInput` in a multi-step (multi-page) form where user can go back and forth. An array of `File` objects to initialize `FileInput`'s list of files.

# Known Issues

If you open a file, then remove it from selection, you cannot select (open) it again immediately (e.g., if you removed it from the selection by mistake).
You have to open another file first. Then you can re-open or select the previous file.

Rest of this document is for me - the developer of this project.

# Build Instructions

## Install Dependencies

```
npm i
```

## Build

```
npm run build
```

# Test Instructions

Below are instructions on how to test the package locally before publishing to npm.
To test the package, create a demo project that will import this package and use it.
E.g., like this (full source code of demo project is not shown):

```
import FileInput from "@siddjain/react-bootstrap-file-input";
import "bootstrap/dist/css/bootstrap.min.css";

export default function App() {
  return (
    <div className="App">
      <h1>Hello CodeSandbox</h1>
      <FileInput></FileInput>
    </div>
  );
}
```

Below are instructions how to use this package from a demo project.

## Step 1: Pack the code

```
npm pack 
```

This will pack all the files under `files` in `package.json` and create a tarball (`.tgz` file).

## Step 2: Copy over tarball to demo folder

Below we copy over the tarball to the demo project:

```
$ mv siddjain-react-bootstrap-file-input-1.0.0.tgz ../react-bootstrap-file-input-demo
```

## Step 3: Install tarball in demo project

```
$ npm i siddjain-react-bootstrap-file-input-1.0.0.tgz
```

Tip: Some docs suggest using `npm link` to test a package locally before publishing to npm.
Do NOT use `npm link` otherwise you run into invalid hook call. see [this](https://github.com/facebook/react/issues/15812).

# Publishing the package

```
npm publish --access public
```

See [this](https://docs.npmjs.com/creating-and-publishing-scoped-public-packages)

# LICENSE

[MIT](LICENSE.txt)