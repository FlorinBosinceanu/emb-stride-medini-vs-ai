I'm attaching 5 Excel files 5 runs of a STRIDE threat analysis of the same architecture by the same model (columns ID, Name, Assets, To Be Assessed, Category, Severity). Find the threats that appear in ALL 5 runs and give me an Excel file with them, keeping the layout of the input files. Follow these rules exactly so the result is comparable with my earlier analyses. Do the matching in code.

1. MATCHING
- Match threats on (STRIDE category, target element), not on wording. Every row of every run must be mapped to at least one element; don't drop rows.
- Use the element names listed at the end. If a run names an element that isn't in the list, add it with a clear name and tell me.
- A threat on a message or signal counts for the element it names WEAFL Actuator Command, MCU Command to WEAFL - WEAFL; Brake Pedal SignalInputPosition - Brake Pedal; Wheel Speed SensorFR Data - that sensor.
- Spoofing of X asby Y - X. Repudiation of ... by X - X. X via Y - X if X is an element, otherwise Y (DoS via Power Supply A Failure - Power Supply A; DoS to MCU via Bus Flooding - MCU and the bus).
- Links a sensorpedalswitch signal link or a power-supply line counts as that device (Brake Pedal to MCU link - Brake Pedal; Power Supply B–MCU power line - Power Supply B). Exception, Architecture 2 only the Brake Pedal–MCU, Brake Pedal–Auxiliary ECU and Parking Switch–Auxiliary ECU buses are their own elements when the threat names the buslink.
- A threat on an ECU does NOT count for a bus just because its Assets list the bus.
- Grouped or generic entries count for every element they cover, taken from the Assets column, and are marked  WEA Control CommandsWEA Status - the WEAs in Assets (all four if unspecified); Vehicle SpeedWheel Speed Sensor Data - all four sensors; Communication Busall links - every bus segment; top pairMCU side - those two sensors; an unqualified Wheel Speed SensorFL in a run that labels every sensor that way - all four; Diagnostic Interface with Assets MCU + the other ECU - both ECUs.
- Architecture 1 only a Brake Pedal or Power Supply threat whose Assets list All WEAs also counts () for Brake Pedal to All WEAs link  Power Supply to All WEAs link, but only if at least one run names that link as its own threat.
- Wheel speed sensors are identified by position FL = top-left, FR = top-right, RL = bottom-left, RR = bottom-right (the diagram labels all four Wheel Speed SensorFL).

2. COMMON THREATS AND THEIR VALUES
- Common = the (category, element) pair appears in all 5 runs.
- Name = Category of Element. IDs T001... ordered by STRIDE category (S, T, R, I, D, E), then by element in the order of the list below.
- Severity = majority of the 5 runs (one vote per run; if a run has several matching rows, use its highest). Ties go to the higher level. Order -  Negligible  Low  Moderate  Major  Severe.
- To Be Assessed = majority of the 5 runs.
- Assets = the most common wording among rows that name the element; if every run words it differently, use the element name.

3. OUTPUT (.xlsx)
- Main sheet(s) copy the input layout exactly sheet names, column widths, fonts, header style, severity colour fills, how TRUEFALSE is stored. If the inputs have a Summary sheet, keep it with its COUNTIF formulas pointed at the new rows. If the runs' layouts differ, use the one most of them share.
- Add a cell comment on the Name of every common threat that only reaches 55 thanks to a  match, naming the run and row.
- Add a sheet Cross-run comparison every threat found in any run (one row per category + element) with Common ID, Category, Threat, one column per run showing ID (Severity) (+  where applicable), Found in (runs) as a COUNTA formula and In all 5 runs as an IF formula. Put short notes on the matching rules above the table.
- Add a sheet Mapping every original row (Run, ID, Name, Assets, To Be Assessed, Category, Severity) with the element(s) it was mapped to, whether by name or Assets, and the Common ID(s).
- Recalculate the formulas; there must be no formula errors. Check that the Mapping sheet contains every original row.

4. YOUR REPLY
Keep it short number of common threats out of the total distinct; counts by category and by severity; how many common threats rely on  matches and the count without them; on how many common threats the runs disagree on severity; the main reasons threats dropped out.

ELEMENT NAMES
Architecture 1 MCU; WEAFL; WEAFR; WEARL; WEARR; Communication bus; Brake Pedal; Brake Pedal to All WEAs link; Parking Switch; Wheel Speed SensorFL (at WEAFL); Wheel Speed SensorFL (at WEAFR); Wheel Speed SensorFL (at WEARL); Wheel Speed SensorFL (at WEARR); Power Supply A; Power Supply B; Power Supply A and Power Supply B (common cause); Power Supply to All WEAs link.
Architecture 2 MCU; Auxiliary ECU; WEAFL; WEAFR; WEARL; WEARR; Communication bus MCU–WEAFL; Communication bus MCU–WEAFR; Communication bus Auxiliary ECU–WEARL; Communication bus Auxiliary ECU–WEARR; Communication bus MCU–Auxiliary ECU; Communication bus Brake Pedal–MCU; Communication bus Brake Pedal–Auxiliary ECU; Communication bus Parking Switch–Auxiliary ECU; Brake Pedal; Parking Switch; Wheel Speed SensorFL (top-left); Wheel Speed SensorFL (top-right); Wheel Speed SensorFL (bottom-left); Wheel Speed SensorFL (bottom-right); Power Supply A; Power Supply B.
Architecture 3 MCU; Axle ECUR; Axle ECUF; WEAFL; WEAFR; WEARL; WEARR; Communication bus MCU–Axle ECUR; Communication bus MCU–Axle ECUF; Communication bus Axle ECUR–WEAFL, WEAFR; Communication bus Axle ECUF–WEARL, WEARR (a run that splits these per WEA counts towards the shared bus); Brake Pedal; Parking Switch; Wheel Speed SensorFL (top-left); Wheel Speed SensorFL (top-right); Wheel Speed SensorFL (bottom-left); Wheel Speed SensorFL (bottom-right); Power Supply A; Power Supply B; Power line Axle ECUR–WEAFL, WEAFR; Power line Axle ECUF–WEARL, WEARR.

This architecture is Architecture 1 2 and 3