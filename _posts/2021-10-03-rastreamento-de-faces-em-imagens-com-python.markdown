---
layout: post
title:  "Rastreamento de faces em imagens com python"
date:   2021-03-06 20:25:03 -0300
categories: python visão-computacional inteligência-artificial
---

![face-detection-python]({{ site.url }}/assets/face-detection-example.png){:style="width: 100%" }
***Fonte***: *https://pixabay.com/pt/photos/bela-mulher-face-mulher-jovem-2150881/*

Fala pessoal blz? No post de hoje eu vou ensinar vocês de forma simples como construir um algoritmo em python realizar a detecção de faces em imagens. E aí, bora aprender algo novo?

## Instalando as bibliotecas a serem utilizadas com o python

Se você quiser utilizar um ambiente virtual para testar o nosso script eu recomendo que veja o artigo [link para o artigo]({% post_url 2019-04-11-criacao-de-um-ambiente-virtual-em-python %}) para ver como utilizar um ambiente virtual fechado em projetos python caso você ainda não saiba fazer isso e queira utilizar esse recurso para manter seus projetos organizados e isolados. Se não, pode continuar a leitura.

O primeiro passo é instalar a biblioteca __opencv__. Ela possui muitos recursos voltados para o processamento digital de imagens e visão computacional.

Abra o seu terminal e digite o comando a seguir para instalar a biblioteca que precisamos utilizar no nosso script:

```bash
pip install opencv-python
```
Para esse projeto vamos utilizar um método bastante famosos chamado __Haar Cascade Classifiers__. Esse método é uma abordagem eficaz de detecção de objetos que foi proposta por Paul Viola e Michael Jones em seu artigo: "__Rapid Object Detection using a Boosted Cascade of Simple Features__" publicado no ano de 2001. Recomendo a leitura do artigo caso você queira entender a fundo a matemática utilizada nesse método.

Os __Haar Cascade Classifiers__ nada mais são do que abordagens baseadas e aprendizado de máquina em que uma função baseada em cascata é treinada a partir de uma base de imagens positivas e negativas (i.e., dataset de treino e validação) e com base nesse treinamento essas funções cascata são utilizadas para detectar determinados objetos em imagens novas.

Para entender como eles funcionam imagine que para cada objetivo (i.e., o que desejamos detectar) temos arquivos gigantes com extensão ".xml" que correspondem a um  caso de uso específico e nesse caso, podemos tomar como exemplo o nosso objetivo nesse post que é a detecção de faces.

Para nosso post você vai precisar baixar o arquivo __xml__ do classificador já treinado
[(haarcascade_frontalface_default.xml)](https://github.com/opencv/opencv/tree/master/data/haarcascades){:target="_blank"}.

O nosso projeto vai seguir a seguinte estrutura de diretórios:

```bash
├── face-detection-in-image.py
├── imagens
│   ├── modificada
│   └── original
│       └── imagem1-original-com-face.jpg
├── modelo
│   └── haarcascade_frontalface_default.xml
```

Como é possível observar precisamos criar o arquivo __face-detection-in-image.py__ dentro da pasta que armazena os códigos do nosso projeto. Precisamos criar uma pasta para guardar nossas imagens utilizadas no projeto e para isso vamos criar a pasta __imagens__ no mesmo diretório do arquivo __face-detection-in-image.py__. Dentro da pasta __imagens__ crie outras duas pastas, uma chama __modificada__ que não irá ter nenhum conteúdo no momento e uma segunda pasta chamada __original__. Dentro da pasta original você vai colocar o arquivo de imagem que você pretender usar para procurar faces. No caso desse post, vamos utilizar a imagem:

![imagem-com-face]({{ site.url }}/assets/imagem1-original-com-face.jpg){:style="width: 100%" }

***Figura 1***: *Fonte: https://pixabay.com/pt/photos/bela-mulher-face-mulher-jovem-2150881/*

Ainda no mesmo diretório de __imagens__ e dp arquivo __face-detection-in-image.py__ crie uma pasta chamada modelo e dentro dela coloque o arquivo [(haarcascade_frontalface_default.xml)](https://github.com/opencv/opencv/tree/master/data/haarcascades){:target="_blank"} que você baixou.

Pronto, agora vamos criar nosso algoritmo para detectar o rosto na __Figura 1__.

Vamos editar o arquivo __face-detection-in-image.py__ com seu editor favorito, digite os comandos abaixo e salve o arquivo quando terminar de editar ele:

{% highlight python linenos %}
# Biblioteca do opencv que instalamos no terminal utilizando o gerenciador de pacotes pip
import cv2
# Aqui carregamos nosso classificador cascata
face_classifier = cv2.CascadeClassifier('modelo/haarcascade_frontalface_default.xml')

imagem_original = cv2.imread('imagens/original/imagem1-original-com-face.jpg')
copia_da_imagem_original = cv2.imread('imagens/original/imagem1-original-com-face.jpg')

#Para que o modelo funcione corretamente é necessário mudar a imagem realizando o processamento de imagem alterando ela para escala de cinza
imagem_original_gray = cv2.cvtColor(imagem_original, cv2.COLOR_BGR2GRAY)

#Variável que armazena objeto(s) com as coordenadas da face encontrada na imagem
faces = face_classifier.detectMultiScale(imagem_original_gray, 1.0485258, 6)

if len(faces) == 0::
    print("Nenhuma face encontrada!")
else:
    for (x,y,w,h) in faces:
        # cv2.rectangle comando utilizado para inserir um retangulo nas coordenadas encontradas pelo modelo cascata
        face_detected = cv2.rectangle(imagem_original, (x,y), (x+w,y+h), (127,0,255), 2)

    # Salva a imagem modificada com a face/rosto encontrado na imagem na pasta modificada    
    cv2.imwrite('imagens/modificada/imagem1-modificada-com-face.jpg', face_detected)

    #Comando utilizado para exibir imagem
    cv2.imshow('Face Detectada', face_detected)
    cv2.imshow("Imagem Original",copia_da_imagem_original)
    #Comando utilizado para permitir que as imagems apareçam e fiquem esperando na tela até que o usuário digite o comando "Esc" para fechar as imagens depois que forem visualizadas com calma
    cv2.waitKey(0)
    #Comando utilizado para destruir as imagens visualizadas e não manter elas na memória
    cv2.destroyAllWindows()

{% endhighlight %}

No código acima, as linhas de código comentadas descrevem o que a linha abaixo dela irá realizar no nosso algoritmo e devido a isso o código já está auto explicativo e por isso basta que você leia os comentários para entender o que cada parte no código faz. Em caso de dúvidas deixe um comentário no fim do post.

Depois que o arquivo __face-detection-in-image.py__ estiver com os códigos acima, abra seu terminal na raiz do seu projeto (i.e., no mesmo nível do arquivo face-detection-in-image.py) e digite o seguinte comando:

```bash
python face-detection-in-image.py
```
Ou
```bash
python3 face-detection-in-image.py
```
No caso de você não estar dentro de um ambiente virtual python e também caso você tenha mais de uma versão do python instalada na sua máquina.

Depois que rodar esse comando irá surgir na sua tela a imagem original e a imagem depois de passar pelo modelo cascata. Depois que visualizar as imagens aperte "ESC" para terminar o processo. Quando as imagens sumirem da sua tela o nosso algoritmo vai salvar a imagem nova com o rosto/face detectado(a) na pasta __imagens/modificada__ com  o nome  __imagem1-modificada-com-face.jpg__.

O resultado gerado será esse aqui se tudo ocorreu bem:

![imagem-com-face]({{ site.url }}/assets/imagem1-modificada-com-face.jpg){:style="width: 100%" }

***Figura 2***: *Fonte: imagem gerada pelo autor*

Espero que tenha gostado do artigo caro(a) leitor(a)! Te vejo no próximo post. Para que nosso trabalho possa ajudar mais pessoas, compartilhe esse artigo com seus amigos nas mídias sociais.
