---
Title: “Plasma Speaker”
Author: “Prince Yadav”
Description: “A cool Speaker without a speaker for my physcis project in college”
Created_At: “2026-05-24”
---

# May 24: Schematic Layout for Input – speaker very sentive to input as arc length depends on it
started with dc input stage first becuase i wanted stable power before touching anything else. using 24v input and making 12v rail using zener diode, initially was thinking of using 7812 regulator but then realised with 24v input the heat dissipation would become annoying so switched the plan midway
used 1N4742 zener for 12v becuase it was available and simple enough. selected 330 ohm 1 watt resistor after calculating dissipation, almost used lower watt resistor without checking properly which couldve ended bad later. added 100uf 16v cap for smoothing, was confused between 100uf and 220uf for sometime but finally went with 100uf to keep things smaller and less bulky
led indicator with 2.2k resistor added because debugging without power indication is honestly painfull. kept test points for both 24v and 12v rails for easier probing later
forgot capacitor polarity once 💀 had to recheck , looked simple in starting but somehow still took more time than expected honestly uk bcz of that multiple point 24v and 12v which I needed claude help also
 <img width="975" height="435" alt="image" src="https://github.com/user-attachments/assets/6b0e613b-5b7d-4105-9d26-5fc72719bed2" />

**Total time Spent: 30min (8:30pm to 9:00pm)**

# May 25: Schematic Layout for Flyback – also very important bcz there could be prev. power surges
worked on main power switching stage today. this part felt way more serious because its handling higher current and later driving the transformer. went with IRFP260N mosfet, cheaper mosfets felt little risky for this project bcz if the gate discharges too slowly, the mosfet stays its linear region long, get hot, and burn out.
added multiple 470uf 35v caps on input side because plasma load can pull sudden spikes and i didnt want supply rail drooping random. started with just one cap and later added more after reading about ripple current handling on claude. 35v rating choosen because input is 24v and wanted enough safety margin
used mkp10 film caps near switching side alongside electrolytics. honestly before this i didnt even know why people mix capacitor types ,later understood film caps handle high frequency switching noise much better with the help of claude 😊claude told: You cannot use normal ceramic or electrolytic caps here because they would overheat from the high-frequency AC currents 
bc327 transistor used for gate drive and diode for discharge path. routing became mess,almost connected drain and source wrong on mosfet and had to recheck pinout like twice 💀 bcz I started fully clumsy but later made it expanded.
<img width="975" height="308" alt="image" src="https://github.com/user-attachments/assets/11a31dd1-e1e1-4bd5-a2c7-d6e844185f82" />

**Note: Used claude to know about electronics and not guide with sch.. sch made based on instincts and datasheets**
 
**Total time Spent: 2hr 30min (6:00pm to 8:30pm)**

# May 26: Schematic Layout for Tunning – boss level for me

worked on zero cross detector section using LM331N (strict mathematical formulas provided by texas instruments – very stupid I feel but ok). this part was genuinly confusing, comparator and timing stuff always feels more theoretical compared to power electronics 😭 spent lot of time just reading datasheet and ate half of claude’s brain
used rc network with 10n capacitors and resistor combinations for filtering. had different values initially but timing response looked unstable (based on claude) so changed few values after experimenting little bit with claude. added decoupling cap near supply because these ic’s can behave weird if supply gets noisy especially with switching section nearby 10k and 1k resistors mainly for biasing and feedback control. got confused between output feedback path and threshold path at one on LM331. rechecked pinout maybe 3 times because datasheet diagram was looking cursed honestly 💀barrel jack and push switch added for easier testing and manual triggering. test points kept throughout becuase probing signals on crowded pcb without them becomes nightmare, already learnt that from previous stages
still not fully sure LM331 will behave exactly how i want until i verify after building it just bcz of few stupid maths
<img width="906" height="576" alt="image" src="https://github.com/user-attachments/assets/5ef4e889-ad30-4c65-842d-8542427dfbe6" />

**Total time Spent: 3hr (9:00pm to 12:00am) – very tiring to do after college**

# May 27: Schematic Layout for oscillation

worked on oscillator section using NE555. choosed 555 because its simple reliable and well documented, didnt want to deal with some complicated pwm controller on top of everything else. used 10n and 4.7n caps with resistor network around the 555 for oscillation frequency. picked values after checking calculations 0061nd. potentiometer added for frequency adjustment because transformer resonance can vary alot and i wanted manual tuning option during testing
I also added led output indicator again because seeing oscillator actually running makes debugging easier. also added test points at output and zcd signal lines too also added decoupling capacitor on supply because hv switching noise nearby could affect oscillator stability. not much else honestly, 555 becomes pretty straightforward once you stop second guessing every pin connection . 
<img width="975" height="1071" alt="image" src="https://github.com/user-attachments/assets/7849c971-c741-4986-be90-8bdab8c9457e" />

And now finally finished the full sch.. including assigning footprints…
<img width="975" height="679" alt="image" src="https://github.com/user-attachments/assets/e69f4ff9-8edc-42bb-85d3-22abed4ba2f0" />

**Total time Spent: 2hr 45min (8:00pm to 10:45pm) **

# May 28 – PCB Routing – It was a holiday in my school so free full day 😊
Started with PCB Routing – Fully mind no planning did just wt ever came to my mind so specific reasons for doing anything
<img width="975" height="981" alt="image" src="https://github.com/user-attachments/assets/126bd2d3-78f9-4199-9ab2-f6c3a682d226" />

Made a rectangle with rough estimate and then made fillet lines (3mm) – just a number which came to my mind
<img width="975" height="735" alt="image" src="https://github.com/user-attachments/assets/f6206765-6f6c-46ea-8fc4-2b678cc4cc64" />

So now my plan is keep the terminal box and aux towards one side of the pcb and the big capacitor towards the right 
<img width="975" height="571" alt="image" src="https://github.com/user-attachments/assets/81c838bf-de26-4a84-87c4-5bc9061f73fc" />

Now I place to finish the power section by placing those big rectangle components as near as possible and keeping the traces small and also I would like to keep the mosfet faced down u know for better cooling so that I can attach a aluminium block behind it
<img width="975" height="551" alt="image" src="https://github.com/user-attachments/assets/6a86c34a-334c-4d38-8b72-b326784d2e39" />

 Now post this I would like to continue with the bottom half of the board where both u1 and u2 I would like to place
<img width="975" height="551" alt="image" src="https://github.com/user-attachments/assets/78dab723-8abb-4786-ba83-9fe5058b24c8" />

Yeah so now I places everthing the only rule I followed was closed connection and u know a bit symmetry which make the board looks good.
Now its time for the wiring.
<img width="975" height="761" alt="image" src="https://github.com/user-attachments/assets/831501b4-f30c-4ab7-b675-5f6a890a56f2" />

Only F.Cu this is and did some very nicr f.silkscreen work 
<img width="975" height="779" alt="image" src="https://github.com/user-attachments/assets/6ec2d3c3-41fb-44a5-869d-8bf307c83fd4" />
 
And this is only B.cu with back silkscreen here also some very tedious work I did 
Now it time to fill these thing with copper zone uk for cooling purpose also and also for less disturbance
<img width="975" height="813" alt="image" src="https://github.com/user-attachments/assets/7170f258-287f-421b-9753-6c589192c587" />
<img width="975" height="797" alt="image" src="https://github.com/user-attachments/assets/faa9cb65-af66-4edf-87ff-78a87377754b" />

Yeah so now my PCB routing and silkscreen work is also done successfully
3D pic of my design:
<img width="975" height="717" alt="image" src="https://github.com/user-attachments/assets/ec865fa4-df96-4a87-8a34-4240f8e82b9e" />
<img width="975" height="797" alt="image" src="https://github.com/user-attachments/assets/85ef2687-fdeb-4cde-bf91-78deb69c9436" />

 
**Total time Spent: 4hr 30min (11:00am to 12:30pm – Then lunch break – from 1:30pm to 3:30pm) **

# May 28 – BOM making and selecting exact parts
Figured out all components in Mouser and made the bom fully and attached all cart photos.. 
<img width="975" height="521" alt="image" src="https://github.com/user-attachments/assets/334d6376-297a-42c9-94f5-62571f9e0e28" />
<img width="975" height="527" alt="image" src="https://github.com/user-attachments/assets/5769c8fa-f66c-4687-937b-69f10c22e162" />
<img width="861" height="1350" alt="image" src="https://github.com/user-attachments/assets/23d3d4ea-9eba-4269-b8b1-7b91c360cb6a" />
<img width="811" height="1350" alt="image" src="https://github.com/user-attachments/assets/df652508-85d1-4c8d-9fd8-07f77930973a" />
<img width="788" height="1350" alt="image" src="https://github.com/user-attachments/assets/20b2f654-33f2-427e-98a6-aeaca657a647" />
<img width="959" height="1350" alt="image" src="https://github.com/user-attachments/assets/6fccd620-6cde-455b-a036-8dacfed36f3c" />
<img width="975" height="531" alt="image" src="https://github.com/user-attachments/assets/290d6ae2-9aaf-4d51-a3b5-d7a7c4c04d21" />
<img width="975" height="537" alt="image" src="https://github.com/user-attachments/assets/a3fade9c-d3a8-4690-a447-0802e54dbc20" />

The most tedious job was to take care that in this project components could heat up and fail so selecting parts take time.. also for justifying the time u can see the bom quality
Final message – This project is for my Physics project in my college … I hope it comes out good

**Total time Spent: 1hr (9:00pm to 10:00pm)**

# June 2 – Cost Cutting

Did the cost cutting by swittching to digikey.. and funding a few things on my own
<img width="1446" height="1719" alt="Screenshot 2026-06-02 192725" src="https://github.com/user-attachments/assets/76529a41-1c2d-4bf9-947e-4109b5170903" />
<img width="1402" height="1721" alt="Screenshot 2026-06-02 192737" src="https://github.com/user-attachments/assets/33730bf7-e2a2-400c-9bbc-2a3fb7416ac2" />
<img width="1388" height="1690" alt="Screenshot 2026-06-02 192749" src="https://github.com/user-attachments/assets/561dc521-a123-420e-87c7-bf6c9abebe0c" />
<img width="1722" height="1712" alt="Screenshot 2026-06-02 192757" src="https://github.com/user-attachments/assets/18979010-415b-4884-8f3d-8998898df921" />


**Total time Spent: 30min(7:00pm to 7:30pm)**
