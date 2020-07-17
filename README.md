# Serbet Helper Doc

This project is one helper doc to use [Serbet lib](https://github.com/mrmurphy/serbet).

## Create endpoint

To crete end point has the props `Serbet.jsonEndpoint` and `Serbet.endpoint`;


## Serbet.jsonEndpoint

The jsonEndpoint response json, sample:

```ocaml
open Async;

type user = {
  id: int,
  email: string,
};

let saveUserInDatabase = (_user: user) => {
  Ok() |> async;
};

let processUser = user => {
  {...user, id: user.id + 2} |> async;
};

let newUser = () => {
  {id: 1, email: "hey man"} |> async;
};

open Serbet.Endpoint;
[@decco]
type body_in = {name: string};

[@decco]
type body_out = {message: string};

let endpoint =
  Serbet.jsonEndpoint({
    verb: POST,
    path: "/",
    body_in_decode,
    body_out_encode,
    handler: (body, _req) => {
      {message: body.name} |> async;
    },
  });

```


## Serbet.endpoint

This method response in text and is easy render. Sample:

```ocaml
open Async;

type user = {
  id: int,
  email: string,
};

let saveUserInDatabase = (_user: user) => {
  Ok() |> async
};

let processUser = user => {
  {...user, id: user.id + 2} |> async;
};

let newUser = () => {
  {id: 1, email: "hey papa"} |> async;
};

open Serbet.Endpoint;

let hello =
  Serbet.endpoint({
    verb: GET,
    path: "/",
    handler: _req => {
      let%Async user = newUser();

      OkString(user.email) |> async;
    },
  });

```

