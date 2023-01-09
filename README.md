# Installation de Foundry

Suivre la documentation au lien suivant: https://book.getfoundry.sh/getting-started/installation

### Linux/MacOS:
```
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

## Initialisation du projet
```
forge init myproject
```

## Verification du fonctionnement de Foundry

Aller dans le dossier "myproject" et lancer la commande
```
forge test
```

Le résultat doit ressembler à:
```
[⠒] Compiling...
No files changed, compilation skipped

Running 2 tests for test/Counter.t.sol:CounterTest
[PASS] testIncrement() (gas: 28356)
[PASS] testSetNumber(uint256) (runs: 256, μ: 27642, ~: 28342)
Test result: ok. 2 passed; 0 failed; finished in 7.77ms
```

##

Pour aller à la prochaine étape du TD, aller dans la branche ``td-02-premier-contrat``
