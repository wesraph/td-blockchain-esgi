# Devoir maison

À rendre au format PDF à l'adresse: westphal.raphael@gmail.com\
Le sujet du mail doit respecter le format suivant: [Nom du groupe] Devoir maison cryptomonnaies.\
Police d'écriture de taille 11. \
Le mail doit inclure les réponses aux questions ainsi que le code final commenté au format zip. Un lien github est également accepté.

Pour rappel, si vous avez besoin de BNBs de test supplémentaire vous pouvez utiliser le faucet officiel: https://testnet.binance.org/faucet-smart/

### Première partie: Créer, déployer et modifer un ERC-20
Dans le même répertoire que le TD précèdent, créer un nouveau contrat "ERC20.sol" et le fichier de test associé.

Pour rappel un ERC-20 doit implémenter les fonctions suivantes:

```solidity
function name() public view returns (string)
function symbol() public view returns (string)
function decimals() public view returns (uint8)
function totalSupply() public view returns (uint256)
function balanceOf(address _owner) public view returns (uint256 balance)
function transfer(address _to, uint256 _value) public returns (bool success)
function approve(address _spender, uint256 _value) public returns (bool success)
function transferFrom(address _from, address _to, uint256 _value) public returns (bool success)
function allowance(address _owner, address _spender) public view returns (uint256 remaining)
```

ainsi qu'émettre les évènements suivants:
```
event Transfer(address indexed _from, address indexed _to, uint256 _value)
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```

### Description des fonctions
##### ``function name() public view returns (string)``
Retourne le nom du token. C'est le nom qui sera affiché sur les explorers.
##### ``function symbol() public view returns (string)``
La fonction `symbol()` doit retourner le symbole du token. Généralement il est composé de trois caractères en majuscule mais il est courant d'en voir quatre ou cinq. Exemple: BNB, ETH, XIV, XRP ...
##### ``function decimals() public view returns (uint8)``
La fonction `decimals()` est optionnelle mais fortement recommandée. Elle indique le nombre de décimales après la virgule maximal accepté. La valeur la plus commune est 19. La plus petite valeur échangeable de votre token sera alors de 0.0000000000000000001 token.
##### ``function totalSupply() public view returns (uint256)``
Indique le nombre total de tokens existants. Sa valeur varie au cours du temps.
##### ``function balanceOf(address _owner) public view returns (uint256 balance)``
Retourne la balance de l'adresse indiquée (le nombre de tokens en sa possession).
##### ``function transfer(address _to, uint256 _value) public returns (bool success)``
Transfère ``value`` tokens du compte de l'appelant vers le compte de ``_to``
##### ``function approve(address _spender, uint256 _value) public returns (bool success)``
Autorise ``_spender`` à dépenser ``_value`` tokens de celui qui appelle la fonction
##### ``function transferFrom(address _from, address _to, uint256 _value) public returns (bool success)``
Transfert ``_value`` tokens de ``_from`` vers ``_to``. Pour que le transfert soit possible, ``_from`` doit avoir approuvé (avec ``approve``) l'adresse effectuant la transaction
##### ``function allowance(address _owner, address _spender) public view returns (uint256 remaining)``
Retourne combien ``_spender``  peut dépenser de tokens de ``_owner`` (précedemment autorisé via ``approve``)


### Première partie: Création et déploiement d'un ERC-20
#### Exercice 1: Déploiement local
Dans cet exercice vous allez créer votre propre token.

Dans le répertoire de forge, copier le ficher ERC-20.sol dans le dossier src/. Le fichier ERC-20 est disponible sur le github à l'adresse https://github.com/wesraph/td-blockchain-esgi/tree/td-03-creer-un-erc20/ERC20.sol

Modifier les variables "name" et "symbol" par la valeur de votre choix.

##### Question 1:
Que fait la fonction `function mint(uint amount) internal` ?

##### Question 2:
Écrire le test nécessaire pour déployer le contrat (dans forge) et afficher la balance de l'utilisateur. Pour rappel, dans l'environnement de test l'adresse de l'utilisateur est à `msg.sender`

Écrire un test effectuant un transfer de 20 tokens vers l'adresse ``0x0000000000000000000000000000000000001000``

#### Exercice 2: Déploiement sur le testnet BSC
Dans cet exercice nous allons reprendre le token précedemment créé en local et allons le déployer sur le testnet de Binance Smart Chain.

Forge permet d'automatiser le procédé en utilisant une seul ligne de commande:
``forge create --rpc-url https://data-seed-prebsc-1-s1.binance.org:8545/  --private-key VOTRE_CLE_PRIVÉE src/ERC20.sol:ERC20``

Pour obtenir votre clé privée (utilisée pour signer la transaction), suivre la méthode suivante:
https://raw.githubusercontent.com/wesraph/td-blockchain-esgi/td-03-creer-un-erc20/privatekey.mp4

La sortie de la commande doit ressembler au message suivant:
```
[⠒] Compiling...
No files changed, compilation skipped
Deployer: 0xBe32De7f285f3b5F464a483BF3B26C35cC796996
Deployed to: 0xD0C0e9912dE93E16044320A5cb724bd7d2F62411
Transaction hash: 0x957d32d1469c0ee47e4fbd61e157840db8d545822ddc54ee467f1609354dcf8b
```

Attention, il faut que vous disposiez de BNBs de test sur votre adresse !

Sur le site https://testnet.bscscan.com/, entrer l'adresse du "Deployed to" dans la barre de recherche.

![Page token](token.png)

##### Question 1:
À quoi correspondent "Deployed to", "Deployer" et "Transaction hash" ?


En allant sur la page associée à votre adresse, en cliquant sur le menu déroulant des tokens possédés vous devriez voir 10000 de vos tokens.

<p align="center">
  <img src="account.png" alt="alternative_text" width="400"/>
</p>

Afin de pouvoir utiliser vos tokens, il est nécessaire de les ajouter dans Metamask.

https://github.com/wesraph/td-blockchain-esgi/assets/16212249/7f6dca3b-bf38-440f-8d40-87e8c051783e

##### Question 2:
En utilisant Metamask, envoyer 1 token à l'adresse ``0x6C750e594ef9A17351a9D3aF8341b59Cc9ed6d9c``.
Inclure le hash de la transaction dans le rapport.

#### Exercice 3: Ajouter un token en liquidité
Pour cet exercice, votre but sera d'obtenir un token d'au moins 5 groupes différent. Pour cela deux solutions sont acceptées:
 - Vous coordonner avec les autres groupes pour faire un échange de tokens.
 - Utiliser PancakeSwap pour "acheter" le token des autres groupes.

Peu importe la solution utilisée, les questions suivantes restent *obligatoires* et sont à répondre dans le rapport.

PancakeSwap est un "fork" d'Uniswap (voir cours) disponible sur le testnet de Binance Smart Chain. Pour rappel, il permet l'échange de cryptomonnaies entre utilisateurs. Dans cet exercice vous allez mettre en vente votre token.

##### Question 1:
Se rentre à l'adresse suivante: ``https://pancakeswap.finance/swap?chain=bscTestnet``

Cliquer sur le bouton de connexion "Connect wallet" en haut à droite. \
Aller dans la section "Liquidity", puis cliquer sur "Add liquidity".

Nous devons choisir ici quels tokens nous souhaitons mettre en liquidité. Dans notre cas, nous voulons utiliser tBNB ainsi que le token que vous venez de créer. Cliquer sur "CAKE" (le token que l'on veut remplacer) et sélectionner votre token. Votre token ne sera pas disponible dans la barre de recherche, il faut le forcer en entrant directement son adresse puis en cliquant sur "Import".

<p align="center">
  <img src="liquidity.png" alt="alternative_text" width="800"/>
</p>

Sélectionner "Add v2 liquidity".

Vous pouvez maintenant choisir le montant de tokens que vous voulez vendre. Comme vu dans le cours, le "ratio" entre tBNB et votre token va en définir son prix.

Pour l'exemple, nous mettrons les valeurs 0,02 et 300.

<p align="center">
  <img src="liquidity2.png" alt="alternative_text" width="500"/>
</p>

Finalement, cliquer sur Enable, puis sur Add.
Inclure le hash de la transaction dans le rapport.

##### Question 2:
À quel prix (en tBNB) avez vous mis votre token en vente ?

##### Question 3:
En utilisant la fonction "swap" de PancakeSwap, acheter 1 de votre propre token.
<p align="center">
  <img src="swap.png" alt="alternative_text" width="200"/>
</p>
Inclure le hash de la transaction dans le rapport.

Suivant l'avancement des autres groupes sur le projet, vous devriez voir leurs tokens à l'adresse `0x6C750e594ef9A17351a9D3aF8341b59Cc9ed6d9c`. Afin d'obtenir les tokens nécessaires à la completion de cet exercice il est possible d'obtenir leur adresse (pour les acheter sur PancakeSwap) en cliquant dessus.

## Deuxième partie: rapport de recherches

Dans une seconde partie (de minimum deux pages et maximum quatre pages), écrire une analyse sur un des sujets suivant:

- MEV (Miner Extractable Value): Définir ce qu'est le MEV, ses avantages et ses inconvénients. Vous pourrez vous appuyer sur l'exemple du "sandwiching" et de la liquidation.

- Les cryptomonnaies et l'environnement: Analysez l'impact environnemental de l'exploitation des cryptomonnaies, notamment l'utilisation intensive d'énergie.

- La régulation des cryptomonnaies: Quel est le statut juridique des cryptomonnaies dans différents pays ? Quels sont les défis à réguler ces nouvelles formes de monnaie ?

- Le rôle des cryptomonnaies dans les pays en développement: Certaines économies en développement utilisent et acceptent les cryptomonnaies plus rapidement que les pays développés. Pourquoi cela se produit-il et quel est l'impact sur l'économie locale ?

- Le Lightning Network et l'évolutivité de Bitcoin: Décrire ce qu'est le Lightning Network et comment il résout les problèmes d'évolutivité de Bitcoin

- La blockchain dans la chaîne d'approvisionnement: Comment la blockchain peut-elle améliorer la traçabilité et l'efficacité dans les chaînes d'approvisionnement ?. Prendre l'exemple de l'agro-alimentaire.
