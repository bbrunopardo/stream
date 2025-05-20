# The stream 🌊

[**The stream**](https://stream.thesephist.com) is like a less noisy, mini Twitter feed created by Linus. It's helpful for me in order to keep track of some of my thoughts. I want to use it as a tool for self-expression.

![The stream, running on a browser and an iPhone](docs/stream-devices.png)

I barely use [Twitter](https://twitter.com/bbruno_pardo) and I want to publish every onces in a while about some things I am exploring. I will be also be using Threads for literature. This one , and I personally use Dot quite often.

The stream is built with [Oak programming language](https://oaklang.org/), built by Linus.

## Basic documentation

Leaving the following paragraphs of the original documentation for me to be able to review it easily:

"The stream is a server-rendered web application written in pure [Oak](https://oaklang.org/), a dynamic programming language I created. It's the first real project using Oak (outside of things like the standard library) for something practical, so I ended up building and revising much of the standard library in the process of building the stream. The stream is server-rendered for the primary reason that Oak doesn't compile to JavaScript yet — there's a little bit of JavaScript code to enable some light interactivity like light/dark mode, but all of the core app logic lives in the backend in Oak code.

The stream keeps all update data in a [JSONL](https://jsonlines.org/) file on the backend, each entry containing a timestamp and the raw Markdown for each update. New updates are efficiently appended to the end of the file, and reading latest updates is as simple as reading the last N entries from the file. Though I give up some performance by going with this format rather than, say, a SQLite database, the ability to edit the data manually or easily inspect and back it up is worth the trouble. (And if performance becomes a problem, I can always easily migrate away later.)

Because the app is so simple (and I'm still trying to figure out what an "idiomatic" Oak web app should look like), there's nothing in the code that resembles a "framework". APIs hit well-defined HTTP routes, which directly call data querying and page rendering functions. Perhaps a better design pattern will appear as I build more sophisticated apps with Oak, but for the stream, this seems simple enough."

## Build and deploy

Oak comes packaged as a single statically-linked executable, available from [the website](https://oaklang.org). I deploy the stream as a systemd process that runs `./src/main.oak`. The server will automatically create a `./db/stream.jsonl` data file if it's not already there when it starts.

I use GNU Make to manage some common development tasks.

- Just `make` to run the server
- `make watch` or `make w` to run the server and re-start anytime the backend code changes
- `make fmt` or `make f` to re-format any files containing unstaged changes using `oak fmt`. This is equivalent to `oak fmt --changes --fix`.
