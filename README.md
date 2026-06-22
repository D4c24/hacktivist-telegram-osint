# hacktivist-telegram-osint

> A structured open-source threat intelligence reference mapping Middle East threat actors to their known Telegram channels, social media accounts, and online presence — with confidence scoring and verified source citations.

---

## Overview

The Middle East has become one of the most active cyber battlegrounds globally, characterized by a volatile mix of nation-state APTs, Iranian proxy hacktivists, Russian-aligned groups, and opportunistic cybercriminals operating simultaneously — often targeting the same sectors during the same geopolitical escalation windows.

This repository provides a structured, investigator-ready reference for monitoring threat actors active across Israel, Kuwait, Jordan, Saudi Arabia, Oman, Bahrain, and Qatar, based on intelligence observed between January and March 2026. The core deliverable is a CSV dataset mapping each actor to their known online presence, with a rigorous confidence scoring system to help analysts prioritize monitoring efforts.

The primary intelligence question this dataset answers is:

> *Where can I find and monitor the self-disclosure channels of these threat actors?*

---

## Scope

**Reporting period:** January 18 – March 5, 2026

**Countries covered:** Israel, Kuwait, Jordan, Saudi Arabia, Oman, Bahrain, Qatar

**Threat actor types:**
- Nation-state APTs (Iran-sponsored: MuddyWater, APT34, APT33, APT39)
- Pro-Iranian hacktivist proxies (Iraq-based Shia militia-aligned groups)
- Russian-aligned hacktivists (NoName057(16), Russian Legion, RuskiNet)
- Southeast and South Asian hacktivist collectives (Bangladesh, Indonesia, Malaysia)
- Ransomware-as-a-Service (RaaS) operators
- Opportunistic data brokers

**Total actors tracked:** 30+ unique threat actors, 44 rows (some actors have multiple platform entries)

---

## Data Sources

This dataset was produced through open-source intelligence (OSINT) collection from the following source categories:

- **Primary threat intelligence reports:** FalconFeeds.io, Radware, SOCRadar, Outpost24, CloudSEK, Rapid7, Unit 42 (Palo Alto Networks), CrowdStrike, Mandiant
- **Government advisories:** CISA, FBI, NSA, NCSC-UK, US Cyber Command
- **Telegram analytics platforms:** TGStat (tgstat.com), Telemetrio (telemetr.io)
- **Threat actor tracking:** MITRE ATT&CK, Rewards for Justice, Wikipedia (verified entries)
- **Dark web monitoring:** BreachForums references via published CTI reports only

No classified, proprietary, or non-public intelligence sources were used. All source URLs are cited per row in the dataset.

---

## Dataset Structure

The file `threat_actors_monitoring.csv` contains the following columns:

| Column | Description |
|---|---|
| `Threat Actor` | Name of the threat actor or group as referenced in published CTI reporting |
| `Origin` | Country or geopolitical alignment of the actor (from FalconFeeds.io threat actor mapping tables) |
| `Platform` | Platform where the actor maintains a presence (Telegram, X/Twitter, GitHub, BreachForums, Dark Web, etc.) |
| `Channel / Account` | Confirmed or likely handle, username, or URL. Where no confirmed handle was found, a search recommendation is provided |
| `Confidence (ID/Activity)` | Dual confidence score (see scoring system below) |
| `Source URL` | Direct URL to the source that confirmed or referenced the channel/account |

---

## Confidence Scoring System

Each entry carries a dual confidence score in the format **ID/Activity**, both on a scale of 0.0 to 10.0.

**Identity Confidence (ID):** How confident are we that this channel/account genuinely belongs to this threat actor, and not an impersonator or unrelated entity?

**Activity Confidence (Activity):** How confident are we that this channel/account is currently active and operational at the time of research?

| Score Range | Interpretation |
|---|---|
| 9.0 – 10.0 | Confirmed — cited in multiple independent CTI reports or verified via Telegram analytics |
| 7.0 – 8.9 | High confidence — cited in at least one credible CTI report with supporting context |
| 5.0 – 6.9 | Moderate — referenced in open sources but handle not independently verified |
| 3.0 – 4.9 | Low — actor known to use platform but no confirmed handle found; search recommended |
| 0.0 – 2.9 | Unverified — speculative; treat with extreme caution |
| N/A | Not applicable — state APTs with no self-disclosure channels; attribution confidence only |

> **Note:** Hacktivist Telegram channels are highly volatile. Groups are frequently banned and recreate channels under new handles. Treat all handles as subject to change and validate before use in automated monitoring pipelines.

---

## Key Findings

- **DieNet** emerged as the highest-volume threat actor in the reporting period, claiming 59 DDoS operations in a 48-hour window across GCC targets. Primary channel: `@DIeNlt`.
- **313 Team** (Islamic Cyber Resistance in Iraq) operates a confirmed, stable Telegram presence at `@xX313XxTeam` with dedicated leak and backup channels.
- **Handala / Handala Hack** is assessed with high confidence as an Iran MOIS persona (Void Manticore / Banished Kitten cluster). Channel is repeatedly taken down and recreated — monitor by name search rather than static handle.
- **Keymous Plus** maintains the most stable multi-channel presence of any actor in the dataset: `@keymous` (primary), `@KeymousTeam` (backup), `@Keymous_V2` (secondary backup), and `@KeymousTeam` on X.
- **Fatimion Cyber Team** operates a confirmed channel at `@hak993`, active since August 2023 with over 5,000 documented messages.
- **MuddyWater, APT34, APT33, APT39** have no self-disclosure channels. These state APTs are attributed exclusively through third-party CTI vendors and government advisories — monitor via ThreatStream, MISP, and MITRE ATT&CK.
- **GCC-wide threat declarations** were issued by DieNet, LulzSec Black, 313 Team, APT IRAN, and FA Team — indicating coordinated intent to attack all Gulf states simultaneously.

---

## Limitations

- Telegram handles are volatile. Channel takedowns are frequent, particularly following Telegram's AI-based moderation policy changes introduced in 2025. Always validate handles before use.
- This dataset reflects open-source intelligence only. Claims made by hacktivist groups on Telegram are often exaggerated or unverified. Confidence scores reflect source quality, not attack impact assessment.
- State APT entries (MuddyWater, APT34, APT33, APT39) do not have platform entries as these groups do not self-disclose. Attribution is based on third-party vendor and government reporting.
- Actors with low confidence scores (below 5.0) should be treated as starting points for further investigation, not confirmed intelligence.
- This dataset was produced during a specific reporting period (Jan–Mar 2026) and may not reflect current actor posture or channel status.

---

## Usage

This dataset is intended for:

- **SOC analysts** building Telegram monitoring watchlists
- **CTI teams** enriching threat actor profiles in platforms like MISP or Anomali ThreatStream
- **Detection engineers** mapping actor presence to monitoring rules
- **Security researchers** studying the Middle East hacktivist ecosystem

**Recommended workflow:**
1. Filter by `Confidence (ID/Activity)` — prioritize rows with scores above 7.0/6.0
2. Cross-reference handles against current Telegram search before adding to monitoring pipelines
3. Use source URLs to pull additional context and IOCs from the referenced CTI reports
4. For actors with no confirmed handle, search Telegram directly by actor name

---

## License

This work is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

You are free to share and adapt this material for any purpose, provided appropriate credit is given to **D4c24**.

© 2026 D4c24

---

## Disclaimer

This repository is intended for defensive cybersecurity research and threat intelligence purposes only. All information was collected from publicly available open sources. No systems were accessed, no accounts were infiltrated, and no illegal activity was conducted in the production of this dataset. Channel handles and account references are provided solely for threat monitoring and defensive intelligence purposes.

The author makes no representations about the current accuracy or operational status of any listed channel or account. Always validate information independently before acting on it.

---

## Contributing

Found a missing handle, a dead link, or a new actor that should be added? Open an issue or submit a pull request. Contributions must include a verifiable open-source citation.

---

*Maintained by [@D4c24](https://github.com/D4c24)*
