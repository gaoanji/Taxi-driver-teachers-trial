# Reading Taxi — Fun Reading Quiz

A motion-controlled taxi game featuring 12 English questions about books, authors and popular characters. Players steer around obstacles, answer questions and receive immediate feedback, with light Singlish passenger reactions.

This README describes the English release with the bottom-right camera preview and 16 collision reactions. It is a static website: no npm installation or build step is required.

## How to play

1. Click the original blue **开始游戏** button on the taxi cover. The Chinese cover artwork is retained intentionally; the setup screen and quiz are in English.
2. Allow camera access. Face the camera and keep both hands visible, as if holding a steering wheel. Use the bottom-right preview to check your hand position.
3. Enter your name and select a class. Choose **Start New Game**, or use the same name and class with **Continue Saved Game**.
4. Raise your **right hand** to steer left or choose the left answer. Raise your **left hand** to steer right or choose the right answer. Hold the direction for **5 seconds** to confirm an answer.
5. Read the feedback before continuing. Each question allows two attempts: **2 points** for a correct first attempt, **1 point** for a correct second attempt, and **0 points** after two incorrect answers. Maximum score: **24 points**.

The passenger has 16 collision reactions, including references to kopi, kaya toast and bubble tea. These are shuffled without repetition within each cycle. The game uses browser speech synthesis, prioritising a Singapore English voice when available; pronunciation and voice availability vary by device. Chrome is recommended for this version.

## Upload to GitHub Pages

1. **Extract the ZIP first.** Upload its contents, not the ZIP itself.
2. Put `index.html` directly in the repository root, with the complete `assets/` folder beside it. Do not move the asset subfolders to the root or change filenames.
3. Commit the files. For a first deployment, configure **Settings → Pages → Deploy from a branch → main → / (root)**.
4. Open the published HTTPS link, allow camera access and test the game.

For updates, replace the changed files. The camera-position and collision-dialogue update requires only `index.html`. If upgrading from a version without the crest, also upload `assets/landing/school-logo.png`.

## Included files

- `index.html`: page layout, styling, motion controls, question bank, scoring, speech, progress saving and result submission.
- `assets/`: original cover and start button, school crest, road and background artwork, taxi and obstacle images, and background music.

The separately supplied **English** `Code.gs` runs in Google Apps Script. It is not included in the game ZIP. Do not substitute the Chinese game's backend.

## Google Sheets and leaderboard

The English game connects to its dedicated Apps Script deployment using `GOOGLE_SCRIPT_URL` inside `index.html`. Keep the configured address and `GAME_ID = "fun-reading-taxi-en-12-v1"` unchanged when moving the same game to another host.

The supplied English backend creates:

- **TaxiProgress**: saved player progress.
- **TaxiResults**: completed sessions, including score, elapsed seconds, first-try accuracy, collisions and answer records.

After completing the quiz, the game submits the result and displays the top ten players, using each player's best session.

Ranking priority is:

1. Higher score.
2. Shorter completion time.
3. Fewer collisions.
4. Earlier submission order.

First-try accuracy is displayed but is not a separate ranking criterion. Repeating the submission of the same session does not add another attempt. Use **Resubmit score** if the final upload fails.

**This English release does not yet have a separate “View Leaderboard” button.** That feature was added to the Chinese version only. The English leaderboard appears after a successful final submission.

### Timing

The on-screen countdown and leaderboard time are different. The countdown controls the current stretch of the game; leaderboard time measures elapsed time from the start of the session.

Elapsed time includes reading feedback. It is not a pure driving timer. A cloud-resumed game retains its original start time, so time spent away can also count. For a fair teacher challenge, use **Start New Game** and complete the quiz in one sitting.

The current frontend recalculates elapsed time when retrying a failed final submission. A delayed successful retry may therefore include the waiting time. Local-only recovery does not preserve the start time consistently. Avoid using resumed sessions or delayed retries for precise timed comparisons.

### Connecting a new spreadsheet

If the current setup works, there is no need to redeploy it.

For a new database, open Apps Script from the new Google Sheet, paste the separately supplied English `Code.gs`, run **setup** and authorise it. Deploy it as a web app running as the owner, with access permitted for the intended players. Replace `GOOGLE_SCRIPT_URL` in `index.html` with the new deployment's `/exec` URL, then republish the HTML.

The spreadsheet itself does not need to be publicly shared. Do not put Google account credentials in the website files.

## Moving from another website

Local progress belongs to the browser and website origin. It does not automatically move to another domain. Keeping the same English backend, game ID, name and class allows the game to look for the same cloud progress.

Camera permission must be granted on the new website. Internet access is needed for the externally loaded hand-tracking software and cloud services. Local saving is a fallback, not a guarantee that a final score reached the leaderboard.

## Local preview

If Python is installed, open a terminal in the folder containing `index.html` and run:

```sh
python -m http.server 8000
```

Open <http://localhost:8000/> in Chrome and allow camera access. Use the published HTTPS URL for the actual activity.

## Checks after publishing

- Confirm the original cover, blue start button, BGSS crest and copyright line appear.
- Check that the camera preview is at the bottom right and remains visible when a question appears.
- Check steering, the five-second answer confirmation and English feedback.
- Listen for varied collision reactions; their text and spoken line should match.
- Complete one session using an identifiable test name, then confirm its score and seconds in **TaxiResults** and its result on the game screen. This creates a real test record.
- If the leaderboard fails, check the final-page error, Apps Script access settings and the English deployment URL. A successful local save does not confirm a successful cloud submission.

## Credits

© 2026 Bedok Green Secondary School · Designed by Miss Gao Anji · For Educational Use Only
