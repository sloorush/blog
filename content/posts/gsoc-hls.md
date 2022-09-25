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

#### Haskell Language Server: Support more LSP features in Haskell Language Server: Folding Ranges

> An encapsulation of my work and experience throughout Google Summer of Code 2022 at Haskell Language Server

Hey there, your today’s read is from Aarush Bhat, final year CS undergrad from India. In this post, I’ll describe the work that I did for Haskell Language Server and brief experience as a part of Google Summer of Code 2022, mentored by [Michael Peyton Jones](https://github.com/michaelpj).

# ---------------------

GSoC GSoC GSoC, I heard this for the first time in my first year of college when I barely understood what FOSS software means. All I understood about GSoC was this program in which pro developers work on open-source software.

But then over the years, I got into open source development, which was accelerated because of the Summer of Bitcoin program. Summer of Bitcoin is a program very similar to Google Summer of Code, where student developers are mentored to contribute to the Bitcoin ecosystem.

Having contributed to Summer of Bitcoin in 2021, I gained the courage to apply for Google Summer of Code. I wanted to make the most out of the program, one thing that I feel and I also mentioned in my proposal is:

> In projects involving low-level technologies like programming languages, operating systems, bitcoin etc. onboarding is one of the most challenging problems. Mentorship programs like Summer of Haskell and GSoC solve this major issue of onboarding and it will enable me to learn more about how the development of a programming language and its tooling takes place.

Aaaaaand it did.

## Pre-mentorship Phase

I was an open-source enthusiast and had contributed to various open-source projects based on Bitcoin, GoLang, and JavaScript. I had recently come across Haskell and its related projects. When I started learning Haskell, after following a basic tutorial, I tried to implement a simple note-taking application using an in-memory database as my first project. While building the application faced an issue with HLS and filed it on the HLS GitHub.

I liked Haskell. At that time, I had started reading a lot about Language Servers and how programming languages are made. Meanwhile, the participating organisations released for Google Summer of Code 2022, and I saw HLS was there!

So I tried to check if I could understand the codebase a little and make some tiny fixes or could solve some good first issues. I picked up two issues from which I could solve one!

The tips on the Summer of Haskell page mention that they welcome new people who want to learn and contribute. This encouraged me to write a proposal and apply!

## The project and the proposal

![Proposed Project](https://i.postimg.cc/9f2NVrqV/image.png)

The haskell-language-server (HLS) project implements a language server for the Language Server Protocol (LSP). A language server talks to a client, which can ask the server to perform various operations, such as reporting errors or providing code completions. Clients and servers can interoperate easily if they all speak the LSP protocol. Many editors can use HLS since editor support for the LSP protocol is widespread.

My project proposed various new features for the haskell language server(HLS). While HLS already comes with the most important ones, a few haven’t been implemented. These important unimplemented features of Language Server Protocol(LSP) have to be implemented. Namely, Semantic Highlighting, Folding ranges, Linked editing, Change Annotation, Document links, and Completion / Code Action / Code Lens resolving.

My project was to choose any of these features and build them.

## After the proposal

I still remember a night before the results were officially released, my friends and I intercepted the GSoC Dashboard API and were able to see our Proposal ranking in the org we applied to.

![Hackerman meme](https://c.tenor.com/TbTe1Nc6j34AAAAC/hacker-hackerman.gif)

This is when I unofficially knew that my chances of getting the mentorship were high xD. And then once I was in i.e. the official GSoC Mail, I was super excited for a fun ride ahead!

## Into the community bonding period

HLS was starting with their monthly meetings. It is a meeting all HLS contributors can attend, and it is a discussion about the present and future of the project. The other GSoCer and I were welcomed to the project and we explained what our plan of action will be.

My mentor and I held a meeting to understand and plan out what would be the best approach to start. We decided I would work on some good first issues to get more familiar with and understand the huge codebase. I read about how HLS was built in this [The tale of a Haskell IDE](https://ndmitchell.com/downloads/paper-building_an_ide_on_top_of_a_build_system-04_sep_2020.pdf).

Then, we decided the first feature to build in was Folding Ranges. Folding Ranges is an essential tool that developers use and having language-specific folding ranges was an essential feature of any Language Server.

## What exactly is a Language server?

Free Code Camp describes LSP like this:

> You see those fancy autosuggestion and error messages popping up in VSCode all the time? And how, just by adding a simple extension from the VSCode marketplace, you get all that IntelliSense power for a completely different language? That comes from LSP.

Language Server Protocol (LSP) is a protocol or a way of talking to language servers (just like HTTP or FTP).

## Way to Folding Ranges

So what exactly are Folding Ranges, You must have seen the small lurky arrows on the side of your code bases which help code readability and section them for easier navigation.

It is provided by the LSP specification [here](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#textDocument_foldingRange)

I began by reading about the architecture of the Haskell language server which is built by plugins. I started reading about relatively small plugins like the Alternate Number Format format plugin was the first plugin I read about which suggests different Number formats to convert numbers in your code base to different formats like bin to hex, dec to bin etc.

After reading plugins like this, We concluded that the Folding Ranges feature should be added to the `hls-code-range-plugin`. This plugin housed an LSP feature called [selection ranges](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#textDocument_selectionRange) which is an intelligent selection of items in a codebase.

## How it looks

![Folding Ranges Demo](https://user-images.githubusercontent.com/54478821/184468510-7c0d5182-c684-48ef-9b39-3866dc2309df.gif)

## How we built it?

We built folding ranges with the help of `CodeRange` which is basically just a concept to unify selection range and folding range. The motivation is to split source code into "ranges". So it is easier to traverse the Abstract Syntax Tree(AST).

The CodeRange looks like this:

```haskell
-- | A tree representing code ranges in a file.
-- This can be useful for features like selection range and folding range
data CodeRange = CodeRange {
    -- | Range for current level
        _codeRange_range    :: !Range,
    -- | A vector of children, sorted by their ranges in ascending order.
    -- Children are guaranteed not to interleave,
    -- but some gaps may exist among them.
        _codeRange_children :: !(Vector CodeRange),
    -- The kind of current code range
        _codeRange_kind     :: !CodeRangeKind
    }
    deriving (Show, Generic, NFData)
```

From these CodeRanges, we parse and form Folding Ranges based on the segments of the AST that we want to pick.

We traverse through the code range and it children to a folding range.

It starts with the root node, converts that into a folding range then moves towards the children.
It converts each child of each root node and parses it to folding range and moves to its children.

There were two cases that are assumed to be taken care on the client side are:

1. When a folding range starts and ends on the same line, it is upto the client if it wants to fold a single line folding or not.

2. As we are converting nodes of the AST into folding ranges, there are multiple nodes starting from a single line.

   A single line of code doesn't mean a single node in AST, so this function removes all the nodes that have a duplicate start line, ie. they start from the same line.

   Eg. A multi-line function that also has a multi-line if statement starting from the same line should have the folding according to the function.
   We think the client can handle this, if not we could change to remove these in future.

After the processing and filtering, we finally get a List of Folding Range. A Folding Range looks like this:

```haskell
-- | Represents a folding range.
data FoldingRange =
  FoldingRange
  { -- | The zero-based line number from where the folded range starts.
    _startLine      :: UInt
    -- | The zero-based character offset from where the folded range
    -- starts. If not defined, defaults to the length of the start line.
  , _startCharacter :: Maybe UInt
    -- | The zero-based line number where the folded range ends.
  , _endLine        :: UInt
    -- | The zero-based character offset before the folded range ends.
    -- If not defined, defaults to the length of the end line.
  , _endCharacter   :: Maybe UInt
    -- | Describes the kind of the folding range such as 'comment' or
    -- 'region'. The kind is used to categorize folding ranges and used
    -- by commands like 'Fold all comments'. See 'FoldingRangeKind' for
    -- an enumeration of standardized kinds.
  , _kind           :: Maybe FoldingRangeKind
  }
  deriving (Read, Show, Eq)
```

With these assumptions we moved forward and added this beautiful feature of Folding Range to the Haskell Language Server.

You can read more about my work on folding ranges and how it went in the PR -> [haskell/haskell-language-server#3058](https://github.com/haskell/haskell-language-server/pull/3058).

## What is my favourite part of participating in GSoC?

My favourite part of participating in GSoC was that I fulfilled why I wanted to be a part of GSoC. I wanted to utilize the mentorship as a way to understand how low-level software development works as it is super tricky to onboard into a project. I am happy that I was able to onboard. It has opened a wide spectrum for me to contribute to other programming languages and their tooling.

## What advice would I give to contributors participating in GSoC in the future?

Don't be intimidated. If you think that this is tough, there are so many things that you thought were tough and you completed them. Do not hesitate to move out of your comfort zone, what if that is where you want to be?

## What next?

My love for open source technologies has grown and I will keep contributing to open source. May the source be with you!

Although it is a simple looking feature, but a lot of stuff happens in the background and in the language server to make that happen. Programs like GSoC empower students to cross the barrier and help them learn how these technologies work!

This concludes my work for now, but I’ll keep working on this domain of tech! For any suggestions or feedback, feel free to reach out via [Twitter](https://twitter.com/realsloorush) or [LinkedIn](https://www.linkedin.com/in/aarush-bhat/). I am also reachable via mail at `hey [at] sloorush [dot] com`. Check out my other work at [github.com/sloorush](https://github.com/sloorush).

Special thanks to [kokobd](https://github.com/kokobd) for helping me out throughout my entire project. Also, thanks to [Harsh](https://github.com/Harsh-1309), [Hemanth](https://github.com/darthbenro008), [Shubham](https://github.com/ShubhamPalriwala), and [Agniva](https://github.com/agnivabasak) for their constant motivation and support. ^\_^

    May the source be with you!
