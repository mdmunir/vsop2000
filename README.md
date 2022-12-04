# vsop2000
time T dalam satuan julian years.
Setiap seri dinyatak dalam 3 angka (A,B,C) yang harus dihitung sebagai `A * COS(B*T + C)`.
Koefisien dalam AU dan sudut dalam radian.

Contoh dalam php
```php
function horner($x, array $c){
    $i = count($c) - 1;
    $y = $c[$i];
    while($i > 0){
        $i--;
        $y = $y * $x + $c[$i];
    }
    return $y;
}

$series = require('data/earth.php');
$T = ($jde - 2451545.0) / 365.25;

// hitung X
$coefs = [];
foreach($series['X'] as $p => $rows){
    $k = 0;
    foreach($rows as $row){
        list($A, $B, $C) = $row;
        $k += $A * cos($B*$T + $C);
    }
    $coefs[$p] = $k;
}

$X = horner($T, $coefs);
```