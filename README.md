# System Spedycyjny „NaWczoraj”

## Opis Projektu
„NaWczoraj” to aplikacja webowa zaprojektowana w celu eliminacji rozproszonej komunikacji oraz usprawnienia procesów w branży spedycyjnej. System cyfryzuje pełną ścieżkę zlecenia transportowego – od pierwszego zapytania ofertowego, przez wycenę i realizację, aż po rozliczenie na podstawie dokumentu POD (*Proof of Delivery*)[cite: 11, 12].

---

## Zakres MVP (Wersja V1)

W wersji V1 system skupia się na krytycznym obiegu informacji i obejmuje następujące funkcjonalności[cite: 11, 12]:
* **F01 (Panel Klienta):** Składanie zapytań o transport oraz podgląd historii zleceń.
* **F02 (Pulpit Spedytora):** Kalkulacja stawek netto, przypisywanie przewoźników i weryfikacja dokumentów POD.
* **F03 (Panel Przewoźnika):** Podgląd przydzielonych tras oraz wgrywanie pliku potwierdzenia dostawy (POD).
* **F04 (Panel Magazyniera):** Obsługa rampy, ruchu towarów oraz potwierdzanie załadunku.

> *Uwaga: Zaawansowane moduły analityczne oraz automatyczna obsługa reklamacji (szkód transportowych) zostały zaplanowane do wersji V2[cite: 11, 13].*

---

## Architektura Bazy Danych (MVP)

Model relacyjny bazy danych opiera się na 6 kluczowych tabelach[cite: 12]:
1. **`Uzytkownicy`** – Tabela bazowa obsługująca konta systemowe[cite: 12].
2. **`Klienci`** – Powiązani relacją 1:N z użytkownikami[cite: 12].
3. **`Spedytory`** – Powiązani relacją 1:N z użytkownikami[cite: 12].
4. **`Przewoznici`** – Powiązani relacją 1:N z użytkownikami[cite: 12].
5. **`Zlecenia`** – Główna tabela procesowa łącząca Klienta, Spedytora i Przewoźnika za pomocą kluczy obcych[cite: 12].
6. **`DokumentyPOD`** – Tabela przechowująca pliki potwierdzeń dostawy w ścisłej relacji 1:1 z tabelą zleceń[cite: 12].

---

## Widoki Interfejsu i Walidacja

| ID Widoku | Nazwa / Rola | Główne Zadanie | Przykładowe Walidacje i Komunikaty Błędów |
| :--- | :--- | :--- | :--- |
| **W01** | Panel Klienta | Nowe zapytanie i podgląd tras[cite: 11] | • Brak wagi/miast: *„Wypełnij wszystkie wymagane pola trasa i ładunek.”*[cite: 12] |
| **W02** | Pulpit Spedytora | Giełda, wycena i przypisanie[cite: 11] | • Brak wolnych pojazdów: *„Wybrany przewoźnik nie posiada wolnych pojazdów w danym terminie.”*[cite: 12] |
| **W03** | Panel Przewoźnika | Realizacja tras i upload POD[cite: 11] | • Zły format pliku: *„Dopuszczalne formaty plików to JPG, PNG oraz PDF.”*[cite: 12] |
| **W04** | Panel Magazyniera | Obsługa rampy[cite: 11] | • *Zdefiniowane operacyjnie na poziomie przepływu rampy.*[cite: 11] |

---

## Przepływ Procesu (Workflow)

1. **Składanie zapytań (Klient - W01):** Wprowadzenie danych trasy oraz wagi ładunku[cite: 11, 12].
2. **Wycena (Spedytor - W02):** Ustalenie stawki netto i przypisanie wolnego przewoźnika[cite: 11, 12].
3. **Realizacja (Przewoźnik - W03):** Wykonanie transportu i wgranie pliku POD (JPG, PNG, PDF)[cite: 11, 12].
4. **Rozliczenie (Spedytor - W02):** Weryfikacja dokumentu POD i zamknięcie zlecenia[cite: 11, 12].

---

## Plan Rozwoju (Wersja V2)
* **UC1:** Automatyczna obsługa protokołów szkód i reklamacji ubezpieczeniowych[cite: 13].
* **UC16 / W05:** Rozbudowany panel analityczno-raportowy dla Właściciela firmy (marże, eksport do PDF/XLS)[cite: 13].
