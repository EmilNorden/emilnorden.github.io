---
layout: single
title: "Doom in Rust: The progress so far"
category: "Doom in Rust series"
tags: rust doom
header:
  teaser: /assets/images/doom-spider.png
---

### How its going
It's been a while since my first post in this series. 20 days actually. It's not that I've been slacking off (*that much*), I have actually gotten pretty far in terms of functionality. I can load WADs, read lumps, render patches to the screen using Dooms palette system and more.

I'm using [winit](https://crates.io/crates/winit) for window handling and [wgpu](https://crates.io/crates/wgpu) for all my graphics rendering purposes. This combination might be a little bit low level for this kind of project, in retrospect something like [SDL2](https://crates.io/crates/sdl2) would probably have saved me a day or two. The main reason I chose to use winit and wgpu though is that I'm working on *Yet Another Project™* right now that uses these two libraries and I thought this would be a good learning exercise.  
(Besides, winit has wasm support where the window is backed by a \<canvas\> element. Imagine rust-doom running in the web browser, how cool would that be?)  
More on this in another post.

So all in all, its going pretty good. Just look at that sweet memory safe Doom main menu.

<p align="center">
<video autoplay="autoplay" loop="loop" width="319" height="226">
  <source src="/assets/images/doom_menu.webm" type="video/webm">
</video>
</p>

### My approach
I'm trying to maintain the correct order of events in the game, in order for the gameplay to be *identical* to the original.  
I am not sure if this is the correct approach or if it's even that important. I just thought that it would be neat if rust-doom was indistinguishable from the original when playing.
There are some stuff in the code that triggers my refactoring senses. Such as the fact that *D_Display*, the function responsible for drawing stuff onto the screen, calls *NetUpdate*, which will update the game tics, process events (keyboard input etc) AND send/receive data on the network. It's not really what I'd call separation of concerns, and it sometimes makes rewriting it while staying true to the original a challenge to say the least.  

Trying to make sense of all the global state in Doom and finding a suitable "home" for them in the Rust codebase is also a challenge. It leads to me creating structs that feel out of place or unnatural, made evident by the generic names I have given them (GameContext, anyone?). I am a bit ashamed of that, so please dont judge me too hard. It'll get better, I promise.

### Whats next
I have admittedly spent far too much time on the main menu and will shift my attention to gameplay next. Being able to load and render a map is my next goal. I don't expect that to be *too difficult* but who knows.
