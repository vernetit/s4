
````markdown
# Three-step Reader

A small experimental HTML/JavaScript reader that transforms a normal text or HTML book into a stepped visual reading layout.

Instead of displaying text as traditional paragraphs, the app splits the text into configurable three-part blocks. Each block creates a visual “stair-step” pattern where the second part starts under the last word of the first part, and the third part starts under the last word of the second part.

Example with a `2 x 4 x 3` layout:

```txt
hello world
      this is a test
                    line
                    line
                    line
````

The goal is to create a guided reading flow where the eyes move through small chunks instead of long horizontal lines.

## Features

* Loads a local HTML file with `fetch()`
* Extracts readable text from the HTML
* Converts the text into a configurable three-step layout
* Supports custom block formats such as:

  * `2 x 4 x 3`
  * `3 x 5 x 2`
  * `4 x 6 x 3`
* Adjustable font size
* Adjustable reading width
* Keyboard navigation:

  * `Right Arrow` = next smart jump
  * `Left Arrow` = previous smart jump
  * `Space` = play / stop
* Smart scrolling:

  * jump by screen
  * jump by block
* Auto-scroll mode based on WPM
* Default speed: `350 WPM`
* Automatically counts visible words on each screen
* Recalculates timing after every scroll
* Reading mode hides the control panel and leaves only a floating Stop button
* Handles partially visible blocks by restarting from the incomplete block on the next jump

## Why?

This project is an experiment in alternative reading interfaces.

Traditional text layouts are optimized for printed pages, but digital reading allows different visual structures. This reader explores whether text can be made easier, faster, or more engaging by breaking it into small stepped chunks.

Possible use cases:

* speed-reading experiments
* attention training
* focused reading sessions
* reading while listening to TTS
* reducing visual fatigue from long lines
* experimenting with eye movement patterns
* studying how layout affects comprehension

This is not meant to replace normal reading. It is a tool for experimenting with reading rhythm, chunking, and visual attention.

## How it works

The app loads an HTML file, removes non-readable elements such as scripts and styles, extracts the text, and splits it into word units.

Then it renders the text into repeated blocks.

A block has three parts:

```txt
Part 1
      Part 2
            Part 3
            Part 3
            Part 3
```

The numbers are configurable.

For example, `2 x 4 x 3` means:

* Part 1: 2 words
* Part 2: 4 words
* Part 3: 3 lines
* Part 3 words per line: configurable separately

## Controls

| Control            | Description                                           |
| ------------------ | ----------------------------------------------------- |
| File               | Path to the HTML file to load                         |
| Part 1: words      | Number of words in the first line                     |
| Part 2: words      | Number of words in the second line                    |
| Part 3: lines      | Number of lines in the third section                  |
| Part 3: words/line | Number of words per line in the third section         |
| Font size          | Text size in pixels                                   |
| Page width         | Maximum reading width                                 |
| Words/minute       | Auto-scroll reading speed                             |
| Smart jump         | Choose between screen-based or block-based navigation |
| Play               | Starts automatic scrolling                            |
| Stop               | Stops reading mode and shows the menu again           |

## Keyboard shortcuts

| Key           | Action                  |
| ------------- | ----------------------- |
| `Right Arrow` | Move forward            |
| `Left Arrow`  | Move backward           |
| `Space`       | Play / stop auto-scroll |

## Auto-scroll behavior

The auto-scroll system is based on visible words.

For each screen, the app:

1. Counts how many words are currently visible.
2. Uses the selected WPM speed to calculate how long the screen should remain visible.
3. Waits for that amount of time.
4. Scrolls to the next readable position.
5. Waits for the scroll animation to settle.
6. Counts the new visible words again.
7. Recalculates the next delay.

Example:

```txt
Visible words: 105
Speed: 350 WPM

105 / 350 = 0.3 minutes
0.3 minutes = 18 seconds
```

So the app waits around 18 seconds before moving to the next screen.

## Local usage

Because the app uses `fetch()` to load a local HTML file, you should run it through a local server instead of opening it directly with `file://`.

Example:

```bash
python3 -m http.server 8000
```

Then open:

```txt
http://localhost:8000/
```

Expected folder structure:

```txt
project/
├── index.html
└── libros/
    └── hp3.html
```

You can change the file path directly in the app.

## Installation

No build step is required.

Just clone the repository and open it through a local web server.

```bash
git clone https://github.com/YOUR-USERNAME/three-step-reader.git
cd three-step-reader
python3 -m http.server 8000
```

Then visit:

```txt
http://localhost:8000/
```

## Project status

Experimental prototype.

The app works as a single-file HTML/JavaScript application, but the reading method itself is experimental. The current goal is to test different visual layouts and scrolling strategies.

## Possible future improvements

* Sentence-aware splitting
* Pause longer at punctuation
* Better support for EPUB files
* Save user settings in `localStorage`
* Light theme
* Import plain `.txt` files
* Drag-and-drop file loading
* TTS integration
* Progress indicator
* Highlight current block
* Export custom layouts
* Mobile reading mode improvements
* More precise word counting
* Reading session statistics



## Disclaimer

This is an experimental reading interface. It is not a scientifically validated speed-reading method, medical tool, or accessibility tool. Reading comfort, comprehension, and speed may vary depending on the user, text type, screen size, and chosen layout.

```
