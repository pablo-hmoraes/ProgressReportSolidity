# Progress Report Solidity

# 1. Introdução
Solidity é a principal linguagem para escrever **Smart Contracts** na rede Ethereum. 

Smart Contracts são "acordos" digitais que são assinados e armazenados numa rede blockchain, onde são executados automaticamente quando os termos e condições do contrato são cumpridos.

Solidity é uma linguagem orientada a objetos e de alto nível de abstração. 

Solidity é executada sobre a **Ethereum Virtual Machine (EVM)**. A EVM é um ambiente virtual descentralizado que executa códigos ao longo de todos os nós da rede Ethereum. Os nós rodam a EVM para executar os smart contracts, usando **gas** para mensurar o esforço computacional exigido pelas operações daquele contrato.  

# 2. Solidity Básico
## 2.1 Contracts
Como foi dito acima, o Solidity é uma linguagem orientada a objetos. Porém, por se tratar de uma linguagem muito voltada ao desenvolvimento de smart contracts, os objetos em Solidity são basicamente contratos. 

Podemos definir um contrato em Solidity da seguinte forma:

```
//SPDX-License-Identifier: MIT

pragma solidity 0.8.13;

contract MyContract {
    string public myString = "Hello world";

    function updateOurString(string memory _myString) public {
        myString = _myString;
    }
}
```

Podemos ver que **contracts** são muito semelhantes às classes em linguagens orientadas à objetos. Os contratos possuem dados em formas de variáveis e funções que podem modificar essas variáveis. 

## 2.2 Tipos de Dados
Solidity possui tipagem estática, ou seja, devemos especificar qual é o tipo do dado que estamos declarando ou retornando em uma função. 

Solidity contempla os tipos de dados comuns em outas linguagens populares, como string, booleanos, etc. Porém, Solidity possui alguns outros tipos de dados não muito comuns e não possui suporte nativo para números de ponto flutuante (floats).

Em Solidity, podemos especificar o tamanho das variáveis de inteiro. 

```
//SPDX-License-Identifier: MIT

pragma solidity 0.8.14;

contract ExampleUint {
    uint256 public myUint; 

    uint8 public myUint8 = 250;

    int public myInt = -10;
}
```

A declaração dos inteiros — signed ou unsigned — pode variar de tamanho, escalando de 8 em 8 bytes (de 8 até 256). ``uint`` e ``ìnt`` são sinôminos de ``uint256`` e ``int256``, respectivamente.

Outro tipo de dado importante de destacar é o o **address**. O tipo address possui duas formas semelhantes:

- **adress:** Armazena um valor de 20 bytes (tamanho de um endereço Ethereum).
- **adress payable:** O mesmo que o address, mas também possui as variáveis de estado **transfer** e **send**.

## 2.3 View vs Pure Functions
Em Solidity podemos declarar funções com dois modificadores: 
- **View:** Uma função ``view`` é uma que lê as variáveis de estado do contrato, mas não consegue escrever sobre o estado. Um exemplo seria uma função getter.
- **Pure:** Uma função ``pure`` é uma que não lê e nem escreve sobre as variáveis de estado do contrato. Essas funções apenas conseguem acessar suas próprias variáveis e outras funções ``pure``.


Exemplos de como declarar cada uma das funções:
```
    function getMyStorageVariable() public view returns(uint) {
        return myStorageVariable;
    }

    function getAddition(uint a, uint b) public pure returns(uint) {
        return a+b;
    }
```

## 2.4 Constructor
O **constructor** é uma função especial que é chamada automaticamente durante o _deploy_ do smart contract e não pode mais ser chamada após isso. O construtor pode ser útil para inicializar as variáveis de estado do contrato durante seu _deploy_.

```
//SPDX-License-Identifier: MIT

pragma solidity 0.8.15;

contract ExampleConstructor {
    address public myAddress;

    constructor(address _someAddress) {
        myAddress = _someAddress;
    }
}
```

# 3. MetaMask
MetaMask é um software de **crypto-wallet**, ou seja, é utilizado para permitir a interação do usuário com a blockchain. A MetaMask te permite comprar, vender, e trocar ativos crypto na rede Ethereum.

Para utilizar a MetaMask, basta obter o plugin ou add-on no seu navegador e criar uma conta. Após criar a conta, a MetaMask irá te disponibilizar uma frase, chamada de **secret recovery phrase**. A secret phrase é composta por 12 palavras. Os seus fundos são conectados à essa frase e te permitem recuperá-los caso perca acesso à sua conta. Por isso, é muito importante que você guarde essa frase de maneira segura.


# 4. Solidity Intermediário
## 4.1 ``payable`` Modifier
Em Solidity podemos especificar que certa funcionalidade de um contrato irá exigir um pagamento de Eth. Fazemos isso utilizando o modificador ``payable`` na declaração de uma função. 

```
//SPDX-License-Identifier: MIT

pragma solidity 0.8.15;

contract SampleContract {
    string public myString = "Hello World";

    function updateString(string memory _newString) public payable {
        if(msg.value == 1 ether) {
            myString = _newString;
        } else {
            payable(msg.sender).transfer(msg.value);
        }
    }
}
```

O objeto ``msg`` é uma variável global que contém informações importantes sobre o smart contract e a blockchain. No código acima utilizamos esse objeto para verificar o valor de Eth enviado na transação e o endereço da conta que fez a transação.

## 4.2 Mappings
Solidity possui o tipo de dado ``mapping``. Podemos pensar nos ``mappings`` como tabelas hash, onde armazenamos os dados em pares chave-valor. A diferença entre eles é que em Solidity o valor da chave não é armazenada no mapping, mas sim o seu valor hash ``keccak256`` (um algoritmo de hasheamento).

Podemos declarar um mapping usando a seguinte sintaxe

``mapping(KeyType KeyName? => ValueType ValueName?) VariableName``

## 4.3 Structs
Solidity também contempla **structs**. Structs são utilizadas para agrupar variáveis que fazem sentido estarem juntas. Essa utilidade é bem parecida com a dos contracts, porém contracts custam **gas**, enquanto structs não. 

## 4.4 ABI Array
O **ABI (Application Binary Interface) Array** contém todas as funções, inputs, outputs e variáveis e seus tipos de um smart contract. 

O ABI fica armazenado em um arquivo JSON no projeto do seu smart contract. 

Exemplo de um ABI Array:

![abi](./images/abi.webp)

É importante entendermos o ABI Array pois iremos utilizá-lo nas funções da biblioteca **web3.js**.


# 5. WEB3.js


# 6. ERC20 Token

# NFT
- openzeppelin
- truffle
- hardhat
- foundry

# Account Abstraction

