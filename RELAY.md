# How the relay works

The daily task renders a Short in a cloud container, which has no way to hand a file
to YouTube directly. This repo is the bridge.

1. The run commits the finished MP4 to `videos/<slug>.mp4` on the `relay` branch.
2. That makes it readable at
   `https://raw.githubusercontent.com/mudassar-saeed/otherwise-relay/relay/videos/<slug>.mp4`
3. Zapier's YouTube action fetches that URL and publishes the video.
4. The run appends a row to `_published.md` on `main` and force-pushes a fresh
   single-commit `relay` branch, so video history never accumulates.

The `relay` branch is rewritten every day on purpose - it holds one video at a time.
`main` holds only text: this file, the README and the published log.
