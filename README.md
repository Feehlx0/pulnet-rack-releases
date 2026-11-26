# PULNET Rack Monitor

Programa da **PULNET Tecnologia** para documentar a infraestrutura de rede de um cliente: o rack em 3D, os cabos de rede e de energia, a topologia, a rede e o histórico de alterações. Ele também **monitora os equipamentos** (ping ou porta TCP) e mostra quem está fora do ar.

Ele é instalado num computador ou servidor do cliente e fica disponível pelo navegador para qualquer máquina da rede local, sem instalar nada nas outras máquinas.

---

## O que você precisa

- Windows 10, Windows 11 ou Windows Server, 64 bits.
- Permissão de administrador para instalar.
- Um navegador atualizado (Chrome, Edge ou Firefox).
- Internet só para receber atualizações. O resto funciona sem internet.

## Instalar

1. Baixe a versão mais recente em **<https://github.com/Feehlx0/pulnet-rack-releases/releases/latest>** (arquivo `PULNET-Rack-Monitor-Setup-<versão>.exe`).
2. Execute o instalador.
   - O instalador ainda não tem assinatura digital. Se o Windows mostrar "O Windows protegeu o computador", clique em **Mais informações → Executar assim mesmo**.
3. Siga as telas:
   - **Senha de edição** (obrigatória, mínimo 6 caracteres): quem souber essa senha pode alterar a documentação.
   - **Senha de visualização** (opcional): deixe em branco para qualquer pessoa da rede local poder ver, sem editar.
   - **Porta:** deixe `8080`, a menos que ela já esteja em uso.
   - **Importar documentação:** deixe em branco para começar do zero.
4. No fim, marque **Abrir no navegador**.

O programa fica instalado como **serviço do Windows**: ele sobe sozinho com o computador, mesmo sem ninguém logado.

Para acessar:

- no próprio computador: `http://localhost:8080`
- de outra máquina da rede: `http://NOME-DO-COMPUTADOR:8080` ou `http://IP-DO-COMPUTADOR:8080`

O passo a passo completo, com os caminhos dos arquivos e os comandos de manutenção, está no `INSTALACAO.md`, que fica na pasta do programa (`C:\Program Files\PULNET Rack Monitor\`).

## Primeiros passos: montar um cliente do zero

Numa instalação nova, a página abre com um rack vazio.

1. Clique em **Editar** e digite a senha de edição.
2. **Cliente e rack:** com nada selecionado, o painel da direita mostra **Dados do rack**. Preencha o nome do cliente, o nome do rack, o local e o tamanho (U).
3. **Equipamentos:** clique em **Adicionar equipamento**. No campo **Modelo do catálogo**, digite parte do nome (ex.: `ccr`, `usw`, `poweredge`) e escolha da lista: tipo, altura e portas vêm preenchidos. Para um modelo que não está no catálogo, cadastre uma vez e use **Salvar como modelo**.
4. **Mais racks:** use **+ Novo rack** na barra de racks.
5. **Fora do rack:** câmeras, access points e estações também podem ser cadastrados e ligados ao rack.
6. **Cabos de rede:** abra um equipamento e clique numa porta para escolher o destino. Também dá para fazer pela aba **Conexões**.
7. **Energia:** abra a régua ou o nobreak e clique na tomada para escolher o equipamento.
8. **Rede:** na aba **Rede**, cadastre as faixas de IP, os links de internet, o DNS e o domínio.
9. **Monitoramento:** preencha o **IP** do equipamento. Se ele não responder a ping, escolha **Porta TCP** na seção **Monitoramento** (ex.: 3389 para Windows, 443 para a página do modem).
10. Clique em **Salvar**. Cada salvamento pede uma descrição e guarda um backup da versão anterior.

## O que dá para fazer

| Onde | O quê |
|---|---|
| **Rack 3D** | Gire, aproxime e veja de frente, 3/4, lateral, topo e fundo. Ligue e desligue porta, cabos de rede, cabos de energia, painéis e etiquetas. Os LEDs mostram quem está online. |
| **Topologia** | Árvore da rede, do link de internet até cada equipamento. |
| **Conexões** | Tabela de todos os cabos, por rack ou de todos os racks. |
| **Rede** | Faixas de IP, links de internet, DNS e domínio. |
| **Histórico** | Quem alterou o quê e quando. Em **Versões guardadas no servidor**, dá para baixar ou restaurar uma versão anterior. |
| **Busca** (Ctrl+K) | Procura por nome, IP ou hostname. |
| **Rastrear caminho até a internet** | Mostra por onde um equipamento chega até o link de internet. |
| **Arquivo → Imprimir / salvar PDF** | Documentação pronta para imprimir. |
| **Arquivo → Baixar cópia offline** | Um arquivo HTML único que abre em qualquer computador, sem o programa. |
| **Arquivo → Exportar versão cliente** | Cópia só para visualização, para entregar ao cliente. Você escolhe se vão fotos, dados de rede, IPs e histórico. Nº de série e observações internas nunca vão. |
| **Arquivo → CSV** | Exporta e importa equipamentos e conexões em planilha. |
| **Arquivo → Carregar dados de outro arquivo HTML** | Traz a documentação de um HTML gerado antes. |

## Atualizações

O programa procura versões novas uma vez por dia. Quando houver uma, quem entrou com a senha de edição vê o botão **Atualizar para X** no topo da página. Também dá para verificar na hora em **Arquivo → Verificar atualizações…**.

Ao clicar, o programa baixa a versão nova, confere a assinatura digital da PULNET e se instala sozinho. Em cerca de 1 minuto a página recarrega na versão nova. Dados, senhas e backups são mantidos.

Sem internet no servidor, baixe o instalador novo pelo link acima e execute-o por cima. Deixe as senhas em branco para manter as atuais.

## Onde ficam os dados

Tudo fica em `C:\ProgramData\PULNET Rack Monitor\` (documentação, backups, configuração e logs). Nem a atualização nem a desinstalação apagam essa pasta.

Se a máquina já teve o programa, a instalação aproveita os dados que estiverem lá. Para começar do zero, renomeie essa pasta antes de instalar.

## Problemas comuns

| Problema | O que fazer |
|---|---|
| A página não abre de outra máquina | Teste `http://localhost:8080` no próprio servidor. Se lá funcionar, confira se as duas máquinas estão na mesma rede local: o firewall só libera a rede local. |
| O selo mostra "Servidor sem resposta" | O serviço parou ou o servidor saiu da rede. Veja `C:\ProgramData\PULNET Rack Monitor\logs\pulnet-rack.log`. |
| Equipamento sempre fora do ar, mas funcionando | Ele provavelmente não responde a ping. Troque o teste para **Porta TCP**. |
| Esqueci a senha de edição | No servidor, abra o PowerShell como administrador em `C:\Program Files\PULNET Rack Monitor\` e rode `.\pulnet-rack.exe definir-senha`. |
| A porta 8080 já está em uso | Rode o instalador de novo e escolha outra porta. |

## Desinstalar

**Configurações → Aplicativos → PULNET Rack Monitor → Desinstalar.** O serviço e a regra de firewall são removidos. A pasta de dados continua lá; apague-a à mão só se tiver certeza.

## Testando? Conte o que achou

Ao relatar um problema, mande:

- a versão (aparece em **Arquivo → Verificar atualizações…**);
- o que você fez, o que esperava e o que aconteceu;
- se possível, um print e o arquivo `C:\ProgramData\PULNET Rack Monitor\logs\pulnet-rack.log`.

Não mande a documentação de um cliente real por canais abertos: ela tem IPs e dados da rede dele.
