Algorithmic Trading z wykorzystaniem uczenia maszynowego

Repozytorium zawiera projekt algorytmicznej strategii inwestycyjnej dla rynku akcji, opartej na algorytmach uczenia maszynowego. Projekt został zrealizowany w celach edukacyjnych w ramach przedmiotu z zakresu finansów ilościowych / analizy danych.

Celem było stworzenie modelu generującego sygnały kupna i sprzedaży, optymalizacja hiperparametrów oraz ocena skuteczności strategii przy użyciu realistycznego backtestu.

Dane

Instrument: Apple Inc. (AAPL)

Źródło danych: Yahoo Finance (yfinance)

Zakres treningowy: 2015-01-01 – 2023-12-31

Zakres testowy: 2024-01-01 – 2024-05-06

Inżynieria cech

Model wykorzystuje zestaw wskaźników technicznych, m.in.:

logarytmiczne stopy zwrotu,

średnie kroczące (SMA, EMA),

RSI,

Bollinger Bands,

miary zmienności (rolling volatility, ATR),

cechy świecowe oraz wolumenowe.

Wszystkie cechy obliczane są wyłącznie na podstawie danych historycznych (bez look-ahead bias).

Model i optymalizacja

Zastosowano dwa modele klasyfikacyjne:

XGBoost

RandomForest

Hiperparametry optymalizowano przy użyciu RandomizedSearchCV z walidacją czasową (TimeSeriesSplit). Metryką optymalizacyjną był ROC AUC.

Strategia inwestycyjna

Model estymuje prawdopodobieństwo wzrostu ceny w kolejnym dniu. Na tej podstawie generowane są sygnały transakcyjne z wykorzystaniem mechanizmu histerezy:

BUY (LONG) gdy P(UP) > upper

SELL → CASH gdy P(UP) < lower

w przeciwnym wypadku pozycja pozostaje niezmieniona

Progi decyzyjne (upper, lower) wyznaczane są jako kwantyle rozkładu prawdopodobieństw na zbiorze treningowym.

Charakterystyka strategii:

long-only (bez krótkiej sprzedaży),

brak lewarowania,

pełne wejście lub pełna gotówka,

uwzględnione prowizje i poślizg cenowy.

Backtest

Backtest przeprowadzono z użyciem biblioteki vectorbt, przystosowanej do testowania strategii ilościowych. Wyniki strategii porównano z benchmarkiem Buy & Hold dla tego samego instrumentu i okresu.

Wyniki

Strategie oparte na uczeniu maszynowym przewyższyły strategię pasywną Buy & Hold w analizowanym okresie testowym.

Najlepsze wyniki uzyskał model XGBoost, który osiągnął:

ok. 9,5% stopy zwrotu,

maksymalne obsunięcie ok. 5,5%,

współczynnik Sharpe’a > 2,5.

Na tej podstawie XGBoost został wybrany jako finalny model.

Ograniczenia

krótki okres testowy,

analiza jednej spółki,

możliwe ryzyko nadmiernego dopasowania,

brak testów w warunkach rzeczywistych (live trading).

Technologie

Python, pandas, numpy, scikit-learn, XGBoost, vectorbt, yfinance

Struktura repozytorium
algorithmic_trading_FINAL.ipynb   # Główny notebook projektu
README.md                         # Dokumentacja

Zastrzeżenie

Projekt ma charakter edukacyjny i nie stanowi porady inwestycyjnej.
