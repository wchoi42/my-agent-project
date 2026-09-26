# Paper Moon

A browser game where you launch paper stars at a drifting moon across a paper-cut night sky.

## How to Play

Click anywhere on the canvas to launch a paper star from the bottom center toward your cursor. You have **7 shots** per round. The moon drifts gently across the sky — aim where it's going, not where it is.

### Scoring

Each shot can earn up to **150 points** based on accuracy. The score is calculated as:

    points = round((1 - distance_from_center / moon_radius) * 150)

A dead-center hit earns 150 points. Grazing the edge earns close to 0. A miss earns nothing. Your total score is the sum across all 7 shots, giving a maximum possible score of **1050**.

After the round ends, enter your name and save your score to the persistent high-score table.

### Controls

- **Click** on the canvas to shoot a paper star
- After the round, type your name and click **Save** (or press Enter)
- Click **Play Again** to start a new round

## Setup and Running

Requires Node.js 22+.

```bash
npm install
npm start
```

The server listens on `http://127.0.0.1:3000` by default. Set the `PORT` environment variable to change:

```bash
PORT=8080 npm start
```

Open the server URL in a browser to play.

## API

- `GET /api/scores` — returns top 20 scores as JSON array, ordered by score descending
- `POST /api/scores` — submit a score. Body: `{"name": "string", "score": integer}`. Name must be 1-20 characters. Score must be an integer 0-10000.

## Persistence

Scores are stored in a SQLite database file (`scores.db` in the project directory). They survive server restarts. Set `DB_PATH` to change the database location.

## Hosting

- All page URLs are relative (works behind a reverse proxy with a path prefix)
- No external dependencies (CDNs, web fonts, etc.)
- No cookies, localStorage, or browser storage required
- CORS enabled for cross-origin requests including preflight
- The server serves the game page and API from a single process
