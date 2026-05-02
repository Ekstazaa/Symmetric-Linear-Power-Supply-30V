# Regulowany symetryczny zasilacz liniowy (Dual-Rail)

https://github.com/Ekstazaa/Symmetric-Linear-Power-Supply-30V/blob/main/PCB_board/README.md

---

## 📖 Opis

Ta płytka PCB implementuje transformatorowy, regulowany, symetryczny zasilacz liniowy oparty na układach LM317 (szyna dodatnia) oraz LM337 (szyna ujemna).  

Projekt jest przeznaczony do zastosowań laboratoryjnych oraz audio, gdzie wymagane jest regulowane napięcie symetryczne.

Zasilacz zawiera tranzystory mocy zwiększające wydajność prądową, zabezpieczenia wyjścia, dodatkową gałąź zasilania dla elektroniki panelowej oraz standardowe elementy stabilizujące zgodne z notami katalogowymi regulatorów.

---

### 🧊 Model 3D:
<img width="1206" height="652" alt="image" src="https://github.com/user-attachments/assets/1e88aec4-d3cf-4337-9dc5-bc78ac05fb59" />

### 📐 Schemat:
<img width="1734" height="1191" alt="image" src="https://github.com/user-attachments/assets/934c705e-9a38-4ae2-ae31-69d0edb05fc9" />

---

## ⚡ Stopień wejściowy

Zasilacz jest zasilany z transformatora o parametrach:

- 2 × 32 VAC  
- Maksymalny prąd: 5 A na uzwojenie  

Prostowanie realizowane jest w konfiguracji dwudiodowej (pełnookresowej).

Po prostowaniu:

Każda szyna zawiera dwa kondensatory filtrujące 4700 µF (łącznie 9.4 mF na szynę).  
Ze względu na umiarkowaną pojemność filtrującą oraz możliwość pracy przy większych obciążeniach, tętnienia napięcia rosną przy wysokim poborze prądu.

---

## 🔧 Stopień regulacji

Regulacja napięcia realizowana jest przy użyciu:

- LM317 (szyna dodatnia)  
- LM337 (szyna ujemna)  

Regulatory są sterowane za pomocą zewnętrznych potencjometrów wieloobrotowych (montowanych na panelu przednim).

Dodatkowo na PCB przewidziano footprinty THT dla potencjometrów, co pozwala:
- używać regulacji bezpośrednio na płytce  
- skonfigurować układ jako źródło napięcia stałego  

<img width="408" height="153" alt="image" src="https://github.com/user-attachments/assets/947a3696-673c-44f5-ad98-845b30751597" />

Każdy regulator zawiera:

- kondensator wejściowy 100 nF  
- kondensator wyjściowy 1 µF  
- diody zabezpieczające przed rozładowaniem wstecznym  
- układ biasu startowego (kontrola zachowania przy starcie)

---

## 🔋 Stopień zwiększenia prądu

Aby zwiększyć wydajność prądową ponad ograniczenie ~1.5 A regulatorów LM317/LM337, zastosowano po jednym tranzystorze mocy (serii TIP) na każdą szynę.

Pozwala to na uzyskanie większego prądu wyjściowego, przy zachowaniu stabilizacji przez regulatory.

Zabezpieczenia wyjścia:

- bezpiecznik 4 A na każdą szynę  

Projekt zakłada maksymalny prąd ciągły na poziomie około 4 A.

---

## 📈 Maksymalne napięcie wyjściowe

Mimo zastosowania transformatora 2 × 30 VAC, maksymalne stabilizowane napięcie wyjściowe wynosi około:

±28 V DC  

Ograniczenie wynika ze spadków napięcia na:

- diodach prostownika  
- rezystancjach pasożytniczych  
- napięciu dropout regulatorów  
- spadku V_BE tranzystorów TIP  

---

## 🌡️ Warunki termiczne

Ze względu na wysokie napięcie wejściowe, przy niskim napięciu wyjściowym wydzielana jest znaczna moc strat.

Przybliżenie:

P ≈ (Vin - Vout) × Iout  

Ciepło wydziela się głównie w:

- regulatorach LM317 / LM337  
- tranzystorach mocy  

Zastosowane radiatory pozwalają na:

- LM317 / LM337: ~10 W  
- tranzystory TIP: ~17 W  

Zakłada to odpowiedni przepływ powietrza i poprawny montaż mechaniczny.  
Przy dużym prądzie i niskim napięciu wyjściowym może być wymagane dodatkowe chłodzenie.

---

## 🔌 Zasilanie pomocnicze

Dodatkowa gałąź oparta o LM7818 zapewnia:

- zasilanie mierników panelowych  
- diodę sygnalizacyjną LED  

<img width="259" height="248" alt="image" src="https://github.com/user-attachments/assets/1b0e8e8a-f235-46d7-a66c-f4c8405376f1" />

---

## ⚠️ Uwagi projektowe i ograniczenia

Projekt został wykonany z użyciem transformatora 2 × 30 V, głównie ze względu na jego dostępność.  

W praktyce bardziej optymalny byłby transformator o niższym napięciu wtórnym (np. 2 × 16–18 V).

W obecnym zastosowaniu wymagane napięcie to maksymalnie ±12 V, co oznacza, że:

- transformator jest przewymiarowany napięciowo  
- występują duże spadki napięcia na regulatorach  
- generowane są znaczne straty mocy  

W przyszłości planowana jest zmiana transformatora na lepiej dopasowany do zastosowania.  
Obecnie testy wykonywane są bez dużych obciążeń.

Dodatkowo:

- PCB umożliwia montaż potencjometrów THT  
- dostępne są dwa terminale śrubowe na każdą szynę (większa wygoda i elastyczność)

---

## 📁 Opis plików projektu

- **Power_supply.kicad_sch**  
  Schemat elektryczny w KiCad

- **Power_supply.kicad_pcb**  
  Layout PCB (rozmieszczenie elementów i ścieżki)

- **Power_supply.kicad_pro**  
  Plik projektu KiCad

- **Power_supply.zip**  
  Pliki produkcyjne (Gerbery + wiercenia)

- **bom.csv**  
  Lista elementów (Bill of Materials)

- **positions.csv**  
  Plik pick-and-place (pozycje komponentów)
