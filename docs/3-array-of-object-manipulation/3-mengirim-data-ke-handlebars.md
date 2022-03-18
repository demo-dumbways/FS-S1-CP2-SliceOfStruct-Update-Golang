---
sidebar_position: 3
---

# 3. Send data to Handlebars

Kita akan mengirim data yang ada didalam variable **blogs** ke halaman `blog` dan `detail blog` agar pengguna dapat melihat data blog.

<br />

<a class="btn-example-code" href="https://github.com/demo-dumbways/ebook-code-result-chapter-2/tree/day3-2.send-data">
Contoh code
</a>

<br />
<br />

```js {35,41,43} title=index.js
// this code below app.use("/public", express.static(path.join(__dirname, "../public")));
app.use(express.urlencoded({ extended: false }))

const blogs = [
  {
    id: 1,
    title: 'Pasar Coding di Indonesia Dinilai Masih Menjanjikan',
    post_date: '12 Jul 2021 22:30 WIB',
    author: 'Ichsan Emrald Alamsyah',
    content: `Ketimpangan sumber daya manusia (SDM) di sektor digital masih
    menjadi isu yang belum terpecahkan. Berdasarkan penelitian
    ManpowerGroup, ketimpangan SDM global, termasuk Indonesia,
    meningkat dua kali lipat dalam satu dekade terakhir. Lorem ipsum,
    dolor sit amet consectetur adipisicing elit. Quam, molestiae
    numquam! Deleniti maiores expedita eaque deserunt quaerat! Dicta,
    eligendi debitis?`,
  },
];

app.get('/', function (req, res) {
    res.send("Hello World")
})

app.get('/home', function (req, res) {
    setHeader(res)
    res.render('index')
})

const isLogin = true

app.get('/blog', function (req, res) {
  setHeader(res)
  res.render('blog', { 
    isLogin: isLogin, 
    blogs: blogs 
  });
});

app.get('/blog/:id', function (req, res) {
  const blogId = req.params.id;
  const blog = blogs.find((item) => item.id == blogId);
  setHeader(res)
  res.render('blog-detail', { blog });
});
```

Untuk mengirim data ke **handlebars**, kita menambahkan `object` pada parameter kedua **function render**. Kita tambahkan property sesuai dengan data yang dikirim dan valuenya adalah variable yang menyimpan data tersebut, contoh `{blogs: data}`.
