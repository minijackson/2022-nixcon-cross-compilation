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

### Configuring

Tools for finding dependencies need to run on the build machine

### Building

Tools that generates code need to run on the build machine

### Testing

Tests need to run on the build machine

## Caveats

- Running unit tests
- Building tools in the compilation process

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
