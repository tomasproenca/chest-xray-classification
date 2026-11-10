# Classificação de radiografias de tórax

Projeto académico de visão por computador organizado como uma sequência de três notebooks:

1. [`01_baseline_cnn.ipynb`](01_baseline_cnn.ipynb) — primeira abordagem com uma CNN simples (Trabalho 1).
2. [`02_data_augmentation.ipynb`](02_data_augmentation.ipynb) — extensão da abordagem com preparação e aumento de dados (Trabalho 2, parte 1).
3. [`03_transfer_learning.ipynb`](03_transfer_learning.ipynb) — experiências com CNN, extração de características e *fine-tuning* (Trabalho 2, parte 2).

`data/` contém apenas a estrutura vazia com `.gitkeep`. `results/` começa vazia e recebe os CSV gerados pelos notebooks. Cada etapa guarda o seu histórico com um nome distinto. Os notebooks usam caminhos relativos e devem ser executados com esta pasta como diretório de trabalho, pela ordem numérica.

Os gráficos de experiências históricas são ignorados quando os respetivos CSV não existem em `results/`. O terceiro notebook recria `data_balanced/` e remove uma versão anterior dessa pasta, se existir.

As imagens em `data/` e a pasta gerada `data_balanced/` estão excluídas do Git. Os `.gitkeep` preservam apenas a estrutura de `data/` e `results/`. As radiografias foram disponibilizadas para o trabalho académico e não são redistribuídas neste repositório. A execução requer acesso próprio e autorizado ao dataset. As conclusões dos notebooks distinguem agora os modelos efetivamente treinados das variantes históricas não reproduzidas nesta execução. O conjunto de teste é usado como validação durante o treino; as métricas não são uma avaliação final independente. Os modelos não foram validados para uso clínico.

## Ambiente para Windows com RTX 3060 Ti

Em Windows nativo, a última versão de TensorFlow com suporte oficial a GPU é a 2.10. Esta combinação requer Python 3.10, CUDA 11.2 e cuDNN 8.1. Criar o ambiente na raiz deste projeto:

```powershell
conda create -n chest-xray python=3.10
conda activate chest-xray
conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1.0
python -m pip install -r requirements.txt
python -m ipykernel install --user --name chest-xray --display-name "Python (chest-xray)"
```

Confirmar a versão de Python e o acesso à GPU antes de treinar:

```powershell
python --version
python -c "import tensorflow as tf; print(tf.__version__); print(tf.config.list_physical_devices('GPU'))"
```

Uma instalação local validada terminou sem erros e devolveu TensorFlow `2.10.1` e uma GPU em `list_physical_devices('GPU')`. Python 3.11 não disponibilizou o pacote TensorFlow 2.10.1 neste ambiente Windows; selecionar o kernel criado com Python 3.10 nos notebooks. Os três notebooks foram executados localmente pela ordem numérica com TensorFlow 2.10.1 e GPU detetada, sem erros reportados. Os resultados e as saídas incorporadas foram removidos após essa execução.

Noutros sistemas, seguir as [instruções oficiais de instalação do TensorFlow](https://www.tensorflow.org/install/pip); WSL2 usa uma configuração diferente.

## Dados esperados

Os notebooks esperam imagens em `data/train/NORMAL`, `data/train/PNEUMONIA`, `data/test/NORMAL` e `data/test/PNEUMONIA`. Antes de executar, colocar um dataset obtido legitimamente nas pastas correspondentes em `data/`, mantendo os `.gitkeep`. Os dados utilizados no trabalho académico não são disponibilizados aqui; qualquer redistribuição depende de autorização do responsável pelos dados. `data_balanced/` não está incluída na pasta inicial: é criada pelo terceiro notebook.
