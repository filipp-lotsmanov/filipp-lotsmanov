Filipp Lotsmanov - portfolio site
=================================

Open index.html in a browser, or drop the whole folder on any static host
(Netlify, Vercel, GitHub Pages, Cloudflare Pages). No build step, no
dependencies, no server.

Fonts (Fraunces, Schibsted Grotesk, JetBrains Mono) load from Google Fonts,
so the page needs a network connection for its real typefaces. Offline it
falls back to Georgia / Helvetica / Consolas and still lays out correctly.

Two image slots are still empty. Each shows a labelled placeholder until
the file exists; nothing breaks in the meantime.

  assets/portrait.jpg      square 1:1, 920x920 or larger
                           circle-cropped, so keep the head centred
  assets/ot2.png           16:10, 1440x900 or larger
                           the Opentrons OT-2 with a petri dish loaded

The screenshots are object-fit: cover, so anything off-ratio is centre-
cropped. Keep critical UI away from the edges.

assets/resume-ci.png is 658x411, cropped from a 658x840 capture. It is
below the 1084x678 a 2x display wants, so it is slightly soft on Retina.
Re-shoot at 200% display scaling and full browser width to replace it.

assets/signlang.jpg was already exactly 16:10 (1264x790) and needed no
crop. Note the practice counter in that frame reads Correct 0 /
Accuracy 0.0%; re-shoot after a few correct letters to replace it.
