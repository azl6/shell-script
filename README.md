# Informações gerais

**Command substitution** - Permite que capturemos a saída de um comando. A sintaxe é a seguinte: `$(<COMMAND>)`

![Screenshot from 2022-11-26 19-52-53](https://user-images.githubusercontent.com/80921933/204111735-350f4dae-5e52-4ce0-b4d7-59d6df1fc96e.png)


**Tilde expansion**: <br>
`~` corresponde a home do usuário atual <br>
`~<nomeUsuario>` se refere à home do usuário \<nomeUsuario> <br>
`~+` se refere a variável ${PWD} <br>
`~-` se refere à ${OLDPWD} <br>

# Processos executados pelo shell ao ler um script

**Quoting** 

Os single-quotes (') preservam o sentido literal de tudo. <br>
Os double-quotes (") aceitam caracteres especiais, como ${<ENV_VARIABLE>}. <br>
Os backslashes (\) escapam um caracter especial. <br>

![Screenshot from 2022-11-28 12-23-46](https://user-images.githubusercontent.com/80921933/204315763-cda03a14-f4d6-401f-ae36-a5f185ead7bf.png)

# Manipulando o valor de uma variável

![Screenshot from 2022-11-26 19-36-54](https://user-images.githubusercontent.com/80921933/204111529-50d2b0f3-4a65-4358-b599-a97883e5493c.png)

# Aritmética

**Arithmethic expansion** - Realiza operações aritméticas. Não consegue apresentar números decimais. Para tal fim, usamos o programa **bc**

![Screenshot from 2022-11-26 21-09-21](https://user-images.githubusercontent.com/80921933/204113603-6dfbcb60-7829-4f7d-b4b7-f4eb22d5890f.png)

Utilização do programa **bc**

![Screenshot from 2022-11-26 21-17-06](https://user-images.githubusercontent.com/80921933/204113758-ae6a1991-7914-4dbe-ba4d-bef53f9b8c20.png)

