---
sort: 4 # Order in the sidebar
---

# Developing

This section is intended for developers that will be working on the BoGL stack. Regardless of whether you are working on the language, the server, or the website, it is helpful to have a development environment setup that allows running them all together.

## Installing BoGL (language & server)

BoGL can be installed via git.

```bash
git clone https://github.com/The-Code-In-Sheep-s-Clothing/bogl.git

cd bogl

stack build
```

Once BoGL has been successfully built, you can choose to work with either the command line (`stack ghci Bogl-Lang:exe:bogl`) or the server (`stack ghci Bogl-Lang:exe:boglserver`). The difference between the two is the forward facing interface, with the first (bogl) providing a standalone command line that works on a given file and the second (boglserver) having only a REST interface. If you want to run BoGL expressions in the command line you want to use the first option, `stack ghci Bogl-Lang:exe:bogl`. For details on this, please read the section [For the Command Line](#for-the-command-line) below.

You can also run `stack ghci` by itself and you'll be prompted to enter `1` or `2` to select between either the command line or server variants. It's worth noting that most language features can be observed using either variant, so it's up to your development preference.

## Installing the BoGL Website

The BoGL editor can also be installed via git.

```bash
git clone https://github.com/The-Code-In-Sheep-s-Clothing/bogl-editor.git

cd bogl-editor

# make sure your 'node' version is recent, version 14 or so should be good.
npm install
```

## Verifying & Running

To verify that changes you've made don't break anything, and that the server and the editor work as expected, you can run them as follows.

### For the server

```bash
stack ghci Bogl-Lang:exe:boglserver

# start the server on port 5174
> startServer 5174
```
You can also run `stack build` and `stack install` to make the executable `boglserver` accessible from the terminal. In that case, you can then run `boglserver 5174` instead.

For the editor.
```bash
npm start
```
This will open up a new tab in your browser that will show the editor. If your BoGL server is running locally on the same network, you'll be able to write programs and evaluate expressions just like you would normally.

### For the Command Line

If you want to test things with the BoGL command line you can start a simple repl as follows.

```bash
stack ghci Bogl-Lang:exe:bogl
> repl
```

or

```bash
> main
```

`main` will check to see if there are any command-line arguments present. In the case where there aren't any arguments present, the repl will be started without loading a file, essentially the same as running `repl`.

Both these options start a repl without loading a file. If you want to start a repl in the context of BoGL program you can use this instead.

```bash
> load "MyProgram.bgl"
```

As a side-note, in ghci the delete key can add characters instead of removing the last character while typing expressions in. The standalone binary does not have this problem. To rectify this you can install `bogl` as a local executable by running `stack build` and `stack install` to setup `bogl` (this installs the same executable from before as well). This executable expects an optional BoGL file as its sole argument, like `bogl "MyProgram.bgl"`, and will start a REPL to evaluate expressions within the context of that program. Typing `exit` or `:q` will close the REPL.

```bash
# starts a repl w/out a file
bogl

# loads a file and starts a repl
bogl "MyProgram.bgl"
```

While the repl is running expressions can be entered and evaluated; much the same as is done on the website. In the case you loaded a file (and you want to reload the file to factor in new changes) you can enter `:r` to reload the file's contents.

## Testing

If you are making changes to any part of the BoGL stack you will want to consider the following points.

When working on any part of the language (addition or a bug-fix).
- Start with one or more failing tests that should *pass* when your change is complete.
- Make the desired changes while observing the tests.
- When all tests pass via `stack test`, verify that the you haven't introduced any other logical issues.
- Start up the web editor, and verify that your changes work as expected from there as well.
    - this can reveal subtle issues that only arise from the server-client setup

When working on the editor it's similar to the later part of the normal testing step. Testing is slightly more difficult to setup on the editor given that it has to work with `React`, but when possible add tests in the appropriate **YourFile.test.tsx** testing file (unless it exists already) to verify your functionality before you add it in. These tests are written using Jasmine, so it may help to double check their documentation. You can always check these tests via `npm run test`.

As a final note, whenever you making changes to any part of the API, or to how the editor talks to the server, you should always verify that your changes do not break the server-client structure. There are no complete tests to verify that the server and client boot and run together as expected, so you will need to test these aspects manually by running them through the web editor itself. On the brightside, you shouldn't have to check too many programs if you know what you're looking for in advance.
