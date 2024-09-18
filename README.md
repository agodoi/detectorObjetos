# NEXT 2024 - AI Computer Systems and Sensors

## Detector de objetos usando YOLOv5 e ESP32-CAM

## Criação do banco de imagens de objetos

Para treinar o nosso detector, precisamos de um bom número de exemplos de imagens dos objetos que queremos detectar, para isso, vamos usar imagens da Internet contendo o nosso objeto em questão. A ideia é ter o máximo de tipos de fotos de diversos ângulos do nosso objeto.

Quanto mais exemplos e situações temos do nosso objeto (Ambiente escuro, ângulos, fases de maturação, etc.) melhor nosso modelo vai detectar. Por exemplo, se tivemos apenas exemplos de fotos de perfil de um objeto, ele provavelmente só irá conseguir detectar um objeto se colocarmos ele de perfil e com uma iluminação focada no objeto.

## Passo-01: Organizando em pastas no Google Drive

Vamos organizar no seu Google Drive para permitir o uso em casa e na sala de aula. E vamos usar o Colab para treinar o seu modelo.

**1.1)** No seu PC, crie 4 pastas/subpastas da seguinte forma:

- **images**
    - **/train**
        - nessa pasta você colocará 48 imagens de treino
    - **/val**
        - nessa pasta você colocará 12 imagens de validação do seu modelo. No total, você terá 60 fotos.
- **labels**
    - **/train**
        - labels das imagens de treino
    - **/val**
        - labels das imagens de validação

## Passo-02: Busca de fotos

**2.1)** Procure imagens contendo o objeto e salve tudo em uma pasta local no seu PC.

**2.2)** Renomeie cada arquivo nesse formato: [NOME DO OBJETO]_[NUMERO DO EXEMPLO] (Opcional)

**2.3)** Exemplo: telhado_01. Isso vai facilitar na visualização e organização dos arquivos.

**2.4)** Após isso, separe 80% em uma nova pasta chamada **train** e o resto em uma pasta chamada **val**

**2.5)** Mova as pastas train e val para uma nova pastas chamada **images**.

**2.6)** O resultado será esse:

```images/train```

```images/val```

Agora que temos as imagens separadas, vamos criar os rótulos de cada objeto, para isso, temos que delimitar onde cada objeto está em cada imagem de treino e validação.

## Passo-03: Site makesense.ai

Observação, pode ser que o site tenha se atualizado e consequentemente, haver alguma pequena alteração das etapas a seguir. Contudo, isso não deve prejudicar o seu avanço.

**3.1)** Entre no site **[makesense.ai](https://www.makesense.ai/)** e clique em **Get started**;

**3.2)** Clique no quadrado **Drop imagens or Click here to select them**, aponte para a sua pasta local **images/train**, dê um ```Ctrl a``` para selecionar todas as imagens ao mesmo tempo, e confirme. (Você precisará repetir esse passo para **images/val**);

**3.3)** Clique em **Object Detection**;

**3.4)** Na tela seguinte, em **Create labels** crie um rótulo que faça sentido para o objeto que você está reconhecendo. Nesse caso, **telhado**.

**3.5)** Clique em **Start project**;

**3.6)** Crie uma caixa delimitadora retangular para cada objeto em cada imagem e à direita da sua tela, escolha o label **telhado**. Na sua seleção da moldura, dê ênfase ao que você está pretendendo reconhecer, que nesse caso, será telhado inundado.


<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/detectorObjetos/blob/main/assets/exemplo_telhado.jpg">
   <img alt="Tecnologias Módulo 02" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/detectorObjetos/blob/main/assets/exemplo_telhado.jpg)">
</picture>


Importante! Se houver mais de um objeto na foto, crie uma caixa para cada objeto, mesmo que eles sejam do mesmo tipo. Exemplo: Se houver dois telhados separados na foto, crie uma caixa para o primeiro telhado e outra caixa para o outro telhado, e não uma caixa só para os dois juntos.

## Passo-04 - Exportando as imagens

**4.1)** Após criar as caixas para todas as imagens, vá em "Actions" e "Export annotations".

**4.2)** Selecione **A .zip package containing files in YOLO format**. Dentro desse zip estão todos os rótulos para cada imagem.

**4.3)** Salve esse zip na subpasta **labes/train** que você criou na ETAPA-01.

**4.4)** Descompacte o conteúdo do .zip nessa subpasta e os seus TXT estarão no **labes/train**.

**4.5)** Repita o processo com as **images/val**.

**4.6)** No final, você terá que ter os labels de treino e validação dentro da sua respectiva pasta da seguinte forma:

- images/
  - train/
    - imagens de treino
  - val/
    - imagens de validação
- labels/
  - train/
    - labels das imagens de treino
  - val/
    - labels das imagens de validação

**4.7)** Guarde essa estrutura de pastas no seu Google Drive, em pasta ou subpasta sem espaços ou caracteres especiais, de preferência, o mais próximo da raiz. Exemplo

```MEU DRIVE\PROJETOS\DRONE\2024\```

Pronto! Agora vamos para o treinamento do nosso modelo numa próxima etapa. Aguarde as orientações do professor.

## Passo-05 - Criando o código no Colab

Primeira coisa que você precisa fazer é instanciar um computador mais poderoso no seu Colab.


**5.1)**
```
from google.colab import drive
drive.mount('/content/drive')
```

**5.2)**
```
! git clone https://github.com/ultralytics/yolov5.git
```

**5.3)**
```
! pip install -r yolov5/requirements.txt
```

**5.4)** Crie um arquivo chamado **telhado.yaml** usando o bloco de notas. E coloque o seguinte conteúdo dentro desse arquivo:

```
train: /content/drive/MyDrive/PROJETOS/DRONE/2024/images/train/
val: /content/drive/MyDrive/PROJETOS/DRONE/2024/images/val/

names: # Defina aqui as labels do seu dataset
  0: "Telhado"
  1: "Pessoa"
  2: "Galhos"
  # ...
```

Após ter criado o arquivo **telhado.yaml**, arraste-o para a raiz do seu Google Drive conforme a figura a seguir.

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/detectorObjetos/blob/main/assets/tela_google_01.jpg">
   <img alt="Tecnologias Módulo 02" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/detectorObjetos/blob/main/assets/tela_google_01.jpg)">
</picture>


```
! cp /content/drive/MyDrive/PROJETOS/DRONE/2024/telhado.yaml yolov5/data/
```

**5.5)** Nessa etapa, você fará o treinamento do seu modelo. Você pode mexer na variável ```--epochs``` mudando o número na frente dele. Exemplo, você pode subir o **40** para **60** e analisar os resultados de acurácia do seu modelo.

```
! python yolov5/train.py --data telhado.yaml --weights yolov5s.pt --img 640 --epochs 40
```

**5.6)** Nessa etapa, você precisa criar uma subpasta chamada ```test```, ficando assim:

**train: /content/drive/MyDrive/PROJETOS/DRONE/2024/test**

```
import os
import subprocess

def get_latest_train_run_folder():
    subfolders = [f.path for f in os.scandir('yolov5/runs/train') if f.is_dir()]
    latest_folder = max(subfolders, key=os.path.getctime, default=None)
    return latest_folder

latest_run = get_latest_train_run_folder()
result = subprocess.run(f'python yolov5/detect.py --weights {latest_run}/weights/best.pt --img 640 --source tests/ --data yolov5/data/trator.yaml', shell=True, capture_output=True, text=True)
if latest_run:
    # COMANDO
    result = subprocess.run(f'python yolov5/detect.py --weights {latest_run}/weights/best.pt --img 640 --source tests/ --data yolov5/data/trator.yaml', shell=True, capture_output=True, text=True)
    print(result.stdout)
    print(result.stderr)
else:
    print("Não foi possível encontrar a pasta de treinamento mais recente.")
```
