<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "a5a67308d3b2c5af97baf01067c6f007",
  "translation_date": "2025-07-17T08:50:29+00:00",
  "source_file": "md/03.FineTuning/FineTuning_Vision.md",
  "language_code": "id"
}
-->
# Resep finetuning Phi-3.5-vision

Ini adalah dukungan resmi untuk finetuning Phi-3.5-vision menggunakan library huggingface.  
Silakan `cd` ke direktori kode [vision_finetuning](../../../../code/03.Finetuning/vision_finetuning) sebelum menjalankan perintah berikut.

## Instalasi

```bash
# create a new conda environment
conda create -n phi3v python=3.10
conda activate phi3v

# install pytorch
conda install pytorch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 pytorch-cuda=12.1 -c pytorch -c nvidia

# other libraries needed to run the example code
pip install -r requirements.txt

# (optional) flash attention -- Ampere+ GPUs (e.g., A100, H100)
pip install ninja
MAX_JOBS=32 pip install flash-attn==2.4.2 --no-build-isolation

# (optional) QLoRA -- Turing+ GPUs (e.g., RTX 8000)
pip install bitsandbytes==0.43.1
```

## Mulai cepat

Kami menyediakan dua contoh skrip finetuning, satu untuk DocVQA dan satu untuk klasifikasi meme kebencian.

Perangkat keras minimal yang diuji adalah 4x RTX8000 (48GB RAM per GPU)

```bash
# minimal script on a mini-train split of DocVQA
torchrun --nproc_per_node=4 finetune_hf_trainer_docvqa.py
```

Phi-3.5-vision kini secara resmi mendukung input multi-gambar. Berikut contoh finetuning untuk NLVR2

```bash
torchrun --nproc_per_node=8 finetune_hf_trainer_nlvr2.py
```

## Panduan penggunaan

Tergantung pada perangkat keras, pengguna dapat memilih strategi finetuning yang berbeda. Kami mendukung  
full-finetuning (dengan Deepspeed Zero-2) dengan opsi parameter vision yang dibekukan, dan LoRA (termasuk 4bit QLoRA).  
Secara umum, kami menyarankan menggunakan full finetuning dengan flash attention dan bf16 kapan pun memungkinkan.

### panduan untuk mengonversi dataset kustom Anda ke format yang dibutuhkan

Kami menggunakan dataset klasifikasi video minimal (subset dari UCF-101) sebagai contoh end-to-end untuk menunjukkan cara mengonversi dataset kustom Anda ke format yang dibutuhkan dan melakukan finetune Phi-3.5-vision di atasnya.

```bash
# convert data
python convert_ucf101.py --out_dir /path/to/converted_ucf101

# training
torchrun --nproc_per_node=4 finetune_hf_trainer_ucf101.py --data_dir /path/to/converted_ucf101
```

Data yang sudah dikonversi akan terlihat seperti ini:

```bash
> tree --filelimit=10 /path/to/converted_ucf101
/path/to/converted_ucf101
├── images
│   ├── test
│   │   ├── ApplyEyeMakeup [48 entries exceeds filelimit, not opening dir]
│   │   ├── ApplyLipstick [32 entries exceeds filelimit, not opening dir]
│   │   ├── Archery [56 entries exceeds filelimit, not opening dir]
│   │   ├── BabyCrawling [72 entries exceeds filelimit, not opening dir]
│   │   ├── BalanceBeam [32 entries exceeds filelimit, not opening dir]
│   │   ├── BandMarching [72 entries exceeds filelimit, not opening dir]
│   │   ├── BaseballPitch [80 entries exceeds filelimit, not opening dir]
│   │   ├── Basketball [88 entries exceeds filelimit, not opening dir]
│   │   ├── BasketballDunk [48 entries exceeds filelimit, not opening dir]
│   │   └── BenchPress [72 entries exceeds filelimit, not opening dir]
│   ├── train
│   │   ├── ApplyEyeMakeup [240 entries exceeds filelimit, not opening dir]
│   │   ├── ApplyLipstick [240 entries exceeds filelimit, not opening dir]
│   │   ├── Archery [240 entries exceeds filelimit, not opening dir]
│   │   ├── BabyCrawling [240 entries exceeds filelimit, not opening dir]
│   │   ├── BalanceBeam [240 entries exceeds filelimit, not opening dir]
│   │   ├── BandMarching [240 entries exceeds filelimit, not opening dir]
│   │   ├── BaseballPitch [240 entries exceeds filelimit, not opening dir]
│   │   ├── Basketball [240 entries exceeds filelimit, not opening dir]
│   │   ├── BasketballDunk [240 entries exceeds filelimit, not opening dir]
│   │   └── BenchPress [240 entries exceeds filelimit, not opening dir]
│   └── val
│       ├── ApplyEyeMakeup [24 entries exceeds filelimit, not opening dir]
│       ├── ApplyLipstick [24 entries exceeds filelimit, not opening dir]
│       ├── Archery [24 entries exceeds filelimit, not opening dir]
│       ├── BabyCrawling [24 entries exceeds filelimit, not opening dir]
│       ├── BalanceBeam [24 entries exceeds filelimit, not opening dir]
│       ├── BandMarching [24 entries exceeds filelimit, not opening dir]
│       ├── BaseballPitch [24 entries exceeds filelimit, not opening dir]
│       ├── Basketball [24 entries exceeds filelimit, not opening dir]
│       ├── BasketballDunk [24 entries exceeds filelimit, not opening dir]
│       └── BenchPress [24 entries exceeds filelimit, not opening dir]
├── ucf101_test.jsonl
├── ucf101_train.jsonl
└── ucf101_val.jsonl

34 directories, 3 files
```

Untuk anotasi `jsonl`, setiap baris harus berupa dictionary seperti:

```json
{"id": "val-0000000300", "source": "ucf101", "conversations": [{"images": ["val/BabyCrawling/v_BabyCrawling_g21_c04.0.jpg", "val/BabyCrawling/v_BabyCrawling_g21_c04.1.jpg", "val/BabyCrawling/v_BabyCrawling_g21_c04.2.jpg", "val/BabyCrawling/v_BabyCrawling_g21_c04.3.jpg", "val/BabyCrawling/v_BabyCrawling_g21_c04.4.jpg", "val/BabyCrawling/v_BabyCrawling_g21_c04.5.jpg", "val/BabyCrawling/v_BabyCrawling_g21_c04.6.jpg", "val/BabyCrawling/v_BabyCrawling_g21_c04.7.jpg"], "user": "Classify the video into one of the following classes: ApplyEyeMakeup, ApplyLipstick, Archery, BabyCrawling, BalanceBeam, BandMarching, BaseballPitch, Basketball, BasketballDunk, BenchPress.", "assistant": "BabyCrawling"}]}
{"id": "val-0000000301", "source": "ucf101", "conversations": [{"images": ["val/BabyCrawling/v_BabyCrawling_g09_c06.0.jpg", "val/BabyCrawling/v_BabyCrawling_g09_c06.1.jpg", "val/BabyCrawling/v_BabyCrawling_g09_c06.2.jpg", "val/BabyCrawling/v_BabyCrawling_g09_c06.3.jpg", "val/BabyCrawling/v_BabyCrawling_g09_c06.4.jpg", "val/BabyCrawling/v_BabyCrawling_g09_c06.5.jpg", "val/BabyCrawling/v_BabyCrawling_g09_c06.6.jpg", "val/BabyCrawling/v_BabyCrawling_g09_c06.7.jpg"], "user": "Classify the video into one of the following classes: ApplyEyeMakeup, ApplyLipstick, Archery, BabyCrawling, BalanceBeam, BandMarching, BaseballPitch, Basketball, BasketballDunk, BenchPress.", "assistant": "BabyCrawling"}]}
```

Perlu dicatat bahwa `conversations` adalah sebuah list, sehingga percakapan multi-giliran dapat didukung jika data tersebut tersedia.

## Meminta Kuota GPU Azure

### Prasyarat

Akun Azure dengan peran Contributor (atau peran lain yang mencakup akses Contributor).

Jika Anda belum memiliki akun Azure, buat [akun gratis sebelum memulai](https://azure.microsoft.com).

### Meminta peningkatan kuota

Anda dapat mengajukan permintaan peningkatan kuota langsung dari My quotas. Ikuti langkah-langkah di bawah ini untuk meminta peningkatan kuota. Untuk contoh ini, Anda dapat memilih kuota yang dapat disesuaikan di langganan Anda.

Masuk ke [portal Azure](https://portal.azure.com).

Ketik "quotas" di kotak pencarian, lalu pilih Quotas.  
![Quota](https://learn.microsoft.com/azure/quotas/media/quickstart-increase-quota-portal/quotas-portal.png)

Di halaman Overview, pilih penyedia, seperti Compute atau AML.

**Catatan** Untuk semua penyedia selain Compute, Anda akan melihat kolom Request increase, bukan kolom Adjustable seperti yang dijelaskan di bawah. Di sana, Anda dapat meminta peningkatan untuk kuota tertentu, atau membuat permintaan dukungan untuk peningkatan tersebut.

Di halaman My quotas, di bawah Quota name, pilih kuota yang ingin Anda tingkatkan. Pastikan kolom Adjustable menunjukkan Yes untuk kuota tersebut.

Di bagian atas halaman, pilih New Quota Request, lalu pilih Enter a new limit.

![Increase Quota](https://learn.microsoft.com/azure/quotas/media/quickstart-increase-quota-portal/enter-new-quota-limit.png)

Di panel New Quota Request, masukkan nilai numerik untuk batas kuota baru Anda, lalu pilih Submit.

Permintaan Anda akan ditinjau, dan Anda akan diberi tahu jika permintaan dapat dipenuhi. Biasanya ini terjadi dalam beberapa menit.

Jika permintaan Anda tidak dipenuhi, Anda akan melihat tautan untuk membuat permintaan dukungan. Saat menggunakan tautan ini, seorang engineer dukungan akan membantu Anda dengan permintaan peningkatan tersebut.

## Saran SKU mesin GPU Azure Compute

[ND A100 v4-series](https://learn.microsoft.com/azure/virtual-machines/nda100-v4-series)

[ND H100 v5-series](https://learn.microsoft.com/azure/virtual-machines/nd-h100-v5-series)

[Standard_ND40rs_v2](https://learn.microsoft.com/azure/virtual-machines/ndv2-series)

Berikut beberapa contoh:

### Jika Anda memiliki GPU A100 atau H100

Full finetuning biasanya memberikan performa terbaik. Anda dapat menggunakan perintah berikut untuk finetune Phi-3-V pada klasifikasi meme kebencian.

```bash
torchrun --nproc_per_node=8 --nnodes=<num_nodes> \
  --master_addr=$MASTER_ADDR --master_port=$MASTER_PORT --node_rank=$NODE_RANK \
  finetune_hf_trainer_hateful_memes.py \
  --output_dir <output_dir> \
  --batch_size 64 \
  --use_flash_attention \
  --bf16
```

### Jika Anda memiliki Standard_ND40rs_v2 8x V100-32GB GPUs

Masih memungkinkan untuk melakukan full finetuning Phi-3-V pada klasifikasi meme kebencian. Namun, harapkan  
throughput jauh lebih rendah dibandingkan GPU A100 atau H100 karena tidak adanya dukungan flash attention.  
Akurasi juga bisa terpengaruh karena tidak adanya dukungan bf16 (pelatihan presisi campuran fp16 digunakan sebagai gantinya).

```bash
torchrun --nproc_per_node=8 --nnodes=<num_nodes> \
  --master_addr=$MASTER_ADDR --master_port=$MASTER_PORT --node_rank=$NODE_RANK \
  finetune_hf_trainer_hateful_memes.py \
  --output_dir <output_dir> \
  --batch_size 64
```

### Jika Anda tidak memiliki akses ke GPU pusat data  
Lora mungkin menjadi satu-satunya pilihan Anda. Anda dapat menggunakan perintah berikut untuk finetune Phi-3-V pada klasifikasi meme kebencian.

```bash
torchrun --nproc_per_node=2 \
  finetune_hf_trainer_hateful_memes.py \
  --output_dir <output_dir> \
  --batch_size 64 \
  --use_lora
```

Untuk GPU Turing+ , QLoRA didukung

```bash
torchrun --nproc_per_node=2 \
  finetune_hf_trainer_hateful_memes.py \
  --output_dir <output_dir> \
  --batch_size 64 \
  --use_lora \
  --use_qlora
```

## Hyperparameter yang disarankan dan akurasi yang diharapkan  
### NLVR2

```bash
torchrun --nproc_per_node=4 \
  finetune_hf_trainer_nlvr2.py \
  --bf16 --use_flash_attention \
  --batch_size 64 \
  --output_dir <output_dir> \
  --learning_rate <lr> \
  --num_train_epochs <epochs>

```

Metode pelatihan | Model vision dibekukan | tipe data | LoRA rank | LoRA alpha | ukuran batch | learning rate | epoch | Akurasi
--- | --- | --- | --- | --- | --- | --- | --- | --- |
full-finetuning |  |bf16 | - | - | 64 | 1e-5 | 3 | 89.40 |
full-finetuning | ✔ |bf16 | - | - | 64 | 2e-5 | 2 | 89.20 |
Hasil LoRA segera hadir |  |  |  |  |  |  |  |  |

### CATATAN  
Hasil DocVQA dan Hateful memes di bawah ini berdasarkan versi sebelumnya (Phi-3-vision).  
Hasil baru dengan Phi-3.5-vision akan segera diperbarui.

### DocVQA (CATATAN: Phi-3-vision)

```bash
torchrun --nproc_per_node=4 \
  finetune_hf_trainer_docvqa.py \
  --full_train \
  --bf16 --use_flash_attention \
  --batch_size 64 \
  --output_dir <output_dir> \
  --learning_rate <lr> \
  --num_train_epochs <epochs>

```

Metode pelatihan | tipe data | LoRA rank | LoRA alpha | ukuran batch | learning rate | epoch | ANLS
--- | --- | --- | --- | --- | --- | --- | --- |
full-finetuning | bf16 | - | - | 64 | 5e-6 | 2 | 83.65 |
full-finetuning | fp16 | - | - | 64 | 5e-6 | 2 | 82.60 |
model gambar dibekukan| bf16 | - | - | 64 | 1e-4 | 2 | 79.19 |
model gambar dibekukan| fp16 | - | - | 64 | 1e-4 | 2 | 78.74 |
LoRA | bf16 | 32 | 16 | 64 | 2e-4 | 2 | 82.46 |
LoRA | fp16 | 32 | 16 | 64 | 2e-4 | 2 | 82.34 |
QLoRA | bf16 | 32 | 16 | 64 | 2e-4 | 2 | 81.85 |
QLoRA | fp16 | 32 | 16 | 64 | 2e-4 | 2 | 81.85 |

### Hateful memes (CATATAN: Phi-3-vision)

```bash
torchrun --nproc_per_node=4 \
  finetune_hf_trainer_hateful_memes.py \
  --bf16 --use_flash_attention \
  --batch_size 64 \
  --output_dir <output_dir> \
  --learning_rate <lr> \
  --num_train_epochs <epochs>

```

Metode pelatihan | tipe data | LoRA rank | LoRA alpha | ukuran batch | learning rate | epoch | Akurasi
--- | --- | --- | --- | --- | --- | --- | --- |
full-finetuning | bf16 | - | - | 64 | 5e-5 | 2 | 86.4 |
full-finetuning | fp16 | - | - | 64 | 5e-5 | 2 | 85.4 |
model gambar dibekukan| bf16 | - | - | 64 | 1e-4 | 3 | 79.4 |
model gambar dibekukan| fp16 | - | - | 64 | 1e-4 | 3 | 78.6 |
LoRA | bf16 | 128 | 256 | 64 | 2e-4 | 2 | 86.6 |
LoRA | fp16 | 128 | 256 | 64 | 2e-4 | 2 | 85.2 |
QLoRA | bf16 | 128 | 256 | 64 | 2e-4 | 2 | 84.0 |
QLoRA | fp16 | 128 | 256 | 64 | 2e-4 | 2 | 83.8 |

## Benchmark kecepatan (CATATAN: Phi-3-vision)

Hasil benchmark baru dengan Phi-3.5-vision akan segera diperbarui.

Benchmark kecepatan dilakukan pada dataset DocVQA. Rata-rata panjang urutan dataset ini  
adalah 2443.23 token (menggunakan `num_crops=16` untuk model gambar).

### 8x A100-80GB (Ampere)

Metode pelatihan | \# node | GPU | flash attention | Ukuran batch efektif | Throughput (img/s) | Percepatan | Memori GPU puncak (GB)
--- | --- | --- | --- | --- | --- | --- | --- |
full-finetuning | 1 | 8 |  | 64 | 5.041 |  1x | ~42
full-finetuning | 1 | 8 | ✔ | 64 | 8.657 | 1.72x | ~36
full-finetuning | 2 | 16 | ✔ | 64 | 16.903 | 3.35x | ~29
full-finetuning | 4 | 32 | ✔ | 64 | 33.433 | 6.63x | ~26
model gambar dibekukan | 1 | 8 |  | 64 | 17.578 | 3.49x | ~29
model gambar dibekukan | 1 | 8 | ✔ | 64 | 31.736 | 6.30x | ~27
LoRA | 1 | 8 |  | 64 | 5.591 | 1.11x | ~50
LoRA | 1 | 8 | ✔ | 64 | 12.127 | 2.41x | ~16
QLoRA | 1 | 8 |  | 64 | 4.831 | 0.96x | ~32
QLoRA | 1 | 8 | ✔ | 64 | 10.545 | 2.09x | ~10

### 8x V100-32GB (Volta)

Metode pelatihan | \# node | GPU | flash attention | Ukuran batch efektif | Throughput (img/s) | Percepatan | Memori GPU puncak (GB)
--- | --- | --- | --- | --- | --- | --- | --- |
full-finetuning | 1 | 8 | | 64 | 2.462 |  1x | ~32
full-finetuning | 2 | 16 |  | 64 | 4.182 | 1.70x | ~32
full-finetuning | 4 | 32 |  | 64 | 5.465 | 2.22x | ~32
model gambar dibekukan | 1 | 8 |  | 64 | 8.942 | 3.63x | ~27
LoRA | 1 | 8 |  | 64 | 2.807 | 1.14x | ~30

## Masalah yang diketahui

- Tidak dapat menjalankan flash attention dengan fp16 (bf16 selalu disarankan jika tersedia, dan semua GPU yang mendukung flash attention juga mendukung bf16).  
- Belum mendukung penyimpanan checkpoint sementara dan melanjutkan pelatihan.

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan layanan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Meskipun kami berupaya untuk mencapai akurasi, harap diketahui bahwa terjemahan otomatis mungkin mengandung kesalahan atau ketidakakuratan. Dokumen asli dalam bahasa aslinya harus dianggap sebagai sumber yang sahih. Untuk informasi penting, disarankan menggunakan terjemahan profesional oleh manusia. Kami tidak bertanggung jawab atas kesalahpahaman atau penafsiran yang keliru yang timbul dari penggunaan terjemahan ini.