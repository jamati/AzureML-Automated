# Workshop Azure Machine Learning Automated 
Este workshop contém instruções sobre como criar seu primeiro experimento utilizando o Azure Machine Learning Designer

## Praparar o ambiente ##

> 1. Crie sua conta gratuita no Azure

Basta seguir o passo a passo do link abaixo. Obs: Utilize um email para criar sua conta Microsoft que nunca tenha utilizado para trial do Azure anteriormente.
Link: https://azure.microsoft.com/pt-br/free/
___
   
>  iar um Resource Group

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
- Region: Selecione uma região onde será feito o deployment do seu workspace. Recomendo East US p questões de custos.
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

Click em **"Automated ML (preview)"** e então click no sinal de + conforme imagens abaixo:

![img13](/img/automated01.png)
___

> 2. Criar seu dataset

- Click em **"Create dataset"** e em seguida selecione **"From datastore"**

![img15](/img/dataset01.png)

- Agora no janela que se abriu siga os as configurações abaixo:

    - Digite um nome para o seu dataset
    - Digite uma descrição para o seu dataset
    - Em seguida click em **"Next"**

    ![img16](/img/dataset02.png)

    - Em **'Datastore selection'** siga as configurações abaixo:

        - Digite um nome para seu datastore
        - Deixe selecionado **"Azure Blob Storage"**
        - Deixe selecionado **"From Azure subscription"**
        - Deixe selecionado sua subscription
        - Selecionar o Storage Account que foi criado anteriormente
        - Selecionar o Container que você criou
        - Deixe selecionado a opção **"No"**
        - Deixe selecionado **"Account Key"**
        - Em Account Key você deve colar a Key copiada na etapa 5 do "Preparar seu ambiente"
        - Click em **'Create datastore'**

        ![img17](/img/dataset03.png)

        - Agora click em **'Browser'** e selecione o arquivo que você havia feito upload

        ![img18](/img/dataset03.png)

        ![img19](/img/dataset04.png)

        - Click em **'Next'**

        ![img20](/img/dataset05.png)
        ___

        >2. 1 - Configurar seus dados

        - No campo **'Column headers'** selecione **'Use headers from the first file'** e em seguida click em **"Next"**

        ![img21](/img/dataset06.png)
        ___

        > 2. 2 - Vamos configurar o esquema dos dados
        
        - Você precisa configurar colunas com o tipo correto de dados. **'String'** para colunas que contêm palavras e **'Integer'** para as colunas que contêm números
        
        - **'String'** para as colunas (Saiu_da_empresa,Viagens,Departamento,Area_de_formacao,Genero,Cargo,Estado_Civel)
        
        - **'Integer'** para as colunas (Idade, Distancia_de_casa, Educacao, ID_funcionario, Nivel_posicao, Renda_mensal, Num_empresas_trabalhou, Aumento_salarial_ultimo_ano_em_%, Nivel_opcao_acoes, Experiencia_anos, Qtd_treinamento_ultimo_ano, Anos_na_empresa, Anos_da_ultima_promocao, Anos_com_mesmo_Gerente)

        - Em seguida click em **'Next'**

        ![img22](/img/dataset07.png)
        ___

        > 2. 3 - Confirmar os detalhes

        - Aqui basta confirmar as informações e click em **'Create'** 

        ![img23](/img/dataset08.png)
        ___

> 3. Selecionar o dataset

- Agora que você já criou seu dataset selecione ele e click em **'Next'**

![img24](/img/selectdataset01.png)
___

> 4. Configurar seu experimento

- Para rodar seu experimento, primeiro você precisa configurar um cluster para processar seus modelos

    - Click em **'Create a new computer'**
    - Digite um nome para seu cluster. Ex.: hr-automl
    - No campo **'Virtual Machine type'** deixe selecionado **'CPU'**
    - No campo **'Virtual Machine priority'** deixe selecionado **'Dedicated'**
    - No campo **'Virtual Machine size'** deixe selecionado **'Standard_DS3_v2'**
    - No campo **'Minimum number of nodes'** deixe **'0'**
    - No campo **'Maximum number of nodes'** deixe **'4'**
    - No campo **'Idle seconds before scale down'** deixe em **'120'**
    - Click em **'Create'**

    ![img25](/img/newcluster01.png)

- Agora que seu cluster foi criado, click em **'Create new'**
- Digite um nome para seu experimento. Ex.: hr-automl
- Em **'Target column'** você deve selecionar a coluna que deseja prever os valores. No nosso caso selecione **'Saiu_da_empresa'**
- Em **'Select computer cluster'** selecione o cluster que criou na etapa anterior
- Click em **'Next'**

![img26](/img/experimento01.png)
___

> 5. Selecione qual tipo de problema quer resolver

- Aqui você deve entender qual tipo de problema precisa resolver. Algoritmos de Classificação são usado para responder "Sim ou Não", "Grupo A ou Grupo B", etc. Já os algoritmos de Regressão deve ser utilizado quando você busca um valor númerico "valor de um carro" baseado em algumas caracteristicas. Já nos algoritmos de Time series forecasting você utiliza para tentar prever o resultado de vendas baseado nos dados de vendas do passado. No nosso experimento vamos utilizar **'Classification'** 

![img27](/img/algoritmo01.png)

- Agora click em **'View featurization settings'**

    - Aqui você pode remover alguma coluna (feature), alterar o tipo de dados ou mesmo adicionar dados nos campos que estão sem dados.
    - Click em **'Save'**

    ![img28](/img/featurization01.png)

- Click em **'Finish'**

![img29](/img/algoritmo02.png)





    




___

## Agora vamos consumir nosso modelo no PBI ##

> 1. Primeiro passo é baixar o Power BI Desktop

- Baixe pelo link: https://www.microsoft.com/pt-br/download/details.aspx?id=58494

- Instale o Power BI seguindo as opções default. Após a instalação abra o mesmo

![img47](/img/pbi01.png) 
___ 

>  ora vamos importar uma amostra para o Power BI

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

![img57](/img/pbi11-p)

- Em seguida é só clicar em **"OK"**

- Irá aparecer uma mensagem sobre Privacidade. Neste momento click em **"Continue"**

![img57](/img/pbi12.png)

- Em **"Privacy levels"** marque a opção **"Ignore Privacy Levels checks..."** e click em **"Save"**

![img58](/img/pbi13.png)

- Em **"Privacy levels"** marque a opção **"Ignore Privacy Levels checks..."** e click em **"Save"**