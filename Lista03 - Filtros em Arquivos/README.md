# Lista de Exercícios - Linux: Arquivos e Filtros

**Instituição:** Instituto Federal de Educação, Ciência e Tecnologia do Ceará - Campus Boa Viagem
**Curso:** Análise e Desenvolvimento de Sistemas (ADS)
**Disciplina:** DevOPS
**Professor:** Renato William
**Aluno:** Rafael Maciel

Este repositório contém as resoluções da lista de exercícios práticos sobre manipulação de arquivos e filtros no Linux (grep, sed, cut, wc, head, tail).

---

## 1. Alguém acaba de doar um laptop para sua escola e você deseja instalar Linux nele. Ele veio sem manual e você é obrigado a inicializá-lo a partir de um pen drive USB sem nenhuma interface gráfica. Aparece um terminal shell e você sabe que, para cada processador presente, haverá uma linha dedicada no arquivo /proc/cpuinfo:

**(a) Usando os comandos grep e wc, exiba o número de processadores presentes.**

    grep "processor" /proc/cpuinfo | wc -l

**(b) Faça o mesmo com sed em vez de grep.**

    sed -n '/processor/p' /proc/cpuinfo | wc -l

---

## 2. Explore seu arquivo local/etc/passwd com os comandos grep, sed, head e tail de acordo com as tarefas descritas abaixo:

**(a) Quais usuários têm acesso a um shell Bash?**

    grep "/bin/bash" /etc/passwd

**(b) Muitos dos usuários de seu sistema existem para lidar com programas específicos ou para fins administrativos. Eles não têm acesso a um shell. Quantos deles estão presentes no sistema?**

    grep -E "/usr/sbin/nologin|/bin/false" /etc/passwd | wc -l

**(c) Quantos usuários e grupos existem em seu sistema (lembre-se: use apenas o arquivo /etc/passwd)?**

    # Quantidade de usuários (total de linhas do arquivo):
    wc -l < /etc/passwd

    # Quantidade de grupos únicos (extraindo o GID, que é o 4º campo):
    cut -d: -f4 /etc/passwd | sort -u | wc -l

**(d) Liste apenas a primeira, a última e a décima linha do arquivo /etc/passwd**

    head -n 1 /etc/passwd && sed -n '10p' /etc/passwd && tail -n 1 /etc/passwd

---

## 3. Considere este arquivo de exemplo /etc/passwd. Copie as linhas abaixo para um arquivo local chamado 'mypasswd' para este exercício.

**(a) Liste todos os usuários no grupo 1000 (use sed para selecionar apenas o campo apropriado) do arquivo mypasswd.**

    sed -n '/:1000:/p' mypasswd

**(b) Liste apenas o nome completo de todos os usuários deste grupo (use sed e cut).**

    sed -n '/:1000:/p' mypasswd | cut -d: -f5

---

## 4. Usando novamente o arquivo mypasswd dos exercícios anteriores, imagine um comando Bash que selecione um indivíduo do Main Office para ganhar uma rifa. Use o comando sed para imprimir apenas as linhas do Main Office e, em seguida, uma sequência de comando cut para recuperar o primeiro nome de cada usuário a partir dessas linhas. Depois, classifique esses nomes aleatoriamente e imprima apenas o nome principal da lista.

    sed -n '/Main Office/p' mypasswd | cut -d: -f5 | cut -d' ' -f1 | sort -R | head -n 1
