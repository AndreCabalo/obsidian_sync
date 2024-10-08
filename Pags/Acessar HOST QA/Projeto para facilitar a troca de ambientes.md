
[Repositório](https://github.com/ps-corp-platform/hosts)

# Scripts de Hosts

[](https://github.com/ps-corp-platform/hosts#scripts-de-hosts)

O projeto de script de hosts foi desenhado para facilitar a troca de ambientes do PagSeguro.

Com esse projeto é possível fazer a troca entre ambientes como o **local**, **qa**, **billing**, **base**, **sandbox** e **produção** executando apenas um comando.

Os scripts foram escritos em `xml` para serem lidos pela ferramenta `apache ant`. Ao executar os scripts, será alterado o arquivo `/etc/hosts` de sua máquina para apontar para o ambiente escolhido.

## Pré Requisitos

[](https://github.com/ps-corp-platform/hosts#pr%C3%A9-requisitos)

- [Apache ant](http://ant.apache.org/)

```shell
sudo apt-get install ant
```

- [Git](https://git-scm.com/)

```shell
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

## Instalação

[](https://github.com/ps-corp-platform/hosts#instala%C3%A7%C3%A3o)

Clone o projeto do repositório com `git`:

```
cd $USER/workspace
git clone git@github.com:ps-corp-platform/hosts.git
```

## Como usar?

[](https://github.com/ps-corp-platform/hosts#como-usar)

Execute o comando `ant` a partir da pasta do projeto, passando o ambiente para qual deseja usar.

**Exemplos:**

```shell
cd $USER/workspace/hosts

sudo ant local-europa       # Aponta para o ambiente local
sudo ant qa-trunk           # Aponta para o ambiente de qa
sudo ant prod-a6-hundblue1  # Aponta para primeira linha da área 6 produção
sudo ant original           # Volta o arquivo ao estado original
```

Para testar a geração de hosts, sem alterar o /etc/hosts, informe o destino do arquivo que será gerado

```shell
sudo ant -Dlinux_hosts_path=./tmp.hosts prod-gt-backoffice-wildfly-fe-1
```

Para listar todos os ambientes, execute:

```shell
sudo ant -p
```

## Referências

[](https://github.com/ps-corp-platform/hosts#refer%C3%AAncias)

- [Versionamento de Hosts](https://confluence.intranet.uol.com.br/confluence/display/PagSeguro/Versionamento+de+Hosts)


