---
sidebar_position: 6
---

# 6. Store data form blog

import useBaseUrl from '@docusaurus/useBaseUrl';

Setelah pengguna mengirim data dari form blog, kita mengumpulkan semua data tersebut menjadi sebuah `object` dan disimpan dalam sebuah `variable`. Kemudian kita push atau masukkan data yang berupa object tersebut kedalam variable `blogs`.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/tree/day3-5.add-blog-post-data">
Contoh code
</a>

<br />
<br />

```js {8-17} title=index.js
// this code below endpoint app.get('/blog/:id', ......
app.get('/add-blog', function (req, res) {
    setHeader(res)
    res.render("form-blog")
})

app.post('/blog', function (req, res) {
  const blog = {
    title: req.body.title,
    post_date: '12 Jul 2021 22:30 WIB',
    author: 'Ichsan Emrald Alamsyah',
    content: req.body.content,
  };

  blogs.push(blog);

  res.redirect('/blog');
});

app.get('/contact-me', function (req, res) {
    setHeader(res)
    res.render('contact')
})
```
<img alt="image1" src={useBaseUrl('img/docs/image-3-5.png')} height="500px"/>

<br />
<br />

<div>
<a class="btn-demo" href="https://ebook-code-result-chapter-2-git-day3-5add-a5efea-demo-dumbways.vercel.app//blog">
Demo
</a>
</div>
<br />

Data yang kita kumpulkan didalam sebuah object antara lain `title`, `post_data`, `author`, dan `content`. Dimana data yang kita dapatkan dari inputan pengguna adalah data `title` dan `content`. Kemudian kita menggunakan function `push` untuk memasukkan value ke sebuah `array` dan disimpan di paling akhir / paling kanan.
