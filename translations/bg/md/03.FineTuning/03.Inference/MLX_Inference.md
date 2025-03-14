# **Извеждане на Phi-3 с Apple MLX Framework**

## **Какво представлява MLX Framework**

MLX е фреймуърк за машинно обучение, създаден за Apple Silicon, разработен от екипа за машинно обучение на Apple.

MLX е проектиран от изследователи в областта на машинното обучение за изследователи в областта на машинното обучение. Фреймуъркът е създаден да бъде удобен за потребителя, но същевременно ефективен за трениране и внедряване на модели. Дизайнът на самия фреймуърк е концептуално опростен. Нашата цел е да улесним изследователите в разширяването и подобряването на MLX, за да могат бързо да изследват нови идеи.

Големите езикови модели (LLMs) могат да бъдат ускорени на устройства с Apple Silicon чрез MLX, като моделите могат да се изпълняват локално изключително удобно.

## **Използване на MLX за извеждане на Phi-3-mini**

### **1. Настройте вашата MLX среда**

1. Python 3.11.x  
2. Инсталирайте MLX библиотеката  

```bash

pip install mlx-lm

```

### **2. Изпълнение на Phi-3-mini в Terminal с MLX**

```bash

python -m mlx_lm.generate --model microsoft/Phi-3-mini-4k-instruct --max-token 2048 --prompt  "<|user|>\nCan you introduce yourself<|end|>\n<|assistant|>"

```

Резултатът (моята среда е Apple M1 Max, 64GB) е:

![Terminal](../../../../../translated_images/01.0d0f100b646a4e4c4f1cd36c1a05727cd27f1e696ed642c06cf6e2c9bbf425a4.bg.png)

### **3. Квантизация на Phi-3-mini с MLX в Terminal**

```bash

python -m mlx_lm.convert --hf-path microsoft/Phi-3-mini-4k-instruct

```

***Забележка:*** Моделът може да бъде квантизиран чрез mlx_lm.convert, като стандартната квантизация е INT4. Този пример квантизира Phi-3-mini до INT4.

Моделът може да бъде квантизиран чрез mlx_lm.convert, като стандартната квантизация е INT4. Този пример квантизира Phi-3-mini до INT4. След квантизацията моделът ще бъде запазен в стандартната директория ./mlx_model.

Можем да тестваме квантизирания модел с MLX от терминала:

```bash

python -m mlx_lm.generate --model ./mlx_model/ --max-token 2048 --prompt  "<|user|>\nCan you introduce yourself<|end|>\n<|assistant|>"

```

Резултатът е:

![INT4](../../../../../translated_images/02.04e0be1f18a90a58ad47e0c9d9084ac94d0f1a8c02fa707d04dd2dfc7e9117c6.bg.png)

### **4. Изпълнение на Phi-3-mini с MLX в Jupyter Notebook**

![Notebook](../../../../../translated_images/03.0cf0092fe143357656bb5a7bc6427c41d8528d772d38a82d0b2693e2a3eeb16e.bg.png)

***Забележка:*** Моля, прочетете този пример [кликнете на този линк](../../../../../code/03.Inference/MLX/MLX_DEMO.ipynb)

## **Ресурси**

1. Научете повече за Apple MLX Framework [https://ml-explore.github.io](https://ml-explore.github.io/mlx/build/html/index.html)

2. Apple MLX GitHub хранилище [https://github.com/ml-explore](https://github.com/ml-explore)

**Отказ от отговорност**:  
Този документ е преведен с помощта на услуги за машинен превод, базирани на изкуствен интелект. Въпреки че се стремим към точност, имайте предвид, че автоматизираните преводи може да съдържат грешки или неточности. Оригиналният документ на неговия оригинален език трябва да се счита за авторитетен източник. За критична информация се препоръчва професионален превод от човек. Не носим отговорност за каквито и да било недоразумения или погрешни тълкувания, произтичащи от използването на този превод.