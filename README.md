# 📄 Automatyzacja Faktur

**Open-source'owe narzędzie do automatycznego odczytu faktur (OCR) i zapisu danych do Google Sheets z użyciem Make i PDF.co.**

---

## 🔧 Co to robi?

To rozwiązanie pozwala zeskanować fakturę telefonem, zapisać ją w formacie PDF w Dropboxie, a następnie automatycznie odczytać dane z faktury i zapisać je w Google Sheets. Dodatkowo, jeżeli już posiadamy fakturę w formacie PDF, wystarczy umieścić ją w odpowiednim folderze w Dropboxie.

---

## 🧰 Wymagania

- Konto na [Make](https://make.com) – darmowy plan wystarczy.
- Konto na [PDF.co](https://pdf.co) – darmowy 30-dniowy okres testowy.  
  Po jego zakończeniu potrzebna jest subskrypcja (ok. 10 USD miesięcznie).  
  To koszt korzystania z zewnętrznego narzędzia – autor projektu nie pobiera z tego tytułu żadnych opłat.
- Konto Google z dostępem do Google Sheets.
- Konto Dropbox – podstawowa wersja (2 GB darmowego miejsca) jest wystarczająca.

---

## 📸 Jak działa?

1. **Skanujesz fakturę telefonem**  
   Za pomocą aplikacji mobilnej Dropbox (dostępna na Android i iOS). Pobierz ją ze sklepu i zaloguj się lub załóż konto.  
   Możesz też dodać plik PDF ręcznie do wskazanego folderu w Dropbox.

2. **Plik trafia do folderu „faktury”**  
   Skan lub PDF należy umieścić w dedykowanym folderze, np. `OCR_Rachunki`.  
   To właśnie ten folder jest monitorowany przez automatyzację.

3. **Automatyzacja w Make uruchamia się**  
   - W darmowym planie Make automatyzacja sprawdza nowe pliki co 15 minut.  
   - Możesz też uruchomić ją ręcznie, jeśli chcesz przetworzyć pliki od razu.  
   - Limit w tej wersji: 3 faktury przetwarzane jednocześnie.

4. **PDF.co przetwarza fakturę (OCR)**  
   Dane są odczytywane z pliku: np. numer faktury, data, kwota, NIP itp.

5. **Dane trafiają do Google Sheets**  
   Wszystko zostaje automatycznie zapisane do przygotowanego arkusza – możesz go później eksportować, analizować lub zintegrować z innym systemem.

---

## 🛠️ Krok po kroku – instrukcja konfiguracji

### 1. Załóż wymagane konta
- Zarejestruj się w [Make.com](https://www.make.com)
- Zarejestruj się w [PDF.co](https://app.pdf.co/signup)
- Załóż konto Dropbox na [dropbox.com](https://www.dropbox.com)
- Upewnij się, że masz konto Google (do Google Sheets)

### 2. Przygotuj arkusz Google Sheets
- Utwórz arkusz z kolumnami, np.:
  - Numer faktury, Data wystawienia, Data sprzedaży, Termin płatności / Zapłacono, Nazwa sprzedawcy, NIP sprzedawcy, Ulica sprzedawcy, Miasto sprzedawcy, Kod pocztowy sprzedawcy, Kraj sprzedawcy, Nazwa nabywcy, Ulica nabywcy, Miasto nabywcy, Kod pocztowy nabywcy, Kraj nabywcy, Produkt/usługa, Wartość netto, Wartość VAT, Wartość brutto, Waluta, VAT%, Metoda płatności, Ilość, Uwagi
- Link do mojego Google Sheeta:
  [Google Sheet - wzór](https://docs.google.com/spreadsheets/d/1XcNod5BhFseqvn1TxVz4i1LwbOT3YndlpyLGaeusaug/edit?usp=sharing) - możesz go skopiować i wykorzystać, ale poczyść sobie wiersze (nagłówki zostaw!)

### 3. Stwórz folder w Dropbox
- Zainstaluj aplikację **Dropbox** na telefon – dostępna na Androida i iOS.
- Jeśli masz faktury na komputerze, możesz również korzystać z Dropbox przez przeglądarkę: [https://www.dropbox.com](https://www.dropbox.com)
- Zaloguj się i utwórz folder, np. `OCR_Rachunki`
- Faktury możesz:
  - wrzucać ręcznie do folderu,
  - lub **zeskanować bezpośrednio telefonem** – aplikacja Dropbox ma funkcję **„Skanuj”**, która pozwala łatwo zapisać dokument jako plik PDF  
    👉 *Ta metoda jest zalecana – daje najlepszą jakość pliku PDF do odczytu przez OCR*

### 4. Skopiuj scenariusz do Make

Aby wszystko zadziałało, musisz zaimportować gotowy scenariusz (tzw. blueprint) do swojego konta Make.

#### 🔽 Krok 1: Pobierz blueprint z GitHub

1. Przejdź do repozytorium na GitHub
2. Znajdź plik `Faktury-rachunki.blueprint.json` (powinien być w głównym katalogu) lub [link do pliku](https://github.com/PabloPapito/AutomatyzacjaFaktur/blob/main/Faktury-rachunki.blueprint.json)
3. Kliknij menu ... po prawej stronie
4. Kliknij przycisk **Download**

![image](https://github.com/user-attachments/assets/ed3b03f2-a61d-4b8a-a351-95ce22216f00)


#### 🧩 Krok 2: Importuj blueprint w Make

1. Zaloguj się do [Make.com](https://www.make.com/)
2. Kliknij w lewym panelu: **Scenarios**
3. W prawym górnym rogu kliknij fioletowy przycisk **+ Create a new scenario**
4. W nowym scenariuszu kliknij trzy kropki `⋮` w górnym menu → wybierz **Import blueprint**
5. Wybierz wcześniej pobrany plik `Faktury-rachunki.blueprint.json`
6. Kliknij **Import**

Gotowe! Masz już załadowany gotowy scenariusz.

---

### 🔌 Krok 3: Skonfiguruj połączenia

W każdym module (kafelku) musisz zalogować się do odpowiedniego narzędzia. Kliknij na każdy kafelek i postępuj zgodnie z poniższą instrukcją:

![image](https://github.com/user-attachments/assets/8cebf142-715e-40f4-8a55-61d31ba38cfb)


#### ✅ Dropbox

1. Kliknij na pierwszy kafelek (Dropbox Watch Files)
2. Kliknij **Add** → zaloguj się do swojego konta Dropbox
3. Nadaj nazwę np. `Dropbox – Faktury` i zatwierdź
4. Wybierz folder, który wcześniej utworzyłeś (np. `/OCR_Rachunki`)

#### ✅ PDF.co (API Key)

1. Wejdź na [https://app.pdf.co](https://app.pdf.co)
2. Kliknij w prawym górnym rogu na swoje imię → wybierz **Profile**
3. Skopiuj **API Key**
4. Wróć do Make → kliknij na kafelek `PDF.co` → kliknij **Add**
5. Wklej klucz API i zatwierdź

![image](https://github.com/user-attachments/assets/1a60b6ab-1b89-4296-a32b-334b8d7c3452)


#### ✅ Google Sheets

1. Kliknij na kafelek `Google Sheets`
2. Kliknij **Add** → zaloguj się do konta Google
3. Zatwierdź wszystkie wymagane zgody
4. Nie musisz wybierać arkusza ani kolumn – są już ustawione w blueprint’cie

#### ✅ JSON (Parser)

Nie wymaga dodatkowej konfiguracji – działa automatycznie na podstawie danych zwróconych przez PDF.co

---

### ▶️ Uruchomienie

1. Wrzuć plik PDF z fakturą do folderu Dropbox
2. Kliknij **Run once**, aby przetestować działanie
3. Po kilku sekundach dane pojawią się w Google Sheets

---

## ⚠️ Uwagi

- W darmowym planie Make automatyzacja sprawdza folder co 15 minut
- Można uruchomić ją ręcznie przyciskiem „Run once”
- Limit faktur ustawiony domyślnie na 3 jednocześnie (można zmienić)
- PDF.co po okresie próbnym wymaga wykupienia dostępu – to koszt po stronie użytkownika, **nie pobieram z tego tytułu żadnych opłat**

---

## 💡 Dla kogo jest to narzędzie?

To narzędzie będzie szczególnie pomocne, jeśli:

- Prowadzisz biuro rachunkowe i codziennie walczysz z fakturami
- Jesteś księgową, księgowym lub właścicielem firmy i chcesz zaoszczędzić czas
- Masz dość ręcznego przepisywania danych do Excela
- Chcesz uprościć sobie życie i wykorzystać technologię, która pracuje za Ciebie

To rozwiązanie jest dla ludzi – nie trzeba być programistą, żeby z niego skorzystać. A jeśli coś utknie? To ja jestem twórcą i zawsze możesz się odezwać.

---

## 🤝 Licencja i wykorzystanie

To narzędzie jest **open-source** – możesz je:

- uruchomić samodzielnie,
- modyfikować pod swoje potrzeby,
- rozwijać i dzielić się dalej.

Chcesz rozszerzyć funkcjonalność? A może potrzebujesz pomocy przy wdrożeniu?

📩 Odezwij się:
- Przez formularz na stronie: [automatyzacjabiurowa.pl](https://automatyzacjabiurowa.pl)
- Na LinkedIn: [linkedin.com/in/golen](https://www.linkedin.com/in/golen/)
- Lub dołącz do mojej zamkniętej grupy na WhatsApp: [Kliknij tutaj, aby dołączyć](https://chat.whatsapp.com/FACPJbMCnp94yqSovEgeQD)

Jestem tu, żeby pomóc.

---

### 🔗 Przydatne linki

- [Make](https://make.com)
- [PDF.co](https://pdf.co)
- [Dropbox](https://dropbox.com)
- [Google Sheets](https://sheets.google.com)

---

Czas to pieniądz. Automatyzacja to jedno i drugie. 🚀

---

## 🧩 Możliwości rozbudowy

- Obsługa różnych formatów faktur (Word, zdjęcia JPG).
- Dodanie integracji z fakturowniami.
- Ustawienie powiadomień (np. e-mail, Slack).
