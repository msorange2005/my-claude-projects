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
- Target share / snap count trend (usage is often more predictive than box score stats)
- Weather forecast for game time (temp, wind, precipitation) — flag if severe, since heavy wind especially affects passing/kicking games
- Home vs. away, and for away games, time zone shift the player's team is dealing with
- Vegas game total / point spread for the matchup — a game expected to be high-scoring or where a team is trailing big tends to shift volume (e.g., trailing teams pass more)

**Contextual factors (mention as color, don't let these override the primary factors alone):**
- Player physical profile (height/weight/speed) vs. positional average, if notably different
- Contract situation (new big deal vs. playing for a contract) — note it, but don't treat "playing for a contract" as a reliable performance predictor; there's no strong evidence this consistently changes output
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
- **Waiver wire suggestions**: 2-4 available players worth considering, with brief reasoning, prioritized by immediate impact this week

## Notes
- Always confirm current week and any lineup lock deadline before finalizing
- If a decision is genuinely close, say so — don't manufacture false confidence
- Update roster/waiver data via web search each time this runs; don't rely on memorized stats
