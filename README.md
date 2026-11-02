<h1 align="center">LINKER-Pred-Lite</h1>
<p align="center"><i>A high-speed Disordered Flexible Linker (DFL) predictor trained on <a href="https://dld.chemeslab.org/">DLD</a> (Domain-Linker-Domain) dataset and <a href="https://disprot.org/">Disprot</a> Database.</i></p>

## 📝 Description
LINKER-Pred-Lite project belongs to a series of LINKER-Pred suite projects which focus on the prediction of Disordered Flexible Linkers (DFLs).
Currently we have <a href="https://github.com/deemeng/punch_linker_light">LINKER-Pred-Lite</a> for fast DFL prediction, and <a href="https://github.com/deemeng/punch_linker">LINKER-Pred</a> and <a href="https://github.com/deemeng/punch_linker2">LINKER-Pred2</a> for more accurate DFL prediction.
LINKER-Pred-Lite is trained on more than 2000 protein sequences from our <a href="https://dld.chemeslab.org/">DLD</a> dataset and additional annotated linkers from <a href="https://disprot.org/">Disprot</a>. Its performance is among the TOP predictors in the CAID 2 and 3 linker datasets.
There is no MSA searching needed for the prediction. Therefore, compared to LINKER-Pred and LINKER-Pred2, the prediction may be slightly worse but it only costs ~0.1 second for one prediction.

## 🌐 Web Server
LINKER-Pred-Lite and LINKER-Pred2 are freely available through the LINKER-Pred web server, with no installation needed: https://linkerpred.chemeslab.org

## 🐣 Getting Started
Currently, we provide two ways to use this predictor: Docker or Download source code from this Github.
### Pre-requirements
This predictor requires sequences embedded with [ProtTrans](https://github.com/agemagician/ProtTrans).
Note, 
* File format should be `[SEQUENCE_NAME/ID].npy`, replace *SEQUENCE_NAME/ID* with the actual sequence ID, it should be the same as the name from `.fasta` file.
* Matrix shape: \
  **ProtTrans**: `(1, SEQUENCE_LENGTH, 1024)`

📣‼️If you don't have them available, please visit the **[embedding](https://github.com/deemeng/embedding)** section of our project first to embed the sequences.‼️

(We maintain this separation due to the requirements from [CAID3](https://caid.idpcentral.org/challenge), but we may edit or merge them in the future.)
### Docker (Recommended)
#### Dependencies
* Go to **[embedding](https://github.com/deemeng/embedding)** if you don't have [ProtTrans](https://github.com/agemagician/ProtTrans) embedded sequences;
* Docker Desktop 4.27.2 or higher;
#### Installing
* Pull the Docker image from  <a href="https://hub.docker.com/repository/docker/dimeng851/punch_linker_light/tags">DockerHub</a>
  ```sh
  docker pull dimeng851/punch_linker_light:v4
  ```

#### Executing program
* RUN the following command:
  >Replace \
  >`CONTAINER_NAME` - any name you like; \
  >`PATH_TO_INPUT_FASTA` - path to input file, which is **ONE** FASTA file including all query sequences; \
  >`PATH_TO_PROTTRANS` - a folder which includes all protTrans embedded sequences; \
  >`PATH_OUTPUT` - a folder which will be used to save all outputs, including: a. timings.csv; b. linker folder, where will keep all the prediction results.
  ```sh
  docker run -d \
  -it \
  --name [CONTAINER_NAME] \
  --mount type=bind,source=[PATH_TO_INPUT_FASTA],target=/punch_linker_light/data/input.fasta \
  --mount type=bind,source=[PATH_TO_PROTTRANS],target=/punch_linker_light/data/protTrans \
  --mount type=bind,source=[PATH_OUTPUT],target=/punch_linker_light/output \
  dimeng851/punch_linker_light:v4
  ```
  > 
  >An example:
  ```sh
  docker run -d \
  -it \
  --name punch_linker_con \
  --mount type=bind,source=/Users/deemeng/Downloads/data/linker/linker.fasta,target=/punch_linker_light/data/input.fasta \
  --mount type=bind,source=/Users/deemeng/Downloads/data/linker/protTrans,target=/punch_linker_light/data/protTrans \
  --mount type=bind,source=/Users/deemeng/Downloads/data/linker/output,target=/punch_linker_light/output \
  dimeng851/punch_linker_light:v4
  ```
* Find the results in **OUTPUT** folder.

## Publication
Meng D<sup>\*</sup>, Garcia Alvarez HM<sup>\*</sup>, Glavina J, Leonetti CO, Pollastri G, Chemes LB<sup>#</sup>. LINKER-Pred: A Deep Learning Method and Web-Server for the Prediction of Disordered Flexible Linkers in Proteins. *bioRxiv* 2026 (version 2). https://www.biorxiv.org/content/10.1101/2025.10.29.685455v2

\* Equally contributing authors \
<sup>#</sup> correspondence: lchemes@iib.unsam.edu.ar

This manuscript is currently under review.

## Help 📩

Contact Heli (hgarciaalvarez@iib.unsam.edu.ar) or Di (di.meng@ucdconnect.ie).

## Project
>https://github.com/deemeng/punch_linker_light
