# Noted! — Team Hinton

**IST 303 – Intro to Software Development · Fall 2026 · Claremont Graduate University**

**Noted!** is a lightweight Flask web app for writing music one note at a time. Users create a piece, pick a key, time signature, and tempo, add notes and rests, and see the result drawn as standard sheet music. Pieces are saved to the user's account in a personal library. Full concept: [proposal/proposal.md](proposal/proposal.md).

## Team Members

| Initials | Name |
|---|---|
| DA | Daniel Abalusi |
| VS | Varuzhan Shahidzadeh |
| YX | Yalei Xu |
| BG | Beijia Gu |
| RM | Ryan Miller |

Each member has about **10 hours per week** for the project.

## Project Schedule

| Part | Due | Points | What's due |
|---|---|---|---|
| A | Thu Oct 1, 2026 | 60 | GitHub repo with README: team members, user stories (estimates and acceptance criteria), tasks, who does what, iteration 1 plan |
| B | Thu Oct 15, 2026 (Week 6) | 80 | End of iteration 1: burndown chart, stand-up evidence, working code and tests, retrospective, iteration 2 plan |
| C | Thu Nov 12, 2026 (Week 10) | 180 | Milestone 1.0: class presentation with live demo and evidence of agile process; final codebase |

| Iteration | Dates | Length |
|---|---|---|
| Iteration 1 | Thu Oct 1 – Wed Oct 14, 2026 | 2 weeks |
| Iteration 2 | Thu Oct 15 – Wed Nov 11, 2026 | 4 weeks |
| Milestone 1.0 demo | Thu Nov 12, 2026 | |

---

# Part A

## 1. Concept

See the [project proposal](proposal/proposal.md). In short: professional notation software is expensive and hard to learn, and quick alternatives (staff paper, voice memos, letter names in a notes app) are hard to edit, share, or play back. Noted! fills that gap with simple, note-by-note entry and server-rendered sheet music. Milestone 1.0 supports a single treble-clef staff; playback, PDF export, more clefs, sharing, audio transcription, and a practice mode are stretch goals.

## 2. Stakeholders

| Stakeholder | What they need from Noted!  |
|---|---|
| **End users: students** | Music students learning to read and write notation | Easy note entry, correct notation, a place to keep exercises | High (primary users) |
| **End users: hobbyists and songwriters** | People who want to jot down a melody quickly | Fast entry, saved library, playback (stretch) | High (primary users) |
| **Music educators** | Teachers who assign and review student work | Printable/exportable pieces, sharing, practice feedback (stretch) | Medium (secondary users) |
| **Course instructor (customer / product owner)** | IST 303 instructor | A Flask app with a data store, agile process evidence, working tested code, on-time milestones | High (sets requirements and grades) |
| **Development team (Team Hinton)** | The five team members | Clear stories, realistic workload, a maintainable codebase, learning outcomes | High (builds the product) |
| **Classmates** | Audience for the Milestone 1.0 demo | A clear demo and explanation of the agile process | Low |
| **Open-source maintainers** | Flask, Flask-SQLAlchemy, Flask-Login, music21, pytest | Dependencies we rely on; their licenses and release changes affect us | Low (indirect) |

## 3. User Stories

### Summary

| ID | Story | Priority | Estimate (hrs) | Iteration |
|---|---|---|---|---|
| E-01 | Project foundation | Must | 16 | 1 |
| US-01 | Register an account | Must | 8 | 1 |
| US-02 | Log in and log out | Must | 9 | 1 |
| US-03 | Create a composition | Must | 10 | 1 |
| US-04 | Add notes one at a time | Must | 18 | 1 |
| US-05 | Add rests | Must | 5 | 2 (planned) |
| SP-01 | Rendering spike | Must | 4 | 1 |
| US-06 | See the sheet music | Must | 17 | 2 (planned) |
| US-10 | My Library: list and open | Must | 8 | 2 (planned) |
| US-07 | Edit a note | Must | 8 | 2 (planned) |
| US-08 | Delete a note | Must | 5 | 2 (planned) |
| US-09 | Rename or delete a composition | Must | 7 | 2 (planned) |
| US-11 | Search my library | Should | 6 | 2 (planned) |
| US-12 | Keep my compositions private | Must | 6 | 2 (planned) |
| US-13 | Play back my composition | Stretch | 14 | 2 (planned) |
| US-14 | Export to PDF | Stretch | 10 | 2 (planned) |
| US-15 | Use other clefs | Stretch | 14 | 2 (planned) |
| US-16 | Share a composition | Stretch | 12 | 2 (planned) |
| US-17 | Transcribe a recording | Stretch | 40 | Backlog |
| US-18 | Practice mode | Stretch | 36 | Backlog |

**Total backlog:** 253 ideal hours.

### Story details and acceptance criteria

#### E-01 — Project foundation

As the **development team**, we want a working Flask skeleton, database, and test setup so that every feature story has a stable base to build on.

**Priority:** Must · **Estimate:** 16 hrs

**Acceptance criteria**

- [ ] Running `flask run` serves a home page with the shared layout.
- [ ] `flask init-db` creates the SQLite database with `User`, `Composition`, and `Note` tables.
- [ ] `pytest --cov` runs and reports coverage, with at least one passing test.
- [ ] The GitHub repo has a README, a task board, and a protected `main` branch that requires a pull request.

#### US-01 — Register an account

As a **new user**, I want to create an account with a username, email, and password so that my compositions are saved under my name.

**Priority:** Must · **Estimate:** 8 hrs

**Acceptance criteria**

- [ ] Given a unique username and email and a password of 8+ characters, submitting the form creates the account and logs me in.
- [ ] A duplicate username or email shows an error and no account is created.
- [ ] Passwords are stored hashed, never in plain text.
- [ ] Missing or invalid fields show a message next to the field.

#### US-02 — Log in and log out

As a **registered user**, I want to log in and out so that only I can reach my compositions.

**Priority:** Must · **Estimate:** 9 hrs

**Acceptance criteria**

- [ ] Correct credentials log me in and send me to My Library.
- [ ] Wrong credentials show "Invalid username or password" and do not log me in.
- [ ] Logging out ends the session and returns me to the home page.
- [ ] Visiting a protected page while logged out redirects to the login page.

#### US-03 — Create a composition

As a **songwriter**, I want to start a new piece by choosing a title, key signature, time signature, and tempo so that my notes are written in the right musical context.

**Priority:** Must · **Estimate:** 10 hrs

**Acceptance criteria**

- [ ] The form offers all 15 major keys, time signatures 2/4, 3/4, 4/4, and 6/8, and a tempo from 40 to 240 BPM.
- [ ] Submitting a valid form creates a composition owned by me and opens it in the editor.
- [ ] A blank title or out-of-range tempo shows an error and nothing is saved.
- [ ] The editor shows the title, key, time signature, and tempo I chose.

#### US-04 — Add notes one at a time

As a **music student**, I want to add notes by choosing pitch, octave, duration, and an accidental so that I can write out a melody.

**Priority:** Must · **Estimate:** 18 hrs

**Acceptance criteria**

- [ ] I can choose pitch A–G, an octave, a duration (whole, half, quarter, eighth, sixteenth), and sharp, flat, or natural.
- [ ] Clicking **Add** appends the note to the end of the piece and it stays after a page reload.
- [ ] Notes outside the treble-clef range (A3–C6) are rejected with a message.
- [ ] The piece converts to a valid music21 `Stream` with the notes in order.

#### US-05 — Add rests

As a **songwriter**, I want to add rests of any duration so that my piece has the right rhythm.

**Priority:** Must · **Estimate:** 5 hrs

**Acceptance criteria**

- [ ] A **Rest** option is available for every duration.
- [ ] Rests are saved in order with notes and appear on the staff.
- [ ] Rests convert to music21 `Rest` objects.

#### SP-01 — Rendering spike

As the **development team**, we want to test how to draw sheet music in Python before building US-06 so that we pick an approach that works and lower the risk to our Milestone 1.0 demo.

**Priority:** Must · **Estimate:** 4 hrs

**Acceptance criteria**

- [ ] We have tried music21 with an external renderer (LilyPond or MuseScore) and drawing our own SVG in Python.
- [ ] A prototype draws a treble staff with at least three notes as SVG from Python code.
- [ ] The chosen approach, its install steps, and why we chose it are written up in `docs/rendering-spike.md`.
- [ ] The approach runs on every team member's machine.

#### US-06 — See the sheet music

As a **user**, I want my piece drawn as standard sheet music on a treble staff so that I can read and check what I wrote.

**Priority:** Must · **Estimate:** 17 hrs

**Acceptance criteria**

- [ ] The editor shows a five-line staff with a treble clef, key signature, and time signature.
- [ ] Each note sits on the correct line or space with the correct head, stem, and flag for its duration; accidentals are shown.
- [ ] Bar lines appear where each measure fills up for the chosen time signature.
- [ ] The staff updates right after a note or rest is added.
- [ ] The SVG is generated on the server in Python.

#### US-10 — My Library: list and open

As a **returning user**, I want to see a list of my saved compositions and open one so that I can keep working on it.

**Priority:** Must · **Estimate:** 8 hrs

**Acceptance criteria**

- [ ] My Library lists only my compositions, newest edit first, with title, key, time signature, and last-edited date.
- [ ] Clicking a title opens it in the editor.
- [ ] With no compositions, the page shows "No compositions yet" and a **New composition** button.

#### US-07 — Edit a note

As a **user**, I want to change a note's pitch, octave, duration, or accidental so that I can fix mistakes without re-entering the piece.

**Priority:** Must · **Estimate:** 8 hrs

**Acceptance criteria**

- [ ] Clicking a note on the staff (or in the note list) selects it and fills the palette with its values.
- [ ] Saving updates only that note; the staff redraws.
- [ ] Invalid values are rejected as in US-04.

#### US-08 — Delete a note

As a **user**, I want to remove a note or rest so that I can clean up my piece.

**Priority:** Must · **Estimate:** 5 hrs

**Acceptance criteria**

- [ ] Deleting a note removes it and the remaining notes keep their order.
- [ ] The staff redraws without the note.

#### US-09 — Rename or delete a composition

As a **user**, I want to rename a piece, change its settings, or delete it so that my library stays organized.

**Priority:** Must · **Estimate:** 7 hrs

**Acceptance criteria**

- [ ] I can change the title, key, time signature, and tempo; the staff redraws.
- [ ] Deleting asks for confirmation, then removes the composition and its notes.
- [ ] The deleted piece no longer appears in My Library.

#### US-11 — Search my library

As a **user with many pieces**, I want to search my library by title so that I can find a piece quickly.

**Priority:** Should · **Estimate:** 6 hrs

**Acceptance criteria**

- [ ] Typing part of a title returns matching compositions, ignoring case.
- [ ] Only my compositions are searched.
- [ ] No matches shows "No compositions match".

#### US-12 — Keep my compositions private

As a **user**, I want my compositions hidden from other users so that my work stays mine.

**Priority:** Must · **Estimate:** 6 hrs

**Acceptance criteria**

- [ ] Opening, editing, or deleting another user's composition by URL returns 404.
- [ ] Every composition and note route checks ownership.

#### US-13 — Play back my composition

As a **songwriter**, I want to hear my piece played back so that I can check that it sounds right.

**Priority:** Stretch · **Estimate:** 14 hrs

**Acceptance criteria**

- [ ] A **Play** button plays the piece in the browser at the chosen tempo.
- [ ] Audio is generated in Python on the server.
- [ ] Audio is regenerated after the piece changes.

#### US-14 — Export to PDF

As a **music teacher**, I want to download a piece as a PDF so that I can print it or hand it out.

**Priority:** Stretch · **Estimate:** 10 hrs

**Acceptance criteria**

- [ ] An **Export PDF** button downloads a PDF with the title and the full staff.
- [ ] The PDF matches what the editor shows.

#### US-15 — Use other clefs

As a **bass or viola player**, I want to write in bass, alto, or tenor clef so that the music matches my instrument.

**Priority:** Stretch · **Estimate:** 14 hrs

**Acceptance criteria**

- [ ] I can choose treble, bass, alto, or tenor clef when creating or editing a piece.
- [ ] Notes are placed correctly for the chosen clef.
- [ ] The note range check follows the chosen clef.

#### US-16 — Share a composition

As a **user**, I want to share a piece with another user so that they can view it.

**Priority:** Stretch · **Estimate:** 12 hrs

**Acceptance criteria**

- [ ] I can share a piece by entering another user's username.
- [ ] The other user sees it under "Shared with me" and can view it but not edit it.
- [ ] I can stop sharing at any time.

#### US-17 — Transcribe a recording

As a **musician**, I want to upload a recording of a single instrument and get sheet music back so that I don't have to write it out by ear.

**Priority:** Stretch · **Estimate:** 40 hrs

**Acceptance criteria**

- [ ] I can upload a WAV or MP3 of one instrument (up to 60 seconds).
- [ ] The app creates a new composition with the detected notes and rhythms.
- [ ] On a clean test recording of a simple melody, at least 80% of pitches are correct.

#### US-18 — Practice mode

As a **music educator**, I want to assign a piece and have the app compare a student's recording with it so that students get feedback on wrong notes and timing.

**Priority:** Stretch · **Estimate:** 36 hrs

**Acceptance criteria**

- [ ] An educator can assign a piece to a student.
- [ ] The student can upload a recording of themselves playing it and hear it back.
- [ ] The app highlights wrong notes and notes that are early or late.

## 4. Tasks

Every story is broken into tasks. Owners are assigned for iteration 1 only; iteration 2 owners will be assigned in Part B.

### E-01 — Project foundation (16 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| E-01-T1 | Set up GitHub repo, branch protection, Projects task board, README skeleton | 2 | DA |
| E-01-T2 | Create Flask app factory, config, and blueprints (auth, compositions, library) | 3 | DA |
| E-01-T3 | Define SQLAlchemy models `User`, `Composition`, `Note` and an `init-db` command | 5 | YX |
| E-01-T4 | Configure pytest + pytest-cov with fixtures (test client, in-memory DB, logged-in user) | 3 | YX |
| E-01-T5 | Build base Jinja layout: nav bar, flash messages, CSS | 3 | VS |

### US-01 — Register an account (8 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-01-T1 | Registration form template | 2 | RM |
| US-01-T2 | Register route with validation (unique username/email, password rules) | 2 | DA |
| US-01-T3 | Hash passwords with Werkzeug and save the user | 1 | DA |
| US-01-T4 | Tests: success, duplicate user, bad input, password is hashed | 3 | RM |

### US-02 — Log in and log out (9 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-02-T1 | Integrate Flask-Login and the user loader | 2 | DA |
| US-02-T2 | Login form and route with error message | 2 | DA |
| US-02-T3 | Logout route and nav bar that changes when logged in | 1 | DA |
| US-02-T4 | Apply `@login_required` to all composition and library routes | 1 | DA |
| US-02-T5 | Tests: good login, bad login, logout, protected-page redirect | 3 | RM |

### US-03 — Create a composition (10 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-03-T1 | New-composition form (title, key, time signature, tempo) | 3 | BG |
| US-03-T2 | Create route: validate and save the composition with the current user as owner | 2 | YX |
| US-03-T3 | Composition editor page shell (header, staff area, note-entry area) | 3 | VS |
| US-03-T4 | Tests: valid create, missing title, tempo out of range, owner is set | 2 | RM |

### US-04 — Add notes one at a time (18 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-04-T1 | Note ordering and storage logic (position index per composition) | 3 | BG |
| US-04-T2 | Note-entry palette UI: pitch, octave, duration, accidental buttons | 5 | VS |
| US-04-T3 | Add-note route that appends to the composition | 2 | YX |
| US-04-T4 | Treble-clef range validation (A3–C6) | 2 | RM |
| US-04-T5 | Service that converts a composition to a music21 Stream | 3 | BG |
| US-04-T6 | Tests: add note, order kept, out-of-range rejected, music21 conversion | 3 | BG |

### US-05 — Add rests (5 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-05-T1 | Add Rest option to the note palette | 1 | — |
| US-05-T2 | Store rests (note with no pitch) in order | 1 | — |
| US-05-T3 | Handle rests in the music21 conversion and the renderer | 1 | — |
| US-05-T4 | Tests: add rest, rest in conversion, rest in rendered SVG | 2 | — |

### SP-01 — Rendering spike (4 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| SP-01-T1 | Try music21 with LilyPond/MuseScore SVG export | 2 | VS |
| SP-01-T2 | Prototype a custom SVG staff with a few notes in Python | 1 | RM |
| SP-01-T3 | Write up the decision and install steps in docs/rendering-spike.md | 1 | VS |

### US-06 — See the sheet music (17 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-06-T1 | Draw staff, treble clef, key signature, and time signature as SVG | 5 | — |
| US-06-T2 | Place notes: vertical position by pitch, heads/stems/flags by duration, accidentals | 6 | — |
| US-06-T3 | Insert bar lines based on time signature | 2 | — |
| US-06-T4 | Embed the SVG in the editor and refresh it after each change | 1 | — |
| US-06-T5 | Tests: SVG structure (line count, note positions, bar lines) | 3 | — |

### US-10 — My Library: list and open (8 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-10-T1 | Library route: query the current user's compositions by last-modified | 2 | — |
| US-10-T2 | Library template (list with title, key, time signature, date) | 2 | — |
| US-10-T3 | Link each item to its editor | 1 | — |
| US-10-T4 | Empty-state message and button | 1 | — |
| US-10-T5 | Tests: lists only my pieces, sort order, empty state | 2 | — |

### US-07 — Edit a note (8 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-07-T1 | Selectable notes in the editor | 2 | — |
| US-07-T2 | Edit form pre-filled with the note's values | 2 | — |
| US-07-T3 | Update route with validation | 2 | — |
| US-07-T4 | Tests | 2 | — |

### US-08 — Delete a note (5 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-08-T1 | Delete control on the selected note | 1 | — |
| US-08-T2 | Delete route and re-index positions | 2 | — |
| US-08-T3 | Tests | 2 | — |

### US-09 — Rename or delete a composition (7 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-09-T1 | Edit-settings form | 2 | — |
| US-09-T2 | Delete with confirmation; cascade-delete notes | 2 | — |
| US-09-T3 | Update and delete routes | 1 | — |
| US-09-T4 | Tests | 2 | — |

### US-11 — Search my library (6 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-11-T1 | Search box on My Library | 1 | — |
| US-11-T2 | Case-insensitive title query scoped to the user | 2 | — |
| US-11-T3 | No-results message | 1 | — |
| US-11-T4 | Tests | 2 | — |

### US-12 — Keep my compositions private (6 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-12-T1 | Ownership-check helper used on every composition route | 2 | — |
| US-12-T2 | Return 404 for non-owners | 1 | — |
| US-12-T3 | Tests: cross-user access attempts on every route | 3 | — |

### US-13 — Play back my composition (14 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-13-T1 | Spike: generate audio in Python (music21 MIDI, simple synth to WAV) | 4 | — |
| US-13-T2 | Generate audio from the composition at its tempo | 4 | — |
| US-13-T3 | HTML audio player in the editor | 2 | — |
| US-13-T4 | Regenerate audio when the piece changes | 1 | — |
| US-13-T5 | Tests | 3 | — |

### US-14 — Export to PDF (10 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-14-T1 | Choose SVG-to-PDF approach (e.g. CairoSVG or ReportLab) | 2 | — |
| US-14-T2 | Build the PDF with a title header and the staff | 4 | — |
| US-14-T3 | Download route | 1 | — |
| US-14-T4 | Tests | 3 | — |

### US-15 — Use other clefs (14 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-15-T1 | Add a clef field to Composition | 2 | — |
| US-15-T2 | Clef selector on the forms | 1 | — |
| US-15-T3 | Draw bass, alto, and tenor clef symbols | 4 | — |
| US-15-T4 | Pitch-to-staff mapping per clef | 3 | — |
| US-15-T5 | Range validation per clef | 1 | — |
| US-15-T6 | Tests | 3 | — |

### US-16 — Share a composition (12 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-16-T1 | Share model (composition, user, read-only) | 2 | — |
| US-16-T2 | Share form by username | 2 | — |
| US-16-T3 | "Shared with me" section | 3 | — |
| US-16-T4 | View-only permission checks | 2 | — |
| US-16-T5 | Tests | 3 | — |

### US-17 — Transcribe a recording (40 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-17-T1 | Spike: pitch detection in Python (e.g. librosa pYIN) | 6 | — |
| US-17-T2 | Upload form and file validation | 3 | — |
| US-17-T3 | Onset detection and pitch tracking | 10 | — |
| US-17-T4 | Quantize durations to the tempo | 8 | — |
| US-17-T5 | Convert results into a new composition | 5 | — |
| US-17-T6 | Tests with sample recordings | 8 | — |

### US-18 — Practice mode (36 hrs)

| Task | Description | Est. (hrs) | Owner |
|---|---|---|---|
| US-18-T1 | Educator role and assignment model | 6 | — |
| US-18-T2 | Record/upload an attempt and play it back | 4 | — |
| US-18-T3 | Align the attempt with the written piece (uses US-17) | 12 | — |
| US-18-T4 | Feedback view highlighting wrong notes and timing | 8 | — |
| US-18-T5 | Tests | 6 | — |

## 5. Iteration 1 Plan

**Iteration 1:** Thu Oct 1 – Wed Oct 14, 2026 (2 weeks, ends at the Part B deadline) · **Iteration 2:** Thu Oct 15 – Wed Nov 11, 2026 (4 weeks) · **Milestone 1.0 demo (Part C):** Thu Nov 12, 2026

### Velocity and capacity

| | |
|---|---|
| Team members | 5 |
| Hours per member per week | 10 |
| Weeks per iteration | 2 |
| Available hours (5 × 10 × 2) | **100** |
| Velocity (first iteration, no history) | **0.7** |
| Capacity (100 × 0.7) | **70 ideal hours** |
| Planned for iteration 1 | **65 ideal hours** |
| Buffer | **5 hours** |

Because this is our first iteration we have no measured velocity, so we start with the standard **0.7**: about 30% of our time will go to meetings, stand-ups, code review, learning Flask and music21, and setup problems. Iteration 1 is only two weeks (it ends at the Part B deadline), so we could not fit **US-06 (rendering sheet music)**, our riskiest story. Instead we added **SP-01**, a 4-hour spike to test rendering approaches now, so US-06 can start on day one of iteration 2 with a proven approach. To make room, **US-10 (My Library)** moves to iteration 2. That brings iteration 1 to 65 hours, leaving a 5-hour buffer. At the end of iteration 1 we will measure our real velocity (ideal hours completed ÷ hours available) and use it to plan iteration 2.

### Stories in iteration 1

| ID | Story | Estimate (hrs) |
|---|---|---|
| E-01 | Project foundation | 16 |
| US-01 | Register an account | 8 |
| US-02 | Log in and log out | 9 |
| US-03 | Create a composition | 10 |
| US-04 | Add notes one at a time | 18 |
| SP-01 | Rendering spike | 4 |
| | **Total** | **65** |

**Iteration 1 goal:** a user can register, log in, create a composition, and add notes to it, and we have a tested prototype and a decision on how to draw sheet music. This gives us working code and tests to show at Part B.

### Tentative iteration 2 plan (to be revised in Part B)

| ID | Story | Priority | Estimate (hrs) |
|---|---|---|---|
| US-05 | Add rests | Must | 5 |
| US-06 | See the sheet music | Must | 17 |
| US-10 | My Library: list and open | Must | 8 |
| US-07 | Edit a note | Must | 8 |
| US-08 | Delete a note | Must | 5 |
| US-09 | Rename or delete a composition | Must | 7 |
| US-11 | Search my library | Should | 6 |
| US-12 | Keep my compositions private | Must | 6 |
| US-13 | Play back my composition | Stretch | 14 |
| US-14 | Export to PDF | Stretch | 10 |
| US-15 | Use other clefs | Stretch | 14 |
| US-16 | Share a composition | Stretch | 12 |
| | **Total** | | **112** |

Iteration 2 is four weeks: 5 × 10 × 4 = 200 available hours, or **140 ideal hours** at velocity 0.7. The plan above uses 112, leaving about 28 hours for work carried over from iteration 1 and for preparing the Milestone 1.0 presentation. US-06 (rendering) goes first, building on the SP-01 spike, because the demo depends on it. Stretch stories will be dropped first if our measured velocity is lower. US-17 (transcription) and US-18 (practice mode) stay in the backlog for Milestone 2.0.

## 6. Iteration 1 Task Allocation

Target per person: about 13 ideal hours (capacity per person: 14).

| Member | Focus | Tasks | Total (hrs) |
|---|---|---|---|
| Daniel Abalusi (DA) | Repo setup, Flask skeleton, accounts and login | E-01-T1, E-01-T2, US-01-T2, US-01-T3, US-02-T1, US-02-T2, US-02-T3, US-02-T4 | 14 |
| Varuzhan Shahidzadeh (VS) | Base layout, editor page, note palette, rendering spike (music21 test, write-up) | E-01-T5, US-03-T3, US-04-T2, SP-01-T1, SP-01-T3 | 14 |
| Yalei Xu (YX) | Database models, test setup, data routes | E-01-T3, E-01-T4, US-03-T2, US-04-T3 | 12 |
| Beijia Gu (BG) | Composition form, note storage, music21 conversion | US-03-T1, US-04-T1, US-04-T5, US-04-T6 | 12 |
| Ryan Miller (RM) | Test lead: registration form, story tests, note-range validation, SVG staff prototype | US-01-T1, US-01-T4, US-02-T5, US-03-T4, US-04-T4, SP-01-T2 | 13 |
| **Team** | | | **65** |

### Detailed allocation

**Daniel Abalusi (DA) — 14 hrs**

- E-01-T1: Set up GitHub repo, branch protection, Projects task board, README skeleton (2 h)
- E-01-T2: Create Flask app factory, config, and blueprints (auth, compositions, library) (3 h)
- US-01-T2: Register route with validation (unique username/email, password rules) (2 h)
- US-01-T3: Hash passwords with Werkzeug and save the user (1 h)
- US-02-T1: Integrate Flask-Login and the user loader (2 h)
- US-02-T2: Login form and route with error message (2 h)
- US-02-T3: Logout route and nav bar that changes when logged in (1 h)
- US-02-T4: Apply `@login_required` to all composition and library routes (1 h)

**Varuzhan Shahidzadeh (VS) — 14 hrs**

- E-01-T5: Build base Jinja layout: nav bar, flash messages, CSS (3 h)
- US-03-T3: Composition editor page shell (header, staff area, note-entry area) (3 h)
- US-04-T2: Note-entry palette UI: pitch, octave, duration, accidental buttons (5 h)
- SP-01-T1: Try music21 with LilyPond/MuseScore SVG export (2 h)
- SP-01-T3: Write up the decision and install steps in docs/rendering-spike.md (1 h)

**Yalei Xu (YX) — 12 hrs**

- E-01-T3: Define SQLAlchemy models `User`, `Composition`, `Note` and an `init-db` command (5 h)
- E-01-T4: Configure pytest + pytest-cov with fixtures (test client, in-memory DB, logged-in user) (3 h)
- US-03-T2: Create route: validate and save the composition with the current user as owner (2 h)
- US-04-T3: Add-note route that appends to the composition (2 h)

**Beijia Gu (BG) — 12 hrs**

- US-03-T1: New-composition form (title, key, time signature, tempo) (3 h)
- US-04-T1: Note ordering and storage logic (position index per composition) (3 h)
- US-04-T5: Service that converts a composition to a music21 Stream (3 h)
- US-04-T6: Tests: add note, order kept, out-of-range rejected, music21 conversion (3 h)

**Ryan Miller (RM) — 13 hrs**

- US-01-T1: Registration form template (2 h)
- US-01-T4: Tests: success, duplicate user, bad input, password is hashed (3 h)
- US-02-T5: Tests: good login, bad login, logout, protected-page redirect (3 h)
- US-03-T4: Tests: valid create, missing title, tempo out of range, owner is set (2 h)
- US-04-T4: Treble-clef range validation (A3–C6) (2 h)
- SP-01-T2: Prototype a custom SVG staff with a few notes in Python (1 h)

### Working agreements

- Weekly stand-up (minutes logged in `meetings/`), plus async updates in the team chat.
- Each task is a GitHub issue on the Projects board, moved To do → In progress → Review → Done.
- Work on a feature branch; merge to `main` by pull request with one reviewer and passing tests.
- Log hours remaining on each task so we can draw the iteration 1 burndown chart for Part B.
