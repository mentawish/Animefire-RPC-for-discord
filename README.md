# 🔥 AnimeFire Discord RPC

Rich Presence automático para o Discord enquanto você assiste animes no AnimeFire.io.

Exibe:
- 🎬 Título do anime
- 📺 Episódio atual
- ⏱️ Barra de progresso em tempo real
- ▶️⏸️ Ícone de reprodução/pausa
- 🔗 Botões de acesso rápido

---

# 📦 Estrutura do Projeto

```text
animefire-rpc/
├── extension/          ← Extensão para Chrome
│   ├── manifest.json
│   ├── content.js      ← Captura as informações do player
│   ├── background.js   ← Envia os dados para o servidor Python
│   ├── popup.html/js   ← Interface da extensão
│   └── icons/          ← Adicione os ícones (16, 48 e 128px)
└── python/
    └── rpc.py          ← Servidor local + Discord RPC
```

---

# ⚙️ Instalação

## 1. Obtenha o Client ID

Acesse:

https://discord.com/developers/applications

Depois:

1. Crie uma nova aplicação (ex.: **AnimeFire**)
2. Copie o **Application ID** na aba **General Information**
3. Em **Rich Presence → Art Assets**, envie as seguintes imagens:

- `logo_xeon` → Ícone principal
- `play_icon` → Ícone de reprodução
- `pause_icon` → Ícone de pausa

---

## 2. Configure o script Python

Abra o arquivo:

```python
python/rpc.py
```

Edite a linha:

```python
CLIENT_ID = "SEU_CLIENT_ID_AQUI"
```

Substitua pelo **Application ID** da sua aplicação no Discord.

---

## 3. Instale as dependências

```bash
pip install pypresence flask flask-cors
```

---

## 4. Inicie o servidor

```bash
python python/rpc.py
```

Mantenha este terminal aberto enquanto estiver assistindo.

---

## 5. Instale a extensão no Chrome

1. Abra:

```
chrome://extensions/
```

2. Ative o **Modo do Desenvolvedor**
3. Clique em **Carregar sem compactação**
4. Selecione a pasta:

```
extension/
```

---

## 6. Adicione os ícones (Opcional)

Coloque estes arquivos na pasta:

```
extension/icons/
```

Arquivos necessários:

- `icon16.png` (16×16)
- `icon48.png` (48×48)
- `icon128.png` (128×128)

Caso não tenha os ícones, basta remover as referências a eles do arquivo `manifest.json`.

---

# 🚀 Como usar

1. Execute:

```bash
python python/rpc.py
```

2. Abra o Chrome com a extensão instalada.

3. Acesse qualquer episódio no AnimeFire.io.

Pronto! O Rich Presence será atualizado automaticamente no Discord.

---

# 🟢 Status da extensão

O ícone da extensão indica o estado da conexão:

🟢 **Verde** → Conectado ao servidor Python.

🔴 **Vermelho** → O servidor Python não está em execução.

---

# ❓ Problemas comuns

### Discord não encontrado

Abra o Discord antes de iniciar o script Python.

---

### Ícone vermelho na extensão

O servidor Python não está sendo executado.

Inicie-o com:

```bash
python python/rpc.py
```

---

### As informações não aparecem

O AnimeFire pode ter alterado a estrutura da página.

Pressione **F12**, inspecione o player de vídeo e atualize os seletores utilizados no arquivo:

```
content.js
```

---

### A barra de progresso não aparece

Isso é normal quando o vídeo está pausado.

A barra de progresso só é exibida enquanto o vídeo estiver em reprodução, devido a uma limitação do Discord Rich Presence.
