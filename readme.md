# ![Docker Registry] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">
**Docker Registy adalah tempat untuk menyimpan docker image Docker Registry memungkinkan kita menyimpan image Docker dan menggunakannya di mana saja.**

**Docker Hub ini adalah tempat untuk menyimpan image di cloud jadi kita bisa mengakses image milik orang lain selain itu docker hub juga gratis**

**Docker Hub https://hub.docker.com/**

# ![Docker Image] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">
**Docker Image mirip seperti installer aplikasi, dimana di dalam Docker Image terdapat aplikasi dan dependency**

**Sebelum kita bisa menjalankan aplikasi di Docker, kita perlu memastikan memiliki Docker Image aplikasi tersebut**

**Perintah untuk melihat semua isi image kita**

```bash
docker image ls
```

**Untuk download Docker Image dari Docker Registry, kita bisa gunakan perintah**

**Kita bisa mencari Docker Image yang ingin kita download di https://hub.docker.com/**

```bash
docker image pull namaimage:tag
```

```bash
docker image rm namaimage:tag
```

# ![Docker Container] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">
**Jika docker image seperti install aplikasi, maka docker container mirip seperti hasil installer**

**Satu docker image bisa digunakan untuk membuat beberapa Docker Container asalkan nama containernya berbeda**

**jika kita sudah membuat docker container maka docker image yang digunakan tidak bisa di hapus, hal ini karena sebenarnya docker container tiang meng-copy isi docker image tapi hanya menggunakan isinya saja**

**Status Container**

- Saat kita membuat container, secara default container tersebut tidak akan berjalan

- Mirip seperti kita menginstall aplikasi, jika tidak kita jalankan maka aplikasi tersebut tidak akan berjalan, begitu juga dengan container

- Oleh karena itu, setelah kita membuat container, Kita perlu menjalankan jika memang ingin di jalankan

**Melihat Container**
untuk melihat semua container, baik sedang berjalan atau tidak di docker daemon, kita bisa ginakan perintah:

```bash
docker container ls -a
```

sedangkan jika kita ingin melihat container yang sedang berjalan saja, kita bisa gunakan perintah:

```bash
docker container ls
```

**Membuat Container**
untuk membuat container kita bisa gunakan perintah:

```bash
docker container create --name namacontainer namaimage:tag
```

**Menjalankan Container**

```bash
docker container start namacontainer
```

**Menghentikan Container**

jika container ingin di hapus maka harus menghentikan containernya terlebih dahulu

```bash
docker container stop containerid/namacontainer
```

**Menghapus Container**

```bash
docker container rm namacontainer
```
# ![Docker Container Log] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">

**kadang saat terjadi masalah dengan aplikasi yang terdapat di container, sering kali kita ingin melihat detail dari log aplikasinya**

**Hal ini dilakukan untuk melihat detail kejadian apa yang terjadi di aplikasi kita, sehingga untuk mempermudah ketika kita mendapatkan masalah**

**melihat log**

```bash
docker container logs containerid/namacontainer
```

**melihat log secara realtime**

```bash
docker container logs -f containerid/namacontainer
```

# ![Docker Container Exec] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">

**Saat kita membuat container, aplikasi yang terdapat di dalam container hanya bisa di akses dari dalam container**

**oleh karena itu, kadang kita perlu masuk kedalam containernya**

**untuk masuk ke dalam container, kita bisa menggunakan fitur Container exec, dimana digunakan untuk mengeksekusi kode program yang terdapat di dalam container**

**Masuk Ke Container**

- untuk masuk ke dalam container, kita bisa mencoba mengeksekusi program bash script yang terdapat di dalam container dengan bantuan Container Exec:

```bash
docker container exec -i -t containerid/namacontainer /bin/bash
```

**-i adalah argument interaktif, menjaga inputan tetap aktif**

**-t adalah argumen untuk alokasi psuedo-TTY (Terminal Akses)**

**/bin/bash Contaoh kode program yang terdapat di dalam container**

# ![Docker Container Port] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">

**saat menjalankan container, container tersebut terisolasi di dalam Docker**

**artinya sistem host (contoh laptop kita), tidak bisa mengakses aplikasi yang ada di dalam container secara langsung, salah satu caranya adalah menggunakan Container Exec untuk masuk ke dalam containernya**

**Biasanya sebuah aplikasi berjalan pada port tertentu, misal saat kita menjalankan aplikasi redis, dia berjalan pada port 6379, kita bisa melihat port apa yang digunakan ketika melihat semua daftar container**

**Port Forwarding**

- Docker memiliki kemampuan untuk melakukan port forwarding, yaitu meneruskan sebuah port yang terdapat di sistem Host nya ke dalam Docker Container.
- Cara ini cocok jika kita ingin mengekspos port yang terdapat di container ke luar melalui sistem Host nya.

**Melakukan Port Forwarding**

- Untuk melakukan port forwarding, kita bisa menggunakan perintah berikut ketika membuat container nya:

```bash
docker container create --name namacontainer --publish posthost:portcontainer image:tag
```

- Jika kita ingin melakukan port forwarding lebih dari satu, kita bisa tambahkan dua kali parameter --publish

- --publish juga bisa disingkat menggunakan -p

# ![Docker Container Environment Variabel] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">

**Saat membuat aplikasi, menggunakan Environment Variable adalah salah satu teknik agar konfigurasi aplikasi bisa diubah secara dinamis**

**Dengan menggunakan environment variable, kita bisa mengubah-ubah konfigurasi aplikasi, tanpa harus mengubah kode aplikasinya lagi**

**Docker Container memiliki parameter yang bisa kita gunakan untuk mengirim environment variable ke aplikasi yang terdapat di dalam container**

**Menambah Environment Variable**

- Untuk menambah environment variable, kita bisa menggunakan perintah --env atau -e, misal:

```bash
docker container create --name namacontainer 1  --env KEY="value" --env KEY2="value" image:tag
```

# ![Docker Container Stats] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">

**Saat menjalankan beberapa container, di sistem Host, penggunaan resource seperti CPU dan Memory hanya terlihat digunakan oleh Docker saja**

**Kadang kita ingin melihat detail dari penggunaan resource untuk tiap container nya**

**Untungnya docker memiliki kemampuan untuk melihat penggunaan resource dari tiap container yang sedang berjalan**

```bash
docker container stats
```

# ![Docker Container Resource Limit] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">

**Saat membuat container, secara default dia akan menggunakan semua CPU dan Memory yang diberikan ke Docker (Mac dan Windows), dan akan menggunakan semua CPU dan Memory yang tersedia di sistem Host (Linux)**

**Jika terjadi kesalahan, misal container terlalu banyak memakan CPU dan Memory, maka bisa berdampak terhadap performa container lain, atau bahkan ke sistem host**

**Oleh karena itu, ada baiknya ketika kita membuat container, kita memberikan resource limit terhadap container nya.**


**Memory**

- Saat membuat container, kita bisa menentukan jumlah memory yang bisa digunakan oleh container ini, dengan menggunakan perintah --memory diikuti dengan angka memory yang diperbolehkan untuk digunakan.

- Kita bisa menambahkan ukuran dalam bentuk b (bytes), k (kilo 1  bytes), m (mega bytes), atau g (giga bytes), misal 100m artinya 100 mega bytes.

**CPU**

- Selain mengatur Memory, kita juga bisa menentukan berapa jumlah CPU yang bisa digunakan oleh container dengan parameter --cpus

- Jika misal kita set dengan nilai 1.5, artinya container bisa menggunakan satu dan setengah CPU core

**Contoh Membatasi Penggunaan Cpu dan Memory**
```bash
docker container create --name smallnginx --publish 8081:80 --memory 100m --cpus 0.5 nginx:latest
```

# ![Docker Bind Mounts] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">

**Bind Mounts merupakan kemampuan melakukan mounting (sharing) file atau folder yang terdapat di sistem host ke container yang terdapat di docker**

**Fitur ini sangat berguna ketika misal kita ingin mengirim konfigurasi dari luar container, atau misal menyimpan data yang dibuat di aplikasi di dalam container ke dalam folder di sistem host**

**Jika file atau folder tidak ada di sistem host, secara otomatis akan dibuatkan oleh Docker**

**Untuk melakukan mounting, kita bisa menggunakan parameter --mount ketika membuat container.**

**Isi dari parameter --mount memiliki aturan tersendiri.**

**jadi ketika kita membuat data di docker nah kita mau data yang sudah kita buat di sebuah container harus tetap ada walaupun containernya kita hapus kita bisa menggunakan docker bind mounts ini**

**Parameter Mount**
- type : Tipe mount, bind atau volume
- source: Lokasi file atau folder di sistem host
- destination: Lokasi file atau folder di container
- readonly: Jika ada, maka file atau folder hanya bisa dibaca di container, tidak bisa ditulis

**Untuk melakukan mounting kita bisa gunakan perintah**

```bash
docker container create --name namacontainer --mount "type=bind,source=folderSistemOperasiKita,destination=folderDocker,readonly" image:tag
```

# ![Docker Volume] <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker" width="50">

**Fitur Bind Mounts sudah ada sejak Docker versi awal, di versi terbaru direkomendasikan menggunakan Docker Volume**

**Docker Volume mirip dengan Bind Mounts, bedanya adalah terdapat management Volume, dimana kita bisa membuat Volume, melihat daftar Volume, dan menghapus Volume**

**Volume sendiri bisa dianggap storage yang digunakan untuk menyimpan data, bedanya dengan Bind Mounts, pada bind mounts, data disimpan pada sistem host, sedangkan pada volume, data di manage oleh Docker**

**Melihat Docker Volume**

- Saat kita membuat container, dimanakah data di dalam container itu disimpan, secara default semua data container disimpan di dalam volume.

- Jika kita coba melihat docker volume, kita akan lihat bahwa ada banyak volume yang sudah terbuat, walaupun kita belum pernah membuatnya sama sekali

- Kita 1  bisa gunakan perintah berikut untuk melihat daftar volume

```bash
docker volume ls
```

**Membuat Volume**

- Untuk membuat volume gunakan perintah

```bash
docker volume create namavolume
```

**Menghapus Volume**

- pastika volume tidak di gunakan oleh container

```bash
docker volume rm namavolume
```










