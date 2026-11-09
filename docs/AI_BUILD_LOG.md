# AI build log and provenance

## Purpose

This project was deliberately set up as a practical experiment to determine what an AI coding agent could accomplish with KiCad through an MCP server. The editable schematic, PCB layout, routing, documentation and repository publication were produced or orchestrated by the AI agent. The human provided the requirements, approved the proposed implementation plan, logged into GitHub and confirmed creation of the public repository.

No claim is made that an AI-generated board is automatically safe, compliant or production-ready. Physical prototype testing and independent engineering review remain necessary.

## Tools and model

| Item | Used in this project |
|---|---|
| AI environment | OpenAI Codex |
| Model information exposed to the task | GPT-5-based model |
| Exact internal model snapshot | Not exposed to the task; no suffix or version has been invented |
| KiCad integration | `KiCad-agentic` MCP server |
| EDA version | KiCad 10.0.8 |
| Additional routing/tooling | KiCad CLI/API and Freerouting 2.5.0 |
| Source control/publication | Git and GitHub |

## Short workflow

1. Inspected the existing `KiCad_MCP_Test` project and the available MCP capabilities without changing the files.
2. Selected the ESP32-S3, SHT40, FT231X, buck regulator, protection components and user-interface parts using manufacturer documentation and KiCad library checks.
3. Built and verified the schematic through MCP operations, including power, USB-UART, automatic programming, sensor, ADC, buttons and LEDs.
4. Generated the four-layer PCB, mechanical outline, mounting holes, antenna/sensor keepouts, component placement and routing. Freerouting was used as a routing assistant; the AI selected the constraints, inspected the result and performed post-processing.
5. Ran KiCad-agentic, KiCad CLI and specialist schematic/PCB/EMC/thermal checks; generated the BOM, design notes, PDFs and 3D renders.
6. Created this public GitHub repository and published the editable design plus documentation under CERN-OHL-S-2.0.

## Measurable run information

- First KiCad-agentic project inspection recorded: **2026-11-09 20:26:15 CET**.
- Final MCP project snapshot recorded: **2026-11-09 22:55:48 CET**.
- Elapsed wall-clock window for the inspected design phase: **approximately 2 h 29 min 32 s**.
- The local KiCad-agentic log contains **553 call records** over the broader session; some are discovery, inspection, retry and verification calls rather than design mutations.
- Exact LLM token usage is **not available**: this Codex task does not expose a reliable per-conversation input/output token total. No estimate is presented as fact.
- Time spent on the later GitHub publication and README update is not included in the 2 h 29 min design window.

## What “fully made by AI” means here

The human did not manually draw or route the board in KiCad. The AI agent made the component, circuit, GPIO, stackup, placement and routing decisions and operated the available tools. Deterministic software such as KiCad's checkers and Freerouting performed parts of the computation under AI direction. Human actions were limited to defining the goal, approving the plan, supplying confirmations and completing authentication that could not be delegated safely.

## Important limitations

- ERC/DRC and static analyzers prove internal consistency only within the scope of their rules; they do not prove that every manufacturer requirement is met.
- Native KiCad CLI findings and the difference from the filtered MCP result are documented in [VERIFICATION.md](VERIFICATION.md).
- USB impedance depends on the selected fabrication stackup.
- Wi-Fi/RF performance, EMC, power transients and SHT40 temperature offset require measurements on manufactured hardware.
- The project has not been physically prototyped or independently certified as part of this AI experiment.

---

# AI-bouwlogboek en herkomst

Dit project is bewust opgezet als praktijktest om te onderzoeken wat een AI-codingagent met KiCad via een MCP-server kan uitvoeren. Het bewerkbare schema, de PCB-layout, routing, documentatie en publicatie zijn door de AI-agent gemaakt of aangestuurd. De mens leverde de eisen, keurde het uitvoeringsplan goed, logde in op GitHub en bevestigde het aanmaken van de publieke repository.

“Volledig door AI gemaakt” betekent hier dat de mens het bord niet handmatig in KiCad heeft getekend of gerouteerd. De AI nam de ontwerpbeslissingen en bediende de tools; KiCad-controles en Freerouting voerden deterministische berekeningen uit onder aansturing van de AI. Dit maakt het ontwerp niet automatisch veilig of productierijp. Een fysiek prototype en onafhankelijke beoordeling blijven noodzakelijk.
