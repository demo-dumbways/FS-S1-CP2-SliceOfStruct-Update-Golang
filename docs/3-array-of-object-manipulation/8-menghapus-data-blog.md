---
sidebar_position: 8
---

# 8. Delete blog data

import useBaseUrl from '@docusaurus/useBaseUrl';

Kita perlu membuat sebuah route untuk menangani proses menghapus data blog.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/tree/day3-7.delete-blog-data">
Contoh code
</a>

<br />
<br />

```js {15-22} title=index.js
// this code below endpoint app.get('/add-blog' ......
app.post('/blog', function (req, res) {
    const blog = {
        title: req.body.title,
        post_date: '12 Jul 2021 22:30 WIB',
        author: 'Ichsan Emrald Alamsyah',
        content: req.body.content,
    };

    blogs.push(blog);

    res.redirect('/blog');
})

app.get('/delete-blog/:index', (req, res) => {
    const index = req.params.index;

    blogs.splice(index, 1);

    setHeader(res)
    res.redirect('/blog');
});

app.get('/contact-me', function (req, res) {
    setHeader(res)
    res.render('contact')
})
```
<img alt="image1" src={useBaseUrl('img/docs/image-3-2.png')} height="500px"/>

<br />
<br />

<div>
<a class="btn-demo" href="https://ebook-code-result-chapter-2-git-day3-7dele-05c1ec-demo-dumbways.vercel.app/blog">
Demo
</a>
</div>
<br />

Nama route yang kita gunakan untuk menghandle proses menghapus data blog yaitu `/delete-blog`, kemudian diikuti `/:index` agar kita dapat menangkap `index` yang dikirim melalui route/url. Untuk mengambil `index` yang dikirim, kita gunakan `req.params.index`, jadi index tersebut tersimpan didalam `req.params`.

Setelah mendapatkan value `index`, kita tampung dalam sebuah variable `index`. Kita menggunakan function `splice`, didalam function `splice` terdapat dua parameter, parameter **pertama** berisikan `index` yang ingin dihapus, parameter **kedua** berisikan jumlah data yang ingin dihapus. Karena hanya satu data blog yang ingin kita hapus, maka di parameter kedua kita isikan value `1`. Kemudian kita gunakan perintah `redirect` agar pengguna dapat diarahkan ke route yang telah diatur, contoh: kembali ke halaman blog `res.redirect('/blog')`
