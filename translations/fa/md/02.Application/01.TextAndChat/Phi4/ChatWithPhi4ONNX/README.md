<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c98217bb3eff6c24e97b104b21632fd0",
  "translation_date": "2025-07-17T03:15:26+00:00",
  "source_file": "md/02.Application/01.TextAndChat/Phi4/ChatWithPhi4ONNX/README.md",
  "language_code": "fa"
}
-->
# **گفتگو با Phi-4-mini ONNX**

***ONNX*** یک فرمت باز است که برای نمایش مدل‌های یادگیری ماشین ساخته شده است. ONNX مجموعه‌ای مشترک از عملگرها را تعریف می‌کند - بلوک‌های سازنده مدل‌های یادگیری ماشین و یادگیری عمیق - و یک فرمت فایل مشترک برای این که توسعه‌دهندگان هوش مصنوعی بتوانند مدل‌ها را با انواع فریم‌ورک‌ها، ابزارها، زمان اجرا و کامپایلرها استفاده کنند.

امیدواریم بتوانیم مدل‌های هوش مصنوعی مولد را روی دستگاه‌های لبه‌ای پیاده‌سازی کنیم و در محیط‌هایی با قدرت محاسباتی محدود یا آفلاین از آن‌ها استفاده کنیم. اکنون می‌توانیم این هدف را با تبدیل مدل به صورت کوانتیزه شده محقق کنیم. می‌توانیم مدل کوانتیزه شده را به فرمت GGUF یا ONNX تبدیل کنیم.

Microsoft Olive می‌تواند به شما در تبدیل SLM به فرمت کوانتیزه شده ONNX کمک کند. روش تبدیل مدل بسیار ساده است

**نصب Microsoft Olive SDK**


```bash

pip install olive-ai

pip install transformers

```

**تبدیل پشتیبانی ONNX برای CPU**

```bash

olive auto-opt --model_name_or_path Your Phi-4-mini location --output_path Your onnx ouput location --device cpu --provider CPUExecutionProvider --precision int4 --use_model_builder --log_level 1

```

***توجه*** این مثال از CPU استفاده می‌کند


### **استنتاج مدل Phi-4-mini ONNX با ONNX Runtime GenAI**

- **نصب ONNX Runtime GenAI**

```bash

pip install --pre onnxruntime-genai

```

- **کد پایتون**

*این نسخه ONNX Runtime GenAI 0.5.2 است*

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


*این نسخه ONNX Runtime GenAI 0.6.0 است*

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

**سلب مسئولیت**:  
این سند با استفاده از سرویس ترجمه هوش مصنوعی [Co-op Translator](https://github.com/Azure/co-op-translator) ترجمه شده است. در حالی که ما در تلاش برای دقت هستیم، لطفاً توجه داشته باشید که ترجمه‌های خودکار ممکن است حاوی خطاها یا نادرستی‌هایی باشند. سند اصلی به زبان بومی خود باید به عنوان منبع معتبر در نظر گرفته شود. برای اطلاعات حیاتی، ترجمه حرفه‌ای انسانی توصیه می‌شود. ما مسئول هیچ گونه سوءتفاهم یا تفسیر نادرستی که از استفاده از این ترجمه ناشی شود، نیستیم.