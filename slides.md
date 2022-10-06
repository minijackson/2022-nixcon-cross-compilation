% Nix for particle accelerators, and the adventure in cross-compilation
% Rémi NICOLE
% TODO: today

---
slide-level: 2
aspectratio: 169

theme: metropolis
colortheme: owl

# Light theme
#colorthemeoptions: snowy
#minted:
#	style: perldoc

links-as-notes: true
beameroption: "show notes on second screen=right"

lang: en-US

references:

- type: speech
  title: LLVM Toolchains in Nixpkgs
  author: John Ericson
  issued: 2021-09-16
  id: llvmNixpkgs
  url: https://www.youtube.com/watch?v=UMDRAmmDBgM
  genre: talk
  event: LLVM Distributor's Conf

- type: speech
  title: An introduction into cross-compiling with nixpkgs
  author: Jörg Thalheim
  issued: 2018-12-29
  id: nixosCross
  url: https://discourse.nixos.org/t/slides-from-my-35c3-cross-compile-workshop/1785
  genre: workshop
  event: 35C3

- type: webpage
  title: Raspberry Pi 4 Model B specifications
  container-title: Raspberry Pi
  issued: 2019-06
  id: rpi
  url: https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/

- type: webpage
  title: MacBook Pro (13-inch, 2019, Two Thunderbolt 3 ports) - Technical Specifications
  container-title: Apple
  issued: 2019-08
  id: macbook
  url: https://support.apple.com/kb/SP799

nocite: "@*"
---

# What is cross-compilation?

## People can't seem to agree

Different workload types, different CPUs, different machine code.

---

:::::: {.columns align=center}

::: column
![`aarch64-linux`  
[@rpi]](./imgs/raspi.png){align=center}
:::

::: column
![`x86_64-darwin`  
[@macbook]](./imgs/macbook.jpg){align=center}
:::

::::::


::: notes

Both of these architectures are considered "Tier 2" for support in nixpkgs

:::

## Definition

Cross-compilation:
: Compiling a package from a given system, for a different system

::: notes
We might do that due to:

- performance issue: a Raspberry Pi doesn't have same computation power or
  memory than a development laptop.
- availability issue: we might want to compile something for Windows without
  having access to one
:::

## Why is it special?

```{.console linenos=false}
user@pc ~ % gcc test.c
```

. . .

```{.console linenos=false}
user@pc ~ % aarch64-linux-gcc test.c
```

```{.console linenos=false}
user@pc ~ % x86_64-darwin-gcc test.c
```

## Why is it special?

```{.console linenos=false highlightlines=1}
user@pc ~ % x86_64-linux-gcc test.c
```

```{.console linenos=false}
user@pc ~ % aarch64-linux-gcc test.c
```

```{.console linenos=false}
user@pc ~ % x86_64-darwin-gcc test.c
```

## Build systems can be complicated

### Running the build

Build systems needs to be run on the build machine

. . .

### Configuring

Tools for finding dependencies need to run on the build machine

. . .

### Building

Tools that generates code need to run on the build machine

. . .

### Testing

Tests need to run on the build machine

::: notes

- Build systems, like `autotools`, `cmake`, `meson`
- For configuring, the most notable one is `pkg-config` which generically finds
  libraries and compilation options for dependencies.
- But other tools exist, for example `llvm-config`, which is specific to LLVM.
- For building, compilers are the most notable, but we can also have tools like
  in wayland or protobuf, which generates C code from protocol description
  files.
- And for compilers the compiler must be configured so that the binary code
  that it generates runs on the platform we're interested in.
- And also, you have a lot of exception, lots of handmade build systems which
  can complicate packaging

:::

# Cross-compilation with Nix

## Platform types

```{=latex}
\definecolor{build}{HTML}{808bed}
\definecolor{host}{HTML}{cfbfad}
\definecolor{target}{HTML}{c080d0}
```

-----------------------------------------------------------------------------------------------------
\textcolor{build}{Build Platform} \textcolor{host}{Host Platform} \textcolor{target}{Target Platform}
--------------------------------- ------------------------------- -----------------------------------
Platform building the software    Platform running the software   Platform for which the software generates code (for e.g. `gcc`)
-----------------------------------------------------------------------------------------------------

::: notes
- Host platform generally is the platform that's the most interesting to you
- Taken from Autotools terminology (de-facto standard)
- Some other software use a different terminology, which makes things confusing
- Graphics adapted from talk [@llvmNixpkgs]
:::

---

![Cross-compiling `htop`](./imgs/canadian-cross-htop.png){width=70%}

## Specifying dependencies in Nixpkgs

![Types of inputs](./imgs/deps-types.png){width=70% align=center}

. . .

`deps${HOST}${TARGET}`{.bash}

::: notes

Those three are the most common, especially `buildInputs` and
`nativeBuildInputs`, but you can find some special cases. For example, the
`gcc` package also uses `depsBuildTarget` and `depsTargetTarget`.

:::

# Let's find a weird case

## An slide

Much content

# Workarounds in practice

## An slide

Much content

# Conclusion

## An slide

Much content

# Bonus: network boot

## An slide

Much content

## Bibliography
