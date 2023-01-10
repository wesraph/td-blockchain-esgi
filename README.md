# Créer un ERC-20
Dans le même répertoire que le TD précèdent, créer un nouveau contrat "ERC20.sol" et le fichier de test associé.

Comme indiqué dans le cours, un ERC-20 doit implémenter les fonctions suivantes:

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

## Description des fonctions

##### Name
Retourne le nom du token. C'est le nom qui sera affiché sur les explorers.
##### Symbol
La fonction symbol doit retourner le symbol du token. Généralement il est composé de trois caractères en majuscule mais il est courant d'en voir quatre ou cinq. Exemple: BNB, ETH, XIV, XRP
##### Decimals
Decimals est optionnel mais fortement recommendée. Elle indique le nombre de décimales après la virgule maximal qui est accepté. La valeur la plus commune est 19. La plus petite valeur échangeable de votre token sera alors de 0.0000000000000000001 token.
##### Total supply
Indique le nombre total de tokens existant. Elle peut varier au cours du temps.
##### BalanceOf
Retourne la balance de l'adresse indiquée (le nombre de tokens en sa possession).
##### Transfer
Transfère ``value`` tokens du compte de l'appelant vers le compte de ``_to``
##### Approve
Autorise ``_spender`` à dépenser ``_value`` tokens de celui qui appelle la fonction
##### Allowance
Retourne combien ``_spender``  peut dépenser de tokens de ```_owner`` (précedemment autorisé via ``approve``)
##### TransferFrom
Transfer ``_value`` tokens de ``_from`` vers ``_to``. Pour que le transfer soit possible, ``_from`` doit avoir approuvé (avec ``approve``) l'adresse effectuant la transaction
