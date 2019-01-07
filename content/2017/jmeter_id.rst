JMeter Testing
##############

:date: 2017-06-15
:modified: 2017-06-15
:tags: JMeter, load test, automated test, performance test
:category: QA
:slug: jmeter-testing-id
:authors: Marco Hudaya, Monika Evelin
:summary: Getting started with JMeter to load testing

Intro
^^^^^
Untuk mencapai target 2000 request per detik (10.000 concurrent users), kita memerlukan sebuah metode pengukuran performa yang tepat. Dalam kasus ini JMeter kita pergunakan karena memungkinkan kita untuk merancang dan mensimulasikan traffic yang tinggi dalam kurun waktu yang pendek.

Instalasi JMeter
^^^^^^^^^^^^^^^^
Unduh JMeter dari sini: `<http://jmeter.apache.org/download_jmeter.cgi>`_

JMeter dijalankan melalui jmeter.bat (Windows) atau jmeter (Mac/Linux)

Bagi pengguna Windows, pastikan JMeter dapat mengakses jaringan

Membuat Test Plan
^^^^^^^^^^^^^^^^^
Untuk mengubah nama Test Plan, klik pada Test Plan, lalu ubah nama pada kolom Name.

    .. image:: /images/1_test_plan_rename.png
         :alt: TestPlan
         :width: 100%

* Membuat Thread

Sebuah thread merepresentasikan seorang pengguna (user), maka Thread Group merepresentasikan sekelompok pengguna. Pada Thread kita dapat melakukan konfigurasi seperti tingkat kepadatan (traffic), dan periode waktu.

Buat sebuah Thread Group dengan klik kanan pada Test Plan → Add → Thread (Users) → Thread Group.

     .. image:: /images/2_add_thread_group.png
         :alt: ThreadGroup
         :width: 100%

Anda dapat melakukan konfigurasi pada Thread Properties.

    .. image:: /images/3_thread_properties.png
         :alt: ThreadGroupConfigs
         :width: 100%

Contoh:
  - Number of Thread (users) : 50
  - Ramp-Up Period : 10
  - Loop Count : 1

Artinya terdapat request dari 50 pengguna yang dieksekusi oleh JMeter  dalam 10 waktu detik, atau dapat dikatakan bahwa setiap 1 detik JMeter akan mengeksekusi request dari 5 pengguna (10 detik / 50 pengguna = 0.2 detik).

Loop Count menjelaskan berapa kali test plan dieksekusi.

* Sampler

Buat sebuah Sampler, misalnya HTTP Request, dengan klik kanan pada Thread Group → Add → Sampler → HTTP Request

    .. image:: /images/4_add_sampler.png
         :alt: SamplerAdd

    - Isi nama Server atau IP (contoh: www.google.com)
    - Isi Path (contoh: /)

    .. image:: /images/5_setting_http_request.png
         :alt: HttpReqConf
         :width: 100%

* Listeners

Untuk melihat hasil tes menggunakan Listener, yang biasa digunakan adalah View Result Tree dan Graph Result. Klik kanan pada Thread Group (atau Test Plan) → Add → Listener → choose Listener you want.

    .. image:: /images/6_add_listener.png
         :alt: ListenersAdd
         :width: 100%

* Jalankan Tes

    - Jalankan tes dengan klik tombol “Start” (Catatan :  Simpan proyek Test Plan sebelum dijalankan).

    .. image:: /images/7_run_testing.png
         :alt: RunTest
         :width: 100%

    - Lingkaran hijau pada pojok kanan atas menunjukkan bahwa tes sedang dijalankan. Ketika tes selesai, lingkaran akan berwarna abu - abu.
    - Lihat hasil tes pada View Result Tree.

    .. image:: /images/8_testing_result_1.png
         :alt: TestResult1
         :width: 100%

    .. image:: /images/9_testing_result_2.png
         :alt: TestResult2
         :width: 100%

Terdapat request berwarna hijau dan merah. Warna hijau artinya request berhasil dieksekusi, sedangkan warna merah berarti terdapat error sehingga request gagal dieksekusi.
    - Berikut ini contoh Graph Results

    .. image:: /images/10_graph_result.png
         :alt: ResultGraph
         :width: 100%

    - Untuk menghapus hasil tes dan melakukan tes baru, klik ikon sapu yang terdapat pada toolbar di atas.



Simulation Recording
^^^^^^^^^^^^^^^^^^^^^
Aktivitas tes dapat direkam menggunakan Recording Controller.

* Setting pada Firefox Browser
    - Buka Tools → Options → Advanced → Network.
    - Pilih “Manual Proxy Configuration”
    - Atur HTTP Proxy = Localhost and Port = 8080
    - Jika menggunakan Chrome, dapat menggunakan Foxy Proxy

* Setting konfigurasi pada JMeter
    - Buat HTTP(S) Test Script Recorder untuk melihat hasil tes dengan klik kanan pada WorkBench → Add → Non-Test Elements → HTTP(S) Test Script Recorder.
    - Port : 8080 (Nomor Port harus sama dengan setting koneksi pada browser).

    .. image:: /images/20_add_recorder.png
         :alt: JmeterRecord1
         :width: 100%

    - Klik kanan pada HTTP(S) Test Script Recorder → Add → Logic Controller → Recording Controller. Step - step yang terekam akan tersimpan di sana.

    .. image:: /images/21_add_recording_controller.png
         :alt: JmeterRecord2
         :width: 100%

* Rekam Hasil Tes
    - Buka HTTP(S) Test Script Recorder, klik “Start”.

    .. image:: /images/22_run_testing.png
         :alt: StartRecord
         :width: 100%

    - Buka browser, lakukan - langkah yang diinginkan.
    - Langkah - langkah yang dilakukan tersebut akan terliaht pada recording controller
    - Klik STOP untuk berhenti merekam.
    - Untuk menghapus hasil rekaman tes sebelumnya, klik Clear All Record Samples


Data Variabel Menggunakan file CSV
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Apabila skenario tes membutuhkan eksekusi pada banyak URL, atau membutuhkan data variabel yang beragam, kita dapat menggunakan sumber data eksternal berupa file CSV. Untuk dapat melakukannya kita memerlukan elemen CSV Data Set Config di dalam test plan. CSV Data Set Config adalah elemen konfigurasi JMeter agar dapat mengakses data eksternal yang berupa file CSV. Dalam contoh berikut, kita akan menggunakan data dari file CSV untuk menguji halaman product detail.

* Add -> Config Element -> CSV Data Set Config
* Konfigurasi elemen sesuai data yang akan diakses

    - Filename: Nama file dan path (bisa menggunakan absolute path dan relative path terhadap file .jmx)
    - Variable Names: nama variabel yang akan dipanggil di JMeter
    - Delimiter: opsi delimiter file CSV ( , atau ; )
    - Recycle on EOF: opsi apakah file akan diulang apabila thread masih belum habis sedangkan data eksternal sudah habis
    - Stop thread on EOF: opsi apakah thread akan dihentikan apabila data eksternal habis

    .. image:: /images/csvdatasetconf.png
       :width: 100 %
       :alt: CSVSetUp

Setelah konfigurasi selesai, kita dapat menggunakan variabel dari file CSV untuk digunakan di dalam tes. Contoh yang kita lakukan di bawah ini adalah variabel 'products' dipanggil dengan notasi ${products} untuk digunakan dalam slug yang terdapat pada HTTP Request.

    .. image:: /images/httpreqdata.png
       :width: 100 %
       :alt: CSVSetUp2

Running the Test from Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To Be Updated....




