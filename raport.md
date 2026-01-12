Wnioski i podsumowanie

Celem projektu było zbudowanie algorytmicznej strategii inwestycyjnej generującej sygnały kupna i sprzedaży na rynku akcji przy wykorzystaniu algorytmów uczenia maszynowego. 
W tym celu zastosowano modele XGBoost oraz RandomForest, których hiperparametry zostały zoptymalizowane z wykorzystaniem walidacji krzyżowej przystosowanej do szeregów czasowych (TimeSeriesSplit). 
Decyzje inwestycyjne generowane były na podstawie prawdopodobieństw predykcji modelu oraz progów decyzyjnych wyznaczonych na danych treningowych.

Przeprowadzony backtest z użyciem biblioteki vectorbt, z uwzględnieniem prowizji i poślizgu transakcyjnego, wykazał, że strategie oparte na uczeniu maszynowym osiągnęły lepsze wyniki 
inwestycyjne niż strategia pasywna typu Buy & Hold w analizowanym okresie testowym. Szczególnie dobre rezultaty uzyskał model XGBoost, który osiągnął stopę zwrotu na poziomie około 9,5% 
przy maksymalnym obsunięciu kapitału wynoszącym około 5,5% oraz współczynniku Sharpe’a przekraczającym 2,5. Dla porównania, strategia Buy & Hold w tym samym okresie zanotowała stratę 
kapitału oraz znacznie wyższe obsunięcie.

Na podstawie wyników backtestu jako finalny model wybrano XGBoost, gdyż zapewniał on najlepszy kompromis pomiędzy stopą zwrotu a ryzykiem inwestycyjnym. Model ten charakteryzował się nie
tylko najwyższą rentownością, ale również mniejszą zmiennością wyników i niższym maksymalnym obsunięciem kapitału w porównaniu do RandomForest. Zastosowanie progów decyzyjnych (histerezy) 
pozwoliło ograniczyć liczbę transakcji i zredukować wpływ szumu rynkowego, koncentrując handel na sytuacjach o większej pewności predykcji modelu.

Należy jednak podkreślić, że uzyskane wyniki obarczone są istotnymi ograniczeniami. Po pierwsze, okres testowy obejmuje stosunkowo krótki fragment historii rynku, co może prowadzić do 
niestabilności wyników w dłuższym horyzoncie. Po drugie, analiza została przeprowadzona wyłącznie dla jednej spółki, co ogranicza możliwość uogólnienia wniosków na inne instrumenty 
finansowe. Dodatkowo, pomimo zastosowania walidacji czasowej, istnieje ryzyko nadmiernego dopasowania modelu do danych historycznych, zwłaszcza w kontekście doboru progów decyzyjnych.

Podsumowując, projekt pokazuje, że odpowiednio zaprojektowany model uczenia maszynowego, wsparty inżynierią cech oraz realistycznym backtestem, może generować konkurencyjne strategie
inwestycyjne w porównaniu do prostych strategii pasywnych. Jednocześnie uzyskane rezultaty należy traktować jako eksperymentalne, a ich praktyczne wykorzystanie wymaga dalszych testów, 
rozszerzenia analizy na wiele instrumentów oraz zastosowania procedur typu walk-forward i okresowej aktualizacji modelu.
