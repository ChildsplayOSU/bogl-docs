---
sort: 3 # Order in the sidebar
---

# Server Implementation

In this section we'll talk about the server that is bundled with BoGL, located in the [API folder of the same BoGL repository on github](https://github.com/The-Code-In-Sheep-s-Clothing/bogl/tree/master/src/API). In earlier sections we have talked about sending and receiving responses from the server, and how it is responsible for performing the work of evaluating expressions. This work is really done by the language implementation, but the server mediates the communication between the language implementation and any external requester.

BoGL's server is written up using a library called [Servant](https://haskell-servant.readthedocs.io/), also written in Haskell. This allows for us to conveniently handle both the language and server work in the same program. We use Servant to prepare fixed API endpoints that are accessible via REST requests, where each endpoint takes a particular kind of request. As of writing this document, we have 5 endpoints.

- /share
- /load
- /runCode
- /read
- /test

These endpoints are accessible via whatever local interface the server is bound to. Most often, the server is run on the local port **5174**, making access to the test endpoint **http://localhost:5174/test/**.

Now, we can explain what each of these endpoints do, and how to query them. As a note, any REST capable application (such as CURL via the terminal) is more than capable of interacting with these endpoints. This also means developing BoGL applications to make use of a BoGL server relieves one of having to redesign a new language implementation from scratch.

The **share** endpoint is used to generate a sharable link to give other people a copy of your BoGL program. It takes JSON data with the keys `gameContent` and `preludeContent`, these being the string contents of the main program and the prelude respectively. The response will contain a UUID that can be used with the **load** endpoint to retrieve the program. The following command is an example of sharing 2 simple files, and getting a UUID back. This UUID can then be used with **load** to retrieve the contents.

```bash
curl --verbose --header "Content-Type: application/json" --data '{"preludeContent":"prelude content","gameContent":"game file content"}' http://localhost:5174/share
```

The **load** endpoint takes a `path` and reads the file at the given location, returning the contents of a program & prelude to populate the editor program and prelude contents (`path` is really a UUID in this case). This endpoint is only utilized with the share feature, with an intent to load files that have been shared by a user. As an example, the CURL command below shows how the UUID from the **share** endpoint can be used to used to load those same files back up in a separate instance.

```bash
curl --verbose --header "Content-Type: application/json" --data '{"fileName":"UUID_From_Share_Response"}' http://localhost:5174/load
```

The **runCode** endpoint takes a program and an expression and returns the evaluated result. This may be anything from a final value, an error of some sort, or a prompt for further input. The following example shows how to evaluate the expression `hello` given the following BoGL program.

```haskell
game Test

hello : Int
hello = 3 + 3
```

Note that the prelude has been provided, but is empty in this case. The input buffer is also provided, but is empty as well. Finally, every request must provide a `programName`, which is used to make it clear that any errors that occur refer to this  program.

```bash
curl --verbose --header "Content-Type: application/json" --data '{"programName":"Example","file":"game Test\nhello : Int\nhello = 3 + 3","prelude":"","input":"hello","buffer":[]}' http://localhost:5174/runCode
```

The **read** endpoint is an old deprecated endpoint to read files. It was used during testing, but should be considered deprecated now.

The **test** endpoint is used to verify that a BoGL server instance is running as expected. It's accessed via a simple GET request, and just indicates whether the service is running as expected.

```bash
curl --verbose http://localhost:5174/test
```

In the response from the **test** endpoint there's a mention to 'Spiel-Lang', which is equivalent to 'BoGL-Lang'. Spiel was the old codeword for one of the earlier candidate implementations of BoGL, but this later become the version that is used today.

All of these endpoints can be inspected in the **API** folder of BoGL. In this folder, the **Server.hs** file provides the high-level organization of the endpoints into a singular server. Most of the other files refer to the specific endpoints that they contain logic for, with the exception of a couple.

The **JSONData.hs** file contains representations of various data types that are used to structure request and response data to and from the server. The **CORSMiddleware.hs** file provides additional configuration options to the server to setup Cross-Origin Resource Sharing (CORS). This is necessary to allow foreign requests to be made to the BoGL server API, foreign meaning that they did not originate from the same domain as the server.
