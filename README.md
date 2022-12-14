**Manipulando options** <br>
[Options e input de usuário](#options-e-input-de-usuário) <br>

**Lógica** <br>
[Lógica e comparando Integers](#lógica-e-comparando-integers) <br>
[Lógica e comparando Strings](#lógica-e-comparando-strings) <br>
[Lógica e if statements](#lógica-e-if-statements) <br>
[Lógica e switch cases](#lógica-e-switch-cases) <br>

**Iterações, percorrer listas e linhas de arquivos** <br>
[While loops](#while-loops) <br>
[While loops com utilização de argumentos e getopts](#while-loops-com-utilização-de-argumentos-e-getopts) <br>
[While read para iterar por linhas de arquivos](#while-read-para-iterar-por-linhas-de-arquivos) <br>
[Arrays](#arrays) <br>
[Readarray](#readarray) <br>
[For](#for) <br>

**Etapas de verificação de um script pelo shell** <br>
[Interpretação de comandos pelo shell ao ler um script](#interpretação-de-comandos-pelo-shell-ao-ler-um-script) <br>

**Utilitários, manipulação de variáveis, aritmética** <br>
[Debugging com Shellcheck](#debugging-com-shellcheck) <br>
[Comando scp para envio de arquivos a um servidor remoto](#comando-scp-para-envio-de-arquivos-a-um-servidor-remoto) <br>
[Manipulando o valor de uma variável](#manipulando-o-valor-de-uma-variável) <br>
[Aritmética](#aritmética) <br>

# Options e input de usuário

Podemos referenciar os inputs passados pelo usuário em cada posição com **$\<POSICAO>** dentro do script. 

![Screenshot from 2022-11-28 21-14-38](https://user-images.githubusercontent.com/80921933/204407559-ffdaead3-a0df-4605-8a26-7744b98e66b7.png)

**Special parameters:**

Alguns parâmetros são reservados, como o $0 e $#

- O **$0** referencia o nome do script executado.
- O **$?** referencia a saída (0 ou 1) do último comando.
- O **$#** referencia a quantidade de parâmetros informados no input.

![Screenshot from 2022-11-28 21-25-40](https://user-images.githubusercontent.com/80921933/204408533-62b1dbab-106a-4d43-970e-3a933f83c1ab.png)

- O **$@** referencia todos os parâmetros informados

![Screenshot from 2022-11-28 21-45-55](https://user-images.githubusercontent.com/80921933/204410841-8ff4f2b7-fe06-4cb9-a13a-16d6573619cc.png)

Para ler um input, podemos utilizar o comando `read`, que por padrão, aguarda por um input de usuário e o armazena na variável ${REPLY}

![Screenshot from 2022-11-28 21-55-11](https://user-images.githubusercontent.com/80921933/204412141-4116bdf2-c12d-4e8f-8a73-207e7ca03ccf.png)

Alternativamente, o `read` pode ser usado para armazenar os inputs em diferentes variáveis

![Screenshot from 2022-11-28 21-54-18](https://user-images.githubusercontent.com/80921933/204412197-e7a1cafe-bb8d-4b91-b41a-b1d10adefdc5.png)

Também podemos escrever um texto antes do input com a flag -p "<PRE_INPUT_TEXT>", ex:

![Screenshot from 2022-11-28 22-03-50](https://user-images.githubusercontent.com/80921933/204412994-2b39c9a0-d5c6-4fa0-ae47-8cb8ba5cccb9.png)

Alternativamente ao comando `read`, podemos usar o `select`, que fornece opções personalizadas para que o usuário selecione. A variável de ambiente **PS3** indica a pergunta que será feita no `select`. Se ela não for informada, o que aparecerá será um **#!**

![Screenshot from 2022-11-28 23-03-00](https://user-images.githubusercontent.com/80921933/204420416-75785137-6c00-4b85-bc2f-b6a91a28a8bc.png)


# Lógica e comparando Integers

- O operador **;** permite que concatenemos múltiplos comandos em uma só linha. Os comandos rodam de forma sequencial, independentemente do resultado do comando anterior.

```
echo 123; echo 456; echo 789
```

- O operador **&** indica que o comando informado será rodado em background <br>
- O operador **&&** indica que o comando à direita do operador só rodará **SE O ANTERIOR FOI BEM SUCEDIDO (retornou 0)**

Exemplo onde o segundo comando rodará com sucesso:
```
echo 123 && echo 456
```

Exemplo onde o segundo comando **NÃO** rodará com sucesso:
```
ech 123 && echo 456
```

- O operador **||** indica que o comando à direita do operador só rodará **SE O ANTERIOR DEU ERRO (retornou != 0)**

A lógica no Shell Script é definida parcialmente por operadores, como:

**(SOMENTE PARA INTEGERS)**

**-eq** = equals <br>
**-ne** = not equals <br>
**-gt** = greater than <br>
**-lt** = less than <br>
**-geq** = greater than or equal to <br>
**-leq** = less than or equal to

Os números de true/false também se invertem no Shell Script, sendo eles:

**0** = FALSE <br>
**1** = TRUE

Sendo assim, podemos definir lógica com o operador **[ \<LÓGICA_AQUI> ]**.

Também podemos referenciar a saída do nosso condicional com o operador **$?**

Exemplos:

![Screenshot from 2022-12-05 16-13-16](https://user-images.githubusercontent.com/80921933/205723020-e00e481b-a1b3-4aae-bf1e-d2c652b58173.png)


# Lógica e comparando Strings

**=** verifica se duas Strings são iguais <br>
**!=** verifica se duas String são diferentes

![Screenshot from 2022-12-05 16-27-24](https://user-images.githubusercontent.com/80921933/205725543-33af80e2-8900-41b3-8656-70ac5a27e800.png)


**-z** verifica se uma String é vazia

![image](https://user-images.githubusercontent.com/80921933/205725671-316916be-a024-47d1-90e2-5be333aa0097.png)

**-e** verifica se um arquivo existe

![Screenshot from 2022-12-05 16-29-45](https://user-images.githubusercontent.com/80921933/205726059-9fa21149-067a-439e-9ce6-65898a172dce.png)

**-f** verifica se o arquivo existe e se é um arquivo <br>
**-d** verifica se o arquivo é existe e é um diretório
 
![Screenshot from 2022-12-05 16-31-37](https://user-images.githubusercontent.com/80921933/205726212-ffd01e8a-e241-4f68-9461-770fa76518bc.png)

**-x** verifica se um arquivo é executável

![Screenshot from 2022-12-05 16-32-34](https://user-images.githubusercontent.com/80921933/205726703-c95b4cab-da52-4706-b15c-1cd4b6aa33e1.png)


# Lógica e if statements

![Screenshot from 2022-12-05 16-47-54](https://user-images.githubusercontent.com/80921933/205729490-250dd515-9a78-474d-93c8-1d1347010247.png)

![Screenshot from 2022-12-05 18-14-59](https://user-images.githubusercontent.com/80921933/205744230-699b6809-af12-4a34-a1e4-6a325904d3e3.png)


# Lógica e switch cases

(É possível utilizar um pipe (**|**) dentro do switch-case para especificar que pode ser um valor **OU** outro)

![Screenshot from 2022-12-05 18-25-04](https://user-images.githubusercontent.com/80921933/205745750-2e7b2820-1a5c-4025-81a1-bc8a49323760.png)


# While loops

![Screenshot from 2022-12-06 00-14-04](https://user-images.githubusercontent.com/80921933/205804135-02cd28de-2795-4a01-a0d9-9f3cc898fedb.png)


# While loops com utilização de argumentos e getopts

O **getopts** é utilizado para pegar os options informados para o comando. A cada vez que ele roda, ele pega o próximo option informado. O parâmetro (key) é armazenado na variável que vem após o comando (nos exemplos abaixo, na variável opt).

Exemplo da utilização em um comando que recebe dois parâmetros, **a** e **b**

```
getopts "ab" opt
```

Para informar que os options podem receber argumentos, inserimos um **:** em sua frente.

```
getopts "a:b:" opt
```

Caso tenhamos inserido a opção de passar argumentos para os options (o operador **:** dentro do **getopts**), podemos usar a variável **$OPTARG** para referenciar cada argumento, dentro de um while que percorre os options. 

![Screenshot from 2022-12-06 12-38-11](https://user-images.githubusercontent.com/80921933/205956627-442ef86e-ceab-4046-b652-b3581f63e6f9.png)


# While read para iterar por linhas de arquivos

Até esse momento, ainda não entendi o motivo do redirect do **$1**, mas basicamente serve para passarmos um arquivo como parâmetro para que o script possa lê-lo.

![Screenshot from 2022-12-07 09-09-02](https://user-images.githubusercontent.com/80921933/206175819-ce022edf-33e7-4700-9787-f9f8c404fbd5.png)


# Arrays

As arrays podem ser criadas da seguinte forma, com seus elementos separados por espaço

![image](https://user-images.githubusercontent.com/80921933/206219095-dc669660-1491-4e7e-91d2-d35008ea8414.png)

Podemos printar um elemento de um array da seguinte forma

![image](https://user-images.githubusercontent.com/80921933/206219634-67e13dfb-1739-49e5-96ce-47cf0d559936.png)

Podemos printar todos os elementos de um array com o operador **@**, e manipular da mesma forma que manipulamos strings

![image](https://user-images.githubusercontent.com/80921933/206220423-c5ee5791-aec4-4d7e-9d72-80f939d80d87.png)

Podemos adicionar elementos ao array com o operador **+=**

![image](https://user-images.githubusercontent.com/80921933/206221292-91d108da-ba89-4db5-8300-3539af34f16b.png) <br>
![image](https://user-images.githubusercontent.com/80921933/206220998-ee055838-f3d9-4e16-a426-962a276a9c81.png)

Podemos remover elementos de um array com o comando unset \<NOME_ARRAY>[\<POSICAO>]

![Screenshot from 2022-12-07 13-10-14](https://user-images.githubusercontent.com/80921933/206230978-fa21c35f-9f00-4637-b26b-acb380d71b7b.png)

Para substituir valores, usamos o operador de atribuição **=**

![image](https://user-images.githubusercontent.com/80921933/206232072-3a512afd-9d6e-4c76-ad82-c24dbb93b34c.png)

Para printar o index de um elemento, usamos o operador **!**

![image](https://user-images.githubusercontent.com/80921933/206232542-258d2b70-8258-48bc-81bc-8dce86ba2452.png)

# Readarray

O comando readarray serve para criarmos um array a partir de conteúdos oriundos de outra fonte, como um arquivo, ou um comando.

Deve ser sempre usado com a flag **-t** para evitar que os itens do array seja criado com caracteres especiais, como mostra a imagem abaixo

![image](https://user-images.githubusercontent.com/80921933/206235103-4aa62149-87fa-4700-9713-3dad3faf7455.png)

Para criar um array a partir de um comando, devemos usar o **process substitution** - \<(<COMANDO_AQUI>) para encapsular o comando, e o operador **<** para redirecionar o stdout do comando para o stdin do readarray. Segue um exemplo da criação de array a partir do comando **cat**

![image](https://user-images.githubusercontent.com/80921933/206237405-1cee1568-e424-4d3a-a7f0-ef85a1902c88.png)

# For

O for pode ser utilizado principalmente com arrays. 

Supondo que temos a seguinte lista

![image](https://user-images.githubusercontent.com/80921933/206256500-127f3481-34a1-4e7e-b401-9433af994ffa.png)

A execução do seguinte script

![image](https://user-images.githubusercontent.com/80921933/206256669-ec2cff44-a529-4426-95cf-d2d0aa5c1ed9.png)

Resultará nisso

![image](https://user-images.githubusercontent.com/80921933/206257764-c78ccfb0-ac1d-4846-a0f1-4d145d2509c4.png)

# Debugging com Shellcheck

Shellcheck é um programa que pode ser usado para encontrar erros nos scripts.

Para instalá-lo, basta rodar

```
sudo apt install shellcheck
```

Sua sintaxe para verificação se scripts é 

```
shellcheck <SCRIPT_AQUI>
```

# Comando scp para envio de arquivos a um servidor remoto

Sintaxe geral do comando: **scp -i \<CHAVE> \<SOURCE> \<DESTINATION>**

**Enviando arquivos:**

```
scp -i <CHAVE> <ARQUIVO> <USER>@<IP>:<DIR_TO_STORE>
```

![image](https://user-images.githubusercontent.com/80921933/206583952-bfaa1e32-3c96-4d11-b127-57fdc537dcee.png)

**Recebendo arquivos:**

Basta inverter o comando acima...

```
scp -i <CHAVE> <USER>@<IP>:<DIR_TO_GATHER_FILE_FROM> <ARQUIVO>
```

# Interpretação de comandos pelo shell ao ler um script

**Quoting** 

Os single-quotes (') preservam o sentido literal de tudo. <br>
Os double-quotes (") aceitam caracteres especiais, como ${<ENV_VARIABLE>}. <br>
Os backslashes (\) escapam um caracter especial. <br>

**Interpretação de comandos**

O shell interpreta os comandos com os 5 seguintes passos:

- **Tokenisation**
- **Command identification**
- **Shell expansions**
- **Quote removal**
- **Redirections**

**Etapa 1:** A etapa de **Tokenisation** consiste em separar **Words** de **Operators**.

![Screenshot from 2022-11-28 18-23-33](https://user-images.githubusercontent.com/80921933/204384005-27864c1e-f418-4bb7-9e49-0fd30e9edac6.png)

**Etapa 2:** A etapa de **Command identification** visa identificar os comandos na String em questão. Os comandos são limitados por um **Control Operator**, podendo ser |, ||, ;, ;;, &, Newline, etc... Redirections **NÃO SÃO CONTROL OPERATORS.** Eles ainda são tratados como parte do comando.

![Screenshot from 2022-11-28 18-52-32](https://user-images.githubusercontent.com/80921933/204389187-7c146da6-72c2-4991-9d0c-f01d84243f59.png)

**Etapa 3:** A etapa de **Shell expansions** consiste em aplicar as expansions, que acontecem em uma ordem pré-definida. Segundo a imagem abaixo, um **parameter expansion** nunca poderá estar dentro de um **brace expansion**, já que os **brace expansions** acontecem primeiro. A ordem de expansions acontece da esquerda para a direita, porém, respeita a hierarquia abaixo:

![Screenshot from 2022-11-28 18-59-26](https://user-images.githubusercontent.com/80921933/204389884-58c38f7b-7688-417a-aabc-7b379dfa25f4.png)

Ainda dentro da etapa, vale explicar que o **Word Splitting** se refere aos separadores que serão usados para aceitar argumentos. A variável de ambiente IFS armazena o valor dos separados usados por padrão, podendo ser acessados pelo comando `echo "${IFS@Q}"`. **WORDPLITTING SÓ ACONTECE FORA DE DOUBLE-QUOTES!**

O **Globbing** se refere às expansões do tipo *.txt, data?.txt, etc...

**Etapa 4:** A etapa de **Quote removal** retira os quotings (', \, ") mais superficiais.

**Etapa 5:** A etapa de **Redirections** Executa os redirections.


# Manipulando o valor de uma variável

![Screenshot from 2022-11-26 19-36-54](https://user-images.githubusercontent.com/80921933/204111529-50d2b0f3-4a65-4358-b599-a97883e5493c.png)


# Aritmética

**Arithmethic expansion** - Realiza operações aritméticas. Não consegue apresentar números decimais. Para tal fim, usamos o programa **bc**

![Screenshot from 2022-11-26 21-09-21](https://user-images.githubusercontent.com/80921933/204113603-6dfbcb60-7829-4f7d-b4b7-f4eb22d5890f.png)

Utilização do programa **bc**

![Screenshot from 2022-11-26 21-17-06](https://user-images.githubusercontent.com/80921933/204113758-ae6a1991-7914-4dbe-ba4d-bef53f9b8c20.png)

