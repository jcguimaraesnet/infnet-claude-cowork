<div align="center">

# 🎬 Demo — Claude Cowork

_Roteiro de demonstração com prompts reutilizáveis para automação de correção de avaliações no Moodle usando Claude Code._

</div>

---

## 📚 Sumário

- [Passo 1 — Renomear pastas](#passo-1--renomear-pastas)
- [Passo 1.1 — Criar skill de renomear](#passo-11--criar-skill-de-renomear)
- [Passo 2 — Descompactar arquivos](#passo-2--descompactar-arquivos)
- [Passo 2.1 — Criar skill de descompactar](#passo-21--criar-skill-de-descompactar)
- [Passo 3 — Criar relatório Excel](#passo-3--criar-relatório-excel)
- [Passo 3.1 — Criar skill de relatório](#passo-31--criar-skill-de-relatório)
- [Passos 1, 2 e 3 — Reutilizando skills](#passos-1-2-e-3--reutilizando-skills)
- [Passo 5 — Criar skill de correção de rubricas](#passo-5--criar-skill-de-correção-de-rubricas)
- [Passo 6 — Competência 1](#passo-6--competência-1)
- [Passo 7 — Competência 2](#passo-7--competência-2)
- [Passo 8 — Competência 3](#passo-8--competência-3)
- [Passo 9 — Competência 4](#passo-9--competência-4)
- [Passo 10 — Competência 5](#passo-10--competência-5)
- [🌐 Conector: Claude in Chrome](#-conector-claude-in-chrome)
- [🎁 Convite](#-convite)

---

## Passo 1 — Renomear pastas

> 📁 Renomeia pastas baixadas do Moodle, mantendo apenas o nome do aluno.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Você é um assistente especializado em renomear pastas em um sistema de arquivos.

# Contexto
Você trabalhará com uma estrutura de pastas que segue o padrão de nomenclatura para download de tarefas do Moodle.

Aqui está o caminho da pasta raiz onde você precisa trabalhar:
<pasta_raiz>
C:\Temp\Assessments
</pasta_raiz>

# Padrão de Nomenclatura Atual
Cada nome de pasta atualmente consiste em três partes nesta ordem:
1. Nome do aluno
2. Uma sequência de 6 números
3. O texto fixo "_assignsubmission_file_"

Por exemplo: "João Silva_123456_assignsubmission_file_"

# Sua Tarefa
Você precisa renomear todas as pastas no diretório raiz, removendo as partes 2 e 3 de cada nome de pasta, mantendo apenas o nome do aluno (parte 1).

Usando o exemplo acima, "João Silva_123456_assignsubmission_file_" se tornaria "João Silva".

# Instruções
Antes de realizar a operação de renomeação, use um rascunho para planejar sua abordagem:

<rascunho>
- Liste os passos que você seguirá
- Identifique como você analisará os nomes das pastas
- Planeje como você extrairá apenas a parte do nome do aluno
- Considere como você verificará se a operação foi bem-sucedida
</rascunho>

Após o planejamento, execute os seguintes passos:
1. Acesse o diretório raiz em C:\Temp\Assessments
2. Liste todas as pastas neste diretório
3. Para cada pasta, identifique e extraia apenas o nome do aluno (parte 1) removendo a sequência de 6 dígitos e o sufixo "_assignsubmission_file_"
4. Renomeie cada pasta para conter apenas o nome do aluno
5. Conte o número total de pastas que foram renomeadas com sucesso

# Verificação
Após concluir a operação de renomeação, verifique se:
- O número de pastas renomeadas é igual ao Número total de pastas existentes no diretório raiz
- Informe se houver alguma discrepância

# Formato de saída
Forneça as seguintes informações na sua resposta final:
- O número total de pastas que foram renomeadas
- Confirmação de que a verificação foi bem-sucedida (ou detalhes caso não tenha sido)

# Formate sua resposta como:
"[X] pastas renomeadas com sucesso. Verificação: [aprovada/reprovada com detalhes]"
````

</details>

---

## Passo 1.1 — Criar skill de renomear

> 🧩 Encapsula o passo anterior em uma skill reutilizável.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use /skill-creator para criar uma skill com o nome "infnet-moodle-renomear-pastas" sobre essa última conversa.
Crie essa skill sem rodar testes, indo diretamente para o empacotamento.
````

</details>

---

## Passo 2 — Descompactar arquivos

> 📦 Descompacta arquivos `.zip` e `.rar` dentro de cada subpasta de aluno.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Você é um assistente especializado em descompactar arquivos compactados em uma estrutura de pastas.

Aqui está o caminho da pasta raiz onde você precisa trabalhar:
<pasta_raiz>
C:\Temp\Assessments
</pasta_raiz>

# Contexto e Restrições
Você está trabalhando com uma estrutura de pastas onde:
- Cada subpasta contém exatamente um arquivo compactado
- Os arquivos compactados podem ser nos formatos .zip ou .rar
- Use a skill /rar-extractor para descompactar arquivos no formato .rar
- Os nomes dos arquivos não seguem uma convenção de nomenclatura padronizada
- Você precisa descompactar cada arquivo na mesma pasta onde ele está localizado

# Sua Tarefa
Você precisa:
1. Identificar todos os arquivos compactados (.zip e .rar) na estrutura de pastas abaixo da pasta raiz
2. Descompactar cada arquivo compactado em sua localização atual (a mesma pasta onde o arquivo compactado é encontrado)
3. Contar o número total de arquivos que foram descompactados com sucesso
4. Verificar se o número de arquivos descompactados corresponde ao número de arquivos compactados encontrados

# Instruções
Antes de começar a descompactar, use um rascunho para planejar sua abordagem:

<rascunho>
- Liste todas as pastas que você precisa verificar
- Identifique cada arquivo compactado e sua localização
- Planeje a ordem de descompactação
- Acompanhe seu progresso à medida que descompacta cada arquivo
</rascunho>

Em seguida, prossiga com a tarefa de descompactação. Para cada arquivo compactado:
1. Anote o caminho e o tipo do arquivo
2. Descompacte-o no mesmo diretório em que está localizado
3. Confirme a descompactação bem-sucedida
4. Mantenha uma contagem dos arquivos descompactados com sucesso

Após concluir todas as descompactações, verifique seu trabalho comparando:
- O número de arquivos compactados que você encontrou inicialmente
- O número de arquivos que você descompactou com sucesso

Esses números devem coincidir. Caso contrário, explique as discrepâncias.

# Formato de Saída
Forneça as seguintes informações na sua resposta final:
- Total de arquivos que foram descompactados com sucesso versus número de arquivos compactados encontrados
````

</details>

---

## Passo 2.1 — Criar skill de descompactar

> 🧩 Encapsula o passo de descompactação em uma skill.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use /skill-creator para criar uma skill com o nome "infnet-moodle-descompactar-arquivos" sobre essa última conversa.
Crie essa skill sem rodar testes, indo diretamente para o empacotamento.
````

</details>

---

## Passo 3 — Criar relatório Excel

> 📊 Cria `relatorio.xlsx` com uma aba por aluno e cabeçalhos padronizados.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Você é um assistente de correção de avaliações especializado na criação de relatórios de correção em formato Excel.

Aqui está o caminho da pasta raiz onde você precisa trabalhar:
<pasta_raiz>
C:\Temp\Assessments
</pasta_raiz>

# Contexto
Você está trabalhando com uma estrutura de pastas onde:
- A pasta raiz contém subpastas
- Cada subpasta representa o trabalho enviado por um aluno

# Sua Tarefa
Você precisa criar um arquivo Excel seguindo as especificações abaixo:

**Criação do Arquivo:**
1. Crie um arquivo Excel chamado "relatorio.xlsx" na pasta raiz (o caminho fornecido acima)

**Estrutura do Excel:**
2. Crie uma planilha (aba) no arquivo Excel para cada subpasta encontrada na pasta raiz
3. Nomeie cada planilha com o nome da subpasta correspondente (nome do aluno).
4 Trunque o nome da aba se for necessário (limite de 31 caracteres no excel)
5. Em cada planilha, crie exatamente 6 colunas com estes cabeçalhos nesta ordem:

- Coluna 1: "Competência"
- Coluna 2: "Rubrica"
- Coluna 3: "Não demonstrou o item da rubrica"
- Coluna 4: "Demonstrou o Item de rubrica"
- Coluna 5: "Parcial"
- Coluna 6: "Comentário"

**Verificação:**
5. Após criar o arquivo, verifique se o número de planilhas no arquivo Excel corresponde ao número de subpastas na pasta raiz.

# Processo
Antes de criar o arquivo, use seu rascunho para:
- Listar as subpastas encontradas no caminho da pasta raiz
- Planejar os nomes das planilhas
- Confirmar a estrutura antes da criação

Use este formato em seu rascunho:
<rascunho>
[Seus passos de planejamento e verificação aqui]
</rascunho>

# Formato de Saída
Após concluir a tarefa, forneça sua resposta considerando as regras abaixo:
- Se bem-sucedido: Uma mensagem de confirmação informando que o arquivo foi criado com sucesso, incluindo o número de planilhas criadas e seus nomes
- Se ocorreram erros: Uma descrição clara dos erros e por que o arquivo não pôde ser criado
````

</details>

---

## Passo 3.1 — Criar skill de relatório

> 🧩 Encapsula a criação do relatório Excel em uma skill.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use /skill-creator para criar uma skill com o nome "infnet-moodle-criar-relatorio" sobre essa última conversa.
Crie essa skill sem rodar testes, indo diretamente para o empacotamento.
````

</details>

---

## Passos 1, 2 e 3 — Reutilizando skills

> 🔁 Executa o pipeline completo usando as três skills criadas.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Realize os seguintes passos na pasta de trabalho:

1 - Renomeie as pastas usando a skill /infnet-moodle-renomear-pastas
2 - Descompacte os arquivos usando a skill /infnet-moodle-descompactar-arquivos
3 - Crie o relatório excel usando a skill /infnet-moodle-criar-relatorio
````

</details>

---

## Passo 5 — Criar skill de correção de rubricas

> 🎯 Skill principal: corrige trabalhos `.NET C#` por rubrica e atualiza o relatório.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use /skill-creator para criar uma skill chamada "infnet-moodle-corrigir-rubricas" com base no prompt base abaixo. Crie essa skill sem rodar testes, indo diretamente para o empacotamento.

Você é um assistente de correção de trabalhos para cursos de programação de graduação, especializado na linguagem .NET C#.

Aqui está o caminho da pasta raiz onde você precisa trabalhar:
<root_folder_path>
C:\Temp\Assessments
</root_folder_path>

# Contexto e Restrições
A estrutura de pastas está organizada da seguinte forma:
- Cada subpasta na raiz representa o trabalho de um aluno.
- Dentro da subpasta de cada aluno, há uma pasta descompactada contendo o trabalho do aluno.
- IGNORE quaisquer arquivos compactados (.zip ou .rar) nas subpastas dos alunos.
- O trabalho de cada aluno é dividido em exercícios, cada um em subpastas separadas.
- Os nomes das pastas de exercícios NÃO seguem um padrão rígido. Procure por pastas com nomes como: "Exec1", "Exercício 1", "Ex1", "Exercicio_1", "Exercicio 1", etc. Seja flexível ao lidar com essas variações.
- Há um único arquivo Excel na raiz da pasta de trabalho, que corresponde ao relatório de notas.
- O nome do relatório de notas pode ter variações, mas pode rementer a algo semelhante a "relatorio.xlsx"

# Tarefa
Sua tarefa consiste nos seguintes passos:

1 - Usar a ferramenta AskUserQuestion para perguntar ao usuário qual o nome da competência.
2 - Usar a ferramenta AskUserQuestion para perguntar ao usuário quais são as rubricas e seus critérios de correções
3 - Avaliar o trabalho de cada aluno e atualizar o relatório de notas

# Como proceder
Para cada aluno:
1. Identifique a pasta de cada aluno.
2. Localize a pasta de cada exercício conforme mencionado em cada critério de correção (lembre-se de ser flexível com variações de nomenclatura).
3. Avalie cada rubrica sistematicamente.

# Exemplos de rubricas e critérios de correção
<exemplo>
**Rubrica 1:**
- No exercício 1, verifique se a classe Program.cs contém um Console.WriteLine que imprime uma frase como "Olá, meu nome é [Nome do Aluno]".
**Rubrica 2:**
- No exercício 1, verifique se a classe Program.cs contém um Console.WriteLine que imprime uma frase como "Nasci em [data de nascimento] e estou aprendendo C#!".
**Rubrica 3:**
- Verifique no exercício 1, se a versão dotnet especificada no arquivo csproj é a versão 9 ou 10
**Rubrica 4:**
- Verifique no exercício 1, se na raiz do projeto, há uma imagem contendo a saída do programa?
- Verifique no exercício 1, se na raiz do projeto, há um arquivo README.md com referência a imagem?
</exemplo>

# Formato de Saída
Você deve atualizar o relatório Excel na pasta raiz em cada aba (por aluno), adicionando uma nova linha para cada rubrica, preenchendo as seguintes colunas:
- **Coluna Competência**: Preencha APENAS com o nome da competência informado pelo usuário
- **Coluna Rubrica**: Preencha com o texto relacionado a rubrica a ser corrigida
- **Coluna "Não demonstrou o item da rubrica"**: Preencha com o texto "Não" se o aluno NÃO demonstrou todos os itens da rubrica
- **Coluna "Demonstrou o item da rubrica"**: Preencha com o texto "Sim" se o aluno demonstrou completamente todos os itens da rubrica
- **Coluna "Parcial"**: Preencha com "Avaliar" para casos que poderiam ser considerados demonstrados com alguma ressalva
- **Coluna "Comentário"**: Se um item da rubrica não for demonstrado (ou for parcialmente demonstrado), explique objetivamente o motivo. Deixe esta coluna em branco para rubricas totalmente demonstradas.

# Diretrizes Adicionais
- Para cada linha no relatório, a nota final deve ser preenchida APENAS em UMA das três colunas: "Não demonstrou o item de rubrica", "demonstrou o item de rubrica" ​​ou "Parcial".
- Preencha a nota final apenas com as palavras "Sim", "Não" ou "Avaliar" conforme explicado no formato de saída
- Seja minucioso na busca por arquivos, pois as convenções de nomenclatura podem variar.
- Ao avaliar instruções Console.WriteLine, procure pelo padrão geral e pela intenção, não por correspondências exatas de texto.

# Verificação
1. Verifique se a coluna "Competência" no arquivo excel foi preenchida apenas com o nome da competencia informado pelo usuário para todos os alunos
2. Verifique se apenas uma das três colunas foi preenchida para todos os alunos: "Não demonstrou o item de rubrica", "demonstrou o item de rubrica" ​​ou "Parcial"
3. Verifique se a coluna "Comentário" foi preenchida apenas quando uma rubrica não foi demonstrada ou parcialmente demonstrada (colunas "Não demonstrou o item de rubrica" ou "Parcial")
````

</details>

---

## Passo 6 — Competência 1

> ✅ Avalia exercício 1: `Program.cs`, versão `.NET`, README com imagem.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use a skill /infnet-moodle-corrigir-rubricas

### Primeiro parâmetro (nome da competência)
Competência 1

### Segundo parâmetro (rubricas)

# Rubrica 1:
- No exercício 1, verifique se a classe Program.cs contém um Console.WriteLine que imprime uma frase como "Olá, meu nome é [Nome do Aluno]".
# Rubrica 2:
- No exercício 1, verifique se a classe Program.cs contém um Console.WriteLine que imprime uma frase como "Nasci em [data de nascimento] e estou aprendendo C#!".
# Rubrica 3:
- Verifique no exercício 1, se a versão dotnet especificada no arquivo csproj é a versão 9 ou 10
# Rubrica 4:
- Verifique no exercício 1, se na raiz do projeto, há uma imagem contendo a saída do programa.
- Verifique no exercício 1, se na raiz do projeto, há um arquivo README.md com referência a imagem.
````

</details>

---

## Passo 7 — Competência 2

> ✅ Avalia exercícios 2 a 5: cifragem, calculadora, datas e formatura.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use a skill /infnet-moodle-corrigir-rubricas

### Primeiro parâmetro (nome da competência)
Competência 2

### Segundo parâmetro (rubricas)

# Rubrica 1:
- No exercício 2, verifique se o programa recebe um nome completo e consegue deslocar cada letra duas posições para frente no alfabeto? Exemplo: Entrada: "Carlos Silva" e Saída: "Ectnquu Ukngxc"
- No exercício 2, verifique se o programa está ignorando espaços e acentos no deslocamento.
# Rubrica 2:
- No exercício 3, verifique se o programa deve receber dois números como operando e um número (de 1 a 4) que indique a operação (soma, subtração, multiplicação ou divisão), e depois calcular a operação e exibir o resultado.
- No exercício 3, verifique se o programa deve aceitar apenas números válidos como operandos. Letras, simbolos e qualquer outro caracter que não seja número não pode ser aceito como operando no programa.
- No exercício 3, verifique se o programa evita de alguma forma divisão por zero.
# Rubrica 3:
- No exercício 4, verifique se o programa recebe uma data de nascimento e calcula quantos dias faltam para o próximo aniversário (considerando a data atual).
- No exercício 4, verifique se o programa considera anos bissextos.
- No exercício 4, verifique se o programa exibe uma mensagem se estiver faltando menos de 7 dias para o aniversário (considerando a data atual).
# Rubrica 4:
- No exercício 5, verifique se o programa recebe uma data (atual) e compara com a data prevista de formatura definida manualmente no código, exibindo quanto tempo falta para a formatura.
- No exercício 5, verifique se o programa exibe a mensagem "A reta final chegou! Prepare-se para a formatura!" se falta menos de 6 meses para a formatura?
- No exercício 5, verifique se o programa exibe a mensagem "Parabéns! Você já deveria estar formado!" se a data de formatura já tiver passado (considerando a data atual)?
````

</details>

---

## Passo 8 — Competência 3

> ✅ Avalia exercício 6: classe `Aluno`, propriedades e encapsulamento.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use a skill /infnet-moodle-corrigir-rubricas

### Primeiro parâmetro (nome da competência)
Competência 3

### Segundo parâmetro (rubricas)
# Rubrica 1:
- No exercício 6, verifique se o programa faz referencia a uma classe Aluno.
# Rubrica 2:
- No exercício 6, verifique se o programa instancia a classe Aluno, e usa as propriedades Nome, Matrícula, Curso, e os  métodos parecido com "VerificarAprovacao()"  e "ExibirDados()".
# Rubrica 3:
- No exercício 6, verifique se o programa usa propriedades auto-implementada
# Rubrica 4:
- No exercício 6, verifique se o programa usa visibilidade private para campos internos
````

</details>

---

## Passo 9 — Competência 4

> ✅ Avalia exercícios 7 e 8: `ContaBancaria`, `Funcionario`, `Gerente` (herança).

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use a skill /infnet-moodle-corrigir-rubricas

### Primeiro parâmetro (nome da competência)
Competência 4

### Segundo parâmetro (rubricas)
# Rubrica 1:
- No exercício 7, verifique se o programa faz referencia a uma classe parecida com o nome "ContaBancaria"?
# Rubrica 2:
- No exercício 7, verifique se a classe parecida com o nome "ContaBancaria" tem alguma propriedade ou campo parecido com o nome "Saldo" com acessibilidade/visibilidade private?
- No exercício 7, verifique se o programa instancia a classe ContaBancaria, e usa três métodos parecidos com "Depositar(decimal valor)", "Sacar(decimal valor)" e ExibirSaldo()?
# Rubrica 3:
- No exercício 8, verifique se o programa faz referencia a uma classe parecida com o nome "Funcionario" e uma classe parecida com "Gerente"?
# Rubrica 4:
- No exercício 8, verifique se o programa instancia a classe Funcionario e a classe Gerente e exibe os salários do funcionario e do gerente?
- No exercício 8, verifique se a classe gerente calcula o salário com um bônus de 20% do salário?
````

</details>

---

## Passo 10 — Competência 5

> ✅ Avalia exercícios 9 a 12: coleções, arquivos, jogo de adivinhação, polimorfismo.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Use a skill /infnet-moodle-corrigir-rubricas

### Primeiro parâmetro (nome da competência)
Competência 5

### Segundo parâmetro (rubricas)
# Rubrica 1:
- No exercício 9, verifique se existe uma versão (a) usando array/coleção para armazenar os dados, e outra versão (b) armazenando os dados em arquivo.
- No exercício 9, verifique se o programa faz referencia a uma classe parecida com o nome "Produto"?
# Rubrica 2:
- No exercício 9, verifique se o programa instancia uma classe com nome parecido com "Produto", e usa métodos com nome parecido "Inserir" e "Listar"?
- No exercício 9, verifique se o programa tem alguma regra de que só pode ser inserido até 5 produtos?
# Rubrica 3:
- No exercício 10, verifique se o programa implementa um jogo de adivinhação de número de 1 a 50 com 5 tentativas?
- No exercício 10, verifique se o programa trata o cenário de quando o usuário informa um número fora do intervalo de 1 a 50?
# Rubrica 4:
- No exercício 11, verifique se o programa implementa um cadastro de contatos e persiste os dados em arquivo?
- No exercício 11, verifique se o programa oferece duas opções de menu parecidas com "adicionar contato" e "listar contato", além de uma opção de sair?
- No exercício 12, verifique se o programa oferece a possibilidade de visualizar dados de contato de tres formas (markdown, tabela, texto puro)?
- No exercício 12, verifique se o programa usa conceitos de herança e polimorfismo?
````

</details>

---

## 🌐 Conector: Claude in Chrome

> 🔗 Atualiza as notas diretamente no Moodle usando o conector do Chrome.

<details>
<summary><b>📋 Ver prompt</b></summary>

````markdown
Faça os seguintes passos para atualizar as notas do aluno "Arthur Costa Camacho Ferreira" no moodle:

1 - Navegue para o link do moodle referente ao aluno: https://lms.infnet.edu.br/moodle/mod/assign/view.php?id=463661&rownum=0&action=grader&userid=3992
2 - Localize a aba referente ao aluno no relatório excel de notas
3 - No relatório Excel de notas, considere apenas as três colunas: "Não demonstrou o item da rubrica",  "Demonstrou o Item de rubrica" e "Comentário".
4 - No link aberto (passo 1), selecione (clique) para cada rubrica se o aluno "Não demonstrou o item de rubrica" ou selecione (clique) "Demonstrou o item de rubrica", de acordo o relatório Excel de notas.
5 - Insira o comentário para cara rubrica conforme cada a coluna Comentário de cada linha no relatório excel de notas do aluno
6 - Cada linha do Excel de notas do aluno corresponde a uma rubrica no link da página, exatamente na mesma ordem (de cima para baixo).
````

</details>

---

## 🎁 Convite

> Uma semana grátis no uso do Claude Cowork:
>
> 🔗 [claude.ai/referral/pm26MvTT0Q](https://claude.ai/referral/pm26MvTT0Q?s=cowork&v=apps)

---

<div align="center">

_Demo preparada para o curso **Infnet — Claude Cowork**_ 🎓

</div>
