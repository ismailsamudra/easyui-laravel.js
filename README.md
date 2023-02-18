# easyui-laravel.js

Cara penggunaan

pasang code di bawah pada meta header halaman laravel anda
```
<meta name="csrf-token" content="{{ csrf_token() }}">
```
lalu ganti file jquery.easyui.min.js dengan file di atas [ replace ]

biasanya ada pada folder easyui/jquery.easyui.min.js

selesai.

tag meta diatas dapat di panggil ke dalam javascript lainnya 
contoh dengan ajax :
```
$.ajax({headers: {'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')});
```
