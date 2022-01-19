# Fluxo atual

- Criamos uma branch `feature` a partir da `develop`
- Desenvolvemos na branch `feature`
- Criamos PR da `feature` para `develop`
- Criamos PR da `develop` para `stage`
- Testamos em `uat`
- Criamos PR da `stage` para `main`

---

# Problemas

- Colocamos código não validado na branch `develop`, que é de onde os novos desenvolvimentos partem
  - Novas branch `features` terão esse código não validado/homologado
- Criamos 2 PRs em sequencia, um para `develop` e um para `stage`
  - Gera commits desnecessários, poluindo o histórico do repo
- Bloqueamos a subida de coisas na `main`, pois pode ter coisa na `stage` que não está validada/homologada
  - Bloqueio é uma palavra forte, dá para resolver, mas gera um retrabalho considerável
  - Geralmente percebemos esse tipo de problema apenas no momento que algo precisa subir para `main`.

---

# Proposta

- Criar branch `feature` a partir da `develop`
- Desenvolver na branch `feature`
- Quando finalizar e precisar validar no ambiente, fazer merge com a branch `stage` SEM PR
- Quando estiver validado, fazer PR da `feature` para `develop`
- A partir de então, a qualquer momento pode fazer um PR da `develop` para a `main`, com o release notes de todas as funcionalidades que estão entrando

Não teríamos um ciclo linear/progressivo de integração de branchs.

A branch `stage` seria apeans um representante do ambiente de stage, contendo sempre: `develop` + `features sendo homologadas`.

A qualquer momento ela poderia ser apagada e recriada a partir da `develop`.

---

# Benefícios

- [X] Não colocamos código não validado na branch `develop`
- [X] Não criamos 2 PRs em sequencia, um para `develop` e um para `stage`
- [X] Não bloqueamos a subida de coisas na `main`
- Se houver algum problema com conflitos, o time terá que conversar durante o tempo de desenvolvimento, não quando a funcionalidade está prestes a ir para produção

# Problemas

- Se uma feature demorar muito para ser desenvolvida/testada, ela pode ficar desatualizada com a `develop`. O Ideal seria atualizar as `feature` branchs toda vez que algo entrasse na develop.

--- 
# Sugestões

- Quando integrar uma branchg na `develop`, fazer o squash da branch `feature`, isso evitaria o poluição da `develop` com commits desnecessários (`wip`, `fix typo`, `teste`)