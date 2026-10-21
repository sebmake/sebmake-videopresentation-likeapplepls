# sebmake-videopresentation-likeapplepls

A Claude Code skill that makes a silent product film, one to two minutes long, cut like the reveal films Apple plays during its keynotes, then re-cuts it into 15 to 60 second versions for social media. Nobody speaks; on-screen text carries the message, over your own music if you have some.

The skill's instructions and check messages are in French. The engine renders whatever text you approve, so an English film works, but a missing figure still shows up as `[À FOURNIR]` ("to be provided").

## Where the rules come from

51 films pulled from eight Apple keynotes, March 2019 to September 2026, timed shot by shot: how long each shot runs, how many text cards appear, how long text stays up and when the product finally shows itself. The product name lands in the last quarter, about four seconds before the end, and the whole object doesn't appear until 60% of the way through. Pacing follows a U, with shots of roughly three seconds at the start, barely one in the middle, then a reveal held for five. A text card stays up 1.2 s plus 0.3 s per word.

Some rules had nothing to measure against, and the skill labels those as conventions. None of the films is vertical, so every 9:16 rule is one. Cuts don't hit the music's beats any more often than chance would (16 hits against 16.4 expected, over the six films with usable audio), which is why syncing to the beat stays an option instead of a default.

## How it works

It asks first: the product, the one line viewers should walk away with, the visuals you have (cut-out product shots, photos, screenshots or screen recordings, a logo), a design-system link or HEX colors, the formats you need, and music. You then see the film's structure and a storyboard sheet, and nothing renders until you've signed off on both.

Rendering runs on [HyperFrames](https://www.npmjs.com/package/hyperframes). You get a 16:9 MP4 plus 9:16 and 1:1 versions rebuilt shot by shot, with text and object moved to fit each frame rather than cropped at the edges.

Twelve shot recipes do the building, among them a light sweeping across the object, a fake 3D orbit, a macro shot with a focus pull, an exploded view, a floating interface panel that zooms into a detail, and windows stacking up out of the depth. Screen recordings become stills, since the engine doesn't take video clips.

## What it won't do

Make up a number. A card waiting on a figure you didn't supply shows `[À FOURNIR]`, dimmed, until you fill it in. It won't go looking for music either: no file from you, no soundtrack.

![Twelve frames from the test film, a made-up app with French on-screen text](skills/sebmake-videopresentation-likeapplepls/assets/apercu-film-test.jpg)

## Install

As a Claude Code plugin:

```bash
claude plugin marketplace add sebmake/sebmake-videopresentation-likeapplepls
claude plugin install sebmake-videopresentation-likeapplepls@sebmake-video
```

Or copy `skills/sebmake-videopresentation-likeapplepls` into `~/.claude/skills/` by hand.

You'll need Node 22 or later, ffmpeg and Python 3.9 or later. `npx` fetches HyperFrames on the first render, and Google Fonts need a connection the first time. The `.skill` file in the latest release imports into Claude.ai, but rendering video takes a machine that runs Node and a browser, so Claude Code is the place to use it.

## Still rough

The example bundled with the skill goes from storyboard to finished renders in a little over a minute. The test film (a made-up app, four schematic screenshots, no music) drags: with so few visuals, text holds the screen 60% of the time, and the check now warns you when visuals run thin. Nobody has tried the physical-object recipes on a real product yet.

Release v1.0.0 carries the three test renders: 88 s in 16:9, 30 s vertical, 15 s square.

---

Not affiliated with, endorsed or sponsored by Apple Inc. Apple and Keynote are trademarks of Apple Inc., registered in the U.S. and other countries. MIT License.
