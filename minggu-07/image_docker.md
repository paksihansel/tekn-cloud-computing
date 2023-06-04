### Image Wordpress DockerHub</br>
WordPress adalah alat blogging sumber terbuka dan gratis dan sistem manajemen konten (CMS) berdasarkan PHP dan MySQL, yang berjalan di layanan hosting web. Fitur termasuk arsitektur plugin dan sistem template. WordPress digunakan oleh lebih dari 22,0% dari 10 juta situs web teratas per Agustus 2013. WordPress adalah sistem blog paling populer yang digunakan di Web, di lebih dari 60 juta situs web. Bahasa yang paling populer digunakan adalah bahasa Inggris, Spanyol dan Bahasa Indonesia.
Untuk melakukan pull dan menjalankan image wordpress kita bisa menjalankan perintah sebagai berikut :
<blockquote>docker run --name some-wordpress -p 8080:80 -d wordpress</br>
</blockquote></br>

![01](image-01.png)


Dengan perintah diatas, docker akan melakukan pull library yang dibutuhkan untuk menjalankan image wordpres.</br>

Setelah proses pull dan run selesai, selanjutnya wordpress bisa kita akses pada web browser dengan alamat : 
<blockquote>http://localhost:8080 or http://host-ip:8080</blockquote></br>

![01](image-02.png)