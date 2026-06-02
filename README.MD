# Plasma Speaker – PCB Design

so this is my plasma speaker project which i made for my college physics project. basically designed the full circuit and pcb myself from scratch, took around 6 days total. hope it comes out good when i actually build it lol

---

## Why I Did This

honestly it started just as a college physics submission but then i got genuinely interested in how it actually works. plasma speakers are cool because theres no physical cone or membrane, sound comes directly from ionised air through a high voltage arc. felt way more interesting than doing some boring experiment so i decided to design the full electronics myself instead of just buying something readymade

---

## How I Did It

split the whole thing into 4 sections, each one feeds into the next

**DC Input Stage**
started here becuase i wanted stable power before touching anything else. 24v input goes down to 12v using a 1N4742 zener diode with 330ohm 1w resistor. added 100uf smoothing cap and a led indicator. was originally thinking of using 7812 regulator but the heat dissipation at 24v input looked annoying so switched to zener setup. forgot cap polarity once and had to recheck 💀

**Power Switching Stage**
this is the main section, handles high current switching and drives the transformer later. used IRFP260N mosfet becuase cheaper mosfets felt risky after checking other plasma speaker builds. put multiple 470uf 35v caps on the input rail for handling sudden current spikes, started with just one and added more after reading about ripple current. also mixed mkp10 film caps with electrolytics becuase film caps handle high frequency noise better, didnt actually know why people do this before this project 😭. bc327 handles gate drive. routing got messy really fast, almost connected drain and source wrong on the mosfet 💀

**Zero Cross Detector**
built around LM331N with rc filter network using 10n caps. this was genuinly the most confusing part, timing and comparator stuff is more theoretical than power electronics. spent alot of time just reading the datasheet and looking at application circuits. got confused between feedback path and threshold pin like 3 times. still not fully sure it will behave exactly how i want until i test it on oscilloscope honestly

**Oscillator**
NE555 in astable mode. choosed 555 becuase its simple and well documented, didnt want to deal with complicated pwm ic on top of everything else. 10n and 4.7n timing caps with 5k pot for manual frequency adjustment because transformer resonance can vary and i wanted tuning option during testing. almost connected discharge pin wrong aswell 💀 led indicator added to atleast visually confirm its running

---

## PCB Design

did this in kicad didnt really have a big plan going in, just placed things with few things in mind

- terminal connectors and aux stuff on one side, big caps on the other side
- power section components as close as possible to keep traces short
- mosfet placed face down so i can attach aluminium block behind for cooling
- lm331 and ne555 grouped together on bottom half of board
- copper zones filled on both layers for cooling and reducing noise

did silkscreen on both front and back copper layers, took quite some time but looks nice. only real rule i followed was keep connections short and make it look atleast a little symmetric

---

## Components

sourced everything from mouser, made full bom and verified all parts. cart is ready

---

## Build Log

| Day | What I did | Time |
|-----|-----------|------|
| 1 | DC input stage schematic | 30min |
| 2 | Power switching stage schematic | 2hr 30min |
| 3 | Zero cross detector schematic | 3hr |
| 4 | Oscillator schematic | 2hr 45min |
| 5 | Full PCB routing and silkscreen | 4hr 30min |
| 6 | BOM and mouser sourcing | 1hr |

---

## Schematic

<img width="3507" height="2480" alt="image" src="https://github.com/user-attachments/assets/7ec02542-c563-4a06-83e8-e262af59c271" />

---

## PCB

<img width="975" height="761" alt="image" src="https://github.com/user-attachments/assets/3a04d2ad-f897-4782-957a-6588ecf0993e" />
<img width="975" height="717" alt="image" src="https://github.com/user-attachments/assets/7cd246b7-c3b8-4aa5-a08f-eacf767012d7" />
<img width="975" height="625" alt="image" src="https://github.com/user-attachments/assets/989beebe-3dd7-4d92-8b19-86e832e3c6c9" />
<img width="975" height="813" alt="image" src="https://github.com/user-attachments/assets/4ca7eacf-0d4e-4160-9b41-7999a67dc339" />
<img width="975" height="797" alt="image" src="https://github.com/user-attachments/assets/4c422671-a0a5-493e-ab5f-c8af19c2a8aa" />
<img width="975" height="779" alt="image" src="https://github.com/user-attachments/assets/2356953d-fa44-43ab-848d-ffe4764d426e" />

---

## Cart

<img width="1229" height="1729" alt="Screenshot 2026-05-18 190808" src="https://github.com/user-attachments/assets/1aa987b0-d2db-464f-9a59-5317d63be798" />
<img width="3138" height="1710" alt="Screenshot 2026-05-18 190657" src="https://github.com/user-attachments/assets/e8003873-b3c6-494f-9e03-dae67ebf5380" />
<img width="3124" height="1721" alt="Screenshot 2026-05-18 190640" src="https://github.com/user-attachments/assets/e3d2c703-7dba-4ec8-973e-29f7ede15881" />
<img width="3199" height="1710" alt="Screenshot 2026-05-18 191033" src="https://github.com/user-attachments/assets/8dfe70c2-0f06-46e6-9dd6-462a064299da" />
<img width="3199" height="1730" alt="Screenshot 2026-05-18 191025" src="https://github.com/user-attachments/assets/cf19c73a-b37d-4bbf-ae44-1cc6df418703" />


---

## BOM

| Index | Qty | Part Number | Manufacturer Part Number | Description | Available | Backorder | Unit Price | Extended Price INR |
|------:|----:|-------------|--------------------------|-------------|----------:|----------:|-----------:|-------------------:|
| 1 | 10 | 2.2KEBK-ND | CFR-12JB-52-2K2 | RES 2.2K OHM 5% 1/6W AXIAL | 10 | 0 | 3.727 | ₹37.27 |
| 2 | 25 | 1.0KEBK-ND | CFR-12JB-52-1K | RES 1K OHM 5% 1/6W AXIAL | 25 | 0 | 3.0936 | ₹77.34 |
| 3 | 10 | 470EBK-ND | CFR-12JB-52-470R | RES 470 OHM 5% 1/6W AXIAL | 10 | 0 | 3.727 | ₹37.27 |
| 4 | 10 | 100EBK-ND | CFR-12JB-52-100R | RES 100 OHM 5% 1/6W AXIAL | 10 | 0 | 3.448 | ₹34.48 |
| 5 | 10 | 10KEBK-ND | CFR-12JB-52-10K | RES 10K OHM 5% 1/6W AXIAL | 10 | 0 | 3.634 | ₹36.34 |
| 6 | 10 | 220EBK-ND | CFR-12JB-52-220R | RES 220 OHM 5% 1/6W AXIAL | 10 | 0 | 3.727 | ₹37.27 |
| 7 | 10 | 33KEBK-ND | CFR-12JB-52-33K | RES 33K OHM 5% 1/6W AXIAL | 10 | 0 | 3.448 | ₹34.48 |
| 8 | 10 | 3.3KEBK-ND | CFR-12JB-52-3K3 | RES 3.3K OHM 5% 1/6W AXIAL | 10 | 0 | 3.448 | ₹34.48 |
| 9 | 10 | 399-6601-ND | ESK107M016AC3AA | CAP ALUM 100UF 20% 16V RADIAL TH | 10 | 0 | 10.064 | ₹100.64 |
| 10 | 10 | 445-8348-ND | FK16X7R1C106KR020 | CAP CER 10UF 16V X7R RADIAL | 10 | 0 | 28.235 | ₹282.35 |
| 11 | 10 | 445-180204-ND | FG18X7R1E105KRT00 | CAP CER 1UF 25V X7R RADIAL | 10 | 0 | 16.96 | ₹169.60 |
| 12 | 20 | 399-6086-ND | ESC477M035AH4AA | CAP ALUM 470UF 20% 35V RADIAL TH | 20 | 0 | 37.74 | ₹754.80 |
| 13 | 2 | IRFP260NPBF-ND | IRFP260NPBF | MOSFET N-CH 200V 50A TO247AC | 2 | 0 | 587.07 | ₹1,174.14 |
| 14 | 10 | WP710A10PGT-ND | WP710A10PGT | LED GREEN CLEAR T-1 T/H | 10 | 0 | 17.426 | ₹174.26 |
| 15 | 10 | 754-1606-ND | WP710A10ID | LED RED DIFFUSED T-1 T/H | 10 | 0 | 14.071 | ₹140.71 |
| 16 | 5 | CKN12301-ND | PTS636SL43 LFS | SWITCH TACTILE SPST-NO 0.05A 12V | 5 | 0 | 15.84 | ₹79.20 |
| 17 | 5 | 3296W-1-252LF-ND | 3296W-1-252LF | TRIMMER 2.5K OHM 0.5W PC PIN TOP | 5 | 0 | 224.58 | ₹1,122.90 |
| 18 | 10 | 13-CFR-25JR-52-270RCT-ND | CFR-25JR-52-270R | RES 270 OHM 5% 1/4W AXIAL | 10 | 0 | 3.262 | ₹32.62 |
| 19 | 10 | 330WCT-ND | FMP100JR-52-330R | RES 330 OHM 5% 1W AXIAL | 10 | 0 | 7.921 | ₹79.21 |
| 20 | 15 | 445-173264-1-ND | FG18X7R1H103KNT06 | CAP CER 10000PF 50V X7R RADIAL | 15 | 0 | 12.021 | ₹180.32 |
| 21 | 10 | 445-173265-1-ND | FG18X7R1H104KNT06 | CAP CER 0.1UF 50V X7R RADIAL | 10 | 0 | 12.953 | ₹129.53 |
| 22 | 10 | 445-173598-1-ND | FG28X7R1H472KNT06 | CAP CER 4700PF 50V X7R RADIAL | 10 | 0 | 12.021 | ₹120.21 |
| 23 | 15 | 1928-MKP1G031004D00KSSD-ND | MKP1G031004D00KSSD | MKP 10 0.1F 400V DC 7X14X18 PCM | 0 | 15 | 54.793 | ₹821.90 |
| 24 | 10 | 4878-BC327-40BK-ND | BC327-40BK | TRANS PNP 45V 0.8A TO-92 | 10 | 0 | 10.157 | ₹101.57 |
| 25 | 5 | LM311NNS/NOPB-ND | LM311N/NOPB | IC COMPARATOR 1 GEN PUR 8DIP | 5 | 0 | 85.73 | ₹428.65 |
| 26 | 5 | LM311NNS/NOPB-ND | LM311N/NOPB | IC COMPARATOR 1 GEN PUR 8DIP | 5 | 0 | 85.73 | ₹428.65 |
| 27 | 10 | 1N4742A-T50ACT-ND | 1N4742A-T50A | DIODE ZENER 12V 1W DO41 | 10 | 0 | 15.842 | ₹158.42 |
| 28 | 10 | 1N4148FS-ND | 1N4148 | DIODE STANDARD 100V 200MA DO35 | 10 | 0 | 5.125 | ₹51.25 |
| 29 | 10 | 102-6203-ND | TB007-508-02BE | TERMINAL BLOCK, SCREW TYPE, 5.08 | 10 | 0 | 36.995 | ₹369.95 |
| 30 | 5 | SC1852-ND | PJRAN1X1U01AUX | CONN RCA JACK MONO 3.2MM R/A | 5 | 0 | 275.83 | ₹1,379.15 |
| 31 | 1 | Power (Own Funded) | - | - | 1 | 0 | 3999 | ₹0 |
| 32 | 2 | Transformer (Own Funded) | - | - | 2 | 0 | 499 | ₹0 |
| 33 | 1 | PCB | - | - | 1 | 0 | 989 | ₹989 |
| | | | | **TOTAL** | | | | **₹9,597.96** |


