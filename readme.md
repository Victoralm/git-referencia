# Meu Guia de referência do Git

## Básico

- Iniciar (criar) repositório Git:
    ```bash
    git init
    ```

- Rastrear arquivos no diretório Git:
    ```bash
    git add <nome_do_arquivo>
    ```

- Verificar estado (área de Stage) do repositório:
    ```bash
    git status
    ```

- Gravando arquivo no repositório (tem de ter as aspas na mensagem):
    ```bash
    git commit -m "<mensagem_desejada>"
    ```

- A cada nova modificação no arquivo, executar:
    ```bash
    git add <nome_do_arquivo> ou git add .
    git commit -m <"mensagem_desejada">
    ```

- Verificar alterações realizadas (área de commits):
    ```bash
    git log
    ```

- Verificando somente os 3 últimos commits:
    ```bash
    git log -n 3
    ```

- Mínimo de informações no log:
    ```bash
    git log --oneline
    ```

- Log com muitas informações (usar as setas para navegar pelo log e q para sair):
    ```bash
    git log --stat
    ```

- Log com múltiplos argumentos:
    ```bash
    git log -n 3 --oneline --stat
    ```

- Rastrear todos os arquivos do diretório atual (incluindo subdiretórios):
    ```bash
    git add .
    ```

- Rastrear um diretório e todos os arquivos contidos nele:
    ```bash
    git add <nome_do_diretório>
    ```

- Rastrear e commitar no mesmo comando:
    ```bash
    git commit -a -m <"mensagem_desejada">
	    ou
    git commit -am <"mensagem_desejada">
    ```

- Verificar mudanças não rastreadas (ainda fora do Stage, já tendo sido adicionados inicialmente mas não após uma alteração):
    ```bash
    git diff
    ```

- Verificar mudanças não rastreadas em um arquivo específico:
    ```bash
    git diff <nome_do_arquivo>
    ```

- Verificar mudanças rastreadas (já no Stage):
    ```bash
    git diff --staged
    ```

#### Exibir mudanças dentro e fora do Stage

- Pegar o código do último commit com git log.
    ```bash
    git log -n 1 --oneline
    // Saída: <N°_do_código_do_commit> <Mensagem_do_commit>
    // EX: 84d3245 Inserido um arquivo qualquer
    // Pegar o código e usar no git diff.
    git diff 84d3245
    ```

- Exibir diferença entre commits (do commit x até o commit y):
    ```bash
    git diff <N°_do_código_do_commit>..<N°_do_código_do_commit>
    // Ex: git diff 84d3245..f5b75eb
    ```

- Exibir as mudanças entre o commit x e os dois anteriores a ele (exibe as alterações commitadas e não-commitadas):
    ```bash
    git diff <N°_do_código_do_commit>~2
    git diff 84d3245~2
    ```

#### Ignorando arquivos e diretórios

- Criar o arquivo ".gitignore" e nele listar o que deverá ser ignorado, no formato (um por linha):
    ```
    dir01/
    dir07/
    arq03.txt
    arq19.html
    *.bk // (todos os arquivos com extenção bk)
    backups/*.bk // (todos os arquivos com extenção bk que estejam dentro do diretório backups)
    ```

- Remover arquivos do repositório:
    ```bash
    git rm <nome_do_arquivo>
    ```

#### Renomear e Mover arquivos do repositório

- Renomear
    ```bash
    git mv <nome_do_arquivo_original> <nome_do_arquivo_destino>
    // Ex: git mv sb.css sidebar.css
    ```

- Mover (criar o diretório antes):
    ```bash
    git mv <nome_do_arquivo_original> <nome_do_diretório_destino>/<nome_do_arquivo_destino>
    Ex: git mv sb.css css/sidebar.css
    ```

- Desfazer modificação não-rastreada (fora do Stage):
    ```bash
    git checkout -- <nome_do_arquivo>
    ```

#### Desfazer modificação rastreada (já no Stage)

- Retira do Stage mantendo as modificações:
    ```bash
    git reset -- <nome_do_arquivo>
    ```
- Retira do Stage desfazendo as modificações:
    ```bash
    git reset --hard
    ```

#### Alterando o último commit

- Pode-se modificar apenas a mensagem, desde que logo após o commit use-se o comando sem executar nenhuma modificação/adição/remoção:
    ```bash
    git commit --amend
    ```

- Pode-se adicionar uma modificação esquecida ao último commit, desde que logo após o commit use-se os commandos:
    ```bash
    git add <nome_do_arquivo>
    git commit --amend
    ```

#### Desfazendo um commit

- Sem edição da mensagem:
    ```bash
    git revert --no-edit <Nº_do_código_do_commit>
    ```
- Editando a mensagem:
    ```bash
    git revert <Nº_do_código_do_commit>
    ```
- Especificamente o último commit:
    ```bash
    git revert --no-edit HEAD
	    ou
    git revert HEAD
    ```
- Usando o 

<br>

### Repositórios remotos

- Criar um repositório remoto (no PC servidor):
    ```bash
    git init --bare <nome_do_repositporio>.git
    ```

- Adicionar um repositório remoto (no PC cliente - sendo possível adicionar mais de um, desde que cada possua um nome difderente):
    ```bash
    git remote add <nome_para_o_repositório> <protocolo>://<ip_do_pc_servidor>/<caminho_completo_para_o_repositório>
    // Ex (protocolo: local):
    // git remote add servidor file://192.168.0.107/home/victoralm/projetos_git/moveis-ecologicos.git
    // Ex: (protocolo: ssh):
    // git remote add servidor ssh://fulano@192.168.0.107:78965/home/victoralm/projetos_git/moveis-ecologicos.git

#### Listar repositórios remotos
- Exibir apenas o nome:
    ```bash
    git remote
    ```
- Exibir nome e endereço
    ```bash
    git remote -v
    ```

- Alterar nome do repositório remoto:
    ```bash
    git remote rename <nome_original> <nome_novo>
    ```

- Alterar endereço do repositório remoto:
    ```bash
    git remote set-url <nome_do_repositório> <novo_endereço_para_o_repositório>
    ```

- Enviando commits para o repositório remoto:
    ```bash
    git push <nome_do_repositório> master
    ```

- Clonar repositórios remotos:
    ```bash
    git clone <protocolo>://<ip_do_pc_servidor>/<caminho_completo_para_o_repositório>
    // Ex (protocolo: local):
    // git clone file://192.168.0.107/home/victoralm/projetos_git/moveis-ecologicos.git
    // Ex (protocolo: ssh):
    // git clone ssh://fulano@192.168.0.107:78965/home/victoralm/projetos_git/moveis-ecologicos.git
    ```

- Sincronizando o repositório local com o remoto:
    ```bash
    git pull <nome_do_repositório> master
    ```

<br>

### Integração com o GitHub (repositório previamente existente localmente)

- Criar o repositório no GitHub, com o mesmo nome do repositório local
- Acessar a pasta do repositório local
- Executar git remote conforme para adicionar a origem:
    ```bash
    git remote add origin https://github.com/<nome_do_usuário_github>/<nome_do_repositório>.git
    ```
- Executar git push inicial para enviar as alterações ao repositório origem:
    ```bash
    git push -u origin master
    ```

- Clonando repositórios (GitHub):
    ```bash
    git clone https://github.com/<nome_do_usuário>/<nome_do_repositório>
    ```
<br>

_____________________________________
#################### Exemplo ####################

### Servidor Linux na rede local, servindo diretório(s) via Samba. Este(s) diretório(s) previamente mapeados como unidades de rede.

- No diretório desejado no servidor:
	```bash
    git init --bare <nome_desejado_para_o_repositorio>
	// Como em:
	//	git init --bare JavaInicial
    ```
		
- Na máquina Windows, já com a unidade de rede mapeada, com o shell aberto no local desejado:
    ```bash
    git clone <endereço_do_repositporio_desejado>
	Como em (Atenção com a direção das barras):
		git clone Z:/Compartilhamento/Usuario/JavaInicial
    ```
- Criando o commit inicial:
    ```bash
    git add .
	git commit -am "Inicializando o repositório"
	git push origin master
    ```

_____________________________________

### Criando branches no repositório

[Referência](https://confluence.atlassian.com/bitbucket/branching-a-repository-223217999.html#BranchingaRepository-CreateaGitbranch)

- Checando o branch atual:
    ```bash
    git branch
    ```

- Criando um novo branch no repositório:
    ```bash
    git branch <nome_para_o_branch>
    ```

- Entrando no novo branch:
    ```bash
    git checkout <nome_do_branch>
    ```

- Adicionando as alterações ao noivo branch:
    ```bash
    git add . 
	git commit -m "mensagem_para_o_novo_branch"
    ```

- Retornando ao branch principal:
    ```bash
    git checkout master
    ```

- Subindo o conteúdo de um branch específico:
    ```bash
    git push origin <nome_do_branch>
    ```
