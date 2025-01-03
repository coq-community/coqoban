<!---
This file was generated from `meta.yml`, please do not edit manually.
Follow the instructions on https://github.com/coq-community/templates to regenerate.
--->
# Coqoban

[![Docker CI][docker-action-shield]][docker-action-link]
[![Contributing][contributing-shield]][contributing-link]
[![Code of Conduct][conduct-shield]][conduct-link]
[![Zulip][zulip-shield]][zulip-link]

[docker-action-shield]: https://github.com/coq-community/coqoban/actions/workflows/docker-action.yml/badge.svg?branch=master
[docker-action-link]: https://github.com/coq-community/coqoban/actions/workflows/docker-action.yml

[contributing-shield]: https://img.shields.io/badge/contributions-welcome-%23f7931e.svg
[contributing-link]: https://github.com/coq-community/manifesto/blob/master/CONTRIBUTING.md

[conduct-shield]: https://img.shields.io/badge/%E2%9D%A4-code%20of%20conduct-%23f15a24.svg
[conduct-link]: https://github.com/coq-community/manifesto/blob/master/CODE_OF_CONDUCT.md

[zulip-shield]: https://img.shields.io/badge/chat-on%20zulip-%23c1272d.svg
[zulip-link]: https://coq.zulipchat.com/#narrow/stream/237663-coq-community-devs.20.26.20users



A Coq implementation of Sokoban, the Japanese warehouse
keeper's game.

## Meta

- Author(s):
  - Jasper Stein (initial)
  - Hugo Herbelin
- Coq-community maintainer(s):
  - Érik Martin-Dorel ([**@erikmd**](https://github.com/erikmd))
- License: [GNU Lesser General Public License v2.1 or later](LICENSE)
- Compatible Coq versions: 8.10 or later
- Additional dependencies: none
- Coq namespace: `Coqoban`
- Related publication(s): none

## Building instructions

The recommended way to use Coqoban is to build the
project locally:

```shell
git clone https://github.com/coq-community/coqoban.git
cd coqoban
make   # or make -j <number-of-cores-on-your-machine> 
```

However, you can also build and install the whole project via
[opam](https://opam.ocaml.org/doc/Install.html):

```shell
opam repo add coq-released https://coq.inria.fr/opam/released
opam install coq-coqoban
```

## Documentation

Welcome to Coqoban!

This is a Coq implementation of Sokoban, the Japanese
warehouse keeper's game. The keeper must push the boxes to specified
destination places. He can only push one box at a time, no more, and
he can't pull. How to put the boxes in place?

Thanks to [jsCoq](https://jscoq.github.io), you can play Coqoban
[directly in your browser](https://coq.vercel.app/fun/coqoban.html)
without installing Coq!

If you want to install and run Coq and Coqoban locally:

* [Coqoban\_engine.v](theories/Coqoban_engine.v) contains the actual Sokoban
    implementing script/program/data. It has a fair amount of
    remarks explaining what's going on, for those interested to know
    more about this implementation.

    You may just load this file into your favorite Coq editor and play.

* [Coqoban\_levels.v](theories/Coqoban_levels.v) contains 355 levels to be
    played with `Coqoban_engine`.

To import both the engine and levels in Coq:
```coq
From Coqoban Require Import Coqoban_levels.
```

The levels are called `Level_1` up to `Level_355`. From
[Coqoban\_levels.v](theories/Coqoban_levels.v):

```coq
(* These Sokoban levels I have taken from the game KSokoban and include all of the *)
(* Sasquatch (1-50), Mas Sasquatch (51-100), Sasquatch III (101-150), Microban *)
(* (151-305), and Sasquatch IV (306-355) collections. These collections are made by *)
(* David W. Skinner (sasquatch@bentonrea.com) http://users.bentonrea.com/~sasquatch/ *)
```

There are more levels on [this website](http://www.abelmartin.com/rj/sokobanJS/Skinner/David%20W.%20Skinner%20-%20Sokoban.htm).
You can download them and transform them into additional `Coqoban_levels`.v-like files using the Haskell program [ksoq2coqsok.hs](src/ksoq2coqsok.hs).
And obviously you can define your own new levels.
Beware that Coq's lexer requires spaces after `X` and `O`!
See [Coqoban\_engine.v](theories/Coqoban_engine.v) for more details on parsing/printing.

To play, say, e.g.,

```coq
Coq < Goal (solvable Level_274).
1 subgoal

  ============================
   (solvable Level_274)

Unnamed_thm < unfold Level_274. (* Optional but useful *)
1 subgoal

  ============================
   solvable
     |> # # # # # # # # # # # # # # <|
     |> # _ _ _ _ _ _ # _ _ _ _ _ # <|
     +> # _ X + X X _ # _ O _ O O # <|
     |> # # _ # # _ # # # _ # # _ # <|
     |> _ # _ # _ _ _ _ _ _ _ # _ # <|
     |> _ # _ # _ _ _ # _ _ _ # _ # <|
     |> _ # _ # # # # # # # # # _ # <|
     |> _ # _ _ _ _ _ _ _ _ _ _ _ # <|
     |> _ # # # # # # # # # # # # # <|
     |><|
```
     
Boards are represented by rows between `|>` and `<|`. Other signs:

* `_` = open field
* `#` = wall
* `+` = YOU
* `O` = destination square
* `X` = box
* `*` = a box on a destination square
* `o` = YOU, on a destination square

Tactics used to play Coqoban are:
* `n.` (step/push north)
* `e.` (step/push east)
* `s.` (step/push south)
* `w.` (step/push west)

These apply even if there's a wall in the way. You can also use Coq
tacticals, e.g.,

```coq
do 5 n.
Undo 3.
Restart.
Abort.
```

Share and enjoy!

