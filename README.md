# Workshop Azure Machine Learning Designer 
Este workshop contém instruções sobre como criar seu primeiro experimento utilizando o Azure Machine Learning Designer

## Praparar o ambiente ##

> 1. Crie sua conta gratuita no Azure

Basta seguir o passo a passo do link abaixo. Obs: Utilize um email para criar sua conta Microsoft que nunca tenha utilizado para trial do Azure anteriormente.
Link: https://azure.microsoft.com/pt-br/free/
___
   
> 2. Criar um Resource Group

No portal do Azure Portal click em **"Create a resource"** e então digite **Resource Group** . Click em **"Create"** 

- Subscription: Selecione sua subscrição
- Resource group: Digite um nome para o sue resource. Ex: MeuML
- Selecione uma região. Aqui você pode utilizar qualquer região disponível.   

![img1](/img/resourcegroup.png)

___

> 3. Criar o Machine Learning

No portal do Azure Portal click em **"Create a resource"** e então digite **Machine Learning** . Click em **"Create"** e siga as configurações abaixo: 

- Subscription: Selecione sua subscrição
- Resource group: Selecione o resource group criado na etapa anterior
- Workspace name: Digite um nome para seu workspace. eg: Meu-workspace
- Region: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US 2 por questões de custos.
- Workspace edition: Aqui você deve selecionar "Enterprise".

![img2](/img/MachineLearningWorkspace.png)

___

> 3. Após a criação volte ao resource group que você criou e click no Storage Account que foi criado conforme imagem abaixo:

![img3](/img/resourcegroup_poscriacao.png)

Uma vez dentro do Storage Account click em "Container" conforme imagem abaixo:

![img4](/img/storageaccount_container.png) 
___

> 4. Crie um novo Container

- Basta clicar em "+ Container", após clicar digite um nome para seu container e click em **"Create"** conforme imagem abaixo:

![img5](/img/createcontainer1.png)  

- Após o container ser criado click nele:

![img6](/img/createcontainer2.png)

___

5. Agora é hora de fazer o upload dos dados que você irá utilizar no seu experimentos.

- Eu utilizei o Kaggle (https://www.kaggle.com/vjchoudhary7/hr-analytics-case-study) para baixar um dataset para esse experimento. No meu caso eu dei uma "abrasileirada" no dataset e o mesmo está disponível neste repositório do GitHub. Basta fazer o download do arquivo para depois fazer o upload para o seu Storage Account Container conforme imagem abaixo?

![img7](/img/upload_data.png)

- Após fazer o upload do dataset click no seu Storage Account conforme imagem abaixo:

![img8](/img/storageaccount_key01.png)

- Em seguida click em **"Access Keys"**

![img9](/img/storageaccount_key02.png)

- Agora você deve colocar a Key. No meu exemple copiei a Key1, mas ambas funcionam

![img10](/img/storageaccount_key03.png)

- Você precisa salvar essa chave, pois iremos utilizar ela em uma etapa mais a frente.
___

> 6. Volte ao seu resource group e click em Machine Learning

![img11](/img/marchinelearningclick.png)

Uma vez dentro do recurso click em **"Launch now"**

![img12](/img/ml_launch.png)
___


## Começando nossos experimentos no Azure Machine Learning Studio ##

> 1. Agora você já está dentro do Azure Machine Learning Studio

Click em **"Designer (preview)"** e então click no sinal de + conforme imagens abaixo:

![img13](/img/ml_designer01.png)

![img14](/img/ml_designer02.png)
___

> 2. Preparar nosso experimento

- Primeiro vamos dar um nome e uma descrição para esse pipeline. Do seu lado direito em **"Draft details"** digite um nome e uma descrição para seu experimento

![img15](/img/ml_designername.png)

- Agora precisamos selecionar o **"Compute target"** esses servidores que irão precessar todas as etapas do nosso workflow

    - Click em **"Select compute target"**
    - Em seguida click em **"Create new"**
    - Vamos manter a opção pré-definida de cluster
    - Digite um nome para o seu cluster (são os servidores que irão precessar seu workflow)
    - Click em **"Save"**
    - Click em **"Save"** novamente

![img16](/img/ml_designer03.png)

![img17](/img/ml_designer04.png)

![img18](/img/ml_designer05.png)

- Agora basta clicar novamente em **"Select compute target"** e selecionar o cluster que você acabou de criar

![img19](/img/ml_designer06.png)
___

> 3. Importar os dados

 - Primeiro passo é importar os dados que serão utilizados para esse experimento. Na coluna **"Modules"** ao lado esquerdo click em **"Data Input and Output"** selecione **"Import Data"** e arraste para o centro da tela no campo vazio.

![img20](/img/ml_designer07.png)

- Após a etapa anterior irá aparecer uma coluna **"Import Data"** 
    
    - Deixe selecionado **"Datastore"** 
    - Click em **"New datastore"**

    ![img21](/img/ml_designer08.png)

    - Digite um nome para seu datastore
    - Deixe selecionado **"Azure Blob Storage"**
    - Deixe selecionado **"From Azure subscription"**
    - Deixe selecionado sua subscription
    - Selecionar o Storage Account que foi criado anteriormente
    - Selecionar o Container que você criou
    - Deixe selecionado a opção **"No"**
    - Deixe selecionado **"Account Key"**
    - Em Account Key você deve colar a Key copiada na etapa 5 do "Preparar seu ambiente"
    - Em seguida click em **"Create"**

    ![img22](/img/datastore01.png)

    - Uma vez criado no campo Datastore selecione o datastore que você acabou de criar
    - Click em **"Browse path"** e selecione o arquivo que você fez upload na etapa 5 do "Preparar seu ambiente"
    - Click em **"Save"**

    ![img23](/img/datastore02.png)

    - Agora você deve clicar em **"Submit"** para o designer copiar os dados para seu experimento. Em seguida irá aparecer um pop-up com o nome de **"Set up pipeline run"**

        - Selecione **"Create new"**
        - Digite um nome para seu experimento
        - Digite uma descrição para seu experimento
        - Click em **"Submit"**

        ![img24](/img/run_experimento01.png)

        - Após a execução click na caixa **'Import Data'** e em seguida em **'Preview schema'**

        ![img25](/img/importdata01.png)

        - Tenha certeza que as colunas estão configuradas corretas com **'Interger'** para colunas que contêm palavras e **'Integer'** para as colunas que contêm números

        ![img26](/img/importdata02.png)
        ___    

> 4. Selecionar as colunas ou features

- Na coluna **"Modules"** ao lado esquerdo click em **"Data Transformation"** selecione **"Select Columns in Dataset"** e arraste para o centro da tela no campo vazio.

- Conecte a caixa **"Import Data"** com a caixa **"Select Columns in Dataset"**

- Após a etapa anterior irá aparecer uma coluna **"Select Columns in Dataset"** a sua direita. Click em **"Edit Column"**

    - Selecione **"All columns"** e click no sinal +
    - Selecione **"Exclude"** e aqui você pode selecionar as colunas que você quer excluir do seu experimento utilizando o **"Column names"** 

    ![img27](/img/select_columns.png)
___  

> 5. Limpar linhas que estão sem dados

- Na coluna **"Modules"** ao lado esquerdo click em **"Data Transformation"** selecione **"Clean Missing Data"** e arraste para o centro da tela no campo vazio.

- Conecte a caixa **"Select Columns in Dataset"** com a caixa **"Clean Missing Data"**

- Após a etapa anterior irá aparecer uma coluna **"Clean Missing Data"** a sua direita. Click em **"Edit Column"**

    - Selecione **"All columns"**
    - Click em **"Save"**
    - Minimum missing value ratio pode deixar em **"0.0"**
    - Maximum missing value ratio pode deixar em **"1.0"**
    - Em Cleaning mode selecionar **"Remove entire row"**

    ![img28](/img/clean_missingdata01.png)

    ![img29](/img/clean_missingdata02.png)
___ 
    
> 6. Agora é hora de dividir os dados para treinamento e validação

- Na coluna **"Modules"** ao lado esquerdo click em **"Data Transformation"** selecione **"Split Data"** e arraste para o centro da tela no campo vazio.

- Conecte a caixa **"Clean Missing Data"** com a caixa **"Split Data"**. Obs: Na caixa **"Clean Missing Data"** existem duas saídas e neste caso você deve utilizar a saída da esquerda porque essa saída é a que contém os dados já transformados.

- Após a etapa anterior irá aparecer uma coluna **"Split Data"** a sua direita. Preencha os campos conforme detalhado abaixo:

    - Deixe selecionado **"Split Rows"**
    - No campo **"Fraction of rows in the first output dataset"** mude para **"0.7"** (com isto 70% das linhas serão utilizadas para treinamento e o restando 30% para validação do modelo)
    - No campo **"Random seed"** pode deixar em **"0"**
    - No campo **"Stratified split** selecione **"False"**
        
    ![img28](/img/splitdata01.png)
___ 

> 7. Vamos treinar o modelo agora

- Na coluna **"Modules"** ao lado esquerdo click em **"Model Training"** selecione **"Train Model"** e arraste para o centro da tela no campo vazio.

- Conecte a caixa **"Split Data"** com a caixa **"Train Model"**. Obs: Na caixa **"Split Data"** existem duas saídas e neste caso você deve utilizar a saída da esquerda, pois ela contém os 70% das linhas do nosso dataset que será utilizado no trainamento.

- Após a etapa anterior irá aparecer uma coluna **"Train Model"** a sua direita. Preencha os campos conforme detalhado abaixo:

    - Click em **"Edit column"**
    - No campo **"Select a single column"** selecione **"Column names"** e digite **'Saiu_da_empresa'** (Essa e sua coluna target, ou seja você irá treinar seu modelo para responder se uma pessoa vai sair da empresa ou não)
    - Click em **"Save"**
            
    ![img29](/img/trainmodel01.png)

    ![img30](/img/trainmodel02.png)
___ 

> 8. Agora vamos escolher qual algoritmo de Machine Learning iremos utilizar

- Na coluna **"Modules"** ao lado esquerdo click em **"Machine Learning Algorithms"** selecione **"MultiClass Boosted Decision Tree"** e arraste para o centro da tela no campo vazio. Obs: Como esse é um problema de classificação (sim ou não, groupo a ou grupo b) temos que utilizar algoritmos de Classificação.

- Conecte a caixa **"MultiClass Boosted Decision Tree"** com a caixa **"Train Model"**. 

- Após a etapa anterior irá aparecer uma coluna **"MultiClass Boosted Decision Tree"** a sua direita. Deixe os campos preenchidos do padrão conforme imagem abaixo:

![img31](/img/algoritmoml01.png)
___ 

> 9. Agora nesta etapa vamos dar uma pontuação para nosso modelo após o treino

- Na coluna **"Modules"** ao lado esquerdo click em **"Model Scoring & Evaluation"** selecione **"Score Model"** e arraste para o centro da tela no campo vazio.

- Conecte a caixa **"Train Model"** com a caixa **"Score Model"**. Aqui você também precisa conectar a caixa **"Split Data"** com a caixa **"Score Model"**. Obs: Para fazer a pontuação vamos utilizar o resultado do trainamento do modelo e validar com os 30% das linhas restantes do dataset.

![img32](/img/scoremodel01.png)
___ 

> 10. E finalmente iremos avaliar nosso modelo

- Na coluna **"Modules"** ao lado esquerdo click em **"Model Scoring & Evaluation"** selecione **"Evaluate Model"** e arraste para o centro da tela no campo vazio.

- Conecte a caixa **"Score Model"** com a caixa **"Evaluate Model"**. 

![img33](/img/evaluatemodel01.png)

- Em seguida click em **"Submit"**
    
    - No pop-up com o nome de **"Set up pipeline run"**
    - Selecione **"Select existing"**
    - Selecione o nome do seu experimento
    - Click em **"Submit"**

    ![img34](/img/run_experimento02.png)
    ___ 

> 11. Verificar o resultado do seu experimento

- Click na caixa **"Evaluate Model"**. Em seguida click em **"Outputs + logs"**, depois click o sinal de um gráfico de barras.

![img35](/img/resultado01.png)

- Você pode clicar em cada caixa e em seguida click em **"Outputs + logs"** para verificar o resultado após a execução.

![img36](/img/resultado02.png)
___ 

> 12. Vamos melhorar nosso modelo agora

- Click com botão da direita do mouse sobre a caixa **"MultiClass Boosted Decision Tree"** e depois click em **"Delete"**

- Na coluna **"Modules"** ao lado esquerdo click em **"Machine Learning Algorithms"** selecione **"Multiclass Decision Forest"** e arraste para o centro da tela no campo vazio.

- Conecte a caixa **"Multiclass Decision Forest"** com a caixa **"Train Model"**. 

- Após a etapa anterior irá aparecer uma coluna **"Multiclass Decision Forest"** a sua direita. Deixe os campos preenchidos do padrão conforme imagem abaixo:

![img37](/img/algoritmoml02.png)

- Em seguida click em **"Submit"**
    
    - No pop-up com o nome de **"Set up pipeline run"**
    - Selecione **"Select existing"**
    - Selecione o nome do seu experimento
    - Click em **"Submit"**

    ![img34](/img/run_experimento02.png)
    ___ 

> 12. Verificar o resultado novamente

- Click na caixa **"Evaluate Model"**. Em seguida click em **"Details"**. 

![img35](/img/resultado03.png)

- Como podemos ver dessa vez atingimos um acurácia de 0.96% o que já está ótimo para nosso experimento
___ 

> 13. Agora vamos criar um endpoint para podermos consumir nosso modelo 

- No menu a esquerda click em **"Compute"**
- Sem seguida em **"Inference Cluster"**
- Depois em **"Create"**

![img36](/img/clusterinf01.png)

- No pop-up com o nome de **"New inference cluster"**
    - Digite um nome para o seu cluster
    - Selecione **"Create new"**
    - Selecione uma região. (Recomento utilizar East US 2/ Leste dos EUA 2 por questões de custo)
    - Selecione um tamanho de VM. (Deixe o padrão recomendado **'Standard_D3_v2'**)
    - Selecione **"Production"**
    - Defina um número de nós para o cluster. Para esse experimento deixe o padrão **"3"**
    - Em "Network Configuration" selecione **"Basic"**
    - Click em **"Create"**

    ![img37](/img/clusterinf02.png)

    - Assim que terminar volte para seu experimento 

    ![img38](/img/clusterinf02.png)

- Click em **"Create inference pipeline"** e em seguida selecione **"Real-time inference pipeline"**

![img39](/img/voltaexp.png)

- Click em **"Submit"**

![img40](/img/deploymodel02.png)

<!-- No pop-up com o nome de **"Set up pipeline run"**
    - Selecione **"Select existing"**
    - Selecione o nome do seu experimento
    - Click em **"Submit"**-->

- Após finalizar click em **"Deploy"**

![img41](/img/deploymodel03.png)

- No pop-up com o nome de **"Set up real-time endpoint"**
    - Selecione **"Deploy new real-time endpoint"**
    - No campo **"Real-time endpoint name"** digite um nome para seu endpoint
    - No campo **"Endpoint description"** digite uma descrição para seu endpoint. Obs: Esse campo é opcional
    - No campo **"Compute target"** Selecione o cluster que você criou
    - Click em **"Deploy"**

    ![img42](/img/deploymodel04.png)

    ![img43](/img/deploymodel05.png)

- Após concluir volte ao Designer e click em **"Publish"**

- No pop-up com o nome de **"Set up published pipeline"**
    - Selecione **"Create new"**
    - No campo **"New PipelineEndpoint name"** digite um nome 
    - No campo **"PipelineEndpoint description"** digite uma descrição. Obs: Esse campo é opcional
    - Deixe marcada as opções **"Set as default pipeline for this endpoint"** e **"Continue on failure step"**
    - Click em **"Publish"**

    ![img44](/img/deploymodel07.png)
    ![img45](/img/consume01.png)
___ 

> 14. Agora é hora de consumir nosso modelo

- Click em **"Endpoints"**

![img45](/img/consume02.png)

- Click no seu **"Real-time endpoints"**

![img46](/img/consume03.png)

- Click na aba **"Test"** e em seguida no botão **"Test"**

![img47](/img/consume03.png)

- Pronto testamos nosso experimento com um retorno bem satisfatório.
___ 

## Agora vamos consumir nosso modelo no PBI ##

> 1. Primeiro passo é baixar o Power BI Desktop

- Baixe pelo link: https://www.microsoft.com/pt-br/download/details.aspx?id=58494

- Instale o Power BI seguindo as opções default. Após a instalação abra o mesmo

![img47](/img/pbi01.png) 
___ 

> 2. Agora vamos importar uma amostra para o Power BI

- Click no icone **"Excel"**

![img48](/img/pbi02.png) 

- Selecione **"Sheet1"** e depois click em **"Load"**

![img49](/img/pbi03.png)
___ 

> 3. Vamos habilitar as features em preview do Power BI

- Click em **"File"**, depois click em **"Options and settings"** e em seguida **"Options"**

![img50](/img/pbi04.png)

![img51](/img/pbi05.png)

- Click em **"Previews features"**, depois click na caixa **"AI Insights function browser"** 

![img52](/img/pbi06.png)
___ 

> 4. Agora vamos consumir nosso modelo

- Click no icone **"Transform data"**, depois click em **"Transform data"** 

![img53](/img/pbi07.png)

- Agora no Power Query Editor você conseguirá visualizar os dados da amostra

- Click no **"Azure Machine Learning"**, depois click em **"Sign in"**

- Agora você precisa logar com suas credenciais do Azure. Após fazer o login basta clicar em **"Connect"**

![img54](/img/pbi08.png)

- Agora dentro do Azure Machine Learning Models, você deve selecionar o seu endpoint criado anteriormente

![img55](/img/pbi11.png)

- Nos campos sem dados você deve colocar um exemplo. Neste caso seria "Sim" no campo **"Saiu_da_empresa"** e no campo **"Num_empresas_trabalhou"** digite um número, no meu caso usei o "4"

![img56](/img/pbi11.png)

![img57](/img/pbi11-2.png)

- Em seguida é só clicar em **"OK"**

- Irá aparecer uma mensagem sobre Privacidade. Neste momento click em **"Continue"**

![img57](/img/pbi12.png)

- Em **"Privacy levels"** marque a opção **"Ignore Privacy Levels checks..."** e click em **"Save"**

![img58](/img/pbi13.png)

- Em **"Privacy levels"** marque a opção **"Ignore Privacy Levels checks..."** e click em **"Save"**