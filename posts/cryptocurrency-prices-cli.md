---
title: CRYPTOCURRENCY PRICES CLI
date: 2024-05-27
description: Script Tools for checking cryptocurrency prices and more on your Terminal
image: /assets/img/Post/Bitcoin.jpeg
author: "cmalf"

## CRYPTOCURRENCY PRICES CLI

This script made by php basic curl. for scraping web data from [CryptoBubble](https://cryptobubbles.net) so we have unlimited api for checking prices cryptocurrencies cli.

## `script` CODE

```php
<?php
/*
 CODER : FURQONFLYNN
WEB SCRAPING CRYPTOCURRENCY PRICES
sc site : cryptobubbles.net
https://github.com/caturmahdialfurqon
*/
error_reporting(FUCKHAPPENINGAGAIN);
system('clear');
$lb = "\033[1;36m"; $pt = "\033[0;37m"; $r = "\033[1;31m"; $gr = "\033[1;32m"; $y = "\33[1;33m"; $mg = "\033[35m";
$bb = "\033[47m"; $rr = "\033[41m";
function own($url, $ua, $data = null) {
    while (True){
        $ch = curl_init();
        curl_setopt_array($ch, array(
            CURLOPT_URL => $url,
            CURLOPT_FOLLOWLOCATION => 1,));
        if ($data) {
            curl_setopt_array($ch, array(
                CURLOPT_POST => 1,
                CURLOPT_POSTFIELDS => $data,));
        }
        curl_setopt_array($ch, array(
            CURLOPT_HTTPHEADER => $ua,
            CURLOPT_SSL_VERIFYPEER => 1,
            CURLOPT_RETURNTRANSFER => 1,
            CURLOPT_COOKIEJAR => 'cookie.txt',
            CURLOPT_COOKIEFILE => 'cookie.txt',));
        $run = curl_exec($ch);
        curl_close($ch);
        if ($run) {
            return $run;
        } else {
            echo "\33[1;33mCheck Your Connection!\n";
            sleep(2);
            continue;
        }
    }
}
function x($x1, $x2, $xdata) {
    $xget = explode($x2, explode($x1, $xdata)[1])[0];
    return $xget;
}

function timer($clk) {
    $ti = time()+$clk;
    while (1) :
    echo "\r                        \r";
    $res = $ti-time();
    if ($res < 1) {
        break;
    }
    echo date('H:i:s', $res);
    sleep(1);
    endwhile;
}

//===================================START_CODE====================================//

/*
==============================================
deactivate while(true) with "//" 
below stop keep running mode
==============================================
*/
while(1){
/*
change the compare currency "default" with yours
available USD,EUR,RUB,BRL,GBP,INR,AUD,CAD,PLN,TRY
BTC,ETH
nb : {lowercase}
*/
$default = "usd";
$af = "backend/data/bubbles1000.".$default.".json";
$lk = "https://cryptobubbles.net/$af";
$u = array(
"Host: cryptobubbles.net",
"User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36",
"Accept: */*",
"Referer: https://cryptobubbles.net/",
"Accept-Language: id-ID,id;q=0.9,en-US;q=0.8,en;q=0.7",
);

$gw = own($lk,$u);
/*
============================================
activate to print json with out decoding
============================================
*/

//print_r($gw);

/*
============================================
activate this code To print output
all list coin rank 1-1000 with array
============================================
*/
//$pretty = json_decode($gw);
//print_r($pretty);
//============================================

$code = readline("$pt INPUT COIN $y => $lb ");
$cap = strtoupper($code);
$a = '"';
$as = $a.$cap.$a;
$coin = x($as,',{"id"',$gw);
$td = x('"symbols":',',"image',$coin);
$cg = x('"cg_id":"','",',$coin);
$price = x('"price":',',',$coin);
$cs = x('"circulating_supply":',',',$coin);
$dm = x('"dominance":',',',$coin);
$rd = x('"rankDiffs":',',"cg',$coin);
$mc = x('"marketcap":',',',$coin);
$vl = x('"volume":',',',$coin);
$pf = x('"performance":','},{"id"',$coin);
$x = "$code/$default";
$x0 = strtoupper($x);
echo "
$pt==================================x
$pt         $x0
$pt==================================x
$r [$pt+$r]$pt NAME/ID $r = $mg $cg
$r [$pt+$r]$pt TICKER  $r = $pt $cap
$r [$pt+$r]$pt PRICE   $r = $gr $price
$y=====================================================x
$r [$pt+$r]$pt circulating_supply $r = $pt $cs
$r [$pt+$r]$pt dominance          $r = $pt $dm
$r [$pt+$r]$pt marketcap          $r = $pt $mc
$r [$pt+$r]$pt volume             $r = $pt $vl
$r [$pt+$r]$pt rankDiffs          $r = $pt $rd
$r [$pt+$r]$pt performance        $r = $pt $pf
$y====================================================x
$lb TRADE ON 
$pt $td
$y====================================================x
\n";

timer(5);
/*
==============================================
deactivate } with "//" 
below stop keep running mode 
(syntax error "in case")
==============================================
*/
}


//===================================END====================================//

```

> I use PHP `7.4.33` (cli).
{: .prompt-warning }

- [x] Just copy paste code into yout fav text editor and save it in php extention.

- [x] Or just visit My github page [CRYPTOCURRENCY PRICES CLI](https://github.com/caturmahdialfurqon/Cryptocurrency-Prices-Console-Terminal)

And clone it with git clone

```bash
git clone https://github.com/caturmahdialfurqon/Cryptocurrency-Prices-Console-Terminal.git
```

open file directory and type `on your terminal`:

```bash
php price.php or ./price.php 
```
> if you choose ./price.php dont forget to change mod for the file with `chmod +x`
{: .prompt-tip }

## This the script look like when your running it.

![Furqonic](/assets/img/Post/price-cli/price1.png)