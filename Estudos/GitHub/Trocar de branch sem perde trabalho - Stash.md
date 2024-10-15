Ao editar um arquivo e ele aparecer no git status (para vc dar o git add .), mas você ainda nao quer commitar, você pode usar o git stash, onde ele ira guardar essas alterações para vc, com isso vc pode criar/acessar outra branch.

- Para aplicar as mudanças que guardou no git stash, damos o comando git stash apply

- Se quiser ver o list de stash, usamos o comando git stash list

- Se quiser apagar oque tiver em stash usamos o comando git stash clear

O comando `git stash` é utilizado para armazenar temporariamente modificações no seu repositório que ainda não estão prontas para serem commitadas. Ele coloca essas alterações em uma área especial (stash) e permite que você volte a um estado "limpo" de seu repositório, sem perder as mudanças não commitadas.

Isso é útil, por exemplo, quando você está no meio de uma implementação e precisa trocar de branch ou resolver um conflito sem perder o progresso atual.

### Exemplos de uso de `git stash`:

#### 1. **Salvar alterações no stash**

Suponha que você tenha feito alterações em alguns arquivos, mas ainda não quer fazer um commit, e precisa mudar de branch para resolver um problema:

```$ 
git status 
On branch feature-x 
Changes not staged for commit:     
	modified:   file1.txt     
	modified:   file2.txt
```

**Você pode "guardar" essas mudanças com o `git stash`:**


```$ 
git stash 
Saved working directory and index state WIP on feature-x: 123abc Fix issue
```

**Agora seu diretório de trabalho estará limpo, e você pode mudar de branch ou fazer outra tarefa.**

#### 2. **Ver o que está guardado no stash**

Para ver uma lista de tudo que está armazenado no stash, você pode usar o comando:


```$ 
git stash list 
stash@{0}: WIP on feature-x: 123abc Fix issue 
stash@{1}: WIP on feature-y: abc456 Add new feature
```

#### 3. **Recuperar alterações do stash**

Quando você estiver pronto para continuar trabalhando nas mudanças que guardou, você pode recuperar essas alterações com:

`$ git stash apply`

**Isso aplica as mudanças guardadas no stash, mas mantém a entrada no stash, caso você precise dela novamente. Para aplicar e remover ao mesmo tempo (limpar o stash), use:**

`$ git stash pop`

#### 4. **Criar um stash com uma descrição**

Você pode criar um stash com uma mensagem personalizada, o que é útil para lembrar do que se trata:

`$ git stash save "WIP: Implementing feature X"`

#### 5. **Stash específico de arquivos**

Se você quiser guardar apenas um arquivo ou alguns arquivos específicos no stash, use:

`$ git stash push file1.txt file2.txt`

#### 6. **Descartar um stash sem aplicar**

Se você quiser remover um stash que não será mais necessário, use:

`$ git stash drop stash@{0}`

**Ou para limpar todos os stashes:**

`$ git stash clear`

#### 7. **Aplicar um stash específico**

Se você tiver vários stashes e quiser aplicar um específico, pode fazer assim:

`$ git stash apply stash@{1}`

### Casos de uso comuns:

- **Trocar de branch sem perder trabalho**: Se você está no meio de uma tarefa e precisa interromper para trabalhar em algo urgente, `git stash` permite salvar temporariamente suas mudanças e voltar a um estado "limpo" para trabalhar em outra coisa.
- **Guardar trabalho incompleto**: Se você está experimentando com uma implementação, mas não quer fazer um commit de código incompleto.
- **Lidar com conflitos**: Durante um merge, às vezes pode ser necessário guardar as alterações locais para resolver conflitos de forma mais limpa.

Esses são alguns dos principais usos de `git stash`. Ele ajuda a manter o fluxo de trabalho organizado, especialmente quando você precisa pausar mudanças momentaneamente.





