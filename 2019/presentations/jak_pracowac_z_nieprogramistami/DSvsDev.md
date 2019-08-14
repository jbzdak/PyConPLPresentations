# Jak pracować z programującymi nieprogramistami

## Wstęp 

### Kim jesteśmy

TODO

### Disclaimer 

1. Podane niżej pomysły sprawdzają się w "młodym" teamie w consultingowym startapie, robiącym dużo małych projektów. 
 

### Praca DS

- Jak wygląda praca DS? Jaki jest flow projektu? Jakie są typowe elementy? Co to transformator? Co jest wynikiem prac DS? (Produkt, mikroserwis, prezentacja)

### Skąd pomysł na taki temat

Anegdotka z Danielem i Grześkiem 

# Co działa

## Wspólne ustalenie API które jest zrozumiałe dla obu stron

Często da się opracować API między częścią *programistyczną* oraz częścią *nie-programistyczną*. 

Ważne uwagi: 

1. API musi być zrozumiałe dla wszystkich, musi być bardzo dokładnie przejrzane, i **wszyscy** muszą być pewni że jest dobre; 
2. Należy być otwartym na jego refaktoryzację;  

### Przykład 

        # TODO: Docstring
        def train_model(data_input_path: Path, model_store_path: Path) -> TrainModelResponse:
            # ...
            return TrainModelResponse(expected_performance=float(mean_auc))
            
        def load_model(model_store_path: Path) -> ModelPackage:            
            return ModelPackage(model=model, category_dicts=category_dicts)
                
        def predict(
            model_package: ModelPackage,
            employees_file: Path,
            shifts_file: Path,
            availability_file: Path,
        ) -> PredictResponse:
        

### Co nie działa

Zrobienie samemu API tak żeby było elegancko i modnie. 

## Przeglądy kodu jako okazja do ulepszenia praktyk 

Czasem przeglądy kodu są nie przyjemne, w naszej firmie przeglądy kodu *nie są* okazją do *gate keepingu* (tj. 
zakładamy, że zgłaszający przegląd zawsze może kliknąć guzik **merge** i odpowiedzialne napisal kod który działa). 

Przeglądy są okazją powolnej poprawy praktyk w firmie. Osoby które więcej czasu spędziły programując napisą czystszy 
kod, celem przelądu jest poprawa najważniejszych rzeczy w kodzie i zapewnienie że ktoś jeszcze go rozumie. 

Procedura przeglądania kodu: 

* Znajdź kilka rzeczy których poprawa zmieni najwięcej; 
* Przejonaj osobę zgłaszającą kod do tego że proponowane poprawki pomogą, albo: daj się przekonać że nie są warte świeczki. 
* Potraktujcie poprawę jako wspólną odpowiedzialność; 

## Brak silosu 

Sytuacja w której nad projektem pracuje jeden team zawierający i DS i Programistów jest fajna. 
        
## Jak pracować z Data scientystami

### Jupyter notebook 

Jupyter jest interaktywnym webowym środowiskiem w którym można pisać kod i od razu obserwować jego wyniki. Jeśli 
go nie znasz, zainstaluj i zacznij używać do prototypowania. 

Świetnie się w nim prototypuje kod data-science ponieważ: 

* Blisko kodu można umieścić wynik jego działania (wykresy, statystyki itp.); 
* Niektóre kroki obliczeniowe mogą trwać godzinami (trenowanie modelu) a jupyter je cacheuje ich wyniki; 
* Niektóre notebooki liczą się godzinami, to wygodnie mieć gotowy zrenderowany raport który można pokazać innym;
 
Dlaczego notebooki są czasem mało fajne: 

* Format danych nie nadaje się do przeglądania; 
* Nie wrzucisz ich na produkcje (sprawdzić czy nie Netflix)[1];

Rozwiązanie: 

* Używamy wtyczki ``jupytext``, która do plików ``*.ipynb`` dodaje pliki ``*.py``;
* Nie komituje się``*.ipynb``, chyba że zawierają wartościowe wyniki; 
* Komitowane notebooki są przeglądane; 
* Wyrzucamy prototypy w trakcie przeglądu; 
 
### 
 
## Testowanie kodu 

Automatyczne testowanie black-boxowych modeli nie ma sensu, modeli nie ma sensu. Odpowiedzialnością osoby budującej model 
jest sprawdzenie, że działa on dostatecznie dobrze i nie ma uprzedzeń. 

1. Model może mieć bardzo wysoką dokładność ze względu na wyciek w danych. Na przykład model może bardzo dobrze diagnozować 
   raka na podstawie tego że pacjent w historii choroby ma długi pobyt w szpitalu onkologicznym. 
2. Model może działać poprawnie, ale mieć uprzedzenia np. rasowe, albo do płci. Takie modele należy również poprawiać. 

Warto testować: 

* Cały pipeline transformacyjny, ew. bugi (np. wycieki danych) wprowadzone podczas obróbki danych są bardzo trudne do 
  znalezienia. 
* Warto zrobić "smoke testy" całego flow przetwarzania dancyh, czyli: uruchamiamy proces z danymi wejściowymi w dobrym
  formacie i patrzymy czy wychodzą dane w dobrym formacie. 
  
  Pomaga bezpiecznie robić deploye na produkcje. 
  
    


Tematy:
- DS kochają Condę - conda freeze nie ma małych wersji, w Condzie paczki mają opóźnione wersje, przykład Pylint który się wysypał.
- DS wszystko piszą w Jupyterze - fajne narzędzie do PROTOTYPOWANIA. Są korporacje które deployują notebooki na produkcję. Musi być używany jupytext, pliki ipynb fatalnie się diffują, muszą być dodane do gitignore.
- Zmuszenie DS do pisania w PyCharmie
- Testowanie kodu - testowanie modeli nie ma sensu, ale transformerów danych tak - przy czym jest trudne, bo dane składają się głównie z corner casów. Powinny być smoke testy całego flow. Sami wypuściliśmy niedziałające API.
- Publikowanie modeli: Docker, modele baked-in w obrazie.
- Praca na instancjach dla wielu osób jednocześnie. Dlaczego pracuje się na instancjach?
-- Praca na małej próbce danych nie na instancji.
-- Edycja pliku zdalna. Prototypowanie notebooków, ustawianie notebooków z certyfikatem https. 
-- Pisanie dłuższego kodu przez NFS.
- Niepushowanie "niegotowego" kodu do gita. Trzeba zrobić bardzo lekkie code review i pushować do repo. Lepiej robić dużo małych commitów, niż jeden duży.
- DSowcy kochają Pandas, który jest super, dopóki dataset jest mały - wszystko jest trzymane w pamięci i powstają dziwne bottlenecki.
- Lint --- czasem jest fajny, ale niektóre zasady są w praktyce trudne do spełnienia w sposób zwiększający jasność kodu. Na przykład ograniczenia ilości parametrów, długośc metod itp

Take away: 
- Zanim zaczniesz proponować rozwiązania nieprogramistom, musisz 3 razy dobrze dowiedzieć się co i jak robią. Procesy muszą z jednej strony zapewniać stabilną pracę, a z drugiej nie mogą być przeszkodą i utrudnieniem.


# Literatura

[1]: https://medium.com/netflix-techblog/notebook-innovation-591ee3221233 