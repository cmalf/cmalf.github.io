---
title: SSL CHECKER AND REVERSE IP
date: 2024-05-28 03:03:03 +07:00
description: Script Tools For Checking SSL AND REVERSE IP On Your Terminal
image: /assets/img/Post/chain.jpeg
author: "cmalf"
---

This script can detect/checking ssl from the domain. And can be use for Reverse IP also.

simple, to find bug operator provider, for free internet inject.

sounds fun right.

## `SOURCE` CODE

- [x] 1. for SSL

```php
<?php

error_reporting(E_ERROR | E_PARSE);
system('clear');

$lb= "\033[1;36m"; $pt= "\033[0;37m"; $r = "\033[1;31m"; $gr = "\033[1;32m"; $y = "\33[1;33m";

function getIps($domain) {
    $ips = [];
    $dnsRecords = dns_get_record($domain, DNS_A + DNS_AAAA);
    foreach ($dnsRecords as $record) {
        if (isset($record['ip'])) {
            $ips[] = $record['ip'];
        }
        if (isset($record['ipv6'])) {
            $ips[] = '[' . $record['ipv6'] . ']'; // bindto of 'stream_context_create' uses this format of ipv6
        }
    }
    return $ips;
}

function getCert($ip, $domain) {
    $g = stream_context_create(["ssl" => ["capture_peer_cert" => true], 'socket' => ['bindto' => $ip]]);
    $r = stream_socket_client("ssl://{$domain}:443", $errno, $errstr, 30, STREAM_CLIENT_CONNECT, $g);
    $cont = stream_context_get_params($r);
    return openssl_x509_parse($cont["options"]["ssl"]["peer_certificate"]);
}

function getOutputColor($daysLeft) {
    if ($daysLeft > 30) return "\e[32m";
    if ($daysLeft > 15) return "\e[33m";
    return "\e[31m";
}

$domains = array_slice($argv, 1);
$domainCount = count($domains);

if ($domainCount == 0){
    echo "
    $lb ------------------------------------------------------------------
    $pt                     Domain SSL Checker
    $lb ------------------------------------------------------------------
    $pt Usage        : $y php ssl.php $pt [$gr Domain $pt]
    $lb ------------------------------------------------------------------
    $pt example      : $y php ssl.php $gr www.furqonflynn.com 
    $lb ------------------------------------------------------------------
    $pt for multiple : $y php ssl.php $gr www.furqonflynn.com $r www.google.com
    $lb ------------------------------------------------------------------
    \n";
}

$now = new DateTime('now', new DateTimeZone('UTC'));
$expiringSoon = [];
$errors = [];
$certCount = 0;

echo "$lb ------------------------------------------------------------------ $pt \n";
echo '             Domain SSL Report for ' . $now->format('jS M Y') . "\n";
echo "$lb ------------------------------------------------------------------ \n";


foreach ($domains as $domain) {
    $ips = getIps($domain);

    if (count($ips) === 0) {
        $errors[] = $domain . " :: FAILED TO FIND SERVER IP\n";
    }

    foreach ($ips as $ip) {
        $certCount++;
        $cert = getCert($ip, $domain);

        if (!$cert) {
            $errors[] =  $domain . '@' . $ip . " :: FAILED TO GET CERTIFICATE INFORMATION\n";
            continue;
        }

        $validFrom = new DateTime("@" . $cert['validFrom_time_t']);
        $validTo = new DateTime("@" . $cert['validTo_time_t']);
        $diff = $now->diff($validTo);
        $daysLeft = $diff->invert ? 0 : $diff->days;
        if ($daysLeft <= 15) $expiringSoon[] = $domain;
        echo getOutputColor($daysLeft);
        echo $domain . (count($ips) > 1 ? " ($ip)" : "") . "\n";
        echo "\tValid From:\t " . $validFrom->format('jS M Y') . ' (' . $validFrom->format('Y-m-d H:i:s') . ")\n";
        echo "\tValid To:\t " . $validTo->format('jS M Y') . ' (' . $validTo->format('Y-m-d H:i:s') . ")\n";
        echo "\tDays Left:\t " . $daysLeft . "\n";
        echo "\e[0m\n";  
    }

}

$expiringCount = count($expiringSoon);
echo "$lb ------------------------------------------------------------ $y \n";
echo "$expiringCount of $certCount certificate" . ($certCount > 1 ? 's':'') 
    ." across $domainCount domain".($domainCount > 1 ? 's':'')." expired or expiring soon\n";
echo "$lb ------------------------------------------------------------\n";


if (count($errors) > 0) {
    echo "$lb------------------------------------------------------------$r\n";
    echo "$r !!!$pt Errors:\n\n" . "$y" . implode("\n", $errors);
    echo "$lb------------------------------------------------------------\n";
}
```

- [x] 2. For Reverse ip both

> running this code include code 1
{: .prompt-tip }

```php
<?php

error_reporting(E_ERROR | E_PARSE);
system('clear');
$lb= "\033[1;36m"; $pt= "\033[0;37m"; $r = "\033[1;31m"; $gr = "\033[1;32m"; $y = "\33[1;33m";
function menu(){
$lb= "\033[1;36m"; $pt= "\033[0;37m"; $r = "\033[1;31m"; $gr = "\033[1;32m"; $y = "\33[1;33m";
echo "
$y ------------------------------------------------------------------
$pt Credit Autor  : $y CaturMahdiAlFurqon
$pt Github        : $lb https://github.com/caturmahdialfurqon/
$pt Tools Version : $gr V.1.0
$y ------------------------------------------------------------------
$gr                   Menu Of This Tools :
$y ------------------------------------------------------------------
$r [+] $pt 1. $lb SSL CHECKER 
$r [+] $pt 2. $gr IP REVERSE
$y ------------------------------------------------------------------
\n";
}
menu();
$pil = readline("$pt ENTER YOUR CHOICE $y=> $lb");

if ($pil == 1){
	system('clear');
	$lb= "\033[1;36m"; $pt= "\033[0;37m"; $r = "\033[1;31m"; $gr = "\033[1;32m"; $y = "\33[1;33m";
    echo "
$y ------------------------------------------------------------------
$pt Credit Autor  : $y CaturMahdiAlFurqon
$pt Github        : $lb https://github.com/caturmahdialfurqon/
$pt Tools Version : $gr V.1.0
$y ------------------------------------------------------------------ 
$gr Example $pt -> 
$pt Single Target   : $lb www.furqonflynn.com
$pt Multiple Target : $gr www.google.com $y space.byu.id $lb api.midtrans.com
$r [for multiple targets separate them with spaces]
$y ------------------------------------------------------------------ 
\n";
	$domain = readline("$pt Enter Target Domain Here $y => $lb ");
	$ex = "php sslchecker.php {$domain}";
	system("$ex");
}

if ($pil == 2){
	system('clear');
	$lb= "\033[1;36m"; $pt= "\033[0;37m"; $r = "\033[1;31m"; $gr = "\033[1;32m"; $y = "\33[1;33m";
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
//===================================START====================================//
echo "
$y ------------------------------------------------------------------
$pt Credit Autor  : $y CaturMahdiAlFurqon
$pt Github        : $lb https://github.com/caturmahdialfurqon/
$pt Tools Version : $gr V.1.0
$y ------------------------------------------------------------------ \n";
$ip = readline("$r [+] $pt Target Domain name Or Ip $y => $lb ");
$lk = "https://domains.yougetsignal.com/domains.php";
$ui = array(
"Host: domains.yougetsignal.com","User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36","Content-type: application/x-www-form-urlencoded; charset=UTF-8","Accept: text/javascript, text/html, application/xml, text/xml, */*","X-Requested-With: XMLHttpRequest","Referer: https://www.yougetsignal.com/","Accept-Language: id-ID,id;q=0.9,en-US;q=0.8,en;q=0.7,ta;q=0.6",
);
$d = "remoteAddress={$ip}&key=&_=";
$go = own($lk,$ui,$d);
$rsl = json_decode($go);
//print_r($rsl);
$status = $rsl->status;
$resultsMethod = $rsl->resultsMethod;
$lastScrape = $rsl->lastScrape;
$domainCount = $rsl->domainCount;
$remoteAddress = $rsl->remoteAddress;
$remoteIpAddress = $rsl->remoteIpAddress;
$domainArray = $rsl->domainArray;
$message = $rsl->message;
if ($status == Success){
echo "
$lb ------------------------------------------------------------------
$pt [$gr+$pt] $gr Status          : $y $status
$lb ------------------------------------------------------------------
$pt [$gr+$pt] $gr ResultsMethod   : $y $resultsMethod
$lb ------------------------------------------------------------------
$pt [$gr+$pt] $gr LastScrape      : $y $lastScrape
$lb ------------------------------------------------------------------
$pt [$gr+$pt] $gr DomainCount     : $y $domainCount
$lb ------------------------------------------------------------------
$pt [$gr+$pt] $gr RemoteAddress   : $y $remoteAddress
$lb ------------------------------------------------------------------
$pt [$gr+$pt] $gr RemoteIpAddress : $y $remoteIpAddress
$lb ------------------------------------------------------------------
\n";
} else if ($status == Fail){
    echo "$r !!! $pt $message\n";
    echo "$y TIPS : $lb Change Your Ip, and try again! \n";
}
$ars = count($domainArray);
for ($a=0;$a<$ars;$a++){
    echo "$pt [$gr+$pt] "."$pt". $domainArray[$a][0].PHP_EOL;
    echo "\n";
}

//===================================ends======================================//
}
```
Just copy the source code with your fav text edit or code edit save it with php extention. and run the script.

> Please use PHP Version `7.4.33` (cli).
{: .prompt-warning }

- [x] Or just visit my `github` page [SSL-CHECKER-AND-REVERSE-IP](https://github.com/caturmahdialfurqon/SSL-CHECKER-AND-REVERSE-IP)

And clone it.

```bash
git clone https://github.com/caturmahdialfurqon/SSL-CHECKER-AND-REVERSE-IP.git
```

open the file directory and run the script by type:

```bash
php flynn.php or ./flynn.php
```

> With change file mod `chmod +x`

