# MunchMatch — First Three Screens

**Live prototype:** https://first-three-screens-rho.vercel.app/
**Repository:** https://github.com/kmetler/First-Three-Screens

MunchMatch is a group decision-making app for choosing where to eat. A group swipes yes/no on nearby restaurants from their own phones; when enough of the group swipes yes on the same place, it's revealed to everyone as the pick.

---

## 1. Need, Persona, Capability, Value

**Need:** When a group can't agree where to eat, they default to back-and-forth texting or vague suggestions, and burn 20–30 minutes before anyone commits.

**Persona:** A friend group of 3–6, meeting up after class 2–3x/week. Everyone's hungry and a little impatient. No one wants to be the one who picks (and gets blamed if it's bad).

**Capability:** Get a group to quickly agree on a restaurant.

**Fundamental Value:** Speed and effortless consensus. The group skips the 20–30 minutes of back-and-forth, and no single person has to own the decision — or the risk of it being a bad one.

## 2. The Three Screens

| Screen           | Job                                                                                                                                 | Design question it answers                                                                                 |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Landing**      | Signal the core value ("Nobody has to pick") and the primary capability (swipe to pick where to eat) before any reading is required | Does a first-time user grasp what this does and why it's better, at a glance?                              |
| **Swipe screen** | Show one restaurant at a time (photo, name, tags, description, live group progress) with a clear yes/no action                      | Are the restaurant info and the decision visually grouped so it reads as one unit, not scattered elements? |
| **Match reveal** | Show the restaurant the group landed on, framed explicitly as a group outcome, with a clear next action                             | Does this moment read as "we decided," and can the user act on it or get back to the group from here?      |

## 3. Feedback Question Plan

| Group      | Question (as I'd ask the persona)                                                                                                                       | Prediction                                                                              | What it tests                                                                      |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Need       | "Walk me through the last time your group couldn't agree on where to eat — what actually happened?"                                                     | Long group-text thread, or someone gives in and picks wherever they were craving        | Whether "Nobody has to pick" names a pain they recognize                           |
| Value      | "If your group could land on a place everyone's okay with in about two minutes instead of twenty, would that actually matter, or is it not a big deal?" | Yes — but mostly because it removes the awkwardness of picking, not just the time saved | Whether "speed" or "shared responsibility" is the real value driver                |
| Persona    | "How often does this come up for your friend group, and is it usually right after class when everyone's already hungry?"                                | 2–3x/week, right after class                                                            | Whether the "Thursday crew" / timing assumptions match real behavior               |
| Capability | (Show swipe screen 5 seconds, hide it) "What do you think this does?"                                                                                   | "You swipe on restaurants, like Tinder"                                                 | Whether the photo + heart/X icons communicate the capability with zero explanation |
| Capability | (Show match reveal screen) "What would you tap first, and what do you expect happens?"                                                                  | Taps the red "Directions" button over "Back to group" or "Keep swiping"                 | Whether color/weight hierarchy signals the correct primary action                  |

## 4. Design Justification and First Read

**Does the landing screen signal the primary capability and fundamental value at first glance, before reading?**
Yes. The dominant visual is a restaurant photo mid-swipe with heart/X icons visible before any body text is read, and the headline "Nobody has to pick" states the value in four words. The supporting paragraph explains the mechanic for anyone who needs more, but isn't required to get the gist.

**Does every element on the landing screen earn its place, or does anything compete with the primary job?**
Mostly yes, with one earlier issue: the original build placed two unlabeled colored dots next to the wordmark with no stated purpose. They didn't compete with the primary message directly, but they were a distraction — an element with no job, sitting right next to the logo, that a first-time user has no way to interpret. See before/after below.

**What information and actions belong together on each screen, and which Gestalt principle communicates that?**

- **Swipe screen:** the restaurant photo, name, tags, and description are stacked with tight spacing and separated from the yes/no buttons by whitespace — **proximity** groups "info about this place" as one unit and "your decision" as a separate one.
- **Match reveal screen:** the group's avatars are colored circles clustered together above "All 5 swiped yes" — **similarity** (same shape, consistent color coding) reads them as one group identity rather than five separate people.
- **Card containers themselves:** the light card background against the dark app background uses **figure/ground** to keep the current restaurant the clear focal point on every screen.

**Do screens 2 and 3 stay on mission, and can you return to the landing screen from everywhere?**
Yes. Both are the product actively working (swiping, then the group result) rather than settings or setup. Navigation back to the landing/group screen exists on both — this was in fact one of the fixes made after reviewing the first AI output (see below).

**What did the AI initially get wrong, skip, or oversimplify, and what did you change?**

1. **No logo, and two unexplained dots** next to the wordmark — visually distracting with no signaling purpose. Replaced with an actual heart-badge logo mark tied to the brand.
2. **Missing navigation** — the swipe and match-reveal screens had no way back to the landing/group screen except the browser back button, breaking the "reachable from everywhere" requirement.
3. **Text sizing on the match reveal screen** — "THE GROUP PICKED" was undersized relative to its importance as the payoff moment of the whole app, so it faded into the background instead of announcing the result. Increased its size so it reads as the headline it should be.

**Before / after:**
Initial make:
!(First_Build.png)

Initial commit (unedited AI output): https://github.com/kmetler/First-Three-Screens/commit/605523ebf1b226bdda0b9643079bacec9eca47c1
!(Second_Build.png)

Final make:
!(Final_Build.png)

Before: header showed two unlabeled colored dots next to plain "MunchMatch" text, with no back-navigation on the swipe or match screens.
After: dots replaced with a heart-badge logo; back-navigation added to both secondary screens; "THE GROUP PICKED" enlarged for visibility.

The core problem in the original: elements with no clear job (the dots) sat directly next to elements with a critical job (the logo/wordmark), no clear way to get back to the landing page (navigation buttons added), and an element with a critical job (the reveal headline) was undersized relative to its importance — both are signaling failures, not just aesthetic ones.
