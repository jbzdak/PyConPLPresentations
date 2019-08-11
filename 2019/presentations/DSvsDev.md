Wstęp:
- Jak wygląda praca DS? Jaki jest flow projektu? Jakie są typowe elementy? Co to transformator? Co jest wynikiem prac DS? (Produkt, mikroserwis, prezentacja)

Tematy:
- DS kochają Condę
- DS wszystko piszą w Jupyterze - fajne narzędzie do PROTOTYPOWANIA. Są korporacje które deployują notebooki na produkcję.
- Zmuszenie DS do pisania w PyCharmie
- Testowanie kodu - testowanie modeli nie ma sensu, ale transformerów danych tak - przy czym jest trudne, bo dane składają się głównie z corner casów. Powinny być smoke testy całego flow. Sami wypuściliśmy niedziałające API.
- Praca na instancjach dla wielu osób jednocześnie. Dlaczego pracuje się na instancjach?
-- Praca na małej próbce danych nie na instancji.
-- Edycja pliku zdalna. Prototypowanie notebooków, ustawianie notebooków z certyfikatem https. 
-- Pisanie dłuższego kodu przez NFS.
- Niepushowanie "niegotowego" kodu do gita. Trzeba zrobić bardzo lekkie code review i pushować do repo. Lepiej robić dużo małych commitów, niż jeden duży.
- DSowcy kochają Pandas, który jest super, dopóki dataset jest mały - wszystko jest trzymane w pamięci i powstają dziwne bottlenecki.

Take away: 
- Zanim zaczniesz proponować rozwiązania nieprogramistom, musisz 3 razy dobrze dowiedzieć się co i jak robią. Procesy muszą z jednej strony zapewniać stabilną pracę, a z drugiej nie mogą być przeszkodą i utrudnieniem.
