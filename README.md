# Beadando_utolso
Projekt munka:Tetovalas
## A program ezeket a funkciókat fogja teljesíteni:

*Interaktív napválasztás és lekérdezés:* A felhasználó egy beviteli mezőben megadhatja a tetoválás óta eltelt napok számát. A Lekérdezés gombra kattintva megjelenik az adott naphoz tartozó gyógyulási szakasz és az ápolási tanács.

*Automatikus dátumszámítás:* A felhasználó megadhatja a tetoválás elkészítésének dátumát év-hónap-nap formátumban. A program a datetime modul segítségével kiszámítja az azóta eltelt napok számát, és megjeleníti a megfelelő gyógyulási információkat.

*Gombokkal történő napválasztás:* A plusz és mínusz gombok segítségével egyesével lehet előre vagy hátra léptetni a napokat. A megjelenített információk automatikusan frissülnek.

*Adatok ellenőrzése:* A program ellenőrzi a beírt napok számát és a dátum helyességét. Hibás, negatív vagy nem egész szám, illetve érvénytelen dátum esetén figyelmeztető üzenetet jelenít meg.

*Gyógyulási folyamat követése:* A program három különböző gyógyulási szakaszt különböztet meg. Az egyes szakaszokhoz különböző higiéniai és ápolási tanácsokat jelenít meg.

*Állapot kiválasztása:* A felhasználó három gomb közül választhat: „Enyhén érzékeny / piros”, „Hámlik / viszket” és „Erősen fáj / terjed a pirosság”.

*Állapotfüggő visszajelzés:* A kiválasztott állapothoz külön szöveges visszajelzés jelenik meg. A program a gombok megnyomásakor automatikusan frissíti az információkat.

*Saját megjegyzések mentése:* A felhasználó rövid megjegyzést írhat a tetoválás állapotáról. A program a megjegyzést az aktuális dátummal, a kiválasztott nappal és állapottal együtt egy tetovalas_naplo.txt nevű szövegfájlba menti.

*Objektumorientált felépítés:* A program saját osztályokat használ a grafikus alkalmazás működtetésére, a kiválasztott nap és állapot tárolására, valamint a gyógyulási információk kezelésére.

*Modulok használata:* A program két Python-fájlból épül fel. A main.py tartalmazza a grafikus felületet és az eseménykezelést, míg a sajat_modul_bn.py a gyógyulási szakaszok kezelését, a dátumszámítást, az adatellenőrzést és a megjegyzések mentését.

A program a tanult tkinter és datetime modulok mellett a Python szabványos könyvtárából származó pathlib modult is használja. A pathlib segítségével határozza meg a naplófájl elérési útját.

*Alaphelyzet és kilépés:* Az Alaphelyzet gomb visszaállítja a program kezdeti állapotát, a Kilépés gomb pedig bezárja az alkalmazást.

A program eseményvezérelt működésű, vagyis a felhasználó gombnyomásai indítják el a különböző műveleteket. A beviteli mezőkbe történő gépelés önmagában nem indít lekérdezést.
