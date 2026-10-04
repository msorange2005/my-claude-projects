---
name: fantasy-lineup-helper
description: Recommends optimal weekly fantasy football starting lineup with detailed per-player reasoning, plus waiver-wire suggestions. Use when the user provides their roster, opponent's roster, and asks for lineup help.
---

# Fantasy Lineup Helper

## What this skill does
Given a user's roster, their opponent's roster, and the current week, this skill:
1. Recommends the optimal starting lineup
2. Explains the reasoning behind each start/sit decision
3. Flags worthwhile waiver-wire pickups
4. Surfaces context that could swing close calls

## Required inputs (ask if not provided)
- Full roster with positions (starters + bench)
- Opponent's full roster
- Current NFL week
- League scoring format (standard / PPR / half-PPR) and any custom scoring rules
- Roster requirements (how many QB/RB/WR/TE/FLEX/etc. must start)

## Research process
For each player who could plausibly start, use web search to gather:

**Primary factors (weight these heavily):**
- Current injury status / practice participation this week
- Recent performance trend (last 3-4 games, not just season average)
- This week's matchup: opposing defense rank vs. that position
- **Snap share / target share trend, and injuries to teammates at the same position** — treat a real role change (e.g., snap % jumping game-over-game, a target-competitor landing on IR or getting hurt mid-game) as strong signal that can outweigh matchup tier or a season-long projection. A player whose role is visibly expanding right now is often a better bet than a proven matchup alone would suggest — don't just log usage as color, let it move the actual recommendation.
- **Actual week-by-week fantasy points, checked against that week's projection — required whenever a player is being pitched on an "opportunity" or "role change" story (waiver adds especially).** Pull the real per-week scoring line (e.g. Week 1: X pts vs. Y proj, Week 2: X pts vs. Y proj), not just a season total or a single cherry-picked game. A snap-count or depth-chart story is not confirmation of value — plenty of players lead a team in snaps or even carries/targets while still scoring next to nothing (pass-pro reps, boundary routes, short-yardage work with no touchdown equity). If the actual points haven't shown up across multiple weeks despite a supposedly improving role, say so plainly and downgrade the recommendation rather than trusting the opportunity narrative alone. Conversely, a player quietly beating projection week over week is a real signal even without a flashy role story.
- Weather forecast for game time (temp, wind, precipitation) — flag if severe, since heavy wind especially affects passing/kicking games
- Home vs. away, and for away games, time zone shift the player's team is dealing with
- Vegas game total / point spread for the matchup — a game expected to be high-scoring or where a team is trailing big tends to shift volume (e.g., trailing teams pass more)
- **Contract status, checked every week for every player under consideration (not just when health/motivation comes up), using basic/known terms rather than a full deep-dive:** walk year, prove-it/cheap-guarantee structure (including a multi-year deal that's practically a one-year guarantee, e.g. cap-friendly team outs after year one), extension-eligible, recently paid long-term and secure, or on an expiring/non-guaranteed deal. Treat this as a real input on two things: (1) **availability/playing-through-pain decisions** — a player with motivation to prove himself (walk year, prove-it deal, needs to perform to get paid) is more likely to tell doctors/coaches he's fine and play through a soft-tissue injury (rib, oblique, hamstring, ankle, etc.) where there's no hard objective disqualifier; a player who's already fully secure long-term has less of that pressure. This does NOT apply to hard structural injuries that show up definitively on imaging (fracture, torn ligament confirmed by MRI/X-ray) — those are governed by medical clearance regardless of contract incentive. (2) **on-field effort/motivation more generally** — note contract status as a mild factor on snap willingness and risk tolerance (e.g., playing banged-up, pushing through a tough matchup) even when health isn't in question. Keep this lightweight: a one-line flag per player (e.g. "walk year, strong incentive to play through minor injury" or "fully secure long-term, no added incentive either way"), not a sourced research report — only go deeper if the user asks.

**Contextual factors (mention as color, don't let these override the primary factors alone):**
- Player physical profile (height/weight/speed) vs. positional average, if notably different
- Team/player narratives in the news: trades, rivalry games, "revenge game" storylines, broadcaster commentary — include if genuinely notable, but label clearly as narrative/motivational context rather than a statistical signal
- Cold-weather-vs-warm-climate-team narrative — mention if relevant, but note the actual performance effect is modest and easy to overstate
- Personal/legal situations affecting a player (e.g., recently cleared of an issue, team situation change) — only include if there's actual current reporting on it; don't speculate

**What NOT to fabricate:**
- Do not invent a "clutch/pressure performance" stat — this isn't a real tracked metric. If discussing this, be explicit that it's subjective/anecdotal, not data-backed.
- Do not state injury-risk percentages as if they're precise calculations unless citing an actual source. Speak in relative terms (e.g., "elevated risk given recent hamstring history") rather than fake precision.
- Do not claim confidence in soft-factor effects (weather, revenge games, rivalries) beyond what's reasonably supported. It's fine to say "this is often discussed but the actual effect is unclear."

## Output format
For each start/sit decision:
1. **Recommendation** (start/sit/flex)
2. **Primary reasoning** (2-3 sentences, matchup + usage + recent form)
3. **Supporting context** (weather, travel, narrative — only if genuinely relevant, kept brief)
4. **Confidence level** (high/medium/low — flag close calls honestly rather than sounding certain about a toss-up)

Then:
- **Waiver wire suggestions**: 2-4 available players worth considering, with brief reasoning, prioritized by immediate impact this week. For each one, include their actual week-by-week fantasy points so far this season (not just a role/opportunity story) — if a candidate's real scoring is flat or bad despite a good-sounding situation, either drop them from the list or flag the mismatch explicitly rather than recommending on narrative alone.

### Flagging an actionable change
Whenever a recommendation requires the user to actually do something (swap a starter, submit a waiver claim, act before a lock), never bury it inside a paragraph of reasoning. Lead with an unmissable block, then explain briefly after:

🚨 **DO THIS BEFORE [deadline — e.g. "TONIGHT'S KICKOFF" or "SUNDAY 1:00 PM"]:**
**START:** [player]
**BENCH:** [player]
[One line on why, plus the exact lock time]

If the situation is still developing (e.g. a questionable tag with no practice-report detail yet), say so plainly and give a concrete time/trigger to recheck (e.g. "final call comes 90 min before kickoff — check back then") rather than issuing a premature action alert.

## Notes
- Always confirm current week and any lineup lock deadline before finalizing
- If a decision is genuinely close, say so — don't manufacture false confidence
- Update roster/waiver data via web search each time this runs; don't rely on memorized stats
- **Don't conflate a past week's pre-game projection with this week's forward-looking projection.** Waiver/trending screens often show last week's "projected vs. actual" side by side (e.g. a "PROJ" column next to a "SCORE" column tied to an already-completed game) — verify which week a projection number actually belongs to before using it to justify a swap. When unsure, ask the user to check the app's per-player "Projections" tab for the current week's number rather than guessing from a list view.
- When the user shares a live app screenshot, prefer those real numbers/news over general web-search priors — the app reflects their specific league's scoring and current roster state.
- **Snap count and "opportunity" narratives can be misleading on their own** — a player can lead a backfield in snaps while another teammate quietly leads in actual carries/production, or a player can be tagged the beneficiary of an injury ahead of him without the box score ever showing up. Always sanity-check a role story against real week-by-week points before recommending a swap or add on it.
