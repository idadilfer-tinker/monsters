# Monster Mirror (built 23 Sept 2026)

A clean rebuild that replaces Costume Conjurer, whose camera view kept going wrong. Built the same way as Glimmer (the pose game for Ida's mum). Everything is in one HTML file: `monster-mirror.html`.

## How it works
- **Mirror:** a portrait mirror that is always the same size (sized by one limit, the Glimmer way). The camera zooms and moves itself to fit the child's whole body, with room at the top for a hat. It follows them smoothly whether they stand near, far or off to one side.
- **Tracking:** only the body tracker (MediaPipe Pose, accurate version, switching to the fast one if needed). Eyes, mouth, hat, cape, costume and held items all attach to body points, and their size comes from the child's own face and shoulder width, so it looks right at any distance.
- **Pointing:** raise either hand. The pointer is measured against the child's own shoulders, not the camera picture, so it has nothing to do with how big the mirror is drawn. Hold on a bubble for about 1 second to pick it. A hand hanging down counts as resting.
- **Voice:** Chrome speech recognition in en-GB, always listening. It understands item names and nicknames, "take off the hat", "take everything off", "surprise me", "cheese" (photo), "next", and category names. When several names match, the longest one wins. One-word names only act once the phrase is finished, so "red" doesn't trigger before "red lips". The mirror says the item's name back and ignores the mic while it's talking.
- **Parts (54):**
  - 8 eyes
  - 16 mouths
  - 12 hats, crowns and antennae
  - 6 face paints drawn in code: cat, skull, zombie, pumpkin cheeks, spider web and sparkles
  - 8 full-body costumes plus a cape. Costume backgrounds were removed, and a soft hole is cut out so the child's face shows through.
  - 3 magic items (lantern, potion, eye staff), held in the hand that isn't pointing
- **Photo:** "Cheese" or the button starts a 3-2-1 countdown, then shows a framed photo card you can save.
- **If something fails:** with no camera, or if the tracker won't load, it switches to mouse control on a practice figure.
- **Settings drawer:** control, hand, reach, hold time, steadiness, voice, talk-back, sound, tracking model, and showing the tracking dots.

## Testing
51/51 headless checks pass on a fake skeleton at 4 screen sizes, and a check with the real MediaPipe library confirms the fallback. Real-camera tracking and the placement of each part still need tuning in the first live session.

## Open
- Placement numbers for each part (sizes and lifts in `02_catalog.js`) are a first pass.
- Voice needs the internet (Chrome sends the audio to Google).
- Could add FaceLandmarker for sharper face-paint placement in close-up.
