.. Docs_Installing_ArduinoIDE documentation master file, created by
   sphinx-quickstart on Sun Oct 13 17:22:48 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to TutorTeknik IoT Workshop!
======================================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`


    I. Internet Of Things
Untuk sistem skala kecil, IoT didefinisikan sebagai sebuah jaringan yang menghubungkan things yang mempunyai identitas unik dengan internet. Things dapat membaca sensor (sensing) maupun melakukan aktivasi aktuator serta memungkinkan untuk di program. Untuk sistem skala besar, IoT didefinisikan sebagai sebuah jaringan yang bersifat self-configuraiton, adaptif dan kompleks yang menghubungkan things dengan internet melalui standar protokol komunikasi[1]. Menurut Khan dkk. arsitektur IoT secara umum dibagi ke dalam lima buah lapisan sebagaimana yang terlihat pada gambar berikut.


Arsitektur IoT Secara Umum[2]
Penjelasan masing-masing lapisan adalah sebagai berikut.

    1. Perception Layer
Perception layer disebut juga ‘Device layer’. Lapisan ini berisi objek fisik dan sensor. Sensor yang digunakan dapat berupa RFID, 2D-barcode atau sensor inframerah, tergantung dari metode identifikasi objek yang digunakan. Aktivitas yang dilakukan berupa identifikasi dan pengumpulan data-data objek melalui sensor. Data-data yang dikumpulkan akan ditransmisikan secara aman ke sistem pengolah informasi melalui lapisan network.

    2. Network Layer
Network layer juga dapat disebut ‘tansmission layer’. Lapisan ini melindungi keamanan transmisi data dari piranti IoT (device) ke sistem pengolah informasi. Medium transmisi dapat berupa wire atau wireless dan teknologi yang digunakan dapat berupa 3G, UMTS, WiFi, Bluetooth, infrared, ZigBee atau teknologi lain tergantung dari device. Network layer mengirimkan data piranti IoT dari perception layer ke middleware layer.

    3. Middleware Layer
Lapisan middleware bertanggung jawab untuk menerima data-data piranti IoT yang ditransmisikan melalui network layer dan menyimpan data-data tersebut tersebut ke database. Selain itu middleware juga dapat melakukan pengolahan dan komputasi informasi serta menentukan keputusan berdasarkan hasil pengolahan. Middleware yang bertugas melakukan pengolahan dan penyimpanan informasi biasanya berupa cloud service, namun ada juga middleware yang hanya bertugas untuk meneruskan data seperti MQTT broker yang biasa digunakan untuk komunikasi Machine to Machine (M2M).

    4. Application Layer
Lapisan ini menyediakan pengelolaan aplikasi berdasarkan hasil pengolahan informasi oleh lapisan middleware. End user dapat berinteraksi dengan sistem IoT melalui lapisan ini. Implementasi aplikasiIoT dapat berupa smart health, smart farming, smart home, smart city, transportasi cerdas dan lain sebagainya.

    5. Bussiness Layer
Lapisan ini bertanggung jawab untuk melakukan pengelolaan secara menyeluruh terhadap sistem IoT termasuk aplikasi dan layanan. Lapisan ini membangun model bisnis, grafik, diagram alir dan sebagainya berdasarkan data yang diterima oleh aplikasi. Model bisnis IoT digunaka nuntuk menentukan strategi dan langkah yang harus diambil untuk pengembangan sistem IoT.

Alternatif arsitektur IoT yang dapat dibangun berdasarkan pengalaman dan preferensi Penulis ditunjukan pada tabel berikut.

Lapisan IoT
Objek
Application 
Cloud Service, mobile/web app, Node-RED
Middleware 
Cloud Service, MQTT Broker
Network
WiFi
Perception 
Device (nodeMCU ESP8266, sensor, actuator)


    II. Imlementasi iot dengan middleware Thingspeak
    A. Berkenalan dengan Thingspeak™, Platform IoT berbasis Cloud

ThingSpeak ™ adalah layanan platform analisis IoT berbasis cloud yang memungkinkan penggunanya untuk mengumpulkan, memvisualisasikan, dan menganalisis aliran data. ThingSpeak memberikan visualisasi instan terhadap data yang diposting oleh perangkat pengguna. Fitur Thingspeak diantaranya mengumpulkan data dalam chanel privat, mendukung Restful dan MQTT API, analisis dan visualisasi berbasis MATLAB®, mendukung Alert, event scheduling, integrasi App dan dukungan komunitas global. Thingspeak dapat bekerja pada perangkat Arduino, Particle Photon dan Elektron, WiFi modul ESP8266 dan Raspberry Pi. Thingspeak juga mendukung integrasi pada aplikasi mobile dan web, Twitter, Twillio dan Matlab[3].
            1) Membuat Akun Thingspeak
Untuk dapat menggunakan layanan Thingspeak, pengguna harus memiliki akun Thingspeak.  Lewati bagian ini jika pengguna sudah memiliki akun.
    1. Buka laman https://thingspeak.com/ maka akan muncul tampilan seperti berikut.

Tampilan halaman utama Thingspeak.com
    2. Klik menu Sign Up untuk membuat akun baru. Tampilannya seperti berikut. 

Tampilan halaman sign up Thingspeak.com
    3. Isi identitas diri. Klik continue. Setelah berhasil maka akan keluar intruksi untuk meverifikasi akun melalui e-mail.
    4. Buka e-mail dan ikuti proses verifikasi akun Thingspeak.
            2) Membuat Chanel
Setelah akun dikonfirmasi oleh Thingspeak, pengguna dapat melakukan sign-in dan membuat chanel baru. Langkahnya adalah sebagai berikut.
    1. Klik tombol "New Channel".

Halaman menu channel
    2. Isi identitas chanel yang akan dibuat.Data utama yang perlu diisi adalah nama dan deskripsi chanel, nama dan jumlah field yang dibutuhkan. Field merupakan identitas data yang akan dikirimkan oleh pengguna (i.e voltage, current, power). Thingspeak menyediakan maksimal 8 field.

Identitas channel
    3. Klik tombol "Save". Kemudian akan muncul tampilan seperti berikut.

Halaman chanel Test IoT 1
    4. Klik sub-menu API Keys untuk melihat API Key dari chanel.

Sub-menu API Keys
    5. Catat "channel ID", "Write API Key" dan "Read API Keys" yang nantinya akan digunakan oleh device untuk mengirimkan data pada chanel tersebut. 
            3) Mengirim data ke Thingspeak melalui Web Browser
Di halaman sub-menu API Key juga terdapat cara yang dapat digunakan oleh pengguna untuk membuat API request untuk mengirim data ke chanel Thingspeak. Caranya ditunjukan pada gambar berikut.

API Request untuk mengirimdata ke chanel Thingspeak
Pengguna dapat mencoba menembak data ke chanel Thingspeak melalui web browser melalui request "Update a Channel Feed". Salin sintak request pada web browser seperti yang ditunjukan pada gambar berikut.

Mengirim data dengan API reuest updata channel feed melalui web browser
Perhatikan sintak "update channel feed", ganti field beserta nilai yang ingin dikirimkan. Formatnya "https://api.thingspeak.com/update?api_key=VO3O0P96JOFPTAXZ" diikuti "&nomor field (&field1=)" diikuti ("5") atau nilai yang akan dikirimkan.  Jika pengguna ingin mengirimkan lebih dari satu file maka tinggal ditambahkan "&nomor field berikutnya" diikuti "nilai datanya". Jika berhasil maka akan ada respon berupa urutan data masuk data tersebut seperti yang ditunjukan pada gambar berikut.

Respon jika data berhasil mengirim data
Nilai "1" berarti data tersebut merupakan data pertama yang masuk pada chanel Thingspeak pengguna. Berikut contoh respon untuk data ketiga yang berhasil dikirimkan.

Respon Thingspeak berupa urutan data masuk
Jika gagal maka respon Thingspeak berupa nilai "0" seperti yang ditunjukan pada gambar berikut.

Respon saat data gagal diterima Thingspeak
Berdasarkan pengalaman penulis, kegagalan ini seringkali diakibatkan oleh jeda pengiriman data sekarang dengan pengiriman data sebelumnya yang kurang dari 15 sekon. Jadi agar data data dapat diterima oleh Thingspeak minimal jeda pengiriman data adalah 15 sekon. Sekali lagi hal ini berdasarkan pengalaman penulis ketika menulis artikel ini perubahan dapat terjadi sewaktu-waktu.

Untuk melihat visualisasi data yang masuk, pengguna dapat menuju sub-menu "Private View". Berikut adalah gambar grafik visualisasi data tersimpan di Thingspeak.

Grafik visualisasi data yang tersimpan di Thingspeak
            4) Mengambil data dari Thingspeak melalui Web Browser
Untuk mengambil data yang tersimpan di dalam chanel Thingspeak, pengguna dapat menggunakan API request "Get a Channel Feed", "Get a Channel Field" atau API request "Get Channel Status Updates". Responnya ditunjukan pada gambar berikut.

Respon API request Get a Channel Feed


Respon API request Get a Channel Field


Respon API request Get Channel Status Updates
Untuk membaca last feed pengguna dapat menggunakan API request berikut
https://api.thingspeak.com/channels/336033/fields/1/last.json?api_key=DX0BSRAUKIGZI9UN. Hasilnya ditunjukan pada gambar berikut.

            5) Meng-export data dari Thingspeak
Pengguna dapat melakukan export data dari thingspeak melalui sub-menu "Data Import/Export". Tampilan sub-menu "Data Import/Export" ditunjukan sebagai berikut.

Sub-Menu "Data Impor/Export"
Hasil data yang di export memiliki format .csv yang dapat diakses menggunakan software office seperti Ms.office. Contoh data hasil export yang diakses melalui Ms.excel ditunjukan pada gambar berikut.

Hasil export data dari Thingspeak
    B. Mengirim data pembacaan suhu LM35 berbasis nodeMCU ESP8266 ke Thingspeak
Pada artikel ini penulis akan membahas secara detail cara mengirimkan data ke Thingspeak menggunakan mikrokontroler nodeMCU ESP8266. Data yang akan dikirim diambil dari pembacaan sensor suhu LM35. Sebelumnya, Penulis telah menjelaskan bagaimana cara menggunakan API request pada Thingspeak. Pada bagian ini penulis akan membuat request ke Thingspeak dengan memanfaatkan library yang dibuat oleh The MathWorks, Inc. Library ini dapat di undah pada laman Download Library Thingspeak.

Arsitektur IoT yang akan dibangun pada bagian ini ditunjukan pada tabel berikut.

Lapisan IoT
Objek
Application 
Thingspeak, mobile app
Middleware 
Thingspeak
Network
WiFi
Perception 
nodeMCU ESP8266, LM35

            1) Alat dan Bahan
    • Sensor suhu analog LM35
    • Dev.board nodeMCU ESP8266
    • Kabel jumper
    • Breadboard (optional)
    • Software Arduino IDE (Library ESP8266WiFi.h dan ThingSpeak.h)
            6) Langkah kerja
    1. Siapkan alat dan bahan percobaan
    2. Buat wiring sensor LM35 dengan nodeMCU ESP8266 seperti yang ditunjukan pada gambar berikut.

Wiring nodemcu esp8266 dan LM35
    3. Tulis kode sumber melalui Arduino IDE.
#include <ESP8266WiFi.h>
#include "ThingSpeak.h"

//WIFI credentials go here
const char* ssid     = "unsoed";
const char* password = "electricalee";
WiFiClient client;

// replace with your channel's thingspeak API key
unsigned long myChannelNumber = 336033;
const char * myWriteAPIKey ="VO3O0P96JOFPTAXZ";
// LM35 analog input
int lm35Pin = A0;
// this runs once
void setup() {                
  // initialize the digital pin as an output.
  pinMode(lm35Pin, INPUT);
  // We start by connecting to a WiFi network
  Serial.begin(115200);
  delay(10);

  // We start by connecting to a WiFi network

  Serial.println();
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);

  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("");
  Serial.println("WiFi connected");  
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
  ThingSpeak.begin(client);
}

void loop() {
  int rawbit=0;
  for(int i=0;i<100;i++){
    rawbit = rawbit+analogRead(lm35Pin);
  }
  float millivolts = ((float)(rawbit/100) / 1024.0) * 3300;
  //dibagi resolusi sensor 10mv
  float celsius = millivolts / 10;
  Serial.print(celsius);
  Serial.println(" degrees Celsius ");

  int respon=ThingSpeak.writeField(myChannelNumber, 1, celsius, myWriteAPIKey);
  Serial.print("Respon : ");
  Serial.println(respon);
  Serial.println("\n");
  delay(12000); 
}

    4. Upload program ke board. Pastikan \memilih jenis board NodeMCU 1.0 (ESP-12E Module) dan menyesuaikan port.
    5. Buka serial monitor untuk melihat hasil pembacaan suhu. Jika respon pengiriman ke Thingspeak bernilai 200 berarti data berhasil terkirim.Hasilnya dapat dilihat pada gambar berikut.

Pembacaan suhu melalui serial monitor Arduino IDE
    6. Buka chanel di Thingspeak untuk melihat data yang masuk. Hasilnya adalah sebagai berikut.

Antarmuka Thingspeak

    C. Menerima data dari Thingspeak ke unit ESP NodeMCU untuk menyalakan LED
Arsitektur IoT yang akan dibangun pada bagian ini ditunjukan pada tabel berikut.

Lapisan IoT
Objek
Application 
Thingspeak, mobile app
Middleware 
Thingspeak
Network
WiFi
Perception 
nodeMCU ESP8266, LED

        1) Alat dan Bahan
    • LED
    • Dev.board nodeMCU ESP8266
    • Kabel jumper
    • Breadboard (optional)
    • Software Arduino IDE (Library ESP8266WiFi.h dan ThingSpeak.h)
                2) Langkah kerja
            1. Siapkan alat dan bahan percobaan
            2. Buat wiring led dengan nodeMCU ESP8266 seperti yang ditunjukan pada gambar berikut.


            3. Tulis kode sumber melalui Arduino IDE. 
#include "ThingSpeak.h"
#include <ESP8266WiFi.h>

char ssid[] = "SSID";    //  your network SSID (name) 
char pass[] = "password";   // your network password
int status = WL_IDLE_STATUS;
WiFiClient  client;

unsigned long myChannelNumber = 376715;
const char * myReadAPIKey = "80KO6PE7WSSVO1PE";
int LED=5; //pin D1

void setup() {

  Serial.begin(9600);
  WiFi.begin(ssid, pass);
  ThingSpeak.begin(client);
  pinMode(LED, OUTPUT);
}

void loop() {
  float setled = ThingSpeak.readFloatField(myChannelNumber, 1, myReadAPIKey);

  Serial.print("Latest setled is: "); 
  Serial.println(setled);
  if(setled ==1)
  {
    digitalWrite(LED,HIGH);
  }
  else
  {
    digitalWrite(LED,LOW);
  }
delay(15000);
}
            4. Menembak data ke Thingspeak melalui browser dengan mengopi API request “Update a Channel Field” seperti yang ditunjukan gambar berikut.


    III. Implementasi IoT dengan MQTT Broker/Server
    A. MQTT
MQTT didefinisikan sebagai protokol komunikasi data berbasis arsitektur publish/subscribe. MQTT ideal untuk digunakan dalam berbagai situasi, termasuk untuk lingkungan dengan sumberdaya terbatas seperti dalam konteks komunikasi pada Machine to Machine (M2M) dan Internet of Things (IoT), dimana ketersediaan ruang untuk pengolahan dan/ atau bandwidth terbatas. ProtokolMQTT berjalan di atas TCP/IP [4].

Model publish/subscribe (pub/ sub) didefinisikan sebagai sebuah alternatif untuk model tradisional client-server, di mana klien berkomunikasi langsung dengan endpoint. Model pub/ sub memisahkan hubungan langsung antara klien yang mengirimkan pesan tertentu (publisher) dan klien yang menerima pesan (subscriber). Hal ini berarti bahwa publisher dan subscriber tidak mengetahui eksistensi satu sama lain. Terdapat komponen ketiga, yang disebut broker, yang dikenal oleh publisher dan subscriber, yang memiliki fungsi menyaring dan mendistribusikan semua pesan yang masuk ke broker[5]. Contoh penggunaan model publish/subscribe protokol MQTT ditunjukan pada Gambar berikut.

Contoh Penggunaan Model Publish/subscribe Protokol MQTT[5]
    D. Monitoring Tegangan Pada Sensor Menggunakan Broker Mqtt

Arsitektur IoT yang akan dibangun pada bagian ini ditunjukan pada tabel berikut.

Lapisan IoT
Objek
Application 
Mobile app
Middleware 
MQTT Broker/Server
Network
WiFi
Perception 
nodeMCU ESP8266, LDR


1) Alat dan Bahan
    • LDR
    • Resistor
    • Dev.board nodeMCU ESP8266
    • Kabel jumper
    • Breadboard (optional)
    • Software Arduino IDE (Library ESP8266 pubsubclient)
    • Aplikasi MQTT DASH (dapat unduh di playstore)
2) Langkah kerja
            1. Siapkan alat dan bahan percobaan
            2. Buat wiring sensor LDR dengan nodeMCU ESP8266 seperti yang ditunjukan pada gambar berikut.


            3. Tulis kode sumber melalui Arduino IDE.
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
const char* ssid = "IndiKost";
const char* password = "tanya davi";
const char* mqtt_server = "103.9.22.234";
WiFiClient espClient;
PubSubClient client(espClient);
long lastMsg = 0;
int LED = 5; //D1
int LDR = A0;
int value = 0;
void setup_wifi() {
delay(10);
   Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connected");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
}

void callback(char* topic, byte* payload, unsigned int length) {
  // Serial.print("Message arrived [");
  Serial.print(length);
  Serial.print(topic);
  Serial.print(": ");
  for (int i = 0; i < length; i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();
  if ((char)payload[0] == '0') {
digitalWrite(LED, LOW);  
  } else {
digitalWrite(LED, HIGH);  
  }
}
void reconnect() {
  // Loop until we're reconnected
  while (!client.connected()) {
    Serial.print("Attempting MQTT connection...");
       String clientId = "ESP8266Client123123-";
    clientId += String(random(0xffff), HEX);
    if (client.connect(clientId.c_str())) {
      Serial.println("connected");
 client.subscribe("SWITCH_");
    }
    else {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      // Wait 5 seconds before retrying
delay(1000);
    }
  }
}
void setup() {
pinMode(LED, OUTPUT);     
pinMode(LDR, INPUT);
Serial.begin(115200);
setup_wifi();
client.setServer(mqtt_server, 1883);
client.setCallback(callback);
}
void loop() {
  if (!client.connected()) {
reconnect();
  }
client.loop();
  long now = millis();
  if (now - lastMsg > 2000) {
    lastMsg = now;
    int sensorValue = analogRead(LDR);
    float voltage = (float)sensorValue * (3.3 / 1023);
client.publish("LDR_Value", String(voltage).c_str());
  }
}



    IV. DISCLAIMER
Dokumen ini disusun untuk keperluan pelatihan jejaring Internet Of Things Teknik Elektro
UNSOED pada tanggal 2 Desember 2017 dan 3 Desember 2017. Penulis tidak bertanggung
jawab untuk penggunaan di luar kegiatan tersebut.

    V. DAFTAR PUSTAKA
[1]	R. Minerva, A. Biru, dan D. Rotondi, “IEEE_IoT_Towards_Definition_Internet_of_Things_Revision1_27MAY15.pdf.” IEEE, 2015.
[2]	R. Khan, S. U. Khan, R. Zaheer, dan S. Khan, “Future Internet: The Internet of Things Architecture, Possible Applications and Key Challenges,” 2012, hal. 257–260.
[3]	“IoT Analytics - ThingSpeak Internet of Things.” [Daring]. Tersedia pada: https://thingspeak.com/. [Diakses: 01-Des-2017].
[4]	H. Kreger dan J. Estefan, “MQTT Version 3.1.1,” 10-Des-2015. [Daring]. Tersedia pada: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.html. [Diakses: 15-Feb-2017].
[5]	“MQTT Essentials Part 2: Publish & Subscribe,” HiveMQ, 19-Jan-2015. .

