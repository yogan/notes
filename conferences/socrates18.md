# SoCraTes 2018

## Meta

* [List of Resources by dcarral](https://github.com/dcarral/socrates2018-resources)
* [Blog post by Katja](https://www.katjasays.com/socrates-conference-2018-germany/)

## Sessions

### Music Programming with Sonic Pi

* [Sonic Pi](http://sonic-pi.net)
* [Benjamin's resources / snippets](https://github.com/benjmin-r/music)
* put together loops in Ruby
* loops can be synced with each other (e.g. a beat with a melody)
* lots of functions to alter amplitude, make minor/major chords, etc.
* can receive MIDI events, e.g. read a note/velocity from a keyboard
* [Sam Aaron live coding an ambient electro set w/ Sonic Pi](https://www.youtube.com/watch?v=G1m0aX9Lpts)

Tracker stuff shown by [eBrnd](https://twitter.com/eBrnd):

* SID Tracker
  * [Cheese Cutter](https://github.com/theyamo/CheeseCutter)
  * no samples, parametrize SID sound chip
* Modern Tracker (Sample based)
  * [Open MTP](https://openmpt.org/)

### Functional Calisthenics

* [Codurance Blog Post](https://codurance.com/2017/10/12/functional-calisthenics/),
  with list of rules to constraint your code

### Outside-in TDD with React

* Acceptance tests with [Geb](http://www.gebish.org/) /
  [Spock](http://spockframework.org/)
  * Groovy/Ruby mixture somehow (not sure what is used where)
  * based on WebDriver
  * PageObject patterns (works nice with React - one page object per Component)
* JS lib for mocking HTTP: [nock](https://github.com/nock/nock)

### Modern Frontend CSS and JS

* Session by Yulia Startsev (Mozilla)
* WebComponents - for fallback, Polymer can be used
* links as shared in Slack by Yulia:
  * [Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
  * [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
  * [JS Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
  * [JS WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)
  * [JS Symbols](https://hacks.mozilla.org/2015/06/es6-in-depth-symbols/)

### Switching your "JS" Backend

* Session by Michelle
* [Nest](https://docs.nestjs.com/): node.js based server-side apps with TypeScript
* Swagger (opt-in)
* GraphQL, etc.

### Rust

* setup with [rustup](https://rustup.rs/) and rls
  * `curl https://sh.rustup.rs -sSf | sh`
  * [rls](https://github.com/rust-lang-nursery/rls)
  * WSL: add ~/.cargo/bin to PATH
  * `rustup update`
  * `rustup component add rls-preview rust-analysis rust-src`
* StanU [CS140e](https://web.stanford.edu/class/cs140e/)

### Unknown Codebase Quality

* [CodeCharta example](https://maibornwolff.github.io/codecharta/visualization/app/index.html?file=codecharta.cc.json)

### Non-Violent Communication

#### Four Components

* Observation (≠ judgement)
  * Person talking loud vs. he is angry
* Feelings (≠ thoughts)
* Needs (≠ strategies)
* Request (≠ demand)
  * Should be doable, concrete, present ("SMART")
  * Can also be request for feedback ("I opened myself, can you repeat it back
    to see if we have a common understanding")

#### Resources

* [Wikipedia](https://en.wikipedia.org/wiki/Nonviolent_Communication)
* Marshall Rosenberg, "Nonviolent Communication: A Language of Life"
* also good YT videos by him
* Nancy Kline: "Time & Think"

### Popcorn Flow

* Session by [@dmn1k](https://twitter.com/dmn1k)
* collect problems & observations (e.g. after daily)
* options; rule of three (single option is bad)
* make experiments with defined end date and expected outcome; remind each other
  (e.g. "why are you working alone, we wanted to do pairing only?")
* review outcome
* can be too much at first (too many experiments at once), makes sense to have
  a limit (e.g. "3 experiments per sprint")
