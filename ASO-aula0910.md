---
marp: true
---

<!-- $theme: gaia -->

# Administração de ==Sistemas Operacionais==
      
### Aula 9 && 10

###### Antônio Sérgio de Sousa Vieira
###### Curso Técnico Integrado em Informática
###### IFCE campus Itapipoca
### Setembro de 2019
###### :email: sergio.vieira@ifce.edu.br

---
# Objetivos da Aula
- Pesquisar vários arquivos com extensão diferente
- Exibir todos os arquivos excluindo certo tipo de padrão
- Exibir arquivos segundo lista de atributos
- Navegar entre pastas
- Criando arquivos, pastas etc com New-Item
- Exibir conteúdo de um arquivo com Get-Content
- Criando conteúdo com Set-Content

---
# PowerShell - Windows 7
<!-- page_number: true -->
- **Exemplo 4**: Exibir todos os arquivos do tipo .odt e .por do diretório atual e seus subdiretórios
	- **Parâmetro**: ==-include p1,p2==
```
get-childitem -recurse -include *.odt,*.por
```

---
# PowerShell - Windows 7
- **Exemplo 4**: Exibir todos os arquivos de um diretório específico
	- **Parâmetro**: ==-path==
```
PS C:\Users\sergi> get-childitem -path c:\windows
```

---
# PowerShell - Windows 7
- **Exemplo 5**: Exibir todos os arquivos excluindo certo tipo de padrão
	- **Parâmetro**: ==-exclude==
```
get-childitem -path c:\windows -exclude *.dll
```

---
# PowerShell - Windows 7
- **Exemplo 6**: também é possível listar os valores do registro do windows
 
```
Get-ChildItem -Path HKLM:\HARDWARE
```

---
# PowerShell - Windows 7
- **Exemplo 7**: Também é possível listar os arquivos/diretórios através do parâmetro Attributes
	- **Parâmetro**: ==-Attributes==
		- Archive (a)
		- Directory (h)
		- ReadOnly (r)
		- System (s)
		- etc

---
# PowerShell - Windows 7
- Para combinar atributos use:
	- $! (NOT)$
	- $+ (AND)$
	- $, (OR)$

```
Get-ChildItem -Attributes d+r+!a
```
---
# Navegação básica do S.O
- **Set-Location**: é através deste comando que você pode "navegar" entre os diretórios e discos do seu computador
- **Exemplo 1**: este comando serve para "entrar" no diretório *downloads*

```
Set-Location Downloads
```

---
# Navegação básica do S.O
- **Set-Location**: para voltar ao diretório anterior use o comando set-location seguido de ".."

```
set-location ..
```

---
# Navegação básica do S.O
- **Set-Location**: para voltar mais de um nível separe os ".." com "\" para cada nível adicional. O Comando abaixo retorna dois níveis

```
set-location ..\..
```

---
# Criando com New-Item
- **New-Item**: o cmdlet *new-item* cria um item e pode atribuir valores a ele.
- O tipo do item que será criado depende de onde ele é criado
	- ==No sistema de arquivos==: cria arquivos e diretórios
	- ==No registro==: cria chaves de registro e entradas

---
# Criando com New-Item
- **Exemplo 1**: criando um arquivo no diretório atual

```
new-item -path . -name "teste01.txt" -itemtype "file" 
-value "alo mundo"
```

---
# Criando com New-Item
- **Exemplo 1**: criando um arquivo no diretório atual

```
new-item -path . -name "level1" -itemtype "directory"
```

---
# Criando com New-Item
- **Exemplo 2**: cria uma estrutura de diretórios e subdiretórios

```
 new-item -path .\ps\script -ItemType "directory"
```

---
# Criando com New-Item
- **Exemplo 3**: criando multiplos arquivos

```
 new-item -itemtype "file" 
 -path ".\ps\file1.txt",.\ps\file2.txt"
```
---
# Criando com New-Item
- Outros parâmetros:
	- **-confirm**: exibe uma pergunta para confirmar cada ação do comando
	- **-force**: força a execução do comando mesmo que o item seja do tipo "read only"

---
# Exibindo o conteúdo de um arquivo
- **get-content**: serve para exibir o conteúdo de um arquivo

```
get-content newfile.txt
```

---
# Exibindo o conteúdo de um arquivo
- **get-content**: para exibir uma quantidade específica de linhas do arquivo utilize o parâmetro -TotalCount <número de linhas>
- **Exemplo**: mostra as 10 primeiras linhas do arquivo newfile.txt

```
get-content newfile.txt -TotalCount 10
```

---
# Criando e substituindo o conteúdo de arquivos
- **set-content**: escreve ou substitui o conteúdo de um item com um novo conteúdo.

- **Exemplo 1**: substitui o conteúdo de múltiplos arquivos em um diretório.

```
set-content -Path ".\test*.txt" -Value "alô,  mundo"
```

---
# Criando e substituindo o conteúdo de arquivos

- **Exemplo 2**: cria um arquivo chamado 10lines.txt com as primeiras dez linhas do arquivo newfile.txt

```
get-content newfile.txt -TotalCount 10 | set-content 10lines.txt
```