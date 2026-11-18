<p align="center"><picture><source media="(prefers-color-scheme: dark)" srcset="marca/loganos-branco.svg"><img src="marca/loganos-preto.svg" width="96" alt="LoganOS"></picture></p>

# LoganOS

[English](README.md) · **Português** · [Español](README.es.md)

Um painel para home lab num arquivo Python só. Atalhos para os seus serviços, monitor do sistema, discos com a saúde pelo SMART, eventos de segurança, notificações, backups e apps pequenos embutidos (Notas, Links, Câmera). Sem pip, sem Docker, sem banco de dados: só a biblioteca padrão do Python.

O nome vem do Logan, o pastor belga do autor.

## Requisitos

- Linux com systemd. Testado no **Debian 13 (x86_64)**. Debian 12, Ubuntu 24.04 e Raspberry Pi OS devem funcionar, mas ainda não foram testados.
- Python 3.11 ou mais novo (já vem nesses sistemas).
- Acesso de root para instalar.

## Instalar

```sh
sudo mkdir -p /opt/painel
sudo curl -fsSL -o /opt/painel/painel.py https://github.com/erisfernandes/loganos/releases/latest/download/loganos.py
sudo python3 /opt/painel/painel.py --instalar
```

Abra `http://<ip-do-servidor>:8092` e crie a sua conta. O idioma segue o navegador (português, inglês ou espanhol) e pode ser trocado em Ajustes.

## Atualizar

Pela página (Ajustes, Segurança, Versões) ou no terminal:

```sh
sudo python3 /opt/painel/painel.py --atualizar
```

A atualização baixa a última release e só instala se o SHA-256 bater com o `loganos.py.sha256` publicado. Se a versão nova não subir, a anterior volta sozinha.

## Desinstalar

```sh
sudo python3 /opt/painel/painel.py --desinstalar
```

Ele pergunta antes de remover e pergunta de novo antes de apagar os seus dados.

## Segurança

- Feito **só para a rede de casa e o Tailscale**. Pedidos vindos de IP público são recusados. Não deixe aberto para a internet.
- Na rede de casa a página usa HTTP sem criptografia. Para HTTPS, use o Tailscale (`--https`).
- O painel roda como um `DynamicUser` do systemd, sem privilégios, e não como root.
- Três ajudantes pequenos rodam como root, cada um com uma lista fixa de ações. Nada digitado na página vira parte de um comando:
  - `painel-servicos`: lê a lista de serviços e as portas abertas.
  - `painel-ajudante`: lê a saúde dos discos (SMART), as atualizações do sistema e as versões.
  - `painel-pedidos`: religa um serviço que falhou, monta e desmonta discos USB, atualiza o LoganOS e o cofre de senhas opcional. O pedido é só um nome de arquivo, conferido contra padrões fixos.
- Sem telemetria. Saídas para a internet, todas opcionais ou sob pedido: teste de velocidade (Cloudflare), versões novas (GitHub), ntfy.sh como reserva dos avisos, conferência do DNS (`www.google.com`) e as páginas que você guarda no Links.

## Suporte

Só pelas [issues do GitHub](https://github.com/erisfernandes/loganos/issues), sem prazo de resposta. Informe a versão, o sistema e o registro exportado.

## Licença

[AGPL-3.0](LICENSE). © 2026 Eris Fernandes.
