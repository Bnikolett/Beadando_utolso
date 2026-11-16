# Beadando_utolso
# Projekt cím: Tetoválás gyógyulási időzítő

**Hallgató:** Ballása Nikolett  
**Neptunkód:** GX5Y1V

**Alcíme:** Grafikus Python alkalmazás friss tetoválások napi ápolásának és gyógyulási fázisainak követésére.

## A projekt rövid bemutatása

A Tetoválás gyógyulási időzítő egy Tkinterrel készített alkalmazás, amely a friss tetoválás óta eltelt napok nyomon követését segíti. A felhasználó beírhatja az eltelt napok számát, vagy megadhatja a tetoválás dátumát, amelyből a program kiszámítja a napok számát. Megjelenik a megfelelő gyógyulási szakasz, az általános ápolási információ és a felhasználó által gombbal kiválasztott bőrállapotra vonatkozó visszajelzés. Rövid saját megjegyzést is lehet szöveges naplóba menteni.

A három gyógyulási szakasz oktatási célú, egyszerűsített felosztás. Az alkalmazás **nem orvosi diagnosztikai eszköz**; a valós ápolásnál a tetováló útmutatása, aggasztó tüneteknél pedig az orvosi tanács az irányadó.

## A program funkciói

1. **Nap megadása és lekérdezés.** Az „Eltelt napok” `Entry` mezőbe 0–3650 közötti egész szám írható. A „Lekérdezés” gomb ellenőrzi és megjeleníti az eredményt.
2. **Napok léptetése.** A „− Előző nap” és a „+ Következő nap” gombok egyesével módosítják a napot. A program azonnal frissíti a feliratokat, és nem lépi át a 0–3650 közötti tartományt.
3. **Számítás dátumból.** A tetoválás dátuma `ÉÉÉÉ-HH-NN` formában adható meg. A `datetime` modul `date` osztálya kiszámítja a mai naphoz viszonyított eltelt napokat. A hibás, jövőbeli vagy 3650 napnál régebbi dátumot elutasítja.
4. **Három gyógyulási szakasz.** 0–3. nap: friss tetoválás; 4–10. nap: hámlás és viszketés; 11. naptól: további regenerálódás. Mindegyikhez általános ápolási szöveg tartozik.
5. **Bőrállapot megadása gombokkal.** Három gomb használható: „Enyhén érzékeny / piros”, „Hámlik / viszket”, „Erősen fáj / terjed a pirosság”. Kattintás után a kiválasztott állapot és a hozzá tartozó szöveg rögtön megjelenik. **Nincs legördülő lista vagy Combobox.**
6. **Személyes megjegyzés mentése.** Egy rövid megjegyzés hozzáfűzhető a `tetovalas_naplo.txt` fájlhoz. A sor tartalmazza a mentés dátumát, a kiválasztott gyógyulási napot, az állapotot és a megjegyzést. Üres bejegyzést nem ment.
7. **Alaphelyzet.** A nap visszaáll 0-ra, az állapot „Nincs kiválasztva” lesz, és a dátum-, illetve megjegyzésmező kiürül. A korábban mentett naplófájlt nem törli.
8. **Kilépés.** Bezárja az alkalmazás ablakát.
9. **Hibakezelés.** Hibás nap vagy dátum, üres megjegyzés, illetve fájlmentési hiba esetén a program figyelmeztető vagy hibaablakot jelenít meg.

Az ablak alján **csak az „Alaphelyzet” és a „Kilépés” gomb** helyezkedik el. A programban nincs külső tájékoztatót vagy böngészőt megnyitó gomb.

## A program felépítése

```text
Tetovalas_gyogyulasi_idozito/
├── main.py
├── sajat_modul_bn.py
├── README.md
```

A `tetovalas_naplo.txt` fájlt az első sikeres mentés hozza létre, ezért a leadandó projektbe nem szükséges előre elkészíteni. Nincs külön tesztmodul vagy tesztfájl. A két Python-fájlban nincs komment.

### 1. main.py – grafikus felület és eseménykezelés

A `TetovalasApp` osztály elkészíti a főablak tartalmát: címeket, `ttk.LabelFrame` és `ttk.Frame` kereteket, `Label` feliratokat, `Entry` mezőket és `Button` gombokat. A gombok `command=` paraméterei a megfelelő metódusra mutatnak. A metódusok a saját adatkezelő osztályt hívják meg, majd a `nezet_frissitese()` a `bn_frissites()` által visszaadott adatokat megjeleníti.

**A főablak tényleges indítása a main.py 232–235. sorában történik:**

```python
if __name__ == "__main__":
    fo_ablak = tk.Tk()
    app = TetovalasApp(fo_ablak)
    fo_ablak.mainloop()
```

A Python a fájl első sorától feldolgozza az importokat és a definíciókat; az alkalmazást a fenti blokk indítja el, ha a `main.py`-t közvetlenül futtatjuk. A `mainloop()` ezután figyeli a felhasználói eseményeket.

### 2. sajat_modul_bn.py – saját adatkezelő modul

A `TetovalasKezeloBN` osztály tárolja a napot, a dátumot és a kiválasztott állapotot. Az ellenőrzést, a dátumszámítást, a napléptetést, az állapotválasztást, az alaphelyzet visszaállítását és a naplómentést metódusok végzik. A saját `bn_elso_fuggveny()`, `bn_masodik_fuggveny()`, `bn_harmadik_fuggveny()` és `bn_allapot_fuggveny()` függvények részt vesznek a gyógyulási szövegek összeállításában. A `bn_frissites()` egy szótárban adja vissza a felület számára szükséges értékeket.

A saját modul **nem indít önálló alkalmazást**: csak definíciókat és konstansként kezelt adatokat tartalmaz. Közvetlenül futtatható Python-fájlként, de nincs benne saját GUI-indító blokk vagy `mainloop()` hívás, így nem nyit ablakot.

## Modulok és a programban használt elemeik

| Modul | Szerepe | Felhasznált elemek |
|---|---|---|
| `tkinter`, `tkinter.ttk`, `tkinter.messagebox` | Tanult grafikus modul | `Tk()`, `Label`, `Entry`, `Button`, `Frame`, `LabelFrame`, `pack()`, `get()`, `insert()`, `delete()`, `config()`, `showwarning()`, `showerror()`, `showinfo()`, `mainloop()`, `destroy()` |
| `datetime` (`date`) | Dátumkezelés | `date.fromisoformat()`, `date.today()`, `date.isoformat()`, dátumok kivonása és `.days` |
| **`pathlib` (`Path`)** | **Új szabványos modul: fájlelérési utak kezelése** | `Path(__file__)`, `.resolve()`, `.parent`, `/` elérésiút-összefűzés, `.open()` |
| `sajat_modul_bn` | Saját adatkezelő modul | `TetovalasKezeloBN`, `max_nap`, `bn_frissites()` és a saját függvények, metódusok |

### A választott új modul: pathlib

A `pathlib` Python szabványos modul, ezért nem kell külön telepíteni. A fájlok és mappák elérési útjait **Path objektumokkal** kezeli. A projektben a `sajat_modul_bn.py` 2. sorában importáljuk:

```python
from pathlib import Path
```

A 6. sorban határozzuk meg a napló helyét:

```python
naplo_fajl = Path(__file__).resolve().parent / "tetovalas_naplo.txt"
```

- `__file__`: az aktuális Python-modulfájl elérési útját jelöli.
- `Path(__file__)`: ebből útvonalobjektumot készít.
- `.resolve()`: abszolút, feloldott elérési utat állít elő.
- `.parent`: a modulfájlt tartalmazó mappát adja vissza.
- `/ "tetovalas_naplo.txt"`: a mappához hozzáilleszti a fájlnevet. Ez **nem osztás**, hanem a `Path` típus által támogatott útvonal-összeállítás.
- `naplo_fajl.open("a", encoding="utf-8")`: megnyitja a naplót hozzáfűzésre, UTF-8 kódolással; a fájlt szükség esetén létrehozza.

Ennek előnye, hogy a napló **mindig a `sajat_modul_bn.py` mellett** jön létre, nem függ attól, honnan indítottuk a programot. A napló mentése a saját modul 147–160. sorában található.

