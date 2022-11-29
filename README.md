# Informações gerais

**Command substitution** - Permite que capturemos a saída de um comando. A sintaxe é a seguinte: `$(<COMMAND>)`

![Screenshot from 2022-11-26 19-52-53](https://user-images.githubusercontent.com/80921933/204111735-350f4dae-5e52-4ce0-b4d7-59d6df1fc96e.png)


**Tilde expansion**: <br>
`~` corresponde a home do usuário atual <br>
`~<nomeUsuario>` se refere à home do usuário \<nomeUsuario> <br>
`~+` se refere a variável ${PWD} <br>
`~-` se refere à ${OLDPWD} <br>

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

Ainda dentro da etapa, vale explicar que o **Word Splitting** se refere aos separadores que serão usados para aceitar argumentos. A variável de ambiente IFS armazena o valor dos separados usados por padrão, podendo ser acessados pelo comando `echo "${IFQ@Q}"`. **WORDPLITTING SÓ ACONTECE FORA DE DOUBLE-QUOTES!**

O **Globbing** se refere às expansões do tipo *.txt, data?.txt, etc...

**Etapa 4:** A etapa de **Quote removal** retira os quotings (', \, ") mais superficiais.

**Etapa 5:** A etapa de **Redirections** Executa os redirections.

# Input de usuário

Podemos referenciar os inputs passados pelo usuário em cada posição com **$\<POSICAO>** dentro do script. 

![Screenshot from 2022-11-28 21-14-38](https://user-images.githubusercontent.com/80921933/204407559-ffdaead3-a0df-4605-8a26-7744b98e66b7.png)

**Special parameters:**

Alguns parâmetros são reservados, como o $0 e $#

- O **$0** referencia o nome do script executado.
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


# Manipulando o valor de uma variável

![Screenshot from 2022-11-26 19-36-54](https://user-images.githubusercontent.com/80921933/204111529-50d2b0f3-4a65-4358-b599-a97883e5493c.png)

# Aritmética

**Arithmethic expansion** - Realiza operações aritméticas. Não consegue apresentar números decimais. Para tal fim, usamos o programa **bc**

![Screenshot from 2022-11-26 21-09-21](https://user-images.githubusercontent.com/80921933/204113603-6dfbcb60-7829-4f7d-b4b7-f4eb22d5890f.png)

Utilização do programa **bc**

![Screenshot from 2022-11-26 21-17-06](https://user-images.githubusercontent.com/80921933/204113758-ae6a1991-7914-4dbe-ba4d-bef53f9b8c20.png)

