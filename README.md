# 🔌 Symetryczny zasilacz liniowy ±30 V

Projekt liniowego zasilacza symetrycznego przeznaczonego do zastosowań laboratoryjnych oraz testowania układów analogowych.

Układ umożliwia regulację napięcia dodatniego i ujemnego względem wspólnej masy oraz został zaprojektowany i zbudowany od podstaw – od schematu, przez PCB, aż po kompletną obudowę.

---

## 📷 Zdjęcia

### 🔧 Wnętrze
<img width="4032" height="3024" alt="1000005380" src="https://github.com/user-attachments/assets/5f52821a-2ec7-4484-b5ad-993e4410f4da" />

### 🎛️ Panel przedni
<img width="4032" height="3024" alt="1000005379" src="https://github.com/user-attachments/assets/8b0b75e2-f306-4886-a346-6a196df75b80" />

### 🔌 Tył
<img width="4032" height="3024" alt="1000005381" src="https://github.com/user-attachments/assets/2b743ea5-b469-4a2f-80a0-49945f78164c" />

---

## ⚙️ Specyfikacja
\
| Parametr | Wartość |
|--------|--------|
| Napięcie wyjściowe | ±1.5 V do ±24 V (testowane) |
| Maksymalny prąd z jednej linii | ~1.5 A (regulatory) / ~4.5 A (z tranzystorami) |
| Transformator | toroidalny |
| Prąd transformatora | ~1.25 A |
| Topologia | liniowa |

---

## 🧠 Architektura

### Główne elementy:
- transformator toroidalny  
- mostek prostowniczy  
- kondensatory filtrujące  
- regulatory LM317 / LM337  
- tranzystory mocy (zwiększenie wydajności prądowej)  

---

## 🔌 Wyjścia

- 🔴 czerwony — +V  
- 🟢 zielony — GND  
- ⚫ czarny — -V  

---

## 🧪 Testy

Zasilacz został przetestowany przy użyciu prostych obciążeń (LED + rezystor).

Obserwacje:
- poprawna regulacja napięcia w całym zakresie  
- stabilna praca  
- brak zauważalnych problemów z regulacją  

---

## ⚠️ Problemy i kompromisy projektowe

### Inrush current

Największym problemem projektu okazał się prąd rozruchowy.

Duże kondensatory filtrujące na wejściu powodują:
- bardzo duży impuls prądu przy starcie  
- przepalanie bezpiecznika 1 A w gnieździe zasilania  

Tymczasowe rozwiązanie:
- zastosowanie bezpiecznika 4.5 A  

Nie jest to rozwiązanie docelowe, ponieważ:
- przekracza nominalny prąd transformatora (~1.25 A)  
- zmniejsza skuteczność zabezpieczenia  

Planowane rozwiązania:
- przeniesienie kondensatorów redukujących tętnienia z przed regulatorami do wyjścia regulatorów, które mają już konstrukcje softstartu.

---

### Ograniczenie prądu

- regulatory LM317 / LM337 posiadają ograniczenie prądowe (~1.5 A)  
- tranzystory mocy nie są zabezpieczone  

Planowane ulepszenie:
- zworka / bezpiecznik w torze tranzystorów  
- łatwiejsze debugowanie i zabezpieczenie układu  

### Kondensatory X i Y

- brakuje kondensatorów bezpieczeństaw X i Y

---

### Pomiar napięcia

Zastosowane analogowe mierniki:
- nie rozróżniają napięcia ujemnego  
- wskazują wartość bez uwzględnienia znaku  

---

### Mechanika i chłodzenie

- obudowa jest dość ciasna  
- ograniczony przepływ powietrza  
- potencjalne problemy termiczne przy dużym obciążeniu  

---

## 💬 Podsumowanie

Projekt jest w pełni działający i spełnia swoje założenia, jednak wymaga dalszego dopracowania w zakresie:

- zarządzania prądem rozruchowym  
- zabezpieczeń  
- warunków termicznych  

