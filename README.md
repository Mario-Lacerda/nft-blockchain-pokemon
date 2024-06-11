# Desafio Dio - **Crie o seu NFT de Pokémon com Blockchain**



### **Projeto completo para criar um NFT de Pokémon usando o Alteon LaunchPad:**



### **Pré-requisitos:**



- #### Carteira de criptomoedas compatível com a rede Polygon (por exemplo, MetaMask)

  

- #### Arquivo de mídia (imagem, GIF ou vídeo) que você deseja transformar em um NFT

  

### **Passos:**

1. **Instale o Opera Crypto Browser:** Acesse o site do Opera e baixe o Opera Crypto Browser.

   

2. **Crie uma carteira:** Se você ainda não tiver uma carteira de criptomoedas, crie uma usando o Opera Crypto Browser.

   

3. **Acesse o Alteon LaunchPad:** Clique no ícone do Opera Crypto Browser na barra lateral e selecione "Alteon LaunchPad".

   

4. **Conecte sua carteira:** Clique em "Conectar carteira" e selecione sua carteira de criptomoedas.

   

5. **Escolha a rede:** Selecione a rede Polygon no menu suspenso.

   

6. **Arraste e solte seu arquivo de mídia:** Arraste e solte o arquivo de mídia que você deseja transformar em um NFT na área designada.

   

7. **Defina os detalhes do NFT:** Insira um nome, descrição e preço para o seu NFT.

   

8. **Cunhe seu NFT:** Clique no botão "Cunhar NFT".

   

9. **Confirme a transação:** Sua carteira solicitará que você confirme a transação. Revise os detalhes e clique em "Confirmar".



### **Explicação do código:**

Este contrato inteligente define uma classe chamada `PokemonNFT` que herda da classe `ERC721` do OpenZeppelin. A classe `ERC721` fornece a funcionalidade básica para criar e gerenciar NFTs.

A função `mintNFT` é usada para cunhar um novo NFT. Ela recebe dois parâmetros: `recipient`, que é o endereço do destinatário do NFT, e `tokenURI`, que é o URI do token que aponta para os metadados do NFT (por exemplo, nome, descrição e imagem).

A função `mintNFT` primeiro incrementa o contador `_tokenIds` para gerar um novo ID de token exclusivo. Em seguida, chama a função `_mint` da classe `ERC721` para criar um novo NFT com o ID de token especificado e atribuí-lo ao destinatário.

Finalmente, a função `_setTokenURI` é chamada para definir o URI do token para o novo NFT.



### **Como usar o contrato inteligente:**



Para usar o contrato inteligente, você precisará implantá-lo na rede Polygon. Você pode fazer isso usando uma ferramenta como o Remix IDE.

Depois de implantar o contrato inteligente, você pode usar a função `mintNFT` para cunhar novos NFTs



O Alteon LaunchPad usa um contrato inteligente para cunhar NFTs na rede Polygon. O contrato inteligente é um programa que é executado na blockchain e define as regras para a criação e transferência de NFTs.

Quando você cunha um NFT usando o Alteon LaunchPad, o contrato inteligente cria um novo NFT e o atribui à sua carteira. O NFT é então armazenado na blockchain do Polygon, o que garante que ele seja imutável e verificável.



### **Código do contrato inteligente:**

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721Enumerable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract PokemonNFT is ERC721, ERC721Enumerable, Ownable {
    constructor() ERC721("PokemonNFT", "PNFT") {}

    // Função para criar um novo Pokémon NFT
    function mintPokemon(address to, uint256 tokenId) public onlyOwner {
        _mint(to, tokenId);
    }

    // Funções obrigatórias para sobrescrever devido ao ERC721Enumerable
    function _beforeTokenTransfer(address from, address to, uint256 tokenId)
        internal
        override(ERC721, ERC721Enumerable)
    {
        super._beforeTokenTransfer(from, to, tokenId);
    }

    function supportsInterface(bytes4 interfaceId)
        public
        view
        override(ERC721, ERC721Enumerable)
        returns (bool)
    {
        return super.supportsInterface(interfaceId);
    }
}   


pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract PokemonNFT is ERC721 {
    using Counters for Counters.Counter;

    Counters.Counter private _tokenIds;

    constructor() ERC721("PokemonNFT", "PKMN") {}

    function mintNFT(address recipient, string memory tokenURI) public returns (uint256) {
        _tokenIds.increment();

        uint256 newTokenId = _tokenIds.current();
        _mint(recipient, newTokenId);
        _setTokenURI(newTokenId, tokenURI);

        return newTokenId;
    }
}
```



### **Como usar o contrato inteligente:**



Para usar o contrato inteligente, você precisará implantá-lo na rede Polygon. Você pode fazer isso usando uma ferramenta como o Remix IDE.

Depois de implantar o contrato inteligente, você pode usar a função `mintNFT` para cunhar novos NFTs. Você precisará fornecer o endereço do destinatário e o URI do token como parâmetros para a função.



### **Exemplo de uso:**

O seguinte código mostra como usar o contrato inteligente para cunhar um novo NFT e atribuí-lo a uma carteira específica:


import web3

# Crie uma instância do Web3 para conectar-se à rede Polygon
web3 = web3.Web3(web3.HTTPProvider("https://polygon-rpc.com"))

# Crie uma instância do contrato inteligente
contract_address = "0x1234567890ABCDEF"
contract = web3.eth.contract(address=contract_address, abi=abi)

# Crie os parâmetros da transação
recipient_address = "0xABCDEF1234567890"
token_uri = "https://example.com/nft-metadata.json"

# Chame a função `mintNFT`
tx_hash = contract.functions.mintNFT(recipient_address, token_uri).transact()

# Aguarde a confirmação da transação
web3.eth.wait_for_transaction_receipt(tx_hash)
```



## **Conclusão:**



Este é um projeto completo para criar um NFT de Pokémon usando o Alteon LaunchPad. Você pode usar este projeto como base para criar seus próprios NFTs personalizados.
