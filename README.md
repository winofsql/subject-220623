# subject-220624

### $.ajax ( jQuery ) : フォームを偽装するサーバへの送信
```javascript
    var formData = new FormData();

    formData.append("id", "こんにちは" );

    $.ajax({
        url: "http://localhost/php-0623-01/ajax.php",
        type: "POST",
        data: formData,
        processData: false,  // jQuery がデータを処理しないよう指定
        contentType: false   // jQuery が contentType を設定しないよう指定
    })
    .done(function( data, textStatus ){
        console.log( "status:" + textStatus );
        console.log( "data:" + JSON.stringify(data, null, "    ") );

    })
    .fail(function(jqXHR, textStatus, errorThrown ){
        console.log( "status:" + textStatus );
        console.log( "errorThrown:" + errorThrown );
    })
    .always(function() {

    })
    ;
```

```php
header( "Content-Type: application/json; charset=utf-8" );
header( "Access-Control-Allow-Origin: *" );
```

### ajax.php
```php
<?php
header( "Content-Type: application/json; charset=utf-8" );
header( "Access-Control-Allow-Origin: *" );


?>
{
    "status": "ok",
    "id": "<?= $_POST["id"] ?>"
}
```

### ファイルアップロード

```javascript
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

<input type="file" name="file" id="file">
<button id="btn" onclick="file_upload();">ボタン</button>

<script>
function file_upload() {

    var formData = new FormData();

    formData.append("id", "こんにちは" );
    formData.append("upload", document.getElementById("file").files[0] );

    $.ajax({
        url: "http://localhost/php-0623-01/ajax.php",
        type: "POST",
        data: formData,
        processData: false,  // jQuery がデータを処理しないよう指定
        contentType: false   // jQuery が contentType を設定しないよう指定
    })
    .done(function( data, textStatus ){
        console.log( "status:" + textStatus );
        console.log( "data:" + JSON.stringify(data, null, "    ") );

    })
    .fail(function(jqXHR, textStatus, errorThrown ){
        console.log( "status:" + textStatus );
        console.log( "errorThrown:" + errorThrown );
    })
    .always(function() {

    })
    ;

}
</script>
```

### ファイルアップロード確認用 ajax.php
```php
<?php
header( "Content-Type: application/json; charset=utf-8" );
header( "Access-Control-Allow-Origin: *" );

file_put_contents("upload.log", print_r($_FILES, true));

?>
{
    "status": "ok",
    "id": "<?= $_POST["id"] ?>"
}
```

### ファイルアップロード実装 ajax.php
```php
<?php
header( "Content-Type: application/json; charset=utf-8" );
header( "Access-Control-Allow-Origin: *" );

file_put_contents("upload.log", print_r($_FILES, true));

@move_uploaded_file( $_FILES['upload']['tmp_name'], "test.dat" );

?>
{
    "status": "ok",
    "id": "<?= $_POST["id"] ?>"
}
```





