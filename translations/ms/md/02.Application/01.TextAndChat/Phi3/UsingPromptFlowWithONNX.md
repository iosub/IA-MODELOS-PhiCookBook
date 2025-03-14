# Menggunakan Windows GPU untuk Membuat Solusi Prompt Flow dengan Phi-3.5-Instruct ONNX

Dokumen berikut adalah contoh cara menggunakan PromptFlow dengan ONNX (Open Neural Network Exchange) untuk mengembangkan aplikasi AI berbasis model Phi-3.

PromptFlow adalah rangkaian alat pengembangan yang dirancang untuk mempercepat siklus pengembangan end-to-end aplikasi AI berbasis LLM (Large Language Model), mulai dari ideasi dan prototipe hingga pengujian dan evaluasi.

Dengan mengintegrasikan PromptFlow dengan ONNX, pengembang dapat:

- **Mengoptimalkan Performa Model**: Memanfaatkan ONNX untuk inferensi dan penerapan model yang efisien.
- **Menyederhanakan Pengembangan**: Menggunakan PromptFlow untuk mengelola alur kerja dan mengotomatiskan tugas-tugas berulang.
- **Meningkatkan Kolaborasi**: Memfasilitasi kolaborasi yang lebih baik antar anggota tim dengan menyediakan lingkungan pengembangan terpadu.

**Prompt flow** adalah rangkaian alat pengembangan yang dirancang untuk mempercepat siklus pengembangan end-to-end aplikasi AI berbasis LLM, mulai dari ideasi, prototipe, pengujian, evaluasi hingga penerapan dan pemantauan di produksi. Alat ini mempermudah rekayasa prompt dan memungkinkan Anda membangun aplikasi LLM dengan kualitas produksi.

Prompt flow dapat terhubung dengan OpenAI, Azure OpenAI Service, serta model yang dapat disesuaikan (Huggingface, LLM/SLM lokal). Kami berharap dapat menerapkan model ONNX yang telah dikuantisasi dari Phi-3.5 ke aplikasi lokal. Prompt flow dapat membantu kami merencanakan bisnis dengan lebih baik dan menyelesaikan solusi lokal berbasis Phi-3.5. Dalam contoh ini, kami akan menggabungkan ONNX Runtime GenAI Library untuk menyelesaikan solusi Prompt flow berbasis Windows GPU.

## **Instalasi**

### **ONNX Runtime GenAI untuk Windows GPU**

Baca panduan ini untuk mengatur ONNX Runtime GenAI untuk Windows GPU [klik di sini](./ORTWindowGPUGuideline.md)

### **Mengatur Prompt flow di VSCode**

1. Instal Ekstensi Prompt flow untuk VS Code

![pfvscode](../../../../../../translated_images/pfvscode.79f42ae5dd93ed35c19d6d978ae75831fef40e0b8440ee48b893b5a0597d2260.ms.png)

2. Setelah menginstal Ekstensi Prompt flow untuk VS Code, klik ekstensi tersebut, dan pilih **Installation dependencies**. Ikuti panduan ini untuk menginstal Prompt flow SDK di lingkungan Anda.

![pfsetup](../../../../../../translated_images/pfsetup.0c82d99c7760aac29833b37faf4329e67e22279b1c5f37a73724dfa9ebaa32ee.ms.png)

3. Unduh [Kode Contoh](../../../../../../code/09.UpdateSamples/Aug/pf/onnx_inference_pf) dan gunakan VS Code untuk membuka contoh ini.

![pfsample](../../../../../../translated_images/pfsample.7bf40b133a558d86356dd6bc0e480bad2659d9c5364823dae9b3e6784e6f2d25.ms.png)

4. Buka **flow.dag.yaml** untuk memilih lingkungan Python Anda.

![pfdag](../../../../../../translated_images/pfdag.c5eb356fa3a96178cd594de9a5da921c4bbe646a9946f32aa20d344ccbeb51a0.ms.png)

   Buka **chat_phi3_ort.py** untuk mengubah lokasi model Phi-3.5-instruct ONNX Anda.

![pfphi](../../../../../../translated_images/pfphi.fff4b0afea47c92c8481174dbf3092823906fca5b717fc642f78947c3e5bbb39.ms.png)

5. Jalankan Prompt flow Anda untuk pengujian.

Buka **flow.dag.yaml** dan klik editor visual.

![pfv](../../../../../../translated_images/pfv.7af6ecd65784a98558b344ba69b5ba6233876823fb435f163e916a632394fc1e.ms.png)

Setelah mengklik ini, jalankan untuk menguji.

![pfflow](../../../../../../translated_images/pfflow.9697e0fda67794bb0cf4b78d52e6f5a42002eec935bc2519933064afbbdd34f0.ms.png)

1. Anda dapat menjalankan batch di terminal untuk memeriksa lebih banyak hasil.

```bash

pf run create --file batch_run.yaml --stream --name 'Your eval qa name'    

```

Anda dapat memeriksa hasil di browser default Anda.

![pfresult](../../../../../../translated_images/pfresult.972eb57dd5bec646e1aa01148991ba8959897efea396e42cf9d7df259444878d.ms.png)

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan perkhidmatan terjemahan berasaskan AI. Walaupun kami berusaha untuk memastikan ketepatan, sila ambil perhatian bahawa terjemahan automatik mungkin mengandungi kesilapan atau ketidaktepatan. Dokumen asal dalam bahasa asalnya harus dianggap sebagai sumber yang berwibawa. Untuk maklumat kritikal, terjemahan manusia profesional adalah disyorkan. Kami tidak bertanggungjawab terhadap sebarang salah faham atau salah tafsir yang timbul daripada penggunaan terjemahan ini.