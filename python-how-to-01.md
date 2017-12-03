# Jak začít s Pythonem

Pokud chceme začít programovat a víme, že se neobejdeme bez knihoven třetích stran, je vhodné takový projekt izolovat a tím zajistsit, že knihovny nebudou instalovány globálně. To by nám mohlo později dělat problémy, pokud bychom potřebovali pro různé projekty. různé verze knihoven. Jak vytvořit izolované tzv. virtuální prostředí pro náš projekt je obsahem tohoto krátkého článku, ve kterém si popíšme několik způsobů.


## 1. Použití balíčku `pipenv`

Tohle je podle mne dnes již nejlepší způsob jak spravovat projekt.


### Instalace balíčku `pipenv`

Naistalujeme balíček `pipenv` globálně abychom ho mohli použít odkudkoliv.

    python3.6 install pipenv

### Vytvoření projektu

Vytvoříme adresář s projektem, přemístíme se do něj a vytvoříme virtuální prostředí pro tento projekt.
    
    mkdir some_project
    cd some_project

    pipenv --python 3.6 

    Creating a virtualenv for this project…
    Using /usr/local/bin/python3.6m to create virtualenv…
    …

V adresáří se vytvoří soubor `Pipfile`, vypíšeme si jeho obsah pomocí `cat Pipfile`.

    [[source]]
    url = "https://pypi.python.org/simple"
    verify_ssl = true
    name = "pypi"

    [packages]

    [dev-packages]

    [requires]
    python_version = "3.6"...

### Instalace balíčku 

Nyní už můžeme instalovat balíčky pomocí:

    pipenv install requests


### Instalace balíčku pro vývoj

Pokud jde o balíček, ketrý se používá jen pro vývoj, použijeme přepínač `--dev`.

    pipenv install --dev pytest

### Spuštění skriptu

Chceme-li spustit nějaký skript, je dobré použít taktkéž `pipenv`, ten zkontroluje, jestli je vše správě instalováno.

    pipenv run python some_script.py

### Zamknutí závislostí do soubori `Pipfile.lock`

    pipenv lock

### Odinstalování balíčku

    pipenv uninstall requests

### Závěr

Nyní už můžeme náš projekt přidat do vzdáleného repozitáře např. na github.com a kdokoliv si ho stáhne, může začít pracovat pomocí jediného příkazu:

    pipenv install


## 2. Použití balíčku `venv` ze standardní knihovny

**Tohle je pořád využívaný, ale již v budoucnu tzv. *old school*.**

Pro vytvoření virtuálního prostředí nám postačí modul `venv`, který je od verze 3.5 (?) součástí standardní knihovny. Jistě víte, že hodně modulů, kromě toho, že je můžeme použít (importovat) ve vlastním programu, může sloužit také jako klasicný konzolový program a to tak, že do kódu přidáme znmámou sekci `if __name__ == '__main__: ...`. Pokud se nacházíme v adresáři našeho projektu můžeme jednoduše zavolat modul `venv` s parametry a ten nám vytvoří adresář obsahující kopii interpreteru a knihoven.


Vytvoříme adresář, který obsahuje jak interpretr, tak standardní knihovnu izolovanou od globální instalace.

    python3.6 -m venv env

Po aktivace, se vše již insatluje do aktuálního virtuální prostředí.

    source env/bin/activate

Nyní můžeme instaloval zvolené knihivny.

    pip install request

Pozor, před každdou prací, musíme toto viirtuální prostředí aktivovat. Po přemístění adresáře `env` nám nebude virtuální prostředí správně fungovat, protože vše je provázané odkazy. Je lepší ho vytvořit prostě znovu.
