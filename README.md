# 🇺🇾 UY22 corpus

This repo contains the notebooks used for scraping the following uruguayan media sites:

* El Observador (elobservador.com.uy)
* El País (elpais.com.uy)
* La Diaria (ladiaria.com.uy)
* Montevideo Portal (montevideo.com.uy)

Every article scraped was stored as a `.json` file with the following structure:

```json
{
    "url":      string,
    "id":       int,
    "date":     string,
    "category": string,
    "title":    string,
    "keywords": []string,
    "cover":    string,
    "body":     string,
}
```

where

* **url**: URL pointing to original article
* **id**: numeric ID (if exists, else random UID)
* **date**: article's timestamp
* **category**: article's category
* **title**: article's title or header
* **keywords**: article's tags
* **cover**: URL pointing to article's front image (if any)
* **body**: article's body

Every site is assagined a directory, and every articles is stored inside
a directory named after its publishing year.

e.g., `uy22-raw/ep22/2019/20190101120000-142502-Los_datos_del_Rey_de.json`

For every corpus, there are two versions available: 

1. **raw**: where `body` contains the raw unprocessed articles' HTML
2. **clean**: where `body` contains just text without HTML tags

Both raw & clean versions are about **6 GiB** & **4 GiB** respectively 
(totalling **10.3 GiB**) and can be downloaded from [here](https://mega.nz/folder/b6JjSDra#mwRZvu4uzkwQcke2m3Jk-w) or [here](https://archive.org/details/uy22-raw).

For every site there's also available an unified+splitted version of every
article in a single `.txt` file. (totalling **2.4 GiB**). Slipped means
that every line contains a single sentence, and unified means every articles is
separated by a blank line. The splitting was made using [pln-fing-udelar/
sentence-splitter](https://github.com/pln-fing-udelar/sentence-splitter)

```
542M dic 28 20:47 ep22-unified-splitted.txt
876M dic 27 23:04 eo22-unified-splitted.txt
854M dic 27 18:58 mp22-unified-splitted.txt
```

The concatenations of these files were used to train a [RoBERTa-like LM](https://huggingface.co/pln-udelar/roberta-base-uy22-cased) using the [HuggingFace](https://github.com/huggingface) library, and can be found here [huggingface.co/datasets/pln-udelar/uy22](https://huggingface.co/datasets/pln-udelar/uy22) or here [archive.org](https://archive.org/details/uy22-raw).
