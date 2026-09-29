You are an automotive cybersecurity analyst performing a threat analysis using the STRIDE methodology (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege).

SYSTEM
The system is an electro-mechanical brake (EMB) system for passenger vehicles. There are no mechanical or hydraulic connections between the brake pedal and the wheels; all braking commands are transmitted electrically to four wheel-end actuators (WEAs), each containing an actuator control unit, a servo motor and a brake caliper.

The attached figure shows the architecture to analyse:
[PASTE ONE ARCHITECTURE DESCRIPTION HERE]

The system has three safety goals:
- SG1: Avoid loss of or insufficient braking (deceleration below 5.15 m/s²)
- SG2: Avoid unintended braking (deceleration above 2.44 m/s²)
- SG3: Avoid braking deviation (lateral displacement above 1.20 m)

TASK
Identify as many STRIDE threats as you can for this architecture. Consider every component shown in the figure (controllers, WEAs, sensors, brake pedal, parking switch, power supplies) and every communication link between them.

RULES
- One threat per row. Do not merge several threats into one row.
- Cover all six STRIDE categories where applicable.
- Use the component names exactly as labelled in the figure (e.g. WEA/FL, MCU, Axle ECU/R).
- Focus on threats that result from this architecture's specific structure (controllers, power and bus layout).
- Base your analysis only on the information provided.
- Do not repeat the same threat with different wording.

OUTPUT FORMAT
Fill in the table below. Column rules:
- ID: T001, T002, T003, ...
- Name: "<STRIDE category> of <asset>", e.g. "Spoofing of MCU"
- Assets: the component(s) or link(s) affected, as labelled in the figure
- To Be Assessed: true if the threat could violate SG1, SG2 or SG3, otherwise false
- Category: one of Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege
- Severity: Severe, Major, Moderate or Negligible, based on the worst effect on the safety goals; "-" if it cannot be judged

| ID | Name | Assets | To Be Assessed | Category |
|---|---|---|---|---|---|
| T001 | Information Disclosure of WEA/FL | WEA/FL | true | Information Disclosure |

Output only the completed table (continue from the example row), followed by the total number of threats per STRIDE category.