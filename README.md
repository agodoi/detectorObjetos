# NEXT 2024 - AI Computer and Sensors

## Detector de objetos usando YOLOv5 e ESP32-CAM

## Criação do banco de imagens de objetos

Para treinar o nosso detector, precisamos de um bom número de exemplos de imagens dos objetos que queremos detectar, para isso, vamos usar imagens da Internet contendo o nosso objeto em questão. A ideia é ter o máximo de tipos de fotos de diversos ângulos do nosso objeto.

Quanto mais exemplos e situações temos do nosso objeto (Ambiente escuro, ângulos, fases de maturação, etc.) melhor nosso modelo vai detectar. Por exemplo, se tivemos apenas exemplos de fotos de perfil de um objeto, ele provavelmente só irá conseguir detectar um objeto se colocarmos ele de perfil e com uma iluminação focada no objeto.

## Passo-01: Organizando em pastas
**1.1)** No seu PC, crie 4 pastas/subpastas da seguinte forma:

- **images**
    - **/train**
        - nessa pasta você colocará imagens de treino
    - **/val**
        - nessa pasta você colocará imagens de validação do seu modelo
- **labels**
    - **/train**
        - labels das imagens de treino
    - **val/**
        - labels das imagens de validação

## Passo-02: Busca de fotos

**2.1)** Procure imagens contendo o objeto e salve tudo em uma pasta local no seu PC.

**2.2)** Se possível, renomeie cada arquivo nesse formato: [NOME DO OBJETO]_[NUMERO DO EXEMPLO] (Opcional)

**2.3)** Exemplo: maca_01. Isso vai facilitar na visualização e organização dos arquivos.

**2.4)** Após isso, separe 80% em uma nova pasta chamada train e o resto em uma pasta chamada val

**2.5)** Mova as pastas train e val para uma nova pastas chamada images

**2.6)** Criação dos labels

Agora que temos as imagens separadas, vamos criar os rótulos de cada objeto, para isso, temos que delimitar onde cada objeto está em cada imagem de treino e validação.

## Passo-03: Site makesense.ai

Observação, pode ser que o site tenha se atualizado e consequentemente, haver alguma pequena alteração das etapas a seguir. Contudo, isso não deve prejudicar o seu avanço.

**3.1)** Entre no site **makesense.ai** e clique em "Get started";

**3.2)** Arraste a pasta de imagens de treino/validacao para o quadrado das imagens. (Você irá precisar fazer esse processo com as duas, uma de cada vez);

**3.3)** Clique em "Object Detection";

**3.4)** No modal de "Create Labels" crie um rótulo para cada tipo de objeto que você irá rotular;

**3.5)** Clique em "Start project";

**3.6)** Crie uma caixa delimitadora retangular para cada objeto em cada imagem. Exemplo: Exemplo label de uma maçã.


<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/detectorObjetos/blob/main/assets/exemplo_maca.png">
   <img alt="Tecnologias Módulo 02" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/detectorObjetos/blob/main/assets/exemplo_maca.png)">
</picture>


Importante! Se houver mais de um objeto na foto, crie uma caixa para cada objeto, mesmo que eles sejam do mesmo tipo. Exemplo: Se houver duas maçãs na foto, crie uma caixa para cada maçã, e não uma caixa só para as duas junto.

## Passo-04 - Exportando as imagens

**4.1)** Após criar as caixas para todas as imagens, vá em "Actions" e "Export annotations".

**4.2)** Dentro do modal, selecione "A .zip package containing files in YOLO format". Dentro desse zip estão todos os rótulos para cada imagem.

**4.3)** Crie uma pasta chamada labels e dentro dela crie uma nova pasta com o tipo de imagem que você estava rotulando (train ou val).

**4.4)** Extraia o conteúdo do .zip para a pasta que você criou do seu projeto no **Passo-01**;

**4.5)** Repita o processo com as imagens de validação/treino. 

**4.6)** No final, você terá que ter os labels de treino e validação dentro da sua respectiva pasta. No final do processo, você terá que ter essa estrutura de arquivos:

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

Pronto! Agora vamos para o treinamento do nosso modelo numa próxima etapa. Aguarde as orientações do professor.

