<!-- $theme: gaia -->

# Administração de ==Sistemas Operacionais==
      
### Aula 7 && 8

###### Antônio Sérgio de Sousa Vieira
###### Curso Técnico Integrado em Informática
###### IFCE campus Itapipoca
### Agosto de 2019
###### :email: sergio.vieira@ifce.edu.br

---
# Objetivos da Aula
- Conhecer o PowerShell
- Navegação Básica
- Manipulação de Arquivos e Textos
- Sistemas de arquivos

---
# PowerShell - Windows 7
- Ambiente de linha de comando
- Criação, manipulação e execução de scripts
- Equivalente ao ambiente de manipulação de scripts do Linux


---
# Diretórios (Pastas)
- Os arquivos dentro do S.O estão localizados em diretórios e subdiretórios
- Caminho (Path)
	- Localização específica de um arquivo
		- No Windows um caminho parece com isto:

# `C:\Usuários\Aluno\Downloads`

---
# Sistema de Arquivos (filesystem)
- Para cada disco instalado no computador existe um sistema de arquivos
- Um sistema de arquivos é responsável por rastrear todos os arquivos armazenados no disco
- No Windows, para cada sistema de arquivo é atribuída uma letra, da seguinte forma:

# `C:, ou D:, ou X:`

---
# Sistema de Arquivos (filesystem)
- O diretório raiz do disco ==C:== deve ser escrito como:
# `C:\`
- Assim como o diretório raiz do disco X: deve ser escrito como:
# `X:\`

---
# Sistema de Arquivos (filesystem)
- No Windows, subdiretórios são separados com
## `\ (Barra invertida - backslash)`
- Já no Linux, subdiretórios são separados com
## `/ (Barra - forward slash)`

---
# Exercício
- Localize através do Windows Explorer o diretório
# `C:\Usuários\Alunos\Downloads`
<!-- Exibir as propriedades do arquivo -->


---
# PowerShell - Windows 7
- Através do PS pode-se realizar operações matemáticas como

```
PS C:\Users\Alunos> 6*7
42
PS C:\Users\Alunos> 3/8
0,375
PS C:\Users\Alunos> (8+2)*3
30
PS C:\Users\Alunos> 2%3
2
```

---
# PowerShell - Windows 7
- Através do PS pode-se exibir uma sequência de números

```
1..10
1..100
10..1
1..10 | % {if($_ % 2 -eq 0) {$_}}
```

---
# PowerShell - Windows 7
- Informações da versão do PS
```
PS C:\Users\sergi> $PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.16299.1004
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
BuildVersion                   10.0.16299.1004
CLRVersion                     4.0.30319.42000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

---
# PowerShell - Windows 7
- Informações da versão do PS
```
PS C:\Users\sergi> $PSVersionTable.PSVersion

Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  1004
```

---
# PowerShell - Windows 7
- Seus comandos são insensíveis ao caso, ou seja, não importa se você escrever em minúsculos, maiúsculo ou misturado.

```
Get-ChildItem
get-childitem
GET-CHILDITEM
```
---
# PowerShell - Windows 7
- **Get-Help**: Exibe ajuda sobre os *cmdlets* e conceitos dos Windows PowerShell
- **Sintaxe**: Get-Help <Nome do CmdLet>
- **Exemplos**:

```
PS C:\Users\alunos> get-help ls
PS C:\Users\alunos> Get-Help * # Exibe todos os tópicos
PS C:\Users\alunos> Get-Help get-* # Tópicos que começam 
# com get- 
```

---
# PowerShell - Windows 7
- **Get-Location**: Exibe informações sobre o diretório atual

```
PS C:\Users\Alunos> get-location

Path
----
C:\Users\Alunos
```

---
# PowerShell - Windows 7
- **Get-ChildItem**: lista o conteúdo de um diretório

---
# PowerShell - Windows 7
- **Exemplo 1**: lista os itens filho de um diretório do sistema de arquivos. 
Os nomes dos arquivos e dos subdiretórios são exibidos. 
Para locais vazios, o comando não retorna nenhuma saída e retorna ao prompt do PowerShell.

---
# PowerShell - Windows 7
```
PS C:\Users\sergi> get-childitem -path C:\Windows\Temp\
# get-childitem : O acesso ao caminho 'C:\Windows\Temp' 
# foi negado.
```

```
PS C:\Users\sergi> get-childitem
    Diretório: C:\Users\sergi
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       03/07/2019     14:07                .cache
d-r---       25/05/2019     20:13                3D Objects
dar---       03/06/2019     19:50                OneDrive
-a----       15/08/2019     06:19           2660 .viminfo
-a----       31/07/2019     15:05             18 main.py
```

---
# PowerShell - Windows 7
- As letras na coluna *Mode* podem ser interpretadas da seguinte forma:
	- l (link)
    - d (diretório)
    - a (arquivo)
    - r (somente leitura)
    - h (escondido)
    - s (arquivo de sistema)

---
# PowerShell - Windows 7
- A coluna LastWrite mostra a data e a hora da última alteração do arquivo

```
PS C:\Users\sergi> get-childitem
    Diretório: C:\Users\sergi
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       03/07/2019     14:07                .cache
d-r---       25/05/2019     20:13                3D Objects
dar---       03/06/2019     19:50                OneDrive
-a----       15/08/2019     06:19           2660 .viminfo
-a---l       28/08/2019     03:40              0 intro.pdf
-a----       31/07/2019     15:05             18 main.py
```

---
# PowerShell - Windows 7
- A coluna Length mostra o tamanho do arquivo em bytes

---
# PowerShell - Windows 7
- **Exemplo 2**: listar apenas os nomes dos arquivos do diretório atual

```
PS C:\Users\sergi> get-childitem -name
.cache
3D Objects
OneDrive
.vimInfo
intro.pdf
main.py
```

---
# PowerShell - Windows 7
- **Exemplo 3**: Exibir todos os arquivos .txt com atributo *Hidden* (escondido)
	- **Parâmetro**: ==-force==

```
PS C:\Users\sergi> get-childitem *.txt -force
    Diretório: C:\Users\sergi
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a-h--       28/08/2019     03:58             16 newfile.txt
```

---
# PowerShell - Windows 7
- **Exemplo 3**: Exibir todos os arquivos .txt do diretório atual e seus subdiretórios
	- **Parâmetro**: ==-recurse==

```
PS C:\Users\sergi> get-childitem *.txt -recurse
    Diretório: C:\Users\sergi
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       28/08/2019     03:58             16 file1.txt
    Diretório: C:\Users\sergi\teste
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       28/08/2019     03:58             16 file2.txt
```

