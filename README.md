# 🏏 IPL Analysis Dashboard (2008–2025)

An end-to-end data analytics project exploring 18 seasons of Indian Premier League (IPL) cricket — from raw ball-by-ball delivery logs to an interactive Power BI dashboard with dynamic season-level KPIs, leaderboards, and team performance tracking.

---

## 📌 Project Overview

This project analyzes the complete history of the IPL (2008–2025) using ball-by-ball delivery data, match results, player profiles, and team metadata. The goal was to build a single, interactive dashboard that lets a user pick any season and instantly see who won, who dominated with bat and ball, and how every team performed — without touching a spreadsheet.

Objective: Turn 278,000+ rows of raw delivery-level data into a decision-ready, self-service analytics tool.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
| **Power BI Desktop** | Data modeling, DAX measures, report/dashboard design |
| **DAX (Data Analysis Expressions)** | Dynamic KPI calculations (season winners, Orange/Purple Cap, team standings) |
| **Power Query (M)** | Data import and shaping from CSV sources |
| **CSV / flat files** | Raw source data (ball-by-ball, matches, players, teams) |
| **Star-schema style data modeling** | Fact table (`ball_by_ball_data`) linked to dimension tables (`ipl_matches_data`, `players-data-updated`, `teams_data`) |
| **Git & GitHub** | Version control and project hosting |

---

## 📂 Repository Structure

IPL-Analysis-Dashboard/
├── IPL_Analysis_Dashboard.pbix     # Power BI report file (data model + visuals)
├── IPL data/
│   ├── ball_by_ball_data.csv       # 278,205 rows — every delivery, 2008–2025
│   ├── ipl_matches_data.csv        # 1,169 rows — match-level results
│   ├── players-data-updated.csv    # 772 rows — player profiles
│   └── teams_data.csv              # 16 rows — franchise info
├── Images Used/
│   └── (dashboard Images)
└── README.md

---

## 🗄️ Dataset

| Table | Rows | Grain | Key fields |
|---|---|---|---|
| `ball_by_ball_data` | 278,205 | One row per delivery | batter, bowler, runs, extras, wicket type, over/ball number |
| `ipl_matches_data` | 1,169 | One row per match | teams, venue, toss, winner, margin, player of match |
| `players-data-updated` | 772 | One row per player | batting/bowling style, fielding position, images |
| `teams_data` | 16 | One row per franchise | team name, short code, logo URL |

**Data model relationships:**
- `ball_by_ball_data[match_id]` → `ipl_matches_data[match_id]` (many-to-one)
- `ipl_matches_data[player_of_match]` → `players-data-updated[player_id]` (many-to-one)
- `ipl_matches_data[team1]`, `[team2]`, `[match_winner]` → `teams_data[team_name]` (many-to-one; `USERELATIONSHIP` used in DAX since a team name plays two roles per match)

---

## 🧮 Key DAX Measures

The report relies on **35 custom DAX measures** to make every KPI season-aware. Highlights:

- **`Season Winner` / `Runnerup`** — pulls the winner and loser of each season's final match, with team logos via `LOOKUPVALUE`
- **`Orange Cap Holder` / `Orange Cap Runs` / `Orange Cap Team`** — dynamically finds the top run-scorer for the selected season using `SUMMARIZE` + `MAXX`
- **`urple Cap Holder` (Purple Cap) / `PurpleCapWicketCount` / `PurpleCapTeam`** — top wicket-taker, explicitly excluding run-outs, retirements, and obstruction dismissals which don't count as bowler wickets
- **`Matches Played` / `Matches Won` / `Matches Lost` / `Total Points`** — team standings, using `USERELATIONSHIP` to resolve the team1/team2 dual-role problem
- **`Centuries` / `Half Centuries` / `Total 6's` / `Total 4's`** — season-level batting milestones aggregated from delivery-level data
- **`Top Fours Player` / `Top Six Player`** — per-season boundary leaderboards with player image lookups

---

## 📊 Dashboard Features

- **Season slicer** — every visual updates for the selected year (2008–2025)
- **Season Winner / Runner-up cards** with team logos
- **Orange Cap & Purple Cap** leaderboard cards with player photos
- **Season snapshot KPIs**: total matches, sixes, fours, centuries, half-centuries, venues used
- **Team standings table**: played / won / lost / tied / no-result / points, per team, per season
- **Boundary leaderboards**: top four-hitter and top six-hitter of the season

---


## 🎯 Skills Demonstrated

- Data modeling (fact/dimension design, relationship management, handling dual-role foreign keys)
- Advanced DAX (`SUMMARIZE`, `FILTER`, `CALCULATE`, `USERELATIONSHIP`, `LOOKUPVALUE`, variables)
- Dynamic, filter-context-aware KPI design (measures that recompute per slicer selection rather than static aggregates)
- Dashboard/UX design for self-service analytics
- Working with large, messy, real-world sports data (nulls, inconsistent categories, multi-format dismissal types)

---


## 📎 Data Source

IPL ball-by-ball, match, player, and team data (2008–2025). Player and team images sourced from ESPN Cricinfo and the official IPL website.

---

## 👤 Author
SRI DURGAA S.K
