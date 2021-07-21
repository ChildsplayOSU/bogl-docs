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

Once BoGL has been successfully built, you can choose to work with either the command line (`stack ghci Bogl-Lang:exe:bogl`) or the server (`stack ghci Bogl-Lang:exe:boglserver`). The only difference between the two is the forward facing interface, with the first providing a standalone command line that works on a given file and the server having only a REST interface.

You can run `stack ghci` and enter `1` or `2` to select between either the command line or server variants. It's worth noting that any language features can be observed using either variant, so it may be up to your development preference.

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

For the server.
```bash
stack ghci Bogl-Lang:exe:boglserver

# start the server on port 5174
> startServer 5174
```
You can also run `stack build` and `stack install` to make `boglserver` accessible from the terminal. In that case, you can then run `boglserver 5174` instead.

For the editor.
```bash
npm start
```
This will open up a new tab in your browser that will show the editor. If your BoGL server is running locally on the same network, you'll be able to write programs and evaluate expressions just like you would normally.

If you want to test things with the BoGL command line run `stack build` and `stack install` to setup `bogl`. This executable expects a BoGL file as its sole argument, like `bogl MyProgram.bgl`, and will start a REPL to evaluate expressions within the context of that program. Typing `exit` or `:q` will close the REPL.

## Testing

If you are making changes to any part of the BoGL stack you will want to consider the following points.

When working on any part of the language (addition or a bug-fix).
- Start with one or more failing tests that should *pass* when your change is complete.
- Make the desired changes while observing the tests.
- When all tests pass via `stack test`, verify that the you haven't introduced any other logical issues.
- Start up the web editor, and verify that your changes work as expected from there as well.
    - this can reveal subtle issues that only arise from the server-client setup

When working on the editor it's similar to the later part of the normal testing step. Testing is slightly more difficult to setup on the editor given that it has to work with `React`, but when possible add tests in advance to verify your functionality before you add it in. You can always check these via `npm run test`.

As a final note, whenever you making changes to any part of the API, or to how the editor talks to the server, you should always verify that your changes do not break the server-client structure. There are no complete tests to verify that the server and client boot and run together as expected, so you will need to test these aspects yourself by running them through the web editor itself. On the brightside, you shouldn't have to check too many programs if you know what you're looking for in advance.
