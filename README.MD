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
<img width="1086" height="1703" alt="Screenshot 2026-05-18 190831" src="https://github.com/user-attachments/assets/54669760-215c-4c06-8936-2f5baa2fb9ea" />
<img width="1037" height="1725" alt="Screenshot 2026-05-18 190827" src="https://github.com/user-attachments/assets/2c94a7f8-7946-4ee5-b3f3-2ac799eadbd7" />
<img width="1015" height="1738" alt="Screenshot 2026-05-18 190817" src="https://github.com/user-attachments/assets/7e11b401-e2a4-4748-8a9d-7aa7142b79b2" />
<img width="1086" height="1703" alt="Screenshot 2026-05-18 190831" src="https://github.com/user-attachments/assets/23067be0-d5c6-4543-aeb4-d4afab988be9" />
<img width="975" height="717" alt="image" src="https://github.com/user-attachments/assets/96b450b0-bb71-4241-9f44-b198a69fe475" />

---

## BOM

| Quantity | References | Value | Code | Link | Cost | Total |
| --- | --- | --- | --- | --- | --- | --- |
| 5 | R1 | 2.2k | CFR-12JB-52-2K2 | [CFR-12JB-52-2K2 YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/CFR-12JB-52-2K2?qs=%2Fha2pyFaduguKzzNh3FFGjcjeCrw6XLi7qO3fcp8uGAeTbdTW3NWpQ%3D%3D) | 18.64 | 93.2 |
| 15 | R2,R9,R12 | 1k | CFR-12JB-52-1K | [CFR-12JB-52-1K YAGEO \| Mouser](https://www.mouser.com/ProductDetail/YAGEO/CFR-12JB-52-1K?qs=8uyp%2Fy7yFW6RQpJpptx%2FjA%3D%3D) | 8.39 | 125.85000000000001 |
| 10 | R3,R14 | 470R | CFR-12JB-52-470R | [CFR-12JB-52-470R YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/CFR-12JB-52-470R?qs=%2Fha2pyFaduguKzzNh3FFGhfDs4OOvhnWTwwBcnn%2FMObWfCDx0mlwug%3D%3D) | 8.39 | 83.9 |
| 10 | R4,R6 | 100R | CFR-12JB-52-100R | [CFR-12JB-52-100R YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/CFR-12JB-52-100R?qs=%2Fha2pyFaduguKzzNh3FFGvC3O2CWFCKi2%252BYSCrlUXeFESMknYkK4sw%3D%3D) | 8.39 | 83.9 |
| 10 | R5,R7 | 10k | CFR-12JB-52-10K | [CFR-12JB-52-10K YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/CFR-12JB-52-10K?qs=%2Fha2pyFaduguKzzNh3FFGoOqFe6wPpVia0lDknWpUfhFHYrSo8JXtQ%3D%3D) | 8.39 | 83.9 |
| 5 | R8 | 220R | CFR-12JB-52-220R | [CFR-12JB-52-220R YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/CFR-12JB-52-220R?qs=%2Fha2pyFaduguKzzNh3FFGsSiGs45uh5Vv%252B%2FtGQVnCAw44AoZD6pelQ%3D%3D) | 18.64 | 93.2 |
| 5 | R10 | 33k | CFR-12JB-52-33K | [CFR-12JB-52-33K YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/CFR-12JB-52-33K?qs=%2Fha2pyFaduguKzzNh3FFGtD5HMOaPBxnrTlnbsSj2Q0XkWIk8qu95g%3D%3D) | 18.64 | 93.2 |
| 5 | R11 | 3.3k | CFR-12JB-52-3K3 | [CFR-12JB-52-3K3 YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/CFR-12JB-52-3K3?qs=%2Fha2pyFaduguKzzNh3FFGvB2%2FXk%252BjjTJRDDA5bSJAXFTvRhEPLksLg%3D%3D) | 18.64 | 93.2 |
| 5 | R13 | 270R | CFR-25JR-52-270R | [CFR-25JR-52-270R YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/CFR-25JR-52-270R?qs=%2Fha2pyFaduiUclxQMvctpKqdUEK9N9SZgQRfFyqRSpWhgFFU6kp0pQ%3D%3D) | 9.32 | 46.6 |
| 5 | R16 | 330R | FMP100JR-52-330R | [FMP100JR-52-330R YAGEO \| Mouser India](https://www.mouser.in/ProductDetail/YAGEO/FMP100JR-52-330R?qs=sGAEpiMZZMukHu%252BjC5l7YU1KDXB2UgZE%252B9bionrPPGU%3D) | 12.11 | 60.55 |
| 5 | C1 | 100u | ESK107M016AC3AA | [ESK107M016AC3AA KEMET \| Mouser India](https://www.mouser.in/ProductDetail/KEMET/ESK107M016AC3AA?qs=9RUIYXQlAdBlfkFfvuUkxQ%3D%3D) | 17.7 | 88.5 |
| 5 | C2 | 10u | FK16X7R1C106K | [FK16X7R1C106K TDK \| Mouser India](https://www.mouser.in/ProductDetail/TDK/FK16X7R1C106K?qs=sGAEpiMZZMvsSlwiRhF8qk5dk0Ff3GLt7CBGZPfzGBA%3D) | 46.59 | 232.95000000000002 |
| 15 | C3,C5,C6 | 10n | FG18X7R1H103KNT06 | [FG18X7R1H103KNT06 TDK \| Mouser India](https://www.mouser.in/ProductDetail/TDK/FG18X7R1H103KNT06?qs=sGAEpiMZZMsh%252B1woXyUXj2I8eAiqPMPDobsvyMfyv4Y%3D) | 8.67 | 130.05 |
| 5 | C4 | 100n | FG18X7R1H104KNT06 | [FG18X7R1H104KNT06 TDK \| Mouser India](https://www.mouser.in/ProductDetail/TDK/FG18X7R1H104KNT06?qs=qf2ddTMq67WA8sH6FratLA%3D%3D) | 22.36 | 111.8 |
| 5 | C7 | 4.7n | FG28X7R1H472KNT06 | [FG28X7R1H472KNT06 TDK \| Mouser India](https://www.mouser.in/ProductDetail/TDK/FG28X7R1H472KNT06?qs=qf2ddTMq67VHPU0W%252B3I8vg%3D%3D) | 20.5 | 102.5 |
| 5 | C8 | 1u | FG18X7R1E105KRT00 | [FG18X7R1E105KRT00 TDK \| Mouser India](https://www.mouser.in/ProductDetail/TDK/FG18X7R1E105KRT00?qs=vNwBHymccZ%252B2%252BCnL09vDMw%3D%3D) | 28.89 | 144.45 |
| 20 | C9,C10,C11,C12 | 470u | ESC477M035AH4AA | [ESH477M035AL3AA KEMET \| Mouser India](https://www.mouser.in/ProductDetail/KEMET/ESH477M035AL3AA?qs=sGAEpiMZZMukHu%252BjC5l7YQgQugTmc6cjprvY1xciEeM%3D) | 34.85 | 697 |
| 15 | C13,C14,C15 | 100n | MKP10-.1/400/5P15 | [MKP10-.1/400/5P15 WIMA \| Mouser India](https://www.mouser.in/ProductDetail/WIMA/MKP10-1-400-5P15?qs=ruR7qzrNb6g3VgX%252BWvHiGQ%3D%3D) | 54.23 | 813.4499999999999 |
| 5 | Q1 | BC327 | BC327-40-AP | [BC327-40 Diotec Semiconductor \| Mouser India](https://www.mouser.in/ProductDetail/Diotec-Semiconductor/BC327-40?qs=OlC7AqGiEDk3RFYgk5gWUg%3D%3D&utm_id=506131562&utm_marketing_tactic=apaccorp&msclkid=3215ecd3c3141fd4a5d986d8d17fc729&utm_source=bing&utm_medium=cpc&utm_campaign=Other%20Suppliers%20PDP%20DSA%20India&utm_term=%2FProductDetail%2F&utm_content=Other%20Suppliers%20PDP%20DSA) | 15.84 | 79.2 |
| 5 | Q2 | IRFP260N | IRFP260NPBF | [IRFP260NPBF Infineon Technologies \| Mouser India](https://www.mouser.in/ProductDetail/Infineon-Technologies/IRFP260NPBF?qs=9%252BKlkBgLFf2Q0aoG2Yfqfg%3D%3D) | 498.51 | 2492.55 |
| 5 | U1 | LM311N | LM311N/NOPB | [LM311N/NOPB Texas Instruments \| Mouser India](https://www.mouser.in/ProductDetail/Texas-Instruments/LM311N-NOPB?qs=X1J7HmVL2ZEW%2F3U%252B2FkA%2Fw%3D%3D) | 85.73 | 428.65000000000003 |
| 5 | U2 | NE555N | NE555PE4 | [NE555PE4 Texas Instruments \| Mouser India](https://www.mouser.in/ProductDetail/Texas-Instruments/NE555PE4?qs=rLYyFdxB%2FmpV6UJXAtWXuA%3D%3D) | 109.02 | 545.1 |
| 5 | D1 | 1N4742 | 1N4742A-T50A | [1N4742A-T50A onsemi \| Mouser India](https://www.mouser.in/ProductDetail/onsemi/1N4742A-T50A?qs=0lQeLiL1qyaUl85kww6yHQ%3D%3D) | 26.09 | 130.45 |
| 5 | D2 | GREEN | WP710A10PGT | [WP710A10PGT Kingbright \| Mouser India](https://www.mouser.in/ProductDetail/Kingbright/WP710A10PGT?qs=jBF9H7RTBaQqx0iDNHF17A%3D%3D) | 25.16 | 125.8 |
| 5 | D3 | RED | WP710A10ID | [WP710A10ID Kingbright \| Mouser India](https://www.mouser.in/ProductDetail/Kingbright/WP710A10ID?qs=wRBQ8ZgBZ98VyHeNIlWGkQ%3D%3D) | 20.5 | 102.5 |
| 5 | D4 | 1N4148 | 1N4148 | [1N4148 onsemi \| Mouser India](https://www.mouser.in/ProductDetail/onsemi/1N4148?qs=i4Fj9T%2FoRm8RMUhj5DeFQg%3D%3D) | 9.32 | 46.6 |
| 5 | B1 | BUTTON | PTS636SL43 LFS | [PTS636SL43 LFS C&K \| Mouser India](https://www.mouser.in/ProductDetail/CK/PTS636SL43-LFS?qs=jcD%2FCkGBYeOwjxNXDGvRDg%3D%3D) | 13.98 | 69.9 |
| 10 | DC | INPUT,OUTPUT | CONN2-200 | [TB007-508-02BE Same Sky \| Mouser India](https://www.mouser.in/ProductDetail/Same-Sky/TB007-508-02BE?qs=sGAEpiMZZMvPvGwLNS671%2FDanv8Jav06gFn0LCcvzWQbXW5uAFVdMA%3D%3D) | 35.78 | 357.8 |
| 5 | RV1 | 5k | 3296W-1-252LF | [3296W-1-252LF Bourns \| Mouser India](https://www.mouser.in/ProductDetail/Bourns/3296W-1-252LF?qs=VW5eOWd7Luy89Xw%2FKwu%2Fxg%3D%3D) | 218.97 | 1094.85 |
| 5 | SIGNAL | RCA-JACK | PJRAN1X1U02AUX | [PJRAN1X1U02AUX Switchcraft \| Mouser India](https://www.mouser.in/ProductDetail/Switchcraft/PJRAN1X1U02AUX?qs=mcPJWgAPNrfnzxVPOaEt1A%3D%3D) | 277.68 | 1388.4 |
| 1 | Power | 24V 30A |  | [SMPS](https://www.electropi.in/24v-30amp-smps-720w-dc-metal-power-supply-nwp-india?gad_source=1&gad_campaignid=23329895947&gbraid=0AAAAA-s6SdUjZWr9YCGbH4icIqFa3hjFX&gclid=CjwKCAjw8arQBhB9EiwAfIKdQgc_rpZojPv0Mygbbj7UUXyriQciigStOZzCfHfr27ALZGUfF0p5OhoCSjsQAvD_BwE) | 3999 | 3999 |
| 2 | Transformer | Flyback | BSC25-T1010A | [Flyback](https://amzn.in/d/0g0eCBQw) | 499 | 998 |
| 5 | PCB |  |  |  | 989 | 989 |
|  |  |  |  |  | Shipping | 1200 |
|  |  |  |  |  | Total (INR) | 17226 |
|  |  |  |  |  | Total (USD) | 172.26 |



