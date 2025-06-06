# LZV-CSLR

Šis repo satur kodu un resursus nepātrauktas zīmju valodas atpazīšanas (CSLR) modeļa apmācībai latviešu zīmju valodai (LZV), izmantojot pārneses mācīšanās (transfer learning) pieeju. Modelis tiek apmācīts, balstoties uz iepriekš trenētu amerikāņu zīmju valodas (ASL) modeli, kas izmanto ar MediaPipe Holistic ietvaru iegūtus 42 roku orientierus (landmarks).

Šis repo satur tikai ļoti mazu daļu no bakalaura darbā paveiktā un izveidotā, tas ir domāts metodikas pārskatei.
Ja mērķis ir eksperimentus atkārtot, ir nepieciešams sagatavot savu korpusu (t.i. sagatavot zīmju valodas lietojuma video materiālus un iegūt MediaPipe orientierus).

Bakalaura darbā sagatavotie .tfrecord faili nav pieejami, jo to izmērs pārsniedz GitHub un GitHub LFS limitu.

---

## Projekts satur

- Kodu modeļa apmācībai (`train_42.ipynb`)
- Kodu training.tfrecord un validation.tfrecord izveidošanai (`preprocess_landmarks.ipynb`)
- LZV vārdnīcu (`char_map.json`)
- LZV metadatu failu (`dataset_info.json`)
- ASL metadatu, trenēšanas un minējumu veikšanas modeļus 543, 75 un 42 orientieru grupām (atrodas zem `models/asl`)
- Piemēru gatavam LZV modelim

## Versijas

* Python - 3.11.9;
* MediaPipe - 0.10.21;
* Tensorflow - 2.19.0;
* Jiwer - 3.1.0;
* NumPy - 1.26.4;
* sklearn - 1.5.2;
* CV2 - 4.10.0.

---

## Datu sagatavošana

Modeļa apmācībai ir nepieciešams sagatavot training.tfrecord un validation.tfrecord.
1. Sagatavojiet Jums vēlamo daudzumu `.npy` formātā saglabātus orientieru masīvus, kas iegūts no video materiāliem.
2. Atveriet un palaidiet Jupyter grāmatiņu `code/preprocess_landmarks.ipynb`.
3. Grāmatiņa veiks training.tfrecord un validation.tfrecord izveidi, no saglabātajiem datiem, kas atrodas `data/processed_landmarks/training_landmarks` mapītē.


## Modeļa apmācība

1.  Sagatvojiet training.tfrecord un validation.tfrecord ar `code/preprocess_landmarks.ipynb`.
2.  Atveriet un palaidiet Jupyter grāmatiņu `code/train_42.ipynb`.
3.  Grāmatiņa veiks LZV modeļa apmācību, izmantojot pārneses mācīšanās stratēģiju no norādītā ASL modeļa (`cslr_model_best_42.keras`).
4.  Apmācības procesa beigās tiks saglabāti faili jaunā direktorijā zem `models/lzv/`, piemēram, `models/lzv/X/` (kur X ir eksperimenta indekss):
    * Apmācītais LZV modelis `.keras` formātā (gan pilnais apmācības modelis, gan modelis minējumu veikšanai).
    * JSON fails ar eksperimenta metadatiem un rezultātiem.
    * PNG attēls ar apmācības grafikiem (kļūdām, WER).
