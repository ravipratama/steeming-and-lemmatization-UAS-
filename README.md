# steeming-and-lemmatization-UAS-
Tugas uas
Ravi
=========

sastrawi is a simple PHP library which allows you to reduce inflected words in Indonesian Language (Bahasa Indonesia) to their base form ([stem](http://en.wikipedia.org/wiki/Stemming)).
Despite its simplicity, this library is  designed to be high quality and well documented.
For more information in english, see [README](https://github.com/andylib/sastrawi/blob/master/README.en.md).


| Development | Master | Releases | Statistics |
| ----------- | ------ | -------- | ---------- |
| [![Build Status](https://travis-ci.org/sastrawi/sastrawi.svg?branch=development)](https://travis-ci.org/sastrawi/sastrawi) [![Code Coverage](https://scrutinizer-ci.com/g/sastrawi/sastrawi/badges/coverage.png?s=942cb014be9bbbf41e62c15389663f4253f5efac)](https://scrutinizer-ci.com/g/sastrawi/sastrawi/) [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/sastrawi/sastrawi/badges/quality-score.png?s=152027ad0516653ff4eb5b05bff7266aeb600bfd)](https://scrutinizer-ci.com/g/sastrawi/sastrawi/) | [![Build Status](https://travis-ci.org/sastrawi/sastrawi.svg?branch=master)](https://travis-ci.org/sastrawi/sastrawi) | [![Latest Stable Version](https://poser.pugx.org/sastrawi/sastrawi/v/stable.png)](https://packagist.org/packages/sastrawi/sastrawi) | [![Total Downloads](https://poser.pugx.org/sastrawi/sastrawi/downloads.png)](https://packagist.org/packages/sastrawi/sastrawi) |


Stemming
---------

[_Stemming_](http://en.wikipedia.org/wiki/Stemming) adalah proses mengubah kata berimbuhan menjadi kata dasar. Contohnya:

- menahan => tahan
- berbalas-balasan => balas


Contoh kasus
-------------

Katakanlah sebuah _blog post_ berisi:

    Rakyat memenuhi halaman gedung untuk menyuarakan isi hatinya.

Pencarian dengan _query_ di bawah ini tidak akan menemukan _post_ di atas,

```slq  
SELECT * FROM posts WHERE content LIKE '%suara%'
```

Proses _stemming_ dapat membantu menemukan dokumen yang sedang dicari yaitu dengan menanggalkan imbuhan-imbuhan hingga hanya menyisakan kata dasar seperti berikut:

    rakyat penuh halaman gedung suara isi hati

Lalu kata kunci pencarian juga dijadikan kata dasar:

    Bersuara => suara












Penggunaan
-----------

Copy kode berikut di directory project anda. Lalu jalankan file tersebut.

```php
<?php
// demo.php

// include composer autoloader
require_once __DIR__ . '/vendor/autoload.php';

// create stemmer
// cukup dijalankan sekali saja, biasanya didaftarkan di service container
$stemmerFactory = new \Sastrawi\Stemmer\StemmerFactory();
$stemmer  = $stemmerFactory->createStemmer();

// stem
$sentence = 'Perekonomian Indonesia sedang dalam pertumbuhan yang membanggakan';
$output   = $stemmer->stem($sentence);

echo $output . "\n";
// ekonomi indonesia sedang dalam tumbuh yang bangga

echo $stemmer->stem('Mereka meniru-nirukannya') . "\n";
// mereka tiru
```

Menambah dan Mengurangi Kata Dasar

```php
<?php

// include composer autoloader
require_once __DIR__ . '/vendor/autoload.php';

// create stemmer
// cukup dijalankan sekali saja, biasanya didaftarkan di service container

$stemmerFactory = new \Sastrawi\Stemmer\StemmerFactory();

$dictionary = $stemmerFactory->createDefaultDictionary();
$dictionary->addWordsFromTextFile(__DIR__.'/my-dictionary.txt');
$dictionary->add('internet');
$dictionary->remove('desa');

$stemmer = new \Sastrawi\Stemmer\Stemmer($dictionary);

var_dump($stemmer->stem('internetan')); //internet
```


Pustaka
--------

#### Algoritma ####

Algoritma yang digunakan pada _library_ ini adalah hak intelektual masing-masing pemiliknya yang tertera di bawah ini.
Lalu untuk meningkatkan kualitas kode, algoritma tersebut diterapkan ke dalam _Object Oriented Design_.

- Algoritma Nazief dan Adriani
- Asian J. 2007. ___Effective Techniques for Indonesian Text Retrieval___. PhD thesis School of Computer Science and Information Technology RMIT University Australia
- Arifin, A.Z., I.P.A.K. Mahendra dan H.T. Ciptaningtyas. 2009. ___Enhanced Confix Stripping Stemmer and Ants Algorithm for Classifying News Document in Indonesian Language___, Proceeding of International Conference on Information & Communication Technology and Systems (ICTS)
- A. D. Tahitoe, D. Purwitasari. 2010. ___Implementasi Modifikasi Enhanced Confix Stripping Stemmer Untuk Bahasa Indonesia dengan Metode Corpus Based Stemming___, Institut Teknologi Sepuluh Nopember (ITS) – Surabaya, 60111, Indonesia

Saya menggunakannya untuk keperluan belajar, karena saya blm memahamami apa itu python. Terimakasih
