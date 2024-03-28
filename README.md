# Pagination dan Pencarian

Pagination adalah proses membagi konten yang panjang menjadi beberapa halaman terpisah untuk meningkatkan keterbacaan dan pengalaman pengguna. Ini adalah teknik umum yang digunakan di banyak situs web, terutama di situs web yang memiliki banyak konten, seperti forum, situs berita, toko online, dan banyak lagi.

Pencarian dalam website adalah fitur yang memungkinkan pengguna untuk mencari konten tertentu di dalam situs web. Pengguna dapat memasukkan kata kunci atau frasa untuk mencari informasi yang relevan dengan kebutuhan mereka. Pencarian dapat menjadi fitur yang sangat berguna dalam mengakses konten yang diinginkan dengan cepat di situs web yang memiliki banyak halaman atau konten.

### Membuat Pagination

1. Untuk membuat pagination, buka Kembali Controller Artikel, kemudian modifikasi kode pada method admin_index seperti berikut.

```php
public function admin_index()
{
    $title = 'Daftar Artikel';
    $model = new ArtikelModel();
    $data = [
        'title' => $title,
        'artikel' => $model->paginate(10), #data dibatasi 10 record per halaman
        'pager' => $model->pager,
    ];
    return view('artikel/admin_index', $data);
}
```

2. Kemudian buka file views/artikel/admin_index.php dan tambahkan kode berikut dibawah deklarasi tabel data.

```
<?= $pager->links(); ?>
```

3. Selanjutnya buka kembali menu daftar artikel, tambahkan data lagi untuk melihat
   hasilnya.

![X-1](https://github.com/liskaniaaprilia/Program4Web/assets/115616044/0f65ee5e-f6cb-45cf-b5a6-2110e9777e79)

### Membuat Pencarian

1. Untuk membuat pencarian data, buka kembali Controller Artikel, pada method
   admin_index ubah kodenya seperti berikut

```php
public function admin_index()
{
    $title = 'Daftar Artikel';
    $q = $this->request->getVar('q') ?? '';
    $model = new ArtikelModel();
    $data = [
        'title' => $title,
        'q' => $q,
        'artikel' => $model->like('judul', $q)->paginate(10), # data dibatasi 10 record per halaman
        'pager' => $model->pager,
    ];
    return view('artikel/admin_index', $data);
}
```

2. Kemudian buka kembali file views/artikel/admin_index.php dan tambahkan form
   pencarian sebelum deklarasi tabel seperti berikut:

```html
<form method="get" class="form-search">
  <input type="text" name="q" value="<?= $q; ?>" placeholder="Cari data" />
  <input type="submit" value="Cari" class="btn btn-primary" />
</form>
```

3. Dan pada link pager ubah seperti berikut.

```
<?= $pager->only(['q'])->links(); ?>
```

4. Selanjutnya ujicoba dengan membuka kembali halaman admin artikel, masukkan kata
   kunci tertentu pada form pencarian.

![X-2](https://github.com/liskaniaaprilia/Program4Web/assets/115616044/2b781ea0-48a2-43c6-91f0-11d30a7687f0)

# FINISH
