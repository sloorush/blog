+++
title = "GSOC 2022: haskell/haskell-language-server"
date = "2022-09-20T19:09:47+05:30"
author = "sloorush"
authorTwitter = "realsloorush" #do not include @
cover = ""
tags = ["GSoC", "Haskell", "HLS"]
keywords = ["", ""]
description = "An encapsulation of my work and experience throughout Google Summer of Code 2022 at Haskell Language Server"
showFullContent = false
draft = false
+++

![GSOC and Haskell logos to form a cover](https://i.postimg.cc/G2bmHHKd/image.png)

#### Haskell Language Server: Support more LSP features in Haskell Language Server

> An encapsulation of my work and experience throughout Google Summer of Code 2022 at Haskell Language Server

Hey there, your today’s read is from Aarush Bhat, final year CS undergrad from India. In this post, I’ll describe the work that I did for Haskell Language Server and brief experience as a part of Google Summer of Code 2022, mentored by [Michael Peyton Jones](https://github.com/michaelpj).

# --------------

GSoC GSoC GSoC, I heard this for the first time in my first year of college when I barely understood what FOSS software means. I understood GSoC was this program in which pro developers work on open-source software.

But then over the years, I got into open source development, which was accelerated because of the Summer of Bitcoin program. Summer of Bitcoin is a program very similar to Google Summer of Code, where student developers are mentored to contribute to the Bitcoin ecosystem.

Having contributed to Summer of Bitcoin in 2021, I gained the courage to apply for Google Summer of Code. I wanted to make the most out of the program, one thing that I feel and I also mentioned in my proposal is:

> In projects involving low-level technologies like programming languages, operating systems, and bitcoin, onboarding is one of the most challenging problems. Summer of Haskell and GSoC solve this major issue of onboarding and it will enable me to learn more about how the development of a programming language and its tooling takes place.

Aaaaaand it did.

## Pre-mentorship Phase

I was an open-source enthusiast and contributed to various open-source projects based on Bitcoin, GoLang, and JavaScript. I had recently come across Haskell and its related projects. When I started learning Haskell, after following a basic tutorial, I tried to implement a simple note-taking application using an in-memory database as my first project. While building the application faced an issue with HLS and filed it on the HLS GitHub.

I liked Haskell. That time, I had started reading a lot about Language Servers and how programming languages are made. Meanwhile, the participating organisations released for Google Summer of Code 2022, and I saw HLS was there!

So I tried to check if I could understand the codebase a little and make some tiny fixes or could solve some good first issues. I picked up two issues from which I could solve one!

The tips on the Summer of Haskell page mention that they welcome new people who want to learn and contribute. This gave me the courage to write a proposal and apply!

## The project and the proposal

![Proposed Project](https://i.postimg.cc/9f2NVrqV/image.png)

The haskell-language-server (HLS) project implements a language server for the Language Server Protocol (LSP). A language server talks to a client, which can ask the server to perform various operations, such as reporting errors or providing code completions. Clients and servers can interoperate easily if they all speak the LSP protocol. Many editors can use HLS since editor support for the LSP protocol is widespread.

My project proposed various new features for the haskell language server(HLS). While HLS already comes with the most important ones, a few haven’t been implemented yet. These important unimplemented features of Language Server Protocol(LSP) have to be implemented. Namely, Semantic Highlighting, Folding ranges, Linked editing, Change Annotation, Document links, and Completion / Code Action / Code Lens resolving.

## After proposal

I still remember a night before the results were officially released, my friends and I intercepted the GSoC Dashboard API and were able to see our Proposal ranking in the org we applied to.

![Hackerman meme](https://c.tenor.com/TbTe1Nc6j34AAAAC/hacker-hackerman.gif)

This is when I unofficially knew that my chances if getting the mentorship were high xD. And then once I was in i.e. the official GSoC Mail, I was super excited for a fun ride ahead!

## To be continuted...
