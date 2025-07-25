<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "be0b2937160c486180ded27e4f14adeb",
  "translation_date": "2025-07-16T16:35:10+00:00",
  "source_file": "code/07.Lab/01/AIPC/extensions/phi3ext/README.md",
  "language_code": "pa"
}
-->
# phi3ext README

ਇਹ ਤੁਹਾਡੇ ਐਕਸਟੈਂਸ਼ਨ "phi3ext" ਦਾ README ਹੈ। ਇੱਕ ਸੰਖੇਪ ਵੇਰਵਾ ਲਿਖਣ ਤੋਂ ਬਾਅਦ, ਅਸੀਂ ਸਿਫਾਰਸ਼ ਕਰਦੇ ਹਾਂ ਕਿ ਹੇਠਾਂ ਦਿੱਤੇ ਅਧਿਆਇ ਸ਼ਾਮਲ ਕਰੋ।

## Features

ਆਪਣੇ ਐਕਸਟੈਂਸ਼ਨ ਦੀਆਂ ਖਾਸ ਵਿਸ਼ੇਸ਼ਤਾਵਾਂ ਦਾ ਵਰਣਨ ਕਰੋ, ਜਿਸ ਵਿੱਚ ਐਕਸਟੈਂਸ਼ਨ ਚੱਲਦੇ ਸਮੇਂ ਦੀਆਂ ਸਕ੍ਰੀਨਸ਼ਾਟ ਵੀ ਸ਼ਾਮਲ ਹਨ। ਤਸਵੀਰਾਂ ਦੇ ਰਸਤੇ ਇਸ README ਫਾਈਲ ਦੇ ਸਬੰਧ ਵਿੱਚ ਹਨ।

ਉਦਾਹਰਨ ਵਜੋਂ, ਜੇ ਤੁਹਾਡੇ ਐਕਸਟੈਂਸ਼ਨ ਪ੍ਰੋਜੈਕਟ ਵਰਕਸਪੇਸ ਵਿੱਚ ਇੱਕ images ਫੋਲਡਰ ਹੈ:

\!\[feature X\]\(images/feature-x.png\)

> ਟਿਪ: ਬਹੁਤ ਸਾਰੇ ਲੋਕਪ੍ਰਿਯ ਐਕਸਟੈਂਸ਼ਨ ਐਨੀਮੇਸ਼ਨ ਵਰਤਦੇ ਹਨ। ਇਹ ਤੁਹਾਡੇ ਐਕਸਟੈਂਸ਼ਨ ਨੂੰ ਦਰਸਾਉਣ ਦਾ ਇੱਕ ਬਹੁਤ ਵਧੀਆ ਤਰੀਕਾ ਹੈ! ਅਸੀਂ ਛੋਟੀਆਂ ਅਤੇ ਕੇਂਦਰਿਤ ਐਨੀਮੇਸ਼ਨਾਂ ਦੀ ਸਿਫਾਰਸ਼ ਕਰਦੇ ਹਾਂ, ਜੋ ਅਸਾਨੀ ਨਾਲ ਸਮਝੀਆਂ ਜਾ ਸਕਦੀਆਂ ਹਨ।

## Requirements

ਜੇ ਤੁਹਾਡੇ ਕੋਲ ਕੋਈ ਮੰਗਾਂ ਜਾਂ ਨਿਰਭਰਤਾਵਾਂ ਹਨ, ਤਾਂ ਕਿਰਪਾ ਕਰਕੇ ਇੱਕ ਅਧਿਆਇ ਸ਼ਾਮਲ ਕਰੋ ਜੋ ਇਹ ਦੱਸਦਾ ਹੋਵੇ ਕਿ ਇਹ ਮੰਗਾਂ ਕੀ ਹਨ ਅਤੇ ਉਹਨਾਂ ਨੂੰ ਕਿਵੇਂ ਇੰਸਟਾਲ ਅਤੇ ਸੰਰਚਿਤ ਕਰਨਾ ਹੈ।

## Extension Settings

ਜੇ ਤੁਹਾਡੇ ਐਕਸਟੈਂਸ਼ਨ ਨੇ `contributes.configuration` ਐਕਸਟੈਂਸ਼ਨ ਪੌਇੰਟ ਰਾਹੀਂ ਕੋਈ ਵੀ VS Code ਸੈਟਿੰਗਜ਼ ਸ਼ਾਮਲ ਕੀਤੀਆਂ ਹਨ, ਤਾਂ ਉਹਨਾਂ ਨੂੰ ਵੀ ਸ਼ਾਮਲ ਕਰੋ।

ਉਦਾਹਰਨ ਵਜੋਂ:

ਇਹ ਐਕਸਟੈਂਸ਼ਨ ਹੇਠਾਂ ਦਿੱਤੀਆਂ ਸੈਟਿੰਗਜ਼ ਦਿੰਦਾ ਹੈ:

* `myExtension.enable`: ਇਸ ਐਕਸਟੈਂਸ਼ਨ ਨੂੰ ਚਾਲੂ/ਬੰਦ ਕਰਨ ਲਈ।
* `myExtension.thing`: ਕਿਸੇ ਚੀਜ਼ ਨੂੰ ਕਰਨ ਲਈ `blah` 'ਤੇ ਸੈਟ ਕਰੋ।

## Known Issues

ਜਾਣੇ-ਪਹਿਚਾਣੇ ਮੁੱਦੇ ਦਰਸਾਉਣਾ ਵਰਤੋਂਕਾਰਾਂ ਨੂੰ ਤੁਹਾਡੇ ਐਕਸਟੈਂਸ਼ਨ ਨਾਲ ਦੁਹਰਾਏ ਜਾਣ ਵਾਲੇ ਮੁੱਦਿਆਂ ਤੋਂ ਬਚਾਉਣ ਵਿੱਚ ਮਦਦ ਕਰਦਾ ਹੈ।

## Release Notes

ਵਰਤੋਂਕਾਰ ਤੁਹਾਡੇ ਐਕਸਟੈਂਸ਼ਨ ਨੂੰ ਅਪਡੇਟ ਕਰਨ ਸਮੇਂ ਜਾਰੀ ਕੀਤੇ ਗਏ ਨੋਟਸ ਦੀ ਕਦਰ ਕਰਦੇ ਹਨ।

### 1.0.0

ਪਹਿਲਾ ਜਾਰੀ ਕੀਤਾ ਗਿਆ ਸੰਸਕਰਣ...

### 1.0.1

ਮੁੱਦਾ # ਠੀਕ ਕੀਤਾ ਗਿਆ।

### 1.1.0

ਫੀਚਰ X, Y ਅਤੇ Z ਸ਼ਾਮਲ ਕੀਤੇ ਗਏ।

---

## Following extension guidelines

ਪੱਕਾ ਕਰੋ ਕਿ ਤੁਸੀਂ ਐਕਸਟੈਂਸ਼ਨ ਗਾਈਡਲਾਈਨਜ਼ ਪੜ੍ਹ ਲਈਆਂ ਹਨ ਅਤੇ ਐਕਸਟੈਂਸ਼ਨ ਬਣਾਉਣ ਦੀਆਂ ਵਧੀਆ ਪ੍ਰਥਾਵਾਂ ਦੀ ਪਾਲਣਾ ਕਰ ਰਹੇ ਹੋ।

* [扩展指南](https://code.visualstudio.com/api/references/extension-guidelines?WT.mc_id=aiml-137032-kinfeylo)

## Working with Markdown

ਤੁਸੀਂ Visual Studio Code ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਆਪਣਾ README ਲਿਖ ਸਕਦੇ ਹੋ। ਇੱਥੇ ਕੁਝ ਲਾਭਦਾਇਕ ਐਡੀਟਰ ਸ਼ਾਰਟਕੱਟ ਹਨ:

* ਐਡੀਟਰ ਨੂੰ ਵੰਡੋ (`Cmd+\` macOS 'ਤੇ ਜਾਂ `Ctrl+\` Windows ਅਤੇ Linux 'ਤੇ)।
* ਪ੍ਰੀਵਿਊ ਬਦਲੋ (`Shift+Cmd+V` macOS 'ਤੇ ਜਾਂ `Shift+Ctrl+V` Windows ਅਤੇ Linux 'ਤੇ)।
* Markdown ਕੋਡ ਸਨਿੱਪੇਟ ਦੀ ਸੂਚੀ ਵੇਖਣ ਲਈ `Ctrl+Space` ਦਬਾਓ (Windows, Linux, macOS)।

## For more information

* [Visual Studio Code 的 Markdown 支持](http://code.visualstudio.com/docs/languages/markdown?WT.mc_id=aiml-137032-kinfeylo)
* [Markdown 语法参考](https://help.github.com/articles/markdown-basics/)

**ਮਜ਼ਾ ਲਓ!**

**ਅਸਵੀਕਾਰੋਪਣ**:  
ਇਹ ਦਸਤਾਵੇਜ਼ AI ਅਨੁਵਾਦ ਸੇਵਾ [Co-op Translator](https://github.com/Azure/co-op-translator) ਦੀ ਵਰਤੋਂ ਕਰਕੇ ਅਨੁਵਾਦਿਤ ਕੀਤਾ ਗਿਆ ਹੈ। ਜਦੋਂ ਕਿ ਅਸੀਂ ਸਹੀਤਾ ਲਈ ਕੋਸ਼ਿਸ਼ ਕਰਦੇ ਹਾਂ, ਕਿਰਪਾ ਕਰਕੇ ਧਿਆਨ ਰੱਖੋ ਕਿ ਸਵੈਚਾਲਿਤ ਅਨੁਵਾਦਾਂ ਵਿੱਚ ਗਲਤੀਆਂ ਜਾਂ ਅਸਮਰਥਤਾਵਾਂ ਹੋ ਸਕਦੀਆਂ ਹਨ। ਮੂਲ ਦਸਤਾਵੇਜ਼ ਆਪਣੀ ਮੂਲ ਭਾਸ਼ਾ ਵਿੱਚ ਪ੍ਰਮਾਣਿਕ ਸਰੋਤ ਮੰਨਿਆ ਜਾਣਾ ਚਾਹੀਦਾ ਹੈ। ਮਹੱਤਵਪੂਰਨ ਜਾਣਕਾਰੀ ਲਈ, ਪੇਸ਼ੇਵਰ ਮਨੁੱਖੀ ਅਨੁਵਾਦ ਦੀ ਸਿਫਾਰਸ਼ ਕੀਤੀ ਜਾਂਦੀ ਹੈ। ਇਸ ਅਨੁਵਾਦ ਦੀ ਵਰਤੋਂ ਤੋਂ ਉਤਪੰਨ ਕਿਸੇ ਵੀ ਗਲਤਫਹਿਮੀ ਜਾਂ ਗਲਤ ਵਿਆਖਿਆ ਲਈ ਅਸੀਂ ਜ਼ਿੰਮੇਵਾਰ ਨਹੀਂ ਹਾਂ।