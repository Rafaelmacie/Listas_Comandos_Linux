# Lista de Exercícios - Usuários, Grupos e Permissões

**Instituição:** Instituto Federal de Educação, Ciência e Tecnologia do Ceará - Campus Boa Viagem
**Curso:** Análise e Desenvolvimento de Sistemas (ADS)
**Disciplina:** DevOPS
**Professor:** Renato William
**Aluno:** Rafael Maciel

Este repositório contém as resoluções da lista de exercícios práticos sobre a gestão de usuários, grupos e permissões no Linux.

---

## 1. Cadastre os usuários alice, bob, carlos, daniel e erica.

    sudo useradd -m alice
    sudo useradd -m bob
    sudo useradd -m carlos
    sudo useradd -m daniel
    sudo useradd -m erica

## 2. Crie no seu diretório home os diretórios producao, rh, financeiro e ti.

    mkdir ~/producao ~/rh ~/financeiro ~/ti

## 3. Cadastre os grupos funcionarios, gerentes e informatica.

    sudo groupadd funcionarios
    sudo groupadd gerentes
    sudo groupadd informatica

## 4. Colocar os usuários dentro do grupo conforme abaixo:
* funcionarios: alice, daniel, erica.
* gerentes: bob, carlos
* informatica: carlos, alice.

    # Grupo funcionarios
    sudo usermod -aG funcionarios alice
    sudo usermod -aG funcionarios daniel
    sudo usermod -aG funcionarios erica

    # Grupo gerentes
    sudo usermod -aG gerentes bob
    sudo usermod -aG gerentes carlos

    # Grupo informatica
    sudo usermod -aG informatica carlos
    sudo usermod -aG informatica alice

## 5. Alterar o usuário dono dos diretórios conforme abaixo:
* producao usuário dono bob e grupo funcionarios.
* rh usuário dono erica e grupo gerentes.
* financeiro usuário dono bob grupo gerentes.
* ti usuário dono carlos grupo informatica.

    sudo chown bob:funcionarios ~/producao
    sudo chown erica:gerentes ~/rh
    sudo chown bob:gerentes ~/financeiro
    sudo chown carlos:informatica ~/ti

## 6. Altere as permissões dos diretórios conforme abaixo:
*(Observação: Em cada item faça a alteração das permissões no modo octal e no modo literal)*

* **producao:** Usuário e outros somente leitura. Grupo leitura, escrita e execução.
  * **Modo Octal:** `sudo chmod 474 ~/producao`
  * **Modo Literal:** `sudo chmod u=r,g=rwx,o=r ~/producao`

* **rh:** Usuário e outros sem permissão. Grupo leitura, escrita e execução.
  * **Modo Octal:** `sudo chmod 070 ~/rh`
  * **Modo Literal:** `sudo chmod u=,g=rwx,o= ~/rh`

* **financeiro:** Usuário somente leitura, grupo escrita e execução e outros nenhuma.
  * **Modo Octal:** `sudo chmod 430 ~/financeiro`
  * **Modo Literal:** `sudo chmod u=r,g=wx,o= ~/financeiro`

* **ti:** Usuário leitura, escrita e execução, grupo leitura e outros nenhuma.
  * **Modo Octal:** `sudo chmod 740 ~/ti`
  * **Modo Literal:** `sudo chmod u=rwx,g=r,o= ~/ti`

---

## 7. Supondo os detalhes dos arquivos pertencentes a um determinado diretório, analise a figura 1 e responda o que se pede:

**a Quais os nomes dos diretórios contidos nessa relação? Qual o nome do arquivos contidos nesta relação?**
* **Diretórios (indicados pelo `d` inicial):** pgms, teste1, teste2, Faturamento.
* **Arquivos (indicados pelo `-` inicial):** Controle, mbox, exemplo, Linux.

**b Existe algum usuário do mesmo grupo de Rui? Caso positivo, qual?**
* Sim. Pedro e Tiago também pertencem ao `Contab`.

**c Qual o tamanho do arquivo Controle?**
* 1565 bytes.

**d Quais as permissões de acesso que os usuários do mesmo grupo de João possuem para acessar o arquivo Controle?**
* O grupo de João é `Financ`. O arquivo Controle também pertence ao grupo `Financ`. Então as permissões do grupo para este arquivo são de leitura e gravação (`rw-`).

**e Eu sou do grupo do usuário Pedro, que permissões tenho com relação ao arquivo exemplo?**
* O grupo do usuário Pedro é `Contab`. O arquivo exemplo pertence a este mesmo grupo. As permissões definidas para o grupo neste arquivo são de leitura e execução (`r-x`).

**f Diga o comando completo para permitir que os usuários do mesmo grupo de Rui possam ler e gravar, mas não possam executar o arquivo Linux.**
* `chmod g=rw Linux`

**g Qual o código octal para a permissão de acesso do arquivo exemplo.**
* **755** (7 para o usuário `rwx`, 5 para o grupo `r-x`, 5 para outros `r-x`).

**h Qual o código literal para a permissão de acesso do arquivo exemplo.**
* `u=rwx,g=rx,o=rx`

**i Altere o dono do arquivo Linux para Rui.**
* `sudo chown Rui Linux`

**j Altere o grupo do arquivo Linux para Staff.**
* `sudo chgrp staff Linux`