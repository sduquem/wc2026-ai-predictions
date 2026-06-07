# Prediction Model — Technical Notes

## Team Strength Ratings

Ratings computed as:
  Blended = (0.60 × market_norm) + (0.40 × hist_norm)

Where:
  market_norm = polymarket_probability / 0.165  (normalized to Spain = 1.0)
  hist_norm   = historical_win_rate / 0.708     (normalized to Germany = 1.0)

## Goal Prediction Model

Expected goals per team:
  exp_home = AVG_GOALS × (rating_home / (rating_home + rating_away) + 0.03)
  exp_away = AVG_GOALS × (rating_away / (rating_home + rating_away) - 0.03)

  AVG_GOALS = 2.7  (WC historical average goals per game)
  +0.03/-0.03 = slight home/neutral advantage for group stage (removed in KO)

Scores rounded to nearest integer. If 0-0 and |diff| > 0.1, stronger team gets 1 goal.

## Knockout Tiebreaker

If predicted score is level: stronger team wins on ET/Penalties
  winner = team_A if rating_A >= rating_B else team_B

## Historical Data Used

Source: FIFA Maldini Dataset (World_Cup_Maldini_app.csv)
Period: 1930-2022 (22 tournaments, 900+ matches)
Fields used: Home/Away goals, Stage, Year, Team names

Win rate computed as: wins / total_games (including group stage)
Only teams with 5+ tournament appearances used for historical weight.

## Market Data (June 5, 2026)

Source: Polymarket "World Cup Winner" market
Total volume: >$1.6 billion USD
Verification: Adversarial 3-vote system (105 sub-agents)

Top probabilities:
  Spain:    16.5%
  France:   16.0%
  England:  11.3%
  Portugal:  9.7%
  Argentina: 8.2%
  Brazil:    7.5%
  Germany:   6.8%

## Bonus Questions — Statistical Basis

Red cards: Historical avg 0.316/game × 104 games = ~33 → "20+" bracket
Pen shootouts: Historical KO rate 16.7% × 32 KO matches = ~5.3 → answer: 8
Total goals: Historical avg 2.51/game × 104 games = ~261 → "240-279" bracket
Final goals: Historical WC final avg 2.6 goals → answer: 3
