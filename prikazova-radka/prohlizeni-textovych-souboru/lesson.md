Prozatím jsme pracovali s adresářovou strukturou a prázdnými soubory. Teď se podíváme jak prozkoumat obsah souboru.

## Stažení a prohlížení ukázkového souboru
Jako ukázkový soubor si stáhneme zdrojový kód textu předchozí lekce ve formátu Markdown. Budeme na tento soubor nahlížet jako na obyčejný textový soubor.

```shell
$ wget https://raw.githubusercontent.com/ZelenyMartin/uvod-do-linuxu/master/prikazova-radka/specifikace-cesty/lesson.md
```

Příkaz pro vypsání obsahu souboru se jmenuje `cat`.

```shell
$ cat lesson.md
```

Název příkazu `cat` nemá nic společného s kočkou. Jedná se o zkratku anglického výrazu _concatenate_, což znamená pospojovat nebo zřetězit. Příkaz `cat` umí nejen vypsat jeden soubor, ale všechny soubory, které jsou mu předány jako parametry příkazové řádky.

Pro ukázku k čemu je to dobré si stáhněme další testovací soubory.

```shell
$ wget https://kodim.cz/czechitas/uvod-do-linuxu/prikazova-radka/prohlizeni-textovych-souboru/assets/data1.txt
$ wget https://kodim.cz/czechitas/uvod-do-linuxu/prikazova-radka/prohlizeni-textovych-souboru/assets/data2.txt
```

Jednotlivě si zobrazme obsahy souborů.

```shell
$ cat data1.txt
31
15
86
10
82
24
$ cat data2.txt
69
21
13
20
24
71
```

Dohromady si soubory vypíšeme.

```shell
$ cat data1.txt data2.txt
```

S předchozí kapitoly můžeme použít i zástupné znaky.

```shell
$ cat data*
```

Pomocí znaku "větší než", který si nyní představme jako šipku, můžeme výpis přesměrovat do nového souboru, který si pojmenujeme např. `data_all.txt`.

**POZOR!** Pokud by náhodou soubor `data_all.txt` už existoval, bude jeho obsah následujícím příkazem nemilosrdně bez jakékoliv ujišťujícího dotazu přepsán.

```shell
$ cat data1.txt data2.txt > data_all.txt
```

Pokud bychom chtěli původní obsah souboru zachovat a zapsat nový text až na konec, musíme použít dvojitou šipku `>>`.


## Přehlednější zobrazení souboru

Vrátíme-li se k příkladu vypsání obsahu souboru `lesson.md`, uvidíme, že pokud je počet řádků souboru větší než výška našeho terminálu, musím na začátek souboru scrollovat kolečkem. Někdy je tento způsob dost nepřehledný, protože se nám začátek textového souboru vizuálně smísí s předchozím textem v našem terminálu a nevidíme pořádně, kde soubor vlastně začíná.

Abychom si pomohli, představíme si další příkazy pro prohlížení souborů.

```shell
$ head lesson.md
```

Příkaz `head` vypíše začátek souboru. Ve výchozím nastavení vypisuje prvních 10 řádků souboru. Toto je možné upravit parametrem `-n`.

```shell
$ head -n 5 lesson.md
```

Podobně funguje příkaz `tail`, který naopak vypisuje poslední řádky souboru.


```shell
$ tail lesson.md
```

```shell
$ tail -n 5 lesson.md
```

Posledním hezkým nástrojem pro zobrazení souboru je program `less`. Tento příkaz, podobně jako program `man`, funguje interaktivně a na celý terminál nám zobrazí obsah souboru. Také nám umožní souborem procházet pomocí šipky nahoru a dolu a kláves _Home_ a _End_. Neméně důležitou funkcionalitou je interaktivní vyhledávání, které spustíme klávesou lomítko `/`, na další výskyt vyhledávaného textu se posuneme klávesou _n_ a na předchozí výskyt velkým _N_. Program `less` ukončíme opět klávesou _q_.

```shell
$ less lesson.md
```

## Další nejzákladnější příkazy nad soubory

Umíme už vypsat celý soubor pomocí příkazu `cat` a umíme vypsat začátek pomocí `head` a konec díky `tail`. Nyní si ukážeme jak textový soubor prohledávat.

K tomu nám poslouží program `grep`.

### grep

```shell
$ grep <co hledávám> <název souboru>
```

Grep budeme používat s dvěma hlavními parametry, a to jako první parametr hledaný řetězec a jako druhý parametr bude název souboru, který se má prohledávat. Program grep neumí jen prosté vyhledávání řetězců v textovém souboru. Jeho hlavní síla tkví ve využití regulárních výrazů. Jedná se však o pokročilou část, kterou nebudeme v úvodním kurzu probírat a zájemce odkážu na [kapitolu o využití regulární výrazů v Pythonu](https://kodim.cz/czechitas/progr2-python/python-pro-data-2/regularni-vyrazy).

Při ukázce použití programu `grep` se vrátíme ke zdrojovému kódu lekce ve formátu Markdown. Markdown formátování kapitol začíná znakem _hash_ _#_ (a nadpis druhé úrovně je vyjádřen dvěma mřížkami _##_). Pozor: hledaný text _##_ zde musíme uzavřít do uvozovek (jedno jestli jednoduchých nebo dvojitých). V linuxovém shellu je znak _#_ považován za začátek komentáře, a tak by se nám zbytek příkazu ignoroval. Komentáře se tedy zapisují stejně jako např. v jazyce Python.

```
$ grep '##' lesson.md
## Specifikace cesty
## Vyhledávání souborů
## Stažení a rozbalení pracovních dat
## Příklady použití příkazu find
```

Program _grep_ má také mnoho užitečných přepínačů. Např. `grep -i` ignoruje velikost písmen v hledaném textu nebo `grep -v` invertuje výběr (vypíše naopak řádky, které neobsahují hledaný výraz).

[[[ excs Cvičení
- spojovani
]]]

### wc

Druhý příkaz, který si ukážeme je program `wc`. Za vtipnou zkratkou se skrývá Word Count. Zavoláme-li příkaz s názvem souboru, vypíší se nám 3 čísla. V manuálové stránce zjistíme, že se jedná o počet řádků, slov a velikost souboru v bytech. Velikost souboru ukazuje i příkaz `ls -l`. Místo trojice čísel je však vhodnější znát jen jednu konkrétní hodnotu. Nejčastěji se příkaz používá jako `wc -l`, které vypíše počet řádků.

```shell
$ wc lesson.md
  88  414 3163 lesson.md
```

```shell
$ wc -l lesson.md
88 lesson.md
```

## Nejdůležitější znak v terminálu je |

<term cs="Roura" en="pipe"> nebo-li svislítko je znak, který máte na anglické klávesnici vlevo nebo nad klávesou Enter. Upřímně si myslím, že roura se používá v linuxovém terminálu tak často, že stojí za to se přeučit na anglickou klávesnici. Tento znak se v shellu používá na tajemnou konstrukci, která se popisuje jako "přesměrování standardního výstupu jednoho programu na standardní vstup druhého programu".

Většina příkazů, která akceptuje jako svůj parametr název souboru, totiž umí načítat text i ze standardního vstupu, který může vypsat jiný program na standardní výstup.

Příklad vydá za tisíc slov

```shell
$ grep '##' lesson.md | wc -l
4
```

Příkaz `grep '##' lesson.md` samotný by nám vypsal v tomto případě 4 řádky. Pokud tyto řádky pošleme spočítat příkazem `wc -l`, vypíše se nám číslo _4_.

Zkusme to zkombinovat s tím co už známe. Vypiš první kapitolu:

```
$ grep '##' lesson.md | head -n 1
## Specifikace cesty
```

Vypiš poslední kapitolu:

```
$ grep '##' lesson.md | tail -n 1
## Příklady použití příkazu find
```

Kolik se v adresáři nachází souborů s příponou _.csv_?

```shell
$ ls *.csv | wc -l
```

V posledním případě je třeba znát, že některé příkazy, jako je např. _ls_ umí poznat, jestli se jejich standardní výstup vypisuje na terminál nebo do roury. Podle toho upraví své chování.

Vyzkoušejte si např.

```shell
$ ls
```

```shell
$ ls | cat
```
