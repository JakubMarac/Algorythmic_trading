Wnioski i podsumowanie

Celem projektu było zbudowanie algorytmicznej strategii inwestycyjnej generującej sygnały kupna i sprzedaży na rynku akcji z wykorzystaniem algorytmów uczenia maszynowego. W tym celu zastosowano modele XGBoost oraz RandomForest, których hiperparametry zostały zoptymalizowane przy użyciu walidacji krzyżowej dostosowanej do szeregów czasowych (TimeSeriesSplit).

Decyzje inwestycyjne były generowane na podstawie prawdopodobieństw predykcji modelu oraz progów decyzyjnych wyznaczonych wyłącznie na zbiorze treningowym, co ograniczało ryzyko dopasowania strategii do danych testowych.

Przeprowadzony backtest z użyciem biblioteki vectorbt, z uwzględnieniem prowizji oraz poślizgu transakcyjnego, wykazał, że strategie oparte na uczeniu maszynowym osiągnęły lepsze wyniki inwestycyjne niż strategia pasywna typu Buy & Hold w analizowanym okresie testowym. Szczególnie dobre rezultaty uzyskał model XGBoost, który osiągnął stopę zwrotu na poziomie około 9,5%, przy maksymalnym obsunięciu kapitału wynoszącym około 5,5% oraz współczynniku Sharpe’a przekraczającym 2,5. Dla porównania, strategia Buy & Hold w tym samym okresie zanotowała stratę kapitału oraz znacznie wyższe obsunięcie.

Na podstawie wyników backtestu jako finalny model wybrano XGBoost, gdyż zapewniał on najlepszy kompromis pomiędzy stopą zwrotu a ryzykiem inwestycyjnym. Model ten charakteryzował się nie tylko najwyższą rentownością, ale również mniejszą zmiennością wyników i niższym maksymalnym obsunięciem kapitału w porównaniu do modelu RandomForest. Zastosowanie progów decyzyjnych (mechanizmu histerezy) pozwoliło ograniczyć liczbę transakcji oraz zredukować wpływ szumu rynkowego, koncentrując handel na sytuacjach o wysokiej pewności predykcji modelu.

Należy jednak podkreślić, że uzyskane wyniki obarczone są istotnymi ograniczeniami. Po pierwsze, okres testowy obejmuje stosunkowo krótki fragment historii rynku, co może prowadzić do niestabilności wyników w dłuższym horyzoncie czasowym. Po drugie, analiza została przeprowadzona wyłącznie dla jednej spółki, co ogranicza możliwość uogólnienia wniosków na inne instrumenty finansowe. Dodatkowo, pomimo zastosowania walidacji czasowej, istnieje ryzyko nadmiernego dopasowania modelu do danych historycznych, zwłaszcza w kontekście doboru progów decyzyjnych.

Podsumowując, projekt pokazuje, że odpowiednio zaprojektowany model uczenia maszynowego, wsparty inżynierią cech oraz realistycznym backtestem, może generować konkurencyjne strategie inwestycyjne w porównaniu do prostych strategii pasywnych. Jednocześnie uzyskane rezultaty należy traktować jako eksperymentalne, a ich praktyczne wykorzystanie wymaga dalszych testów, rozszerzenia analizy na wiele instrumentów oraz zastosowania procedur typu walk-forward i okresowej aktualizacji modelu.

Strategia inwestycyjna

Celem strategii inwestycyjnej jest wykorzystanie modelu uczenia maszynowego do generowania sygnałów kupna i sprzedaży dla wybranej spółki giełdowej na podstawie danych historycznych oraz obliczonych wskaźników technicznych.

Model klasyfikacyjny XGBoost estymuje dla każdego dnia prawdopodobieństwo wzrostu ceny instrumentu w kolejnym dniu sesyjnym (klasa UP). Na podstawie tych prawdopodobieństw generowane są sygnały transakcyjne zgodnie z jasno określoną regułą decyzyjną.

Generowanie sygnałów

Zastosowano mechanizm histerezy decyzyjnej, który ogranicza częstotliwość transakcji oraz redukuje wpływ krótkoterminowego szumu rynkowego.

Wejście w pozycję długą (BUY / LONG) następuje, gdy:

- P(UP)>upper

Wyjście z pozycji (SELL → CASH) następuje, gdy:

- P(UP)<lower

Jeżeli prawdopodobieństwo znajduje się pomiędzy progami, aktualna pozycja jest utrzymywana.

Progi upper oraz lower zostały wyznaczone jako kwantyle rozkładu prawdopodobieństw predykcji modelu na zbiorze treningowym, co zapobiega ich dostosowaniu do danych testowych.

Charakterystyka strategii

- strategia typu long-only (brak krótkiej sprzedaży),
- brak zastosowania dźwigni finansowej,
- portfel w danym momencie znajduje się w całości w gotówce lub w całości w instrumencie,
- transakcje realizowane są na cenach zamknięcia (Adjusted Close),
- uwzględniono prowizje oraz poślizg transakcyjny.

Backtest

Backtest strategii został przeprowadzony z wykorzystaniem biblioteki vectorbt, przeznaczonej do testowania strategii ilościowych. Wyniki strategii porównano z benchmarkiem Buy & Hold dla tego samego instrumentu i okresu inwestycyjnego.

Interpretacja strategii

Strategia opiera się na założeniu, że model uczenia maszynowego jest w stanie identyfikować okresy o podwyższonym prawdopodobieństwie wzrostu ceny instrumentu. Zastosowanie progów decyzyjnych powoduje, że transakcje zawierane są wyłącznie w momentach, gdy model wykazuje wysoką pewność co do kierunku ruchu ceny, co przekłada się na mniejszą liczbę transakcji, niższe koszty obrotu oraz korzystniejszy profil ryzyka.
