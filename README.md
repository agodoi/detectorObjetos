# Global Solutions 2023 - AI Challenges and Solutions

## Detector de objetos usando YOLOv5 e ESP32-CAM

## Criação do banco de imagens de objetos

Para treinar o nosso detector, precisamos de um bom número de exemplos de imagens dos objetos que queremos detectar, para isso, vamos usar imagens da internet contendo o nosso objeto em questão. A ideia é ter o máximo de tipos de fotos de diversos ângulos do nosso objeto.

Quanto mais exemplos e situações temos do nosso objeto (Ambiente escuro, ângulos, fases de maturação, etc.) melhor nosso modelo vai detectar. Por exemplo, se tivemos apenas exemplos de fotos de perfil de um objeto, ele provavelmente só irá conseguir detectar um objeto se colocarmos ele de perfil e com uma iluminação focada no objeto.

Busca de fotos
Procure imagens contendo o objeto e salve tudo em uma pasta local.
Se possível, renomeie cada arquivo nesse formato: [NOME DO OBJETO]_[NUMERO DO EXEMPLO] (Opcional)
Exemplo: maca_01. Isso vai facilitar na visualização e organização dos arquivos.
Após isso, separe 80% em uma nova pasta chamada train e o resto em uma pasta chamada val
Mova as pastas train e val para uma nova pastas chamada images
Criação dos labels
Agora que temos as imagens separadas, vamos criar os rótulos de cada objeto, para isso, temos que delimitar onde cada objeto está em cada imagem de treino e validação.

Vamos usar o site makesense.ai para isso.

Entre no site e clique em "Get started"
Arraste a pasta de imagens de treino/validacao para o quadrado das imagens. (Você irá precisar fazer esse processo com as duas, uma de cada vez)
Clique em "Object Detection"
No modal de "Create Labels" crie um rótulo para cada tipo de objeto que você irá rotular.
Clique em "Start project"
Crie uma caixa delimitadora retangular para cada objeto em cada imagem. Exemplo: Exemplo label de uma maçã
Importante! Se houver mais de um objeto na foto, crie uma caixa para cada objeto, mesmo que eles sejam do mesmo tipo. Exemplo: Se houver duas maçãs na foto, crie uma caixa para cada maçã, e não uma caixa só para as duas junto.

Após criar as caixas para todas as imagens, vá em "Actions" e "Export annotations".
Dentro do modal, selecione "A .zip package containing files in YOLO format". Dentro desse zip estão todos os rótulos para cada imagem.
Crie uma pasta chamada labels e dentro dela crie uma nova pasta com o tipo de imagem que você estava rotulando (train ou val).
Extraia o conteúdo do .zip para a pasta que você criou.
Repita o processo com as imagens de validação/treino. No final, você terá que ter os labels de treino e validação dentro da sua respectiva pasta.
No final do processo, você terá que ter essa estrutura de arquivos:

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
Pronto! Agora vamos para o treinamento do nosso modelo
