# easyui-laravel.js

Cara penggunaan

pasang code di bawah pada meta header halaman laravel anda
```
<meta name="csrf-token" content="{{ csrf_token() }}">
```
![ice_screenshot_20230218-170140](https://user-images.githubusercontent.com/67509798/219851831-cda94be4-64ad-40df-b7e3-2d79bf562395.png)

lalu ganti file jquery.easyui.min.js dengan file di atas [ replace ]

biasanya ada pada folder easyui/jquery.easyui.min.js

cotroller sampel code 
```
  public function get_data()
    {
        $page = isset($_POST['page']) ? intval($_POST['page']) : 1;
        $rows = isset($_POST['rows']) ? intval($_POST['rows']) : 50;
        $sort = isset($_POST['sort']) ? strval($_POST['sort']) : 'col1';
        $order = isset($_POST['order']) ? strval($_POST['order']) : 'asc';
        $search = isset($_POST['search']) ? strval($_POST['search']) : '';
        $offset = ($page - 1) * $rows;
        $result = array();
        $result['total'] = num_rows('tabel_data');
        $country = db('tabel_data')
            ->where('nama','LIKE','%'.$search.'%')
            ->orWhere('url','LIKE','%'.$search.'%')
            ->orderBy($sort, $order)
            ->orderBy('col2', $order)
            ->orderBy('col3', $order)
            ->limit($rows)
            ->offset($offset)
            ->get();
        $result = array_merge($result, ['rows' => $country]);
        return response()->json($result, 200);
     }
```

Route sampel code :
```
Route::post('/get_data', [DevCon::class,'get_data'])->name('get_data')->middleware('auth');
```
selesai.

tag meta diatas dapat di panggil ke dalam javascript lainnya 
contoh dengan ajax :
```
$.ajax({headers: {'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')});
```
