# **فائی فیملی کی مقدار بندی**

ماڈل کوانٹائزیشن سے مراد نیورل نیٹ ورک ماڈل کے پیرامیٹرز (جیسے وزن اور ایکٹیویشن ویلیوز) کو ایک بڑے ویلیو رینج (عام طور پر ایک مسلسل ویلیو رینج) سے ایک چھوٹے، محدود ویلیو رینج میں میپ کرنے کا عمل ہے۔ یہ ٹیکنالوجی ماڈل کے سائز اور حسابی پیچیدگی کو کم کر سکتی ہے اور موبائل ڈیوائسز یا ایمبیڈڈ سسٹمز جیسے وسائل کی پابندی والے ماحول میں ماڈل کی کارکردگی کو بہتر بنا سکتی ہے۔ ماڈل کوانٹائزیشن پیرامیٹرز کی درستگی کو کم کرکے کمپریشن حاصل کرتی ہے، لیکن اس سے درستگی میں کچھ کمی بھی آتی ہے۔ لہذا، کوانٹائزیشن کے عمل میں ماڈل کے سائز، حسابی پیچیدگی، اور درستگی کے درمیان توازن قائم کرنا ضروری ہوتا ہے۔ عام کوانٹائزیشن طریقوں میں فکسڈ پوائنٹ کوانٹائزیشن، فلوٹنگ پوائنٹ کوانٹائزیشن وغیرہ شامل ہیں۔ آپ مخصوص منظرنامے اور ضروریات کے مطابق مناسب کوانٹائزیشن حکمت عملی کا انتخاب کر سکتے ہیں۔

ہم GenAI ماڈل کو ایج ڈیوائسز پر ڈیپلائے کرنے کی امید رکھتے ہیں اور مزید ڈیوائسز کو GenAI کے منظرناموں میں شامل کرنا چاہتے ہیں، جیسے موبائل ڈیوائسز، AI پی سی/کوپائلٹ+پی سی، اور روایتی IoT ڈیوائسز۔ کوانٹائزیشن ماڈل کے ذریعے، ہم اسے مختلف ڈیوائسز کی بنیاد پر مختلف ایج ڈیوائسز پر ڈیپلائے کر سکتے ہیں۔ ہارڈویئر مینوفیکچررز کی طرف سے فراہم کردہ ماڈل ایکسلریشن فریم ورک اور کوانٹائزیشن ماڈل کو ملا کر، ہم بہتر SLM ایپلیکیشن منظرنامے بنا سکتے ہیں۔

کوانٹائزیشن کے منظرنامے میں، ہمارے پاس مختلف درستگیاں ہیں (INT4، INT8، FP16، FP32)۔ ذیل میں عام طور پر استعمال ہونے والی کوانٹائزیشن درستگیوں کی وضاحت دی گئی ہے۔

### **INT4**

INT4 کوانٹائزیشن ایک جرات مندانہ کوانٹائزیشن طریقہ ہے جو ماڈل کے وزن اور ایکٹیویشن ویلیوز کو 4-بٹ انٹیجرز میں کوانٹائز کرتا ہے۔ INT4 کوانٹائزیشن عام طور پر زیادہ درستگی کے نقصان کا سبب بنتی ہے کیونکہ اس کی نمائندگی کی حد چھوٹی ہوتی ہے اور درستگی کم ہوتی ہے۔ تاہم، INT8 کوانٹائزیشن کے مقابلے میں، INT4 کوانٹائزیشن ماڈل کی اسٹوریج کی ضروریات اور حسابی پیچیدگی کو مزید کم کر سکتی ہے۔ یہ نوٹ کرنا ضروری ہے کہ عملی اطلاق میں INT4 کوانٹائزیشن نسبتاً کم ہوتی ہے، کیونکہ بہت کم درستگی ماڈل کی کارکردگی میں نمایاں کمی کا سبب بن سکتی ہے۔ اس کے علاوہ، ہر ہارڈویئر INT4 آپریشنز کو سپورٹ نہیں کرتا، اس لیے کوانٹائزیشن طریقہ کا انتخاب کرتے وقت ہارڈویئر کی مطابقت کو مدنظر رکھنا ضروری ہے۔

### **INT8**

INT8 کوانٹائزیشن ماڈل کے وزن اور ایکٹیویشنز کو فلوٹنگ پوائنٹ نمبرز سے 8-بٹ انٹیجرز میں تبدیل کرنے کا عمل ہے۔ اگرچہ INT8 انٹیجرز کے ذریعے ظاہر کردہ عددی حد چھوٹی اور کم درست ہے، لیکن یہ اسٹوریج اور حساب کتاب کی ضروریات کو نمایاں طور پر کم کر سکتی ہے۔ INT8 کوانٹائزیشن میں، ماڈل کے وزن اور ایکٹیویشن ویلیوز کو کوانٹائزیشن کے عمل سے گزارا جاتا ہے، جس میں اسکیلنگ اور آفسیٹ شامل ہوتے ہیں، تاکہ اصل فلوٹنگ پوائنٹ معلومات کو زیادہ سے زیادہ محفوظ رکھا جا سکے۔ انفیرینس کے دوران، ان کوانٹائزڈ ویلیوز کو حساب کتاب کے لیے دوبارہ فلوٹنگ پوائنٹ نمبرز میں ڈی کوانٹائز کیا جائے گا، اور پھر اگلے مرحلے کے لیے دوبارہ INT8 میں کوانٹائز کیا جائے گا۔ یہ طریقہ زیادہ تر ایپلیکیشنز میں کافی درستگی فراہم کر سکتا ہے جبکہ اعلیٰ حسابی کارکردگی کو برقرار رکھتا ہے۔

### **FP16**

FP16 فارمیٹ، یعنی 16-بٹ فلوٹنگ پوائنٹ نمبرز (float16)، 32-بٹ فلوٹنگ پوائنٹ نمبرز (float32) کے مقابلے میں میموری کے استعمال کو آدھا کر دیتا ہے، جو بڑے پیمانے پر ڈیپ لرننگ ایپلیکیشنز میں اہم فوائد فراہم کرتا ہے۔ FP16 فارمیٹ بڑی ماڈلز کو لوڈ کرنے یا ایک ہی GPU میموری کی حدود کے اندر مزید ڈیٹا پروسیس کرنے کی اجازت دیتا ہے۔ جیسے جیسے جدید GPU ہارڈویئر FP16 آپریشنز کو سپورٹ کرتا جا رہا ہے، FP16 فارمیٹ کا استعمال حسابی رفتار میں بہتری بھی لا سکتا ہے۔ تاہم، FP16 فارمیٹ کے اپنے اندرونی نقصانات بھی ہیں، یعنی کم درستگی، جو کچھ صورتوں میں عددی عدم استحکام یا درستگی کے نقصان کا سبب بن سکتی ہے۔

### **FP32**

FP32 فارمیٹ اعلیٰ درستگی فراہم کرتا ہے اور بڑی حد تک ویلیوز کو درست طریقے سے ظاہر کر سکتا ہے۔ ان منظرناموں میں جہاں پیچیدہ ریاضیاتی آپریشنز کیے جاتے ہیں یا اعلیٰ درستگی کے نتائج کی ضرورت ہوتی ہے، FP32 فارمیٹ کو ترجیح دی جاتی ہے۔ تاہم، اعلیٰ درستگی کا مطلب زیادہ میموری کا استعمال اور طویل حساب کتاب کا وقت بھی ہوتا ہے۔ بڑے پیمانے پر ڈیپ لرننگ ماڈلز کے لیے، خاص طور پر جب ماڈل کے پیرامیٹرز کی تعداد زیادہ ہو اور ڈیٹا کی مقدار بہت زیادہ ہو، FP32 فارمیٹ GPU میموری کی کمی یا انفیرینس کی رفتار میں کمی کا سبب بن سکتا ہے۔

موبائل ڈیوائسز یا IoT ڈیوائسز پر، ہم Phi-3.x ماڈلز کو INT4 میں تبدیل کر سکتے ہیں، جبکہ AI پی سی/کوپائلٹ پی سی جیسے ڈیوائسز زیادہ درستگی جیسے INT8، FP16، FP32 استعمال کر سکتے ہیں۔

فی الحال، مختلف ہارڈویئر مینوفیکچررز کے پاس جنریٹیو ماڈلز کو سپورٹ کرنے کے لیے مختلف فریم ورک ہیں، جیسے Intel کا OpenVINO، Qualcomm کا QNN، Apple کا MLX، اور Nvidia کا CUDA وغیرہ، جو ماڈل کوانٹائزیشن کے ساتھ مقامی ڈیپلائمنٹ مکمل کرتے ہیں۔

ٹیکنالوجی کے لحاظ سے، ہمارے پاس کوانٹائزیشن کے بعد مختلف فارمیٹ سپورٹ موجود ہیں، جیسے PyTorch / Tensorflow فارمیٹ، GGUF، اور ONNX۔ میں نے GGUF اور ONNX کے درمیان فارمیٹ کا موازنہ اور ایپلیکیشن منظرنامے کیے ہیں۔ یہاں میں ONNX کوانٹائزیشن فارمیٹ کی سفارش کرتا ہوں، جو ماڈل فریم ورک سے ہارڈویئر تک اچھی سپورٹ فراہم کرتا ہے۔ اس باب میں، ہم GenAI کے لیے ONNX Runtime، OpenVINO، اور Apple MLX پر ماڈل کوانٹائزیشن پر توجہ مرکوز کریں گے (اگر آپ کے پاس کوئی بہتر طریقہ ہے، تو آپ ہمیں PR کے ذریعے دے سکتے ہیں)۔

**یہ باب شامل کرتا ہے**

1. [Llama.cpp کے ذریعے Phi-3.5 / 4 کو کوانٹائز کرنا](./UsingLlamacppQuantifyingPhi.md)

2. [Generative AI extensions for onnxruntime کے ذریعے Phi-3.5 / 4 کو کوانٹائز کرنا](./UsingORTGenAIQuantifyingPhi.md)

3. [Intel OpenVINO کے ذریعے Phi-3.5 / 4 کو کوانٹائز کرنا](./UsingIntelOpenVINOQuantifyingPhi.md)

4. [Apple MLX Framework کے ذریعے Phi-3.5 / 4 کو کوانٹائز کرنا](./UsingAppleMLXQuantifyingPhi.md)

**اعلانِ لاتعلقی**:  
یہ دستاویز مشین پر مبنی AI ترجمہ خدمات کا استعمال کرتے ہوئے ترجمہ کی گئی ہے۔ اگرچہ ہم درستگی کی پوری کوشش کرتے ہیں، براہ کرم آگاہ رہیں کہ خودکار ترجمے میں غلطیاں یا خامیاں ہو سکتی ہیں۔ اصل دستاویز کو اس کی اصل زبان میں مستند ذریعہ سمجھا جانا چاہیے۔ اہم معلومات کے لیے، پیشہ ور انسانی ترجمہ تجویز کیا جاتا ہے۔ ہم اس ترجمے کے استعمال سے پیدا ہونے والی کسی بھی غلط فہمی یا غلط تشریح کے ذمہ دار نہیں ہیں۔