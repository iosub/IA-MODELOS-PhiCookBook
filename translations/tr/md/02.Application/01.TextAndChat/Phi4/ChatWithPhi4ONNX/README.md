<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c98217bb3eff6c24e97b104b21632fd0",
  "translation_date": "2025-07-17T03:17:23+00:00",
  "source_file": "md/02.Application/01.TextAndChat/Phi4/ChatWithPhi4ONNX/README.md",
  "language_code": "tr"
}
-->
# **Phi-4-mini ONNX ile Sohbet**

***ONNX***, makine öğrenimi modellerini temsil etmek için oluşturulmuş açık bir formattır. ONNX, makine öğrenimi ve derin öğrenme modellerinin yapı taşları olan ortak bir operatör seti ve AI geliştiricilerinin modelleri çeşitli frameworkler, araçlar, çalışma zamanları ve derleyicilerle kullanabilmesini sağlayan ortak bir dosya formatı tanımlar.

Üretken AI modellerini uç cihazlarda çalıştırmayı ve sınırlı hesaplama gücü veya çevrimdışı ortamlarda kullanmayı hedefliyoruz. Artık bu hedefe, modeli kuantize ederek ulaşabiliyoruz. Kuantize edilmiş modeli GGUF veya ONNX formatına dönüştürebiliriz.

Microsoft Olive, SLM’yi kuantize ONNX formatına dönüştürmenize yardımcı olabilir. Model dönüşümünü gerçekleştirme yöntemi oldukça basittir.

**Microsoft Olive SDK’yı Yükleyin**


```bash

pip install olive-ai

pip install transformers

```

**CPU ONNX Desteğini Dönüştürün**

```bash

olive auto-opt --model_name_or_path Your Phi-4-mini location --output_path Your onnx ouput location --device cpu --provider CPUExecutionProvider --precision int4 --use_model_builder --log_level 1

```

***Not*** bu örnek CPU kullanmaktadır


### **ONNX Runtime GenAI ile Phi-4-mini ONNX Modelini Çıkarım Yapma**

- **ONNX Runtime GenAI’yi Yükleyin**

```bash

pip install --pre onnxruntime-genai

```

- **Python Kodu**

*Bu ONNX Runtime GenAI 0.5.2 sürümüdür*

```python

import onnxruntime_genai as og
import numpy as np
import os


model_folder = "Your Phi-4-mini-onnx-cpu-int4 location"


model = og.Model(model_folder)


tokenizer = og.Tokenizer(model)
tokenizer_stream = tokenizer.create_stream()


search_options = {}
search_options['max_length'] = 2048
search_options['past_present_share_buffer'] = False


chat_template = "<|user|>\n{input}</s>\n<|assistant|>"


text = """Can you introduce yourself"""


prompt = f'{chat_template.format(input=text)}'


input_tokens = tokenizer.encode(prompt)


params = og.GeneratorParams(model)


params.set_search_options(**search_options)
params.input_ids = input_tokens


generator = og.Generator(model, params)


while not generator.is_done():
      generator.compute_logits()
      generator.generate_next_token()

      new_token = generator.get_next_tokens()[0]
      print(tokenizer_stream.decode(new_token), end='', flush=True)

```


*Bu ONNX Runtime GenAI 0.6.0 sürümüdür*

```python

import onnxruntime_genai as og
import numpy as np
import os
import time
import psutil

model_folder = "Your Phi-4-mini-onnx model path"

model = og.Model(model_folder)

tokenizer = og.Tokenizer(model)
tokenizer_stream = tokenizer.create_stream()

search_options = {}
search_options['max_length'] = 1024
search_options['past_present_share_buffer'] = False

chat_template = "<|user|>{input}<|assistant|>"

text = """can you introduce yourself"""

prompt = f'{chat_template.format(input=text)}'

input_tokens = tokenizer.encode(prompt)

params = og.GeneratorParams(model)

params.set_search_options(**search_options)

generator = og.Generator(model, params)

generator.append_tokens(input_tokens)

while not generator.is_done():
      generator.generate_next_token()

      new_token = generator.get_next_tokens()[0]
      token_text = tokenizer.decode(new_token)
      # print(tokenizer_stream.decode(new_token), end='', flush=True)
      if token_count == 0:
        first_token_time = time.time()
        first_response_latency = first_token_time - start_time
        print(f"firstly token delpay: {first_response_latency:.4f} s")

      print(token_text, end='', flush=True)
      token_count += 1

```

**Feragatname**:  
Bu belge, AI çeviri servisi [Co-op Translator](https://github.com/Azure/co-op-translator) kullanılarak çevrilmiştir. Doğruluk için çaba gösterilse de, otomatik çevirilerin hatalar veya yanlışlıklar içerebileceğini lütfen unutmayınız. Orijinal belge, kendi dilinde yetkili kaynak olarak kabul edilmelidir. Kritik bilgiler için profesyonel insan çevirisi önerilir. Bu çevirinin kullanımı sonucu oluşabilecek yanlış anlamalar veya yorum hatalarından sorumlu değiliz.