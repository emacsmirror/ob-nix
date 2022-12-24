# ob-nix

A simple org-babel language extension to evaluate nix expressions using `nix-instantiate`.

## Background of this Project/Code Quality

I recently started using `NixOS` as well as getting into `nix`. As I heavily rely on `org-mode`/`org-roam` for personal knowledge management and `org-babel` to add literate examples I needed a simple way to evaluate `nix` source-blocks with `org-babel`.

The code was written in one-sitting, I intent to improve `ob-nix` further. I took quite some inspiration from [arnm/ob-mermaid](https://github.com/arnm/ob-mermaid) as well as from the `ob-template.el`, so the code structure of this project is loosely based on the aforementioned projects as this is the first time that I've written `org-babel` support for a programming language.

## Examples

```
#+begin_src nix
23+19
#+end_src

#+RESULTS:
: 42
```

### Output-Formats

I've implemented support for =nix-instantiates= JSON as well as XML output format:

```
--json
	When used with --eval, print the resulting value as an JSON representation of the abstract syntax tree rather than as an ATerm.

--xml
	When used with --eval, print the resulting value as an XML representation of the abstract syntax tree rather than as an ATerm.  The schema is the same  as  that
	used by the toXML built-in <../language/builtins.md>.
```

#### JSON-Output

```
#+begin_src nix :json t
rec { x = "foo"; y = x; }
#+end_src

#+RESULTS:
: {"x":"foo","y":"foo"}
```

#### XML-Output

```
#+begin_src nix :xml t
  let
    delimiter = " ";
    a = abort "thanks for the fish";
    b = "hello";
    c = "world";
  in b + delimiter + c
#+end_src


#+RESULTS:
: <?xml version='1.0' encoding='utf-8'?>
: <expr>
:   <string value="hello world" />
: </expr>
```

